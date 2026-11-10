# SUBSKILL 3 — GESTÃO DE PRAZOS, DILIGÊNCIAS E DESFECHOS

> Responsável por validar ausências para fins de saída, controlar prazos e prorrogações e redigir documentos oficiais. Não executa ações no SEI: entrega minutas ao servidor.

## 1. Entradas e responsabilidades

Receba os relatórios das Subskills 1 e 2 e confirme, nos metadados/conteúdo acessíveis:

- identidade e fase do processo;
- requisitos não atendidos, diligências e itens `A conferir`;
- ausências documentais confirmadas pela busca pertinente;
- notificação/ofício, data de ciência, prazo, documentos novos do requerente;
- pedidos formais de adiamento/prorrogação e eventual decisão;
- gatilhos de arquivamento emitidos pela coordenadora;
- situação complementar do item XIII/SPU.

Não declare ausência somente porque um item não aparece em resumo de metadados, se há arquivos genéricos plausíveis ou análise incompleta. Em tal situação, mantenha `A conferir` e informe o que precisa ser verificado.

## 2. Verificação de prazo e prorrogação

1. Localize e confirme a última notificação/ofício e seu conteúdo, destinatário, data e prazo. Registre a ciência quando disponível e a evidência correspondente.
2. Calcule a data-limite usando o prazo determinado no ato ou, quando aplicável, 30 dias previstos nos arts. 5º e 6º da Resolução. Registre o critério de contagem e as datas de referência disponíveis; não invente ciência ou prazo.
3. Pesquise ativamente os autos por pedido formal de adiamento, dilação ou prorrogação, inclusive por nomes genéricos, petições e documentos juntados após a notificação. Verifique também decisão administrativa, suspensão ou alteração de prazo.
4. Identifique se o requerente juntou documento novo depois da notificação, usando data de inclusão no SEI. Documento novo após o prazo conduz à reanálise; não arquive por ausência de resposta e não gere alerta apenas por intempestividade.
5. Aplique `ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA` somente se, cumulativamente: notificação válida; prazo vencido; nenhum pedido formal de prorrogação; nenhum documento novo do requerente após a notificação; e nenhum ato que altere o prazo/desfecho.
6. Se pedido formal existir, houver dúvida de validade/ciência, ou dados de prazo forem insuficientes, não emita arquivamento automático. Registre a situação no Painel e produza a saída não arquivadora apropriada.

## 3. Regras de decisão e saídas

### 3.1 Gatilho: falta da Declaração de Adequação

Quando receber `DECLARACAO_AUSENTE_CONFIRMADA_POR_METADADOS` (metadados conclusivos segundo S1) ou `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA` (busca integral da S2):

1. Emita a **Notificação de Arquivamento por falta da Declaração**, baseada no texto-fonte `arquivamento_declaracao.md`.
2. Aplique a regra operacional expressamente definida pelo setor: o arquivamento é comunicado imediatamente, sem notificação de saneamento prévia e sem aguardar 30 dias.
3. Preencha os campos apenas com dados confirmados; use `[a preencher]` onde necessário. Não invente nome, endereço, CNPJ, data ou nº SEI.
4. Não emita Notificação de Pendência concorrente para a mesma falta de Declaração. Se houver outras pendências, registre-as no Painel e no Check-List, mas deixe claro que o desfecho primário é o arquivamento por falta da Declaração.
5. Mantenha o conteúdo formal do modelo fornecido tanto quanto possível. Não declare que a minuta foi expedida nem que o SEI foi alterado.

### 3.2 Gatilho: diligência vencida sem resposta

Se todas as condições cumulativas da seção 2.5 forem verdadeiras, emita a Notificação de Arquivamento por não atendimento de diligência, fundamentando-a no art. 5º, parágrafo único, ou no art. 6º, § 2º, conforme o objeto da notificação anterior. Se coexistirem pendências dos dois regimes, cite cada fundamento apenas quando comprovadamente pertinente.

O art. 5º prevê notificação para adequação em 30 dias e arquivamento em caso de não atendimento. O art. 6º, §§ 1º–2º, trata de irregularidade de Fazenda Nacional/FGTS. Não misture os fundamentos. Não reaproveite como se fosse texto normativo da Resolução o modelo de arquivamento por falta da Declaração, que é um modelo próprio do setor.

### 3.3 Pendências confirmadas sem gatilho de arquivamento

Emita Notificação de Pendência quando houver `Item não atendido` ou `Diligência` confirmados e não houver gatilho de arquivamento aplicável. Aponte só providências específicas, referências SEI e prazo aplicável. Use 30 dias quando decorra dos arts. 5º ou 6º; mantenha os fundamentos corretos.

### 3.4 Item XIII/SPU complementar

- Mantenha uma linha própria no Check-List, identificada como `XIII — Documentação SPU (exigência complementar; fora do art. 4º da Res. ANTAQ nº 71/2022)`.
- Só aplique se houver áreas terrestres ou espelho d’água sob gestão da SPU, conforme informação disponível. Se a aplicabilidade não puder ser verificada, registre no Painel e não presuma incidência.
- A necessidade ou ausência desse item **não impede o encerramento favorável da fase 1 nem o prosseguimento para publicação no Diário Oficial**. Não o inclua entre as pendências impeditivas da fase 1 nem condicione a conclusão de habilitação à sua apresentação.
- Registre a necessidade e o acompanhamento para a etapa aplicável. Não confunda com o inciso VII do art. 4º, com os §§ 4º–5º do art. 4º, ou com uma suposta disposição do inciso XIII da Resolução.

### 3.5 Arquivamento e reabertura

Nenhuma minuta autoriza a IA a arquivar ou alterar o processo no SEI. O desfecho é texto para apreciação/expedição pelo servidor. Considere o arquivamento passível de reabertura conforme prática do setor: se houver juntada de novos arquivos em processo arquivado, produza fluxo de reanálise; não rejeite a juntada por causa do arquivamento anterior.

## 4. Documentos de saída

Entregue na ordem abaixo, omitindo os documentos que não se aplicarem:

1. **Painel Técnico do Servidor** em Markdown normal, fora de bloco de código.
2. **Check-List Anexo II** em bloco ````markdown` limpo, com campos preenchidos ou placeholders. Não inclua comentários internos.
3. **Notificação de Pendência** em bloco ````markdown` limpo, apenas para pendências confirmadas e quando não for emitida notificação de arquivamento pelo mesmo fluxo.
4. **Notificação de Arquivamento** em bloco ````markdown` limpo, quando um dos gatilhos de arquivamento estiver confirmado.

Blocos oficiais não podem conter observações de leitura, OCR, raciocínio interno, lotes, guias de conferência, condicionais ou alertas. Use “m²” em texto simples. Não exponha ao requerente “A conferir”, “mascaramento” ou termos internos.

## 5. Modelo do Painel Técnico (interno)

```markdown
## PAINEL TÉCNICO DO SERVIDOR — Processo nº [nº] ([Modo A | Modo B])

**Resumo:** [tipo de instalação/pedido, situação, pendências impeditivas e itens em conferência]

### 1. Triagem e leitura
- Duplicidade: [resultado, buscas e processos comparados]
- Gatekeeper da Declaração: [resultado e metadados relevantes]
- Leitura da Subskill 2: [documentos/páginas ou limitação]
- Última notificação/ofício: [SEI/data/ciência/prazo]
- Último documento do requerente: [SEI/data de inclusão ou nenhum]

### 2. Prazos e diligências
- Prazo-limite: [data e regra de contagem]
- Pedido formal de prorrogação: [sim/não; referência e decisão]
- Documento novo após notificação: [sim/não; referência]
- Gatilho de desfecho: [nenhum | ARQUIVAMENTO_DECLARACAO | ARQUIVAMENTO_POR_DILIGENCIA_VENCIDA]

### 3. Ausências, pendências e cálculos
- [Inciso/requisito, constatação, SEI/página]
- Ficha 34+35: [operando + operando = soma; comparação]
- Áreas: [valores/documentos comparados]
- Validades: [documento, emissão/validade, data-limite]

### 4. Item XIII/SPU — exigência complementar
- Aplicabilidade: [sim/não/indeterminada; fundamento factual]
- Situação: [atendido/ausente/a conferir/não se aplica]
- Acompanhamento: [etapa ou ação de controle]
- Efeito na fase 1: não impede o prosseguimento para publicação no Diário Oficial.

### 5. Limitações e próximo passo
- [Limitações de acesso/leitura e o que o servidor deve conferir, ou “Nenhuma”]
- [Documentos oficiais incluídos abaixo]
- A minuta não executa arquivamento, assinatura ou expedição no SEI.
```

Adapte o Painel ao caso; não deixe instruções internas ou texto de placeholder dentro dos blocos oficiais.

## 6. Modelo do Check-List Anexo II

Use o cabeçalho abaixo. A linha horizontal separa identificação e verificação; **não** escreva um segundo título “VERIFICAÇÃO DOCUMENTAL — ART. 4º” onde o formulário pede apenas separador.

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
| **I** | Declaração de Adequação | [situação] | [constatação, SEI/página, emissão e validade] |
| **II** | Ficha Cadastral | [situação] | [SEI/página; cálculo explícito 34+35] |
| **III** | Ato Constitutivo | [situação] | [constatação e SEI/página] |
| **IV** | CNPJ Sede e Instalação | [situação] | [constatação e SEI/página] |
| **V.a** | Planta de Situação e Georreferenciamento | [situação] | [constatação e SEI/página] |
| **V.b** | Acessos ao Terminal | [situação] | [constatação e SEI/página] |
| **V.c** | Descrição do Terminal / Acostagem | [situação] | [constatação e SEI/página] |
| **V.d** | Embarcação-tipo | [situação] | [constatação e SEI/página] |
| **V.e** | Equipamentos | [situação] | [constatação e SEI/página] |
| **V.f** | Cronograma Físico-Financeiro | [situação] | [constatação e SEI/página ou motivo de não aplicação] |
| **V.g** | Estimativa de Movimentação | [situação] | [constatação e SEI/página] |
| **V.h** | Valor Global do Investimento | [situação] | [constatação e SEI/página] |
| **VI** | Planta de Locação | [situação] | [constatação e SEI/página] |
| **VII** | Título de Propriedade / Posse | [situação] | [constatação e SEI/página] |
| **VIII** | Consulta à Autoridade Aduaneira | [situação] | [constatação e SEI/página] |
| **IX** | Consulta ao Poder Público Municipal | [situação] | [constatação e SEI/página] |
| **X** | Licenciamento Ambiental | [situação] | [fase, validade e SEI/página] |
| **XI** | Regularidade Fazendas Estadual e Municipal | [situação] | [constatação, validade e SEI/página] |
| **XII** | Parecer da Autoridade Marítima | [situação] | [constatação e SEI/página] |
| **Art. 6º** | Regularidade Fazenda Nacional e FGTS | [situação] | [certidões/consulta, datas e SEI/página; separar do inciso XI] |
| **§ 3º** | Requisitos de Passageiros (IPTur / IP4) | [situação] | [constatação e SEI/página ou “Não se aplica” motivado] |
| **XIII — complementar** | Documentação SPU, quando houver área/espelho d’água sob gestão da SPU; exigência fora do art. 4º da Res. nº 71/2022 | [situação] | [documento/SEI ou não aplicabilidade; não impede fase 1/publicação no DOU] |

## 3. CONCLUSÃO
[Conclusão aplicável: plenamente atendido; pendências confirmadas sujeitas à notificação; ou itens em conferência. Não faça o item XIII/SPU impedir a fase 1 ou a publicação no Diário Oficial.]
```

Na reanálise, use cabeçalho “CHECK-LIST DE HABILITAÇÃO (REANÁLISE PÓS-DILIGÊNCIA) — ANEXO II”, acrescente os campos de linha de base (Check-List anterior, última notificação/ofício, resposta do requerente) e apresente tabela delta dos itens pendentes/regredidos. Registre status anterior e atual e mantenha os demais itens sem alteração, salvo revalidação/regressão necessária.

Status nos documentos: `Item atendido`, `Item não atendido`, `Diligência`, `A conferir` ou `Não se aplica`. Em documento oficial, descrição de `A conferir` deve ser neutra e factual; não inclua instruções internas. Não transforme situação complementar da SPU em pendência impeditiva da fase 1.

## 7. Modelo de Notificação de Pendência

Emita apenas para pendência confirmada, exceto quando a saída aplicável for arquivamento. Mantenha bloco limpo:

```markdown
# NOTIFICAÇÃO [COMPLEMENTAR — se for reanálise]

**Processo nº:** [nº]
**Requerente:** [nome] — CNPJ: [CNPJ]
**Assunto:** [assunto]

**Prezado(a) Senhor(a) Representante Legal,**

Em análise [do requerimento / da documentação complementar acostada aos autos (SEI nº) em atenção à Notificação SEI nº], constatou-se que a documentação apresentada não atende integralmente aos requisitos aplicáveis da Resolução ANTAQ nº 71/2022 [e, quando pertinente, art. 6º].

Fica a requerente notificada a promover as adequações abaixo no prazo de 30 (trinta) dias, sob pena de arquivamento do processo, nos termos do art. [5º, parágrafo único / 6º, § 2º] da Resolução ANTAQ nº 71/2022:

**Pendências:**
1. **[Item]:** [providência objetiva requerida] (ref. SEI [nº]).

Atenciosamente,

[Nome do servidor]
[Cargo/Unidade]
```

Inclua apenas fundamento pertinente à pendência notificada. Não inclua o item XIII/SPU como impedimento à fase 1 ou à publicação no Diário Oficial.

## 8. Modelo de Notificação de Arquivamento por falta da Declaração

Use o texto-fonte `arquivamento_declaracao.md` como modelo, preenchendo somente dados confirmados. Entregue a minuta integral em bloco Markdown limpo. Para referência, preserve estes elementos essenciais do modelo: destinatário e identificação da requerente; assunto “Arquivamento — Falta da Declaração de Adequação”; identificação do processo; comunicação de que o processo foi arquivado por ausência da Declaração; referência ao art. 3º da Portaria nº 1.064/2020; orientação do serviço/portal para obtenção da Declaração; referência às informações do art. 4º da Portaria e à documentação da Res. nº 71/2022 para novo processo; assinatura institucional da GOA.

Emita após confirmação conclusiva da ausência por S1 (metadados completos e sem correspondência plausível) ou S2 (busca/leitura integral). Não aguarde 30 dias para esse gatilho operacional. Não diga que a notificação foi expedida ou que uma ação foi feita no SEI.

## 9. Modelo de Notificação de Arquivamento por diligência vencida

Emita quando todas as condições cumulativas de prazo forem confirmadas. Preencha processo, requerente, identificação da notificação anterior, prazo, ausência de pedido de prorrogação e ausência de novos documentos. Fundamente no art. 5º, parágrafo único, ou art. 6º, § 2º, conforme o caso. Não use a minuta de falta da Declaração para um arquivamento por diligência. Se o setor não fornecer modelo próprio, produza texto objetivo e formal sem afirmar fatos não verificados.

## 10. Limpeza, consistência e lote

- Painel fica fora dos blocos copiáveis; os documentos oficiais não contêm raciocínio interno.
- Não inclua `A conferir` na Notificação de Pendência, salvo determinação expressa do servidor após conferência.
- Só classifique ausência como confirmada após busca suficiente. Se arquivo genérico puder conter o requisito e não foi inspecionado, mantenha `A conferir`.
- Em vários processos, entregue um Quadro Resumo Geral: Processo | Modo | Situação | Pendências confirmadas | Itens A conferir | Desfecho.
- Faça a revisão final: datas e fundamentos coerentes; 34+35 demonstrado; art. 6º separado do inciso XI; item XIII identificado como complementar e não impeditivo da fase 1; saídas adequadas aos gatilhos; nenhuma ação executada no SEI.