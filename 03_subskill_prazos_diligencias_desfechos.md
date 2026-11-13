# SUBSKILL 3 — PRAZOS, CHECK-LIST (22 LINHAS) E DESFECHOS

> Converte os relatórios validados das S1/S2 em Painel Técnico, Check-List Anexo II e minutas externas limpas. Não executa atos no SEI.

## 1. Regras de integridade e higiene de saída

* **Preenchimento:** Use todos os dados extraídos pela S2 (especialmente identificação completa da Ficha Cadastral). Use `[a preencher]` apenas quando ausente ou mascarado nos autos.

* **Blocos externos limpos:** Check-List e Notificações não podem conter comentários internos, menção a OCR, mascaramento, lotes de leitura ou instruções ao servidor.

* **Vocabulário único na coluna Situação:** `Item atendido`, `Item não atendido`, `Diligência`, `A conferir`, `Não se aplica`.

* **Proibição de cobrança sem confirmação:** Itens `A conferir` nunca entram na Notificação de Pendência (inclusive o Item XIII, se estiver `A conferir`).

## 2. Regras de prazos, arquivamento e Item XIII

1. **Ausência da Declaração (`ARQUIVAMENTO_DECLARACAO`):** Acione somente com gatilho válido (`DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS` ou `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA`). Emita imediatamente a minuta da Seção 7 (regra operacional do setor, sem notificação prévia de 30 dias) e não emita Notificação de Pendência concorrente.

2. **Diligência vencida (`ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA`):** Exige notificação válida, prazo vencido, ausência de pedido de prorrogação, ausência de documento novo após notificação (documento novo exige reanálise, mesmo intempestivo) e ausência de suspensão. Separe art. 5º, parágrafo único (documental) do art. 6º, §§ 1º–2º (Fazenda Nacional/FGTS).

3. **Item XIII (SPU):**

   * Sempre ocupa a **22ª linha** da tabela do Check-List (nunca em parágrafo solto fora da tabela).

   * Só entra na Notificação de Pendência se a ausência/pendência estiver **confirmada** nos autos (frase genérica na petição sem documento conclusivo gera apenas registro no Painel e `A conferir`, sem minuta).

   * Quando incluído na Notificação, aparece em **seção separada** com o **aviso literal** de que não impede a conclusão da Fase 1 nem a publicação do extrato no DOU.

## 3. Ordem obrigatória de entrega

1. **Painel Técnico do Servidor** (Markdown fora de bloco de código).

2. **Check-List Anexo II** (bloco `markdown` limpo, obrigatoriamente com as **22 linhas** no Modo A).

3. **Notificação de Pendência** (bloco `markdown` limpo, apenas se houver pendência confirmada ou Item XIII confirmado).

4. **Notificação de Arquivamento** (bloco `markdown` limpo, apenas com gatilho comprovado).

## 4. Modelo — Painel Técnico do Servidor

```
## PAINEL TÉCNICO DO SERVIDOR — Processo nº [nº] ([Modo A | Modo B])

**Resumo:** [instalação/pedido, coerência assunto x objeto, status geral, pendências impeditivas, Item XIII e itens em conferência]

### 1. Leitura realizada
- Lotes de `documento_ler`: [Lote 1 (n arquivos): ...; Lote 2 (n arquivos): ...]
- Documentos ignorados pelo Filtro de Relevância: [nº SEI — tipo; ...]
- Documentos cancelados/sigilosos/sem acesso: [nº SEI ou "nenhum"]
- Suposições adotadas / ambiguidades: [ou "nenhuma"]
- (Modo B) Linha de base: Check-List SEI [nº] de [data]; Notificação SEI [nº]; ciência em [data]; prazo-limite [data]; resposta SEI [nº] em [data] — [tempestiva | intempestiva | sem resposta | prorrogação nos autos]
- (Modo B) Itens A conferir da linha de base mantidos sem releitura: [itens ou "nenhum"]

### 2. Prazos e gatilhos
- **Prazo-limite e critério:** [data/regra ou não calculável]
- **Prorrogação / Documento novo após notificação:** [fatos e SEIs]
- **Gatilho de arquivamento:** [nenhum | ARQUIVAMENTO_DECLARACAO | ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA]

### 3. Cálculos obrigatórios e alertas
- **Declaração (Item I):** emissão [data]; validade até [emissão + 18 meses]; ref. [SEI/pág.].
- **Ficha Cadastral (Item II):** `34 = [X] m² + 35 = [Y] m² = [Soma] m² vs. Total declarado = [Z] m²`. Sobreposição: [explicação/nenhuma].
- **Triangulação de áreas:** [título x Ficha x plantas e diferenças observadas].
- **Alertas de validade (≤ 30 dias) e inconsistências:** [certidões prestes a vencer, divergência assunto/objeto ou endereço de alvará].

### 4. Pendências e enquadramento Fase 1
- [Itens `Item não atendido` ou `Diligência` com SEI]
- [Art. 6º — Fazenda Nacional/FGTS, separado do inciso XI]
- [Item XIII/SPU — aplicabilidade, situação e aviso de não impedimento da Fase 1/DOU]

### 5. Guia Rápido de Conferência Visual (1 linha por item `A conferir`)
| Item | Abrir SEI nº | O que checar visualmente | Motivo (lista fechada) | Texto-sugestão de pendência (se confirmada falha) |
| :--- | :--- | :--- | :--- | :--- |
| [item] | [SEI] | [checagem objetiva] | [motivo] | [texto externo sugerido] |

### 6. Próximo passo
- [Minutas geradas e convite ao servidor para confirmar os itens `A conferir`. Nenhuma ação foi executada no SEI.]

```

## 5. Modelo — Check-List Anexo II (Modo A — 22 linhas fixas)

```
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

## 2. VERIFICAÇÃO DOCUMENTAL (22 ITENS OBRIGATÓRIOS)

| Item | Requisito / Exigência Normativa | Situação | Constatação e Ref. SEI |
| :--- | :--- | :--- | :--- |
| **I** | Declaração de Adequação | [status] | [SEI/pág.; emissão: data; validade até: data — emissão + 18 meses] |
| **II** | Ficha Cadastral | [status] | [SEI/pág.; 34 = X m² + 35 = Y m² = soma m² vs. Total declarado = Z m²; sobreposição, se houver] |
| **III** | Ato Constitutivo | [status] | [constatação e SEI/pág.] |
| **IV** | CNPJ Sede e Instalação | [status] | [constatação e SEI/pág.] |
| **V.a** | Planta de Situação e Georreferenciamento | [status] | [constatação e SEI/pág.] |
| **V.b** | Acessos ao Terminal | [status] | [constatação e SEI/pág.] |
| **V.c** | Descrição do Terminal / Acostagem | [status] | [constatação e SEI/pág.] |
| **V.d** | Embarcação-tipo | [status] | [constatação e SEI/pág.] |
| **V.e** | Equipamentos | [status] | [constatação e SEI/pág.] |
| **V.f** | Cronograma Físico-Financeiro | [status] | [constatação e SEI/pág. ou motivação de não aplicação] |
| **V.g** | Estimativa de Movimentação | [status] | [constatação e SEI/pág.] |
| **V.h** | Valor Global do Investimento | [status] | [constatação e SEI/pág.] |
| **VI** | Planta de Locação | [status] | [constatação e SEI/pág.] |
| **VII** | Título de Propriedade / Posse | [status] | [constatação e SEI/pág.] |
| **VIII** | Consulta à Autoridade Aduaneira | [status] | [constatação e SEI/pág.] |
| **IX** | Consulta ao Poder Público Municipal | [status] | [constatação/diferimento motivado e SEI/pág.] |
| **X** | Licenciamento Ambiental | [status] | [fase, validade impressa e SEI/pág.] |
| **XI** | Regularidade Fazendas Estadual e Municipal | [status] | [somente Estadual/Municipal; constatação, validade e SEI/pág.] |
| **XII** | Parecer da Autoridade Marítima | [status] | [constatação e SEI/pág.] |
| **Art. 6º** | Regularidade Fazenda Nacional e FGTS | [status] | [certidões/consulta, datas e SEI/pág.; separado do inciso XI] |
| **§ 3º** | Requisitos de Passageiros (IPTur / IP4) | [status] | [constatação e SEI/pág. ou “Não se aplica” motivado] |
| **XIII — complementar** | Documentação SPU (área/espelho d’água da União; fora do art. 4º da Res. nº 71/2022) | [status] | [documento/SEI ou justificativa de não aplicação; não impede Fase 1/DOU] |

## 3. CONCLUSÃO
[Conclusão factual sem condicionar Fase 1/DOU ao Item XIII.]

```

*(Para o **Modo B**, preserve o bloco de identificação com linha de base e apresente na Seção 2 a tabela delta `Item | Requisito | Situação Anterior | Situação | Constatação e Ref. SEI`, mantendo o Item XIII dentro da tabela sempre que reavaliado ou pendente.)*

## 6. Modelo — Notificação de Pendência

```
# NOTIFICAÇÃO

**Processo nº:** [nº]  
**Requerente:** [nome] — CNPJ: [CNPJ]  
**Assunto:** [assunto]  

**Prezado(a) Senhor(a) Representante Legal,**

Em análise do requerimento e da documentação acostada aos autos, inclusive da documentação complementar apresentada em resposta à Notificação SEI nº [nº, se aplicável], constatou-se que a documentação não atende integralmente aos requisitos aplicáveis da Resolução ANTAQ nº 71/2022.

Fica a requerente notificada a promover as adequações impeditivas abaixo no prazo de 30 (trinta) dias, sob pena de arquivamento do processo, nos termos do art. [5º, parágrafo único | 6º, §§ 1º e 2º] da Resolução ANTAQ nº 71/2022:

**Pendências impeditivas:**
1. **[Item]:** [providência objetiva requerida] (ref. SEI [nº]).

**Exigência complementar — Item XIII (SPU), não impeditiva da Fase 1:**
[Providência de saneamento/controle SPU objetivamente requerida e referência SEI.]

A ausência da documentação do Item XIII — exigência complementar relativa à SPU, fora do art. 4º da Resolução ANTAQ nº 71/2022 — não impede a conclusão desta primeira fase de habilitação nem a publicação do extrato do anúncio no Diário Oficial da União. Sua apresentação destina-se ao saneamento e ao controle nas etapas subsequentes da outorga.

Atenciosamente,

[Nome do servidor]  
[Cargo/Unidade]

```

*(Omita a seção XIII se não houver pendência confirmada; omita as pendências impeditivas e o parágrafo de arquivamento se a única pendência confirmada for o Item XIII.)*

## 7. Modelo — Notificação de Arquivamento (Ausência da Declaração)

```
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
