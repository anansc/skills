# SUBSKILL 1 — PRÉ-TRIAGEM E GATEKEEPER DE ADMISSIBILIDADE

> Esta subskill pode rodar isoladamente em sistema apartado. Sua função é identificar duplicidade e realizar triagem preliminar de admissibilidade; **não analisa mérito nem lê o conteúdo dos documentos**.

## 1. Escopo e proibições

- Use `processos_pesquisar`, `processo_consultar` e `documentos_listar` quando disponíveis.
- Não use `documento_ler`, OCR, extração de texto ou trechos de conteúdo para decidir admissibilidade ou presença da Declaração.
- Não avalie validade, assinatura, conteúdo, conformidade técnica ou suficiência da Declaração.
- Não crie, assine, tramite ou altere documentos ou metadados no SEI.
- Retorne um relatório estruturado ao sistema chamador. Se isolada, apresente esse relatório ao operador.

## 2. Ordem de execução

### Etapa 1 — Obter a identidade mínima

1. Consulte o protocolo fornecido com `processo_consultar` e registre número do processo, especificação, interessados e demais metadados pertinentes, conforme disponibilidade.
2. Obtenha o CNPJ da requerente e da instalação apenas de metadados acessíveis ou de parâmetros fornecidos pelo operador. Não abra documentos para extraí-los.
3. Registre a identificação da instalação (nome, endereço/localidade ou especificação disponível). Se CNPJ ou instalação não puderem ser identificados, registre `INDETERMINADO` para a verificação que dependa desses dados.

### Etapa 2 — Pesquisa prévia de duplicidade

Faça esta etapa antes de qualquer leitura de conteúdo. Pesquise processos em todo o órgão usando `processos_pesquisar`:

1. Pesquise pelo CNPJ exato da requerente e, se conhecido, também pelo CNPJ da instalação, sem restringir desnecessariamente a unidade.
2. Use filtros como `em: "processos"`, `texto`, `especificacao`, `tipo_processo` ou período, conforme o esquema da ferramenta. Solicite limite suficiente para os resultados relevantes (máximo 200 por chamada) e registre filtros, data da pesquisa e eventual sinalização de truncamento.
3. Faça buscas adicionais por CNPJ sem pontuação, nome empresarial e nome da instalação quando a primeira pesquisa puder não localizar variações cadastrais. Não interprete resultado vazio isolado como prova universal de inexistência se a pesquisa estiver limitada, truncada ou sem identificadores confiáveis.
4. Para cada processo candidato, use `processo_consultar` para confirmar os metadados disponíveis. Compare **mesmo CNPJ e mesma instalação**. Nome empresarial semelhante, CNPJ igual sem instalação coincidente, ou instalação semelhante sem CNPJ coincidente não bastam para confirmar duplicidade.
5. Classifique:
   - `DUPLICIDADE_CONFIRMADA`: pelo menos outro processo ativo/localizável com mesmo CNPJ e mesma instalação, conforme metadados comparáveis. Registre os números dos processos e os atributos coincidentes.
   - `SEM_DUPLICIDADE_IDENTIFICADA`: busca adequada, sem resultados candidatos correspondentes, sem limitação relevante conhecida.
   - `INDETERMINADO`: dados insuficientes, resultados truncados ou não acessíveis, divergência de identificação, ou pesquisa indisponível.
6. Duplicidade confirmada interrompe a pré-triagem e gera relatório ao operador/coordenadora. Não arquive, não cancele e não decida qual processo deve prevalecer.

### Etapa 3 — Gatekeeper da Declaração usando apenas metadados

1. Execute `documentos_listar` para obter a relação de documentos do processo, com nº SEI, tipo/nome, data de inclusão, situação (cancelado/substituído), restrição e demais metadados disponíveis.
2. Procure correspondência explícita no tipo, nome ou descrição, incluindo variantes: “Declaração de Adequação”, “Declaração de adequação do empreendimento”, “adequação às diretrizes”, “SNPTA”, “Secretaria Nacional de Portos” ou “MPOR/Ministério de Portos e Aeroportos”. A busca de palavras é apenas indício de metadado, não avaliação do conteúdo.
3. Considere versões não canceladas. Registre documentos cancelados e versões substituídas; não use documento cancelado como prova de presença atual se existir versão substitutiva.
4. Classifique:
   - `IDENTIFICADA`: metadado identifica claramente a Declaração. Registre nº SEI, nome/tipo e data de inclusão. Encaminhe à S2 para leitura e validação de mérito.
   - `NÃO_IDENTIFICADA`: lista de documentos suficientemente completa; nenhuma entrada corresponde à Declaração; não há pacote ou documento de nome genérico que plausivelmente possa contê-la; não há lacuna, restrição ou truncamento de metadados. Este achado permite o gatilho de ausência conforme a regra de negócio; não afirme que leu o conteúdo.
   - `INCONCLUSIVA`: metadados incompletos, documento com nome genérico (por exemplo, “Anexos”, “Documentos diversos”, “Anexo 3”), pacote, restrição, cancelamento ambíguo ou qualquer possibilidade razoável de a Declaração estar agrupada sem identificação. Não conclua ausência; encaminhe à S2 para leitura integral.
5. Se os metadados estiverem inconclusivos, siga para a próxima fase sem pedir autorização, sem bloquear o processo e sem gerar arquivamento. A S2 verificará o conteúdo e a S3 cuidará da notificação/desfecho se a ausência for confirmada.

## 3. Relatório obrigatório de saída

Retorne exatamente os campos abaixo, preenchidos com fatos disponíveis:

```yaml
processo: "[protocolo]"
data_da_consulta: "[data ou a preencher]"
duplicidade:
  status: "DUPLICIDADE_CONFIRMADA | SEM_DUPLICIDADE_IDENTIFICADA | INDETERMINADO"
  cnpj_comparado: "[valor ou não disponível]"
  instalacao_comparada: "[identificação ou não disponível]"
  consultas_realizadas: "[filtros, consultas e eventuais limitações]"
  processos_candidatos: "[protocolos e atributos coincidentes, ou nenhum]"
gatekeeper_declaracao:
  status: "IDENTIFICADA | NÃO_IDENTIFICADA | INCONCLUSIVA"
  documentos_candidatos: "[nº SEI, metadado e data, ou nenhum]"
  limitacoes: "[limitações ou nenhuma]"
encaminhamento:
  acionar_subskill_2: "sim | não"
  gatilho_para_subskill_3: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS"
  motivo: "[fundamentação factual breve]"
```

Regras de roteamento:

- `DUPLICIDADE_CONFIRMADA`: acione a coordenadora/operador e encerre sem análise documental adicional.
- `IDENTIFICADA`: acione S2; não acione arquivamento por ausência.
- `INCONCLUSIVA`: acione S2; jamais acione arquivamento por ausência a partir desse resultado.
- `NÃO_IDENTIFICADA`: não acione S2 apenas para provar presença; encaminhe o gatilho à S3 para minuta imediata de arquivamento conforme a regra operacional do setor.