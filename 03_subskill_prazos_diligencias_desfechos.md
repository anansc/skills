# SUBSKILL 3 — PRAZOS, DILIGÊNCIAS, CHECK-LIST E DESFECHOS

> Converte os achados das S1/S2 em Painel Técnico, Check-List Anexo II e minutas. Não executa ações no SEI. Não confirma ausência que dependa de documento genérico não lido integralmente.

## 1. Entradas, escopo e salvaguardas

Receba relatórios S1/S2 e metadados acessíveis: identidade/fase; status e evidências; log de leitura/paginação; ausências; última notificação, ciência, prazo e resposta; documento novo; pedido/decisão de prorrogação; gatilhos; aplicabilidade e situação SPU.

- Use fatos confirmados; dado faltante: `[a preencher]` ou “não localizado”. Não invente data, nome, nº SEI, ciência, validade ou decisão.
- Não declare ausência se houver arquivo genérico plausível não inspecionado até o final. Mantenha `A conferir` e especifique o que falta.
- Não altere, arquive, assine, tramite ou expeça no SEI. A saída é minuta para o servidor.
- Blocos oficiais são limpos: não contêm raciocínio interno, mascaramento, OCR, lotes, logs, instruções ao servidor ou texto condicional.
- Status permitido na coluna `Situação`, sem variações: **`Item atendido`**, **`Item não atendido`**, **`Diligência`**, **`A conferir`**, **`Não se aplica`**. Expressões como “Apresentada; conferir escopo” são proibidas como status; ressalvas vão em `Constatação e Ref. SEI`.

## 2. Verificação de prazo e prorrogação

1. Confirme última notificação/ofício, conteúdo, destinatário, data, prazo, ciência e evidências, na medida disponível.
2. Calcule data-limite pelo prazo indicado ou, quando aplicável, 30 dias dos arts. 5º/6º. Registre regra e datas usadas; não invente ciência nem convenção de contagem. Se a contagem depender de regra não confirmada nos autos, indique a limitação e não declare vencimento conclusivo.
3. Pesquise pedidos formais de dilação/prorrogação e atos decisórios, inclusive em documentos genéricos e petições posteriores. Considere suspensão ou alteração de prazo.
4. Verifique documentos novos do requerente pela data de inclusão SEI. Documento novo após notificação conduz à reanálise, mesmo após prazo. Não arquive por falta de resposta nem gere alerta apenas por intempestividade.
5. Use `ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA` somente se, cumulativamente: notificação válida; prazo vencido; nenhum pedido formal de prorrogação; nenhum documento novo após notificação; e nenhum ato que altere prazo/desfecho. Qualquer dúvida impede arquivamento automático.
6. Separe fundamentos: art. 5º, parágrafo único, para descumprimento de diligência documental; art. 6º, §§ 1º–2º, para Fazenda Nacional/FGTS. Cite somente o fundamento pertinente ao objeto.

## 3. Regras para ausência da Declaração

Receba somente estes gatilhos válidos:

- `DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS`: emitido pela S1 apenas com lista completa e explícita, sem documento genérico/composto plausível.
- `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA`: emitido pela S2 somente após leitura integral de todos os documentos plausíveis, com final real atingido.

Em qualquer dos casos, produza imediatamente minuta de arquivamento conforme o modelo integral da seção 9, sem notificação de saneamento prévia e sem aguardar 30 dias, segundo regra operacional informada pelo setor. Não afirme que o arquivamento foi efetivado ou que a minuta foi expedida. Use apenas dados confirmados. Não produza Notificação de Pendência concorrente para a falta da Declaração; pendências adicionais podem constar no Painel e Check-List.

Sem gatilho válido, não use a minuta. Metadados inconclusivos ou documento plausível não paginado não comprovam ausência.

## 4. Decisão sobre pendências, Fase 1 e Item XIII

- Pendência confirmada (`Item não atendido` ou `Diligência`) sem gatilho de arquivamento: gere Notificação de Pendência, com providência específica, referência SEI e prazo/fundamento aplicável.
- Itens `A conferir` não entram como pendência na Notificação, salvo após conferência do servidor que confirme falha; registre-os no Painel e no Check-List com constatação externa neutra.
- O Item XIII/SPU tem linha própria, complementar e fora do art. 4º. Se houver pendência aplicável, **inclua-a na Notificação de Pendência** numa seção distinta das exigências impeditivas. Inclua literalmente o aviso de que sua ausência não trava a Fase 1/habilitação nem a publicação do extrato no DOU e que se destina ao saneamento/controle das etapas subsequentes.
- A pendência XIII não pode constar na lista de pendências impeditivas nem ser fundamento de “sob pena de arquivamento” da Fase 1. Se for a única pendência, a Notificação deve deixar claro que a Fase 1 pode prosseguir e não associar o XIII ao prazo sancionatório dos arts. 5º/6º. Havendo outras pendências impeditivas, mantenha o fundamento/prazo delas separado e apresente o XIII como complementar, sem confundir regimes.
- Se Item XIII estiver apenas `A conferir`, não o inclua como pendência na Notificação; indique no Painel a verificação visual e mantenha a situação factual no Check-List.
- Não confunda Item XIII com art. 4º, VII, art. 4º, §§ 4º–5º, nem com inciso XIII regulamentar.

## 5. Ordem de saída

Para cada processo, entregue nesta ordem e omita apenas o que não se aplicar:

1. **Painel Técnico do Servidor**, em Markdown normal, fora de bloco de código.
2. **Check-List Anexo II**, em bloco `markdown` limpo. Em Modo B, cabeçalho e tabela delta, com linha de base.
3. **Notificação de Pendência**, em bloco `markdown` limpo, apenas quando houver pendências confirmadas ou pendência complementar XIII confirmada; observar a separação da seção 4.
4. **Notificação de Arquivamento**, em bloco `markdown` limpo, quando gatilho confirmado. Para ausência da Declaração, usar o modelo da seção 9.

Se gatilho de ausência da Declaração estiver confirmado, a minuta de arquivamento é o desfecho primário; não emitir notificação concorrente para sanar a mesma ausência. Itens adicionais podem ser registrados no Painel e Check-List sem alterar o desfecho.

## 6. Painel Técnico do Servidor — modelo interno

Adapte ao caso sem deixar placeholders vazios se houver informação disponível. Inclua sempre as seções **Cálculos obrigatórios** e **Guia Rápido de Conferência Visual**; se não houver conteúdo, use “Nenhum”.

```markdown
## PAINEL TÉCNICO DO SERVIDOR — Processo nº [nº] ([Modo A | Modo B])

**Resumo:** [tipo de instalação/pedido, situação, pendências impeditivas, Item XIII complementar e itens em conferência]

### 1. Triagem e leitura
- Duplicidade: [status, consultas e candidatos]
- Gatekeeper da Declaração: [status e metadados]
- Último Check-List: [SEI/data ou inexistente]
- Última notificação/ofício: [SEI/data/ciência/prazo]
- Último documento do requerente: [SEI/data de inclusão ou nenhum]
- Documentos lidos e paginação: [resumo das faixas; fim real atingido ou limitação]
- Documentos ignorados pelo filtro: [SEI — tipo — motivo, ou “Nenhum”]
- Capas ZIP/externos: [SEI — limitação — item afetado, ou “Nenhum”]

### 2. Prazos e diligências
- Prazo-limite e critério: [data/regra ou não calculável]
- Pedido formal de prorrogação: [sim/não/indeterminado; SEI/decisão]
- Documento novo após notificação: [sim/não; SEI/data de inclusão]
- Intempestividade: [fato, se houver; sem alerta isolado]
- Gatilho: [nenhum | ARQUIVAMENTO_DECLARACAO | ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA]

### 3. Cálculos obrigatórios
- Declaração (Item I): emissão [data]; validade de 18 meses desde a emissão: [data calculada]; referência [SEI/página]. Se emissão indisponível, registrar “não calculável” e motivo.
- Ficha Cadastral (Item II): 34 = [X] m² + 35 = [Y] m² = [Soma] m² vs. Total declarado = [Z] m². Sobreposição expressamente declarada: [explicação/nenhuma/não aplicável].
- Áreas e outros cálculos: [parcelas, documentos, diferenças, ou “Nenhum”].

### 4. Pendências e alertas
- [Item, situação controlada, constatação e SEI/página]
- [Art. 6º — Fazenda Nacional/FGTS, separado do inciso XI]
- [Item XIII/SPU — aplicabilidade, situação e etapa de acompanhamento]
- Fase 1/DOU: Item XIII é complementar e sua ausência não impede habilitação/publicação.

### 5. Guia Rápido de Conferência Visual (itens `A conferir`)
| Item | Abrir SEI nº | O que checar visualmente | Motivo | Texto-sugestão de pendência (se confirmada a falha) |
| :--- | :--- | :--- | :--- | :--- |
| [item] | [SEI] | [checagem objetiva] | [limitação] | [texto externo sugerido] |

### 6. Limitações e próximo passo
- Limitações de acesso/leitura: [precisas ou “Nenhuma”]
- Próximo passo: [documentos/minutas incluídos e ação de conferência]
- [Se aplicável: convite final ao servidor para informar, por item, o que conferiu regular e o que deve ser cobrado. Não fazer pergunta intermediária nem usar ferramenta de pergunta.]
- A minuta não executa arquivamento, assinatura, expedição ou alteração no SEI.
```

O Guia Visual deve ter uma linha por requisito `A conferir`, com SEI, tarefa visual concreta, motivo e texto-sugestão. Não inclua neste guia situações definitivamente atendidas ou diligências já confirmadas.

## 7. Check-List Anexo II — Modo A

Entregue bloco oficial limpo, com todos os campos que puder preencher. Toda célula Situação deve conter exatamente um dos cinco valores permitidos. A constatação pode conter ressalva, referência, cálculo e emissão/validade.

```markdown
# CHECK-LIST DE HABILITAÇÃO — ANEXO II
**Análise de requerimento de autorização para instalação portuária ([TUP/ETC/IP4/IPTur])**
**Construção / Exploração / Alteração**
Lei nº 12.815/2013 — Decreto nº 8.033/2013 — Resolução ANTAQ nº 71/2022

## 1. IDENTIFICAÇÃO

| Campo | Informação |
| :--- | :--- |
| **Data de análise:** | [data] |
| **Data do requerimento:** | [data] |
| **Motivo do requerimento:** | [motivo] |
| **Processo Nº:** | [protocolo] |
| **Assunto:** | [assunto] |
| **Nome da requerente:** | [nome] |
| **Endereço da sede da requerente:** | [endereço] |
| **CEP da sede:** | [CEP] |
| **CNPJ da sede:** | [CNPJ] |
| **Pessoa de contato na sede - Cargo:** | [informação] |
| **Tel/Fax/Celular do contato na sede:** | [informação] |
| **E-mail do contato na sede:** | [informação] |
| **Nome da instalação:** | [nome] |
| **Endereço da instalação da requerente:** | [endereço] |
| **CEP da instalação:** | [CEP] |
| **CNPJ da instalação:** | [CNPJ] |
| **Pessoa de contato na instalação - Cargo:** | [informação] |
| **Tel/Fax/Celular do contato na instalação:** | [informação] |
| **E-mail do contato na instalação:** | [informação] |
| **Coordenadas Geográficas (dois pontos) *obrigatório:** | [coordenadas ou situação] |

---

| Item | Requisito / Exigência Normativa | Situação | Constatação e Ref. SEI |
| :--- | :--- | :--- | :--- |
| **I** | Declaração de Adequação | [status permitido] | [SEI/página; emissão: data; validade até: data calculada — emissão + 18 meses] |
| **II** | Ficha Cadastral | [status permitido] | [SEI/página; 34 = X m² + 35 = Y m² = soma m² vs. Total declarado = Z m²; sobreposição expressa, se houver] |
| **III** | Ato Constitutivo | [status permitido] | [constatação e SEI/página] |
| **IV** | CNPJ Sede e Instalação | [status permitido] | [constatação e SEI/página] |
| **V.a** | Planta de Situação e Georreferenciamento | [status permitido] | [constatação e SEI/página] |
| **V.b** | Acessos ao Terminal | [status permitido] | [constatação e SEI/página] |
| **V.c** | Descrição do Terminal / Acostagem | [status permitido] | [constatação e SEI/página] |
| **V.d** | Embarcação-tipo | [status permitido] | [constatação e SEI/página] |
| **V.e** | Equipamentos | [status permitido] | [constatação e SEI/página] |
| **V.f** | Cronograma Físico-Financeiro | [status permitido] | [constatação e SEI/página ou motivação de não aplicação] |
| **V.g** | Estimativa de Movimentação | [status permitido] | [constatação e SEI/página] |
| **V.h** | Valor Global do Investimento | [status permitido] | [constatação e SEI/página] |
| **VI** | Planta de Locação | [status permitido] | [constatação e SEI/página] |
| **VII** | Título de Propriedade / Posse | [status permitido] | [constatação e SEI/página] |
| **VIII** | Consulta à Autoridade Aduaneira | [status permitido] | [constatação e SEI/página] |
| **IX** | Consulta ao Poder Público Municipal | [status permitido] | [constatação/diferimento motivado e SEI/página] |
| **X** | Licenciamento Ambiental | [status permitido] | [fase, validade impressa e SEI/página] |
| **XI** | Regularidade Fazendas Estadual e Municipal | [status permitido] | [somente Estadual/Municipal; constatação, validade e SEI/página] |
| **XII** | Parecer da Autoridade Marítima | [status permitido] | [constatação e SEI/página] |
| **Art. 6º** | Regularidade Fazenda Nacional e FGTS | [status permitido] | [certidões/consulta, datas e SEI/página; separado do inciso XI] |
| **§ 3º** | Requisitos de Passageiros (IPTur / IP4) | [status permitido] | [constatação e SEI/página ou “Não se aplica” motivado] |
| **XIII — complementar** | Documentação SPU, quando houver área/espelho d’água sob gestão da SPU; exigência fora do art. 4º da Res. nº 71/2022 | [status permitido] | [documento/SEI ou justificativa de não aplicação; não impede Fase 1/publicação no DOU] |

## 3. CONCLUSÃO
[Conclusão factual: plenamente atendido; pendências confirmadas sujeitas à notificação; ou itens em conferência. Nunca condicionar Fase 1/DOU ao Item XIII.]
```

## 8. Check-List Anexo II — Modo B (reanálise)

Use tabela delta: linhas de itens pendentes/regredidos/afetados por documento novo e linha própria do Item XIII se houve mudança/pendência. Registre status anterior e atual. Mantenha sem alteração os demais itens, exceto validade ou regressão necessária. Inclua data/referência de linha de base e cálculo obrigatório de I/II em constatação quando pertinentes.

```markdown
# CHECK-LIST DE HABILITAÇÃO (REANÁLISE PÓS-DILIGÊNCIA) — ANEXO II
**Análise complementar de requerimento de autorização para instalação portuária ([TUP/ETC/IP4/IPTur])**
**Construção / Exploração / Alteração**
Lei nº 12.815/2013 — Decreto nº 8.033/2013 — Resolução ANTAQ nº 71/2022

## 1. IDENTIFICAÇÃO E CONTROLE DE REANÁLISE

| Campo | Informação |
| :--- | :--- |
| **Data de análise:** | [data] |
| **Check-List anterior (Referência e Data):** | SEI [nº], de [data] |
| **Ofício/Notificação de diligência:** | SEI [nº/data] |
| **Data de ciência e prazo:** | [data, prazo e data-limite ou não localizados] |
| **Protocolo de resposta da requerente:** | SEI [nº/data de inclusão ou nenhum] |
| **Data do requerimento:** | [data] |
| **Motivo do requerimento:** | [motivo] |
| **Processo Nº:** | [protocolo] |
| **Assunto:** | [assunto] |
| **Nome da requerente:** | [nome] |
| **Endereço da sede da requerente:** | [endereço] |
| **CEP da sede:** | [CEP] |
| **CNPJ da sede:** | [CNPJ] |
| **Pessoa de contato na sede - Cargo:** | [informação] |
| **Tel/Fax/Celular do contato na sede:** | [informação] |
| **E-mail do contato na sede:** | [informação] |
| **Nome da instalação:** | [nome] |
| **Endereço da instalação da requerente:** | [endereço] |
| **CEP da instalação:** | [CEP] |
| **CNPJ da instalação:** | [CNPJ] |
| **Pessoa de contato na instalação - Cargo:** | [informação] |
| **Tel/Fax/Celular do contato na instalação:** | [informação] |
| **E-mail do contato na instalação:** | [informação] |
| **Coordenadas Geográficas (dois pontos) *obrigatório:** | [coordenadas ou situação] |

## 2. VERIFICAÇÃO COMPLEMENTAR — ITENS REANALISADOS
*Os itens não incluídos nesta tabela permanecem conforme Check-List SEI [nº], salvo as revalidações expressamente registradas.*

| Item | Requisito | Situação Anterior | Situação | Constatação e Ref. SEI |
| :--- | :--- | :--- | :--- | :--- |
| [item] | [requisito] | [um dos cinco status] | [um dos cinco status] | [nova análise, SEI/página, cálculo I ou II quando pertinente] |
| **XIII — complementar** | Documentação SPU, quando aplicável; fora do art. 4º | [status anterior] | [um dos cinco status] | [documento/SEI ou acompanhamento; não impede Fase 1/publicação no DOU] |

## 3. CONCLUSÃO DA REANÁLISE
[Conclusão: pendências sanadas, pendências remanescentes ou itens em conferência. Distinguir pendências impeditivas das complementares; Item XIII não impede Fase 1/DOU.]
```

## 9. Notificação de Arquivamento — ausência da Declaração

Usar o modelo fornecido `arquivamento_declaracao.md` como redação-fonte. Preservar a estrutura, as citações, o Portal de Serviços/SUPER, o endereço eletrônico e a assinatura institucional. Preencher somente dados confirmados; manter placeholders do modelo quando não confirmados. Entregar o texto integral abaixo em bloco `markdown` limpo. A redação comunica o arquivamento como minuta, mas a IA não afirma que executou qualquer ação no SEI.

```markdown
# NOTIFICAÇÃO

Ao Senhor  
**[Nome do Representante Legal]**  
Administrador da empresa **[Razão Social da Requerente]**  
[Endereço da Sede]  
CEP: [CEP da Sede] — [Município/UF da Sede]  
E-mail: [E-mail do Representante/Empresa]  

**Assunto:** Arquivamento — Falta da Declaração de Adequação  
**Referência:** (Caso responda este Ofício, indicar expressamente o Processo nº **[Número do Processo]**)  

Senhor Representante,

Ao tempo de cumprimentá-lo, informo que o processo **[Número do Processo]**, aberto pela empresa **[Razão Social da Requerente]**, foi arquivado em razão da ausência da Declaração de Adequação, emitida pela Secretaria Nacional de Portos do Ministério de Portos e Aeroportos (MPOR).

A Declaração de Adequação é um documento obrigatório para abertura de processo de autorização de Instalações Portuárias Privadas junto à ANTAQ, conforme consta no art. 3º da Portaria nº 1.064/2020-MINFRA, que dispõe:

> *"Art. 3º O interessado em obter autorização para exploração de instalação portuária deverá requerer à Secretaria Nacional de Portos e Transportes Aquaviários a emissão de declaração de adequação do empreendimento às diretrizes do planejamento e das políticas do setor portuário."*

Para obter a Declaração de Adequação, a empresa interessada deve solicitar de forma online por meio do Portal de Serviços do Governo Federal utilizando o peticionamento eletrônico no sistema SUPER (endereço: https://www.gov.br/pt-br/servicos/autorizacao-para-exploracao-indireta-de-areas-nao-afetas-a-operacao-portuaria).

A documentação exigida para emissão da Declaração de Adequação está disposta no art. 4º da Portaria nº 1.064/2020-MINFRA:

> *"Art. 4º O requerimento de emissão de declaração de adequação de que trata o art. 3º deverá conter ou estar acompanhado das seguintes informações e documentos:*  
> *I - planta de situação do empreendimento, destacando a poligonal georreferenciada da área a ser ocupada, tanto em terra como em água;*  
> *II - planta de localização georreferenciada do empreendimento em escala compatível, destacando a área em terra, berços, canal de acesso, bacia de evolução e área de fundeio;*  
> *III - memorial descritivo do empreendimento, destacando tipo e perfil de carga a ser movimentada no terminal, bem como sua projeção de capacidade estática e de movimentação; e*  
> *IV - estimativa global de investimento."*

Após a obtenção da Declaração de Adequação, a empresa poderá abrir novo processo na ANTAQ inserindo-a em conjunto com todos os documentos listados no art. 4º da Resolução ANTAQ nº 71/2022.

Atenciosamente,

[Nome do Servidor]  
Gerência de Outorgas e Autorizações — GOA  
Agência Nacional de Transportes Aquaviários — ANTAQ
```

## 10. Modelo de Notificação de Pendência

Gere somente para pendências confirmadas. Inclua fundamento e prazo correspondentes aos itens impeditivos. Se houver Item XIII confirmado, ele deve aparecer em seção distinta, com o aviso fixo abaixo. Não associe ameaça de arquivamento ao Item XIII isoladamente.

```markdown
# NOTIFICAÇÃO

**Processo nº:** [nº]
**Requerente:** [nome] — CNPJ: [CNPJ]
**Assunto:** [assunto]

**Prezado(a) Senhor(a) Representante Legal,**

Em análise do requerimento e da documentação acostada aos autos, inclusive da documentação complementar apresentada em resposta à Notificação SEI nº [nº, se aplicável], constatou-se que a documentação não atende integralmente aos requisitos aplicáveis da Resolução ANTAQ nº 71/2022.

Fica a requerente notificada a promover as adequações impeditivas abaixo no prazo de 30 (trinta) dias, sob pena de arquivamento do processo, nos termos do art. [fundamento aplicável: 5º, parágrafo único, ou 6º, §§ 1º e 2º] da Resolução ANTAQ nº 71/2022:

**Pendências impeditivas:**
1. **[Item]:** [providência objetiva requerida] (ref. SEI [nº]).

**Exigência complementar — Item XIII (SPU), não impeditiva da Fase 1:**
[Providência de saneamento/controle SPU objetivamente requerida e referência SEI.]

A ausência da documentação do Item XIII — exigência complementar relativa à SPU, fora do art. 4º da Resolução ANTAQ nº 71/2022 — não impede a conclusão desta primeira fase de habilitação nem a publicação do extrato do anúncio no Diário Oficial da União. Sua apresentação destina-se ao saneamento e ao controle nas etapas subsequentes da outorga.

Atenciosamente,

[Nome do servidor]
[Cargo/Unidade]
```

Instruções de preenchimento: omita a seção XIII se não houver pendência confirmada; omita a seção de pendências impeditivas e o parágrafo de arquivamento se o único assunto for Item XIII. Nesse caso, preserve a seção XIII e o aviso não impeditivo e declare que a Fase 1 pode prosseguir. Em hipóteses exclusivamente fiscais, use apenas o regime do art. 6º; não cite art. 5º como fundamento fiscal.

## 11. Notificação de Arquivamento por diligência vencida

Emitir apenas com todas as condições da seção 2 comprovadas. Não reutilizar o modelo de ausência da Declaração. Se não houver modelo setorial, redigir minuta objetiva identificando notificação anterior, ciência, prazo vencido, ausência de prorrogação e ausência de documento novo, com fundamento estritamente pertinente no art. 5º, parágrafo único, ou art. 6º, § 2º. Não declarar que a minuta foi expedida ou que o SEI foi alterado.

## 12. Rodada de fechamento e lote

- Se o servidor fornecer resultado de conferência visual de itens `A conferir`, atualizar com base nessa informação sem reler autos: regular → `Item atendido`, registrando “conferido pelo servidor”; falha → `Diligência` ou `Item não atendido` conforme o fato. Reemitir Check-List e Notificação definitiva, sem instruções internas nos blocos.
- Se não restar pendência, informar que Notificação deixa de ser necessária. Em reanálise concluída sem pendências, incluir no Painel Situação Final Consolidada com todos os requisitos aplicáveis e respectivas evidências.
- Para vários processos, encerrar com `Processo | Modo | Situação | Pendências confirmadas | Itens A conferir | Desfecho`.
- Revisão final: Situações dentro do vocabulário; data de emissão + 18 meses no Item I; fórmula completa 34+35 no Item II; sobreposição respeitada; XI separado do art. 6º; XIII complementar, incluído na notificação se pendente e acompanhado do aviso; nenhum `A conferir` cobrado como falha sem confirmação; nenhum ato no SEI.