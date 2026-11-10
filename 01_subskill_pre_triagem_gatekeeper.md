# SUBSKILL 1 — PRÉ-TRIAGEM E GATEKEEPER

> Função: consultar metadados, identificar duplicidade e fazer triagem preliminar da Declaração de Adequação. Pode rodar isoladamente. Não avalia mérito, validade nem suficiência documental. A leitura cadastral limitada abaixo é exceção expressa e não constitui leitura de mérito.

## 1. Ferramentas, limites e proibições

- Use `processo_consultar`, `documentos_listar` e `processos_pesquisar` quando disponíveis.
- Use `documento_ler` **somente** na Etapa 1B, quando CNPJ e/ou nome da instalação não estiverem explícitos nos metadados. Uma chamada por documento, `tamanho: 5000`, no máximo dois documentos, nesta ordem: comprovante de CNPJ; Ficha Cadastral; página 1 da Petição Inicial. Leia somente o trecho cadastral necessário. Não use a chamada para mérito, Declaração ou conteúdo técnico.
- Não use OCR ou extração adicional fora do mecanismo disponível. Não infira texto não retornado.
- Nunca crie, assine, expeça, tramite ou altere documentos/metadados do SEI.
- Não faça perguntas intermediárias. Se a identidade permanecer inacessível, marque `INDETERMINADO` e siga à S2.

## 2. Sequência operacional

### Etapa 1 — consulta inicial obrigatória

1. Execute `processo_consultar` para o protocolo recebido. Registre número, especificação, interessado, tipo e identificadores efetivamente visíveis.
2. Execute `documentos_listar`. Registre nº SEI, nome/tipo, data de inclusão, estado cancelado/substituído, sigilo/restrição, truncamento e indicação de pacote/arquivo único.
3. Extraia dos metadados o CNPJ da requerente, CNPJ da instalação e nome/localização da instalação, sem inferências. Valor mascarado (ex.: `[PESSOA_1]`, `[CNPJ_1]`) não é comparável.

### Etapa 1B — extração cadastral pontual autorizada

Se CNPJ e/ou nome da instalação não estiverem explícitos nos metadados — inclusive se aparecerem mascarados —, tente extraí-los pontualmente dos documentos cadastrais abaixo, desde que a lista não indique pacote único genérico/consolidado:

1. Selecione, conforme disponível: comprovante de CNPJ; na falta, Ficha Cadastral; na falta, página inicial da Petição Inicial.
2. Leia o documento com `documento_ler(documentos: ["SEI"], tamanho: 5000)`. Limite total de dois documentos/tentativas, somente para extrair CNPJ e nome da instalação.
3. Se a lista indicar pacote único genérico/consolidado, não percorra o pacote em busca cadastral: marque identidade dependente como `INDETERMINADO` e avance à S2.
4. Se a ferramenta truncar, não revelar os dados ou retornar marcadores, registre `INDETERMINADO` imediatamente. Não entre em loop nem bloqueie o fluxo.
5. Registre nº SEI, fonte e limitação. Use apenas os identificadores necessários à pesquisa.

Essa exceção é restrita à identificação cadastral. A busca de duplicidade ocorre depois dela e antes da leitura de mérito da S2.

### Etapa 2 — pesquisa de duplicidade

Pesquise com identificadores confiáveis por `processos_pesquisar`, sem restringir desnecessariamente a unidade. Faça as consultas necessárias a: (a) CNPJ da requerente formatado; (b) CNPJ sem pontuação, se a ferramenta puder retornar resultado distinto; (c) nome da instalação. Inclua CNPJ da instalação se identificado e pertinente. Limite cada chamada ao máximo de 200 resultados; registre filtro, data, truncamento e limitações. Não repita consultas equivalentes nem entre em loop.

Para cada candidato, use `processo_consultar` e compare **mesmo CNPJ e mesma instalação**. Razão social semelhante, CNPJ igual sem instalação coincidente ou nome de instalação isolado não confirmam duplicidade.

- `DUPLICIDADE_CONFIRMADA`: outro processo ativo/localizável tem mesmo CNPJ e mesma instalação, com evidência comparável. Registre processos e atributos coincidentes; encaminhe à coordenadora e encerre análise documental.
- `SEM_DUPLICIDADE_IDENTIFICADA`: identificadores confiáveis, pesquisa adequada sem candidato correspondente e sem limitação relevante.
- `INDETERMINADO`: CNPJ/nome ausente ou mascarado, pacote que impede extração, pesquisa indisponível/truncada/limitada ou candidatos não comparáveis. Não bloqueie: encaminhe à S2, salvo duplicidade confirmada.

Resultado vazio ou truncado não prova inexistência universal de processo correspondente.

### Etapa 3 — gatekeeper da Declaração por metadados

1. Examine títulos/tipos/descrições em busca de variantes: “Declaração de Adequação”, “adequação do empreendimento”, “diretrizes do setor portuário”, “SNPTA”, “Secretaria Nacional de Portos”, “MPOR” ou “Ministério de Portos e Aeroportos”. É indício de metadado, não avaliação de conteúdo.
2. Registre documentos cancelados/substituídos. Documento cancelado não comprova presença atual se houver substituição identificável.
3. Classifique:
   - `IDENTIFICADA`: título/tipo/descrição identifica claramente a Declaração não cancelada. Encaminhe à S2 para validar conteúdo, escopo, emissão e validade.
   - `INCONCLUSIVA`: não localizada por título, mas existe documento genérico/extenso, petição inicial, “Anexos”, pacote, PDF único consolidado, arquivo sem descrição, lacuna/truncamento da lista, restrição, cancelamento ambíguo ou qualquer possibilidade razoável de estar embutida. Encaminhe à S2. Não bloqueie nem arquive.
   - `AUSENTE_POR_METADADOS`: somente se a árvore de documentos estiver comprovadamente 100% completa e explícita, sem arquivo genérico/composto, pacote, restrição, truncamento ou lacuna, e nenhuma entrada plausível corresponder à Declaração. Permite encaminhar o gatilho à S3 sem S2.
4. Se a árvore não for demonstravelmente completa e explícita, use `INCONCLUSIVA`, nunca `AUSENTE_POR_METADADOS`.

## 3. Roteamento e saída obrigatória

Roteamento: duplicidade confirmada → encerrar sem arquivamento; Declaração identificada/inconclusiva → S2; ausência estrita por metadados → S3 com `DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS`; duplicidade indeterminada → S2 sem repetir tentativas cadastrais improdutivas.

Entregue o relatório abaixo com fatos disponíveis:

```yaml
processo: "[protocolo]"
data_da_consulta: "[data ou a preencher]"
identidade:
  cnpj_requerente: "[valor | mascarado | indisponível]"
  cnpj_instalacao: "[valor | mascarado | indisponível]"
  instalacao: "[nome/localização | mascarado | indisponível]"
  fonte: "[metadados ou SEI da extração cadastral; método e limitação]"
duplicidade:
  status: "DUPLICIDADE_CONFIRMADA | SEM_DUPLICIDADE_IDENTIFICADA | INDETERMINADO"
  consultas_realizadas: "[filtros, data, truncamento e limites; sem repetição equivalente]"
  processos_candidatos: "[protocolos e atributos coincidentes | nenhum]"
declaracao_metadados:
  status: "IDENTIFICADA | INCONCLUSIVA | AUSENTE_POR_METADADOS"
  documentos_candidatos: "[SEI/título/data/estado | nenhum]"
  arvore_completa_e_sem_genericos: "sim | não | indeterminado"
  limitacoes: "[pacotes, títulos genéricos, restrição, truncamento | nenhuma]"
encaminhamento:
  proximo_modulo: "S2 | S3 | ENCERRAR_POR_DUPLICIDADE"
  gatilho: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS"
  motivo: "[fato breve]"
```

## 4. Autoverificação

- Consulta inicial e listagem executadas antes do gatekeeper?
- Leitura cadastral limitada a `tamanho: 5000`, até dois documentos e somente CNPJ/nome da instalação?
- Identidade inacessível resultou em `INDETERMINADO`, sem loop?
- Duplicidade confirmada apenas com CNPJ e instalação coincidentes?
- PDF único, petição extensa ou título genérico resultou em `INCONCLUSIVA`?
- `AUSENTE_POR_METADADOS` usado apenas com árvore completa, explícita e sem conteúdo genérico/composto?
- Nenhum documento alterado ou expedido no SEI?