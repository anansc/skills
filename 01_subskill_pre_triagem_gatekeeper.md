# SUBSKILL 1 — PRÉ-TRIAGEM (VERIFICAÇÃO INICIAL)

> Função: consultar metadados, avaliar duplicidade, identificar o tipo de atividade (análise ou reanálise) e fazer a verificação preliminar da Declaração de Adequação. Pode rodar isoladamente. Não avalia mérito, validade nem suficiência documental. O nome técnico antigo desta etapa nunca aparece nas saídas ao servidor.

## 1. Ferramentas, limites e proibições

- Use `processo_consultar`, `documentos_listar` e `processos_pesquisar` em modo somente leitura.
- Use `documento_ler` **somente** na Etapa 1B, quando CNPJ e/ou nome da instalação não estiverem explícitos nos metadados. Máximo de **2 documentos**, uma chamada por documento com `tamanho: 5000`, nesta ordem: (1) comprovante de CNPJ; (2) Ficha Cadastral; (3) página 1 da Petição Inicial. **Os dados extraídos aqui são repassados à S2; não releia esses documentos sem necessidade.**
- Não infira texto oculto. Valor entre colchetes vindo do sistema (ex.: `[PESSOA_1]`, `[CNPJ_1]`) não é comparável.
- Nunca crie, assine, expeça, tramite ou altere documentos/metadados do SEI. Não faça perguntas intermediárias.

## 2. Sequência operacional

### Etapa 1 — Consulta inicial obrigatória

1. `processo_consultar`: registre número, **assunto/especificação**, interessado, tipo e identificadores visíveis.
2. `documentos_listar`: registre nº SEI, nome/tipo, data de inclusão, estado cancelado/substituído, sigilo/restrição, truncamento, indicação de pacote/arquivo único e, quando houver, **número de páginas/tamanho** (alimenta o Portão de Peso da S0 §3.1).
3. Extraia dos metadados o CNPJ da requerente, o CNPJ da instalação e o nome/localização da instalação.
4. **Tipo de atividade (preliminar):** procure na árvore Notificação, Ofício, Check-List, Despacho de prorrogação/decisão ou resposta do requerente posteriores. Se existir qualquer um → `REANALISE` (a S2 confirma e lista); caso contrário → `ANALISE`.

### Etapa 1B — Extração cadastral pontual autorizada

Se CNPJ e/ou nome da instalação não estiverem explícitos nos metadados, e a árvore não for um pacote único genérico: selecione até 2 documentos cadastrais e leia com `documento_ler(documentos: ["SEI"], inicio: 0, tamanho: 5000)`. Se a leitura truncar antes dos dados, trouxer marcadores de ocultação ou se tratar de pacote consolidado, registre `INDETERMINADO` e avance sem loop.

### Etapa 2 — Pesquisa de duplicidade

Pesquise com identificadores confiáveis em `processos_pesquisar` (sem restringir desnecessariamente a unidade): (a) CNPJ da requerente formatado; (b) CNPJ sem pontuação; (c) nome da instalação. Até 200 resultados por chamada; não repita consultas equivalentes.

- **`DUPLICIDADE_CONFIRMADA`:** outro processo ativo/localizável com **mesmo CNPJ e mesma instalação**, confirmado via `processo_consultar`. Encerre a análise documental e informe o servidor.
- **`SEM_DUPLICIDADE_IDENTIFICADA`:** identificadores pesquisados sem candidato correspondente **e** a consulta retornou ao menos o próprio processo (índice funcional).
- **`INDETERMINADO`:** CNPJ/nome ausente ou oculto; pesquisa indisponível/truncada; ou zero resultados (nem o próprio processo). Nunca bloqueie o fluxo por `INDETERMINADO`: siga para a S2.

### Etapa 3 — Verificação preliminar da Declaração por metadados

Examine títulos/tipos/descrições buscando: "Declaração de Adequação", "adequação do empreendimento", "diretrizes do setor portuário", "SNPTA", "Secretaria Nacional de Portos", "MPOR", "Ministério de Portos e Aeroportos".

- **`IDENTIFICADA`:** título/tipo identifica claramente a Declaração não cancelada → S2 valida conteúdo, escopo, emissão e validade.
- **`INCONCLUSIVA`:** não localizada por título, mas há documento genérico/extenso, petição inicial, "Anexos", pacote, PDF único consolidado, arquivo sem descrição, lacuna/truncamento, restrição ou cancelamento ambíguo → S2.
- **`AUSENTE_POR_METADADOS`:** somente se a árvore estiver comprovadamente **100% completa e explícita**, sem arquivo genérico/composto, pacote, restrição ou lacuna, e nenhuma entrada plausível corresponder à Declaração → S3 com `DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS`.

## 3. Saída

### 3.1 Registro interno (não exibir ao servidor)

```yaml
processo: "[protocolo]"
data_da_consulta: "[data ou a preencher]"
assunto_metadados: "[assunto exato registrado no processo]"
tipo_atividade_preliminar: "ANALISE | REANALISE"
documentos_marcos_reanalise: "[SEI/tipo/data de Notificação, Ofício, Check-List, Despacho, resposta | nenhum]"
identidade:
  cnpj_requerente: "[valor | oculto | indisponível]"
  cnpj_instalacao: "[valor | oculto | indisponível]"
  instalacao: "[nome/localização | oculto | indisponível]"
  fonte: "[metadados ou SEI da extração cadastral]"
duplicidade:
  status: "DUPLICIDADE_CONFIRMADA | SEM_DUPLICIDADE_IDENTIFICADA | INDETERMINADO"
  proprio_processo_retornado: "sim | não"
  processos_candidatos: "[protocolos e atributos coincidentes | nenhum]"
declaracao_metadados:
  status: "IDENTIFICADA | INCONCLUSIVA | AUSENTE_POR_METADADOS"
  documentos_candidatos: "[SEI/título/data/estado | nenhum]"
  arvore_completa_e_sem_genericos: "sim | não | indeterminado"
peso_de_leitura:
  documentos_relevantes_estimados: "[n]"
  pdfs_longos_mais_de_30_paginas: "[SEI + título | nenhum]"
  texto_estimado_total: "[n | indeterminado]"
  modo_sugerido: "DIRETO | HIBRIDO"
encaminhamento:
  proximo_modulo: "S2 | S3 | ENCERRAR_POR_DUPLICIDADE"
  gatilho: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS"
  motivo: "[fato breve]"
```

### 3.2 Resumo para o Painel (linguagem simples)

- **Duplicidade:** `SEM_DUPLICIDADE_IDENTIFICADA` → "Não há outro processo com o mesmo CNPJ e instalação." | `INDETERMINADO` → "Nenhum outro processo coincidente foi localizado; a pesquisa disponível não permite confirmação plena." | `DUPLICIDADE_CONFIRMADA` → informar o protocolo coincidente.
- **Tipo de atividade:** "Análise" ou "Reanálise".
- **Declaração de Adequação:** "Presente (SEI nº)", "Ausente" ou "A confirmar na leitura dos documentos".

## 4. Autoverificação

1. Consulta e listagem executadas antes da verificação da Declaração?
2. `assunto_metadados` e `peso_de_leitura` registrados?
3. Leitura cadastral limitada a até 2 documentos, `tamanho: 5000`, só CNPJ/instalação?
4. Pesquisa com zero resultados (sem retornar o próprio processo) marcada como `INDETERMINADO`?
5. Qualquer arquivo genérico, petição extensa ou pacote marcado como `INCONCLUSIVA`?
6. O Resumo para o Painel não contém termos técnicos (S0 §6)?
