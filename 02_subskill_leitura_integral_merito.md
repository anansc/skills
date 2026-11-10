# SUBSKILL 2 — LEITURA INTEGRAL, PAGINAÇÃO EXAUSTIVA E ANÁLISE DE MÉRITO

> Responsável pela leitura de mérito da primeira à última parte acessível de cada documento relevante. Aplica-se à primeira análise e à reanálise de TUP, ETC, IP4, IPTur e pedidos relacionados. Metadados localizam documentos, mas não substituem a leitura de mérito.

## 1. Papel, ferramentas e limites

- Use `documentos_listar` e `documento_ler` conforme disponíveis e autorizados.
- Assinatura funcional de `documento_ler`: `documentos` é lista de 1 a 20 strings (números SEI); `inicio` é opcional, inteiro ≥ 0; `tamanho` é opcional, inteiro entre 500 e 60000 caracteres, padrão 12000.
- Em leitura de mérito, use lotes de 1 a 5 documentos e `tamanho: 60000`. Prefira chamadas individuais para Memorial Descritivo, Petição Inicial, pareceres do IBAMA, contratos/documentos SPU e PDFs únicos consolidados.
- Chamadas podem ser cortadas por limite total (frequentemente cerca de 18.000 caracteres), ainda que `tamanho: 60000`. O aviso `[..., resultado cortado: X caracteres omitidos. Peça um trecho menor ou use os parâmetros de paginação da ferramenta.]` exige continuação.
- Nunca crie, edite, assine, tramite ou altere documentos no SEI. Entregue constatações e relatório à S3.
- Preserve a separação entre art. 4º (I–XII), art. 6º e Item XIII complementar. Não atribua à norma requisito inexistente no texto fornecido.

## 2. Reanálise e controle temporal

1. Identifique a última Notificação/Ofício, data, conteúdo, destinatário, ciência quando acessível e prazo; localize pedidos e decisões de prorrogação/suspensão.
2. Identifique o último Check-List e data de inclusão SEI; use-o como linha de base. Se houver vários ciclos, use o mais recente.
3. Identifique documentos juntados pelo requerente após a linha de base/notificação pela data de inclusão SEI e nº SEI, não pela data impressa no arquivo.
4. Recibos, despachos administrativos e atos internos não contam como resposta documental. Petição de resposta é relevante e deve ser lida.
5. Sem documento novo, registre `SEM_NOVO_DOCUMENTO_DO_REQUERENTE` e encaminhe pendências à S3 para avaliar prazo. Havendo documento novo, analise-o mesmo intempestivo; não gere alerta só por intempestividade.
6. No Modo B, leia linha de base, notificação, resposta, documentos novos e atos de prorrogação/prazo. Reavalie pendências e itens `A conferir` tratados por documentos novos; revalide itens sujeitos à validade vencidos ou sem data-limite calculável; reveja itens afetados por documento substitutivo. Registre o motivo de releituras de documentos antigos.
7. Reanálise de processo arquivado é permitida quando há juntada nova; não altere status no SEI.

## 3. Filtro de relevância pré-leitura

Antes de qualquer chamada de mérito, catalogue os documentos e separe:

- **Ler para mérito/contexto:** requerimento/petição inicial e resposta; Ficha Cadastral; CNPJ; atos societários; Declaração; Memorial; plantas; títulos; licenças; consultas; certidões; pareceres; contratos; documentos SPU; anexos potencialmente probatórios; linha de base pertinente.
- **Ler para prazo/contexto, mesmo sendo ordinatório:** Notificação/Ofício; prova de ciência se necessária à contagem; petição de prorrogação; decisão sobre prazo; petição de resposta; Check-List anterior da linha de base.
- **Ignorar na leitura de mérito:** Recibos Eletrônicos de Protocolo, Termos de Encaminhamento, despachos de mero expediente sem conteúdo decisório, certidões de intimação, comprovantes de ciência/AR e similares, desde que não necessários à ciência/contagem. Registre nº SEI e tipo de cada item ignorado e o motivo.

Não descarte ato que possa alterar prazo, identificar resposta ou conter decisão. Documento cancelado não é evidência vigente; consulte-o apenas se necessário para entender substituição. Versão substitutiva vigente prevalece, com registro.

## 4. Algoritmo obrigatório de leitura e paginação

### 4.1 Preparação dos lotes

1. Liste nº SEI, título/tipo, data de inclusão, estado, restrição, indicação de pacote e quantidade de páginas, se disponível.
2. Ordene por relevância. Leia individualmente âncoras prioritárias; agrupe os demais em lotes de 1 a 5. A prioridade organiza, mas não permite omitir documento pertinente.
3. Não inclua no lote de mérito os itens descartados pelo filtro. Preserve as exceções de prazo/contexto.

### 4.2 Leitura paginada por documento

Para cada documento relevante:

1. Inicie com `inicio: 0`, `tamanho: 60000`.
2. Conte caracteres efetivamente recebidos do documento, excluindo o aviso de corte e o envelope/metadados da resposta.
3. Se houver aviso de corte, chame novamente o mesmo SEI com `inicio = offset anterior + caracteres efetivamente recebidos` e `tamanho: 60000`. Continue até fim conforme critério abaixo.
4. Se lote tiver sido cortado e não for possível identificar quais documentos foram afetados, releia individualmente os documentos do lote e pagine cada um.
5. Considere fim atingido se a ferramenta indicar EOF/fim, ou se resposta sem aviso de corte contiver menos caracteres que o `tamanho` solicitado, ou se novo offset retornar vazio. Registre o critério. Não deduza fim apenas da quantidade estimada de páginas.
6. Se o mesmo offset devolver conteúdo idêntico duas vezes sem indicador de fim, pare por limitação técnica, registre faixas lidas e marque os requisitos dependentes como `A conferir`. Não alegue leitura integral.
7. Não há limite artificial de páginas ou chamadas: cubra PDFs únicos de até 200 páginas e textos com mais de 50.000 caracteres até o final real.
8. Avance pelo número real de caracteres do conteúdo recebido, não pelo tamanho pedido, número de páginas estimado ou caracteres omitidos. Não conte o aviso. Não deixe lacunas nem duplique faixas. Se observar comportamento de offset diferente, registre e ajuste para cobrir o conteúdo sem saltos.

### 4.3 Capas de ZIP e referências externas

Se o retorno tiver menos de 300 caracteres e for apenas capa/link para `.zip` ou arquivo externo (ex.: “Doc. 4 - Matriculas.zip”): pare de tentar ler esse documento; registre nº SEI, retorno e limitação; não presuma conteúdo; classifique como `A conferir` o requisito dependente e encaminhe à S3 para o Guia Visual. Se houver conteúdo útil além da capa, continue a paginação normal.

### 4.4 Mascaramento e OCR

- É estritamente proibido interromper leitura ou paginação por marcadores como `[PESSOA_1]`, `[TELEFONE_1]`, `[ENDERECO_1]`, `[CPF_2]`, campos ocultos ou falhas de OCR.
- Continue até o final real. Ignore valor mascarado para cruzamento; não infira dado oculto.
- Falha de OCR em uma página não autoriza abandonar as páginas seguintes. Registre trecho afetado e continue.
- Marque `A conferir` somente o dado/requisito afetado; não estenda automaticamente a incerteza aos demais itens.

### 4.5 Log de leitura

Para cada documento, registre nº SEI, título, offsets/faixas, caracteres recebidos por chamada, chamadas, aviso de corte, fim real atingido, páginas/folhas quando fornecidas e limitação. Não invente folha; se a ferramenta não fornecer paginação, cite nº SEI e registre isso.

## 5. Modo de análise

### Modo A — primeira análise

Leia requerimento, Ficha Cadastral, identificação empresarial, Declaração, Memorial e todos os documentos técnicos/administrativos relevantes. Cubra todos os requisitos aplicáveis da seção 7. Priorização de âncoras não autoriza omissão.

### Modo B — reanálise

1. Registre SEI/data do último Check-List, notificação/ofício, resposta, ciência e prazo disponíveis.
2. Inclua documentos posteriores ao último Check-List, petição de resposta e pedidos/decisões de prorrogação.
3. Reavalie pendências, `A conferir` afetados, validade e documentos novos que substituam/alterem Ficha, ato societário, planta, Memorial ou título; faça triangulação apenas na extensão necessária.
4. Mantenha itens antigos `A conferir` sem releitura se nenhum documento novo os tratar, salvo revalidação necessária; registre motivo.
5. Documento novo após o prazo é reanalisado. Intempestividade isolada não fundamenta rejeição nem alerta; arquivamento cabe à S3 e depende dos requisitos cumulativos.

## 6. Situações e evidências

Use exclusivamente: `Item atendido`, `Item não atendido`, `Diligência`, `A conferir`, `Não se aplica`.

- `Item atendido`: requisito satisfeito por evidência lida e referência SEI/página quando disponível. Se ferramenta não fornecer página, cite SEI e registre limitação.
- `Item não atendido`: ausência confirmada após busca integral, vencimento comprovado ou desconformidade explícita.
- `Diligência`: documento presente e lido, com vício sanável que requer providência.
- `A conferir`: conteúdo relevante inacessível, restrito, ilegível, máscara que impede cruzamento específico, pacote/capa ZIP não inspecionável ou imagem/planta que exija conferência visual. Delimite o item/trecho.
- `Não se aplica`: requisito incompatível com modalidade/pedido, com motivação.

Não declare ausência se houver arquivo genérico plausível sem leitura integral. Máscara não autoriza inferir dado nem rebaixar itens não afetados.

## 7. Matriz normativa e técnica

### 7.1 Enquadramento

- **TUP:** movimentação e/ou armazenagem de cargas fora do porto organizado.
- **ETC:** exclusivamente transbordo de cargas em navegação interior ou cabotagem; requisito incompatível pode ser `Não se aplica`, motivadamente.
- **IP4:** passageiros ou cargas em navegação interior; havendo passageiros, aplica-se art. 4º, § 3º.
- **IPTur:** passageiros de turismo; aplica-se art. 4º, § 3º.
- **Alteração/acréscimo de perfil:** considerar art. 34 da Resolução e arts. 26–31 da Portaria. Usar documentos de origem somente se acessíveis e pertinentes. Declaração para alteração vale 18 meses desde a emissão (art. 29, § 2º). Reavaliar perfil novo, estimativa, compatibilidade estrutural/licença e documentos alterados; motivar documentos reaproveitados.

### 7.2 Resolução nº 71/2022, art. 4º — incisos I a XII

| Item | Conferência |
| :--- | :--- |
| I | Declaração de adequação emitida pelo poder concedente. Calcular vencimento em 18 meses desde a emissão: Portaria nº 1.064/2020, art. 6º, § 2º; alteração de perfil, art. 29, § 2º. Registrar emissão e vencimento no Painel e Check-List, mesmo com ressalva de escopo/razão social. Ausência confirmada após leitura integral: gatilho à S3. |
| II | Ficha Cadastral do modelo aplicável: presença, preenchimento e cruzamentos. Calcular campos 34+35 e comparar com total declarado, aplicando seção 7.5. |
| III | Ato constitutivo/estatuto/contrato social vigente e registrado; em S.A., eleição de administradores registrada e mandato vigente. Poderes do signatário são observação complementar quando verificáveis. |
| IV | CNPJ da sede e instalação, conforme aplicável; comparar Ficha e ato sem inferir dado mascarado. |
| V.a | Planta de situação/poligonal georreferenciada, áreas separadas (terra, água, berços, bacia e canal), coordenadas decimais ou UTM/SIRGAS2000, planilha editável, formato gráfico aceito, acessos/adjacências, escala, legenda, cotas e ART/RRT com responsável, assinatura e registro. |
| V.b | Descrição de acessos aquaviários e terrestres, existentes e a construir. |
| V.c | Descrição de acostagem, berços/finalidades, armazenagem, circulação, instalações gerais/suprimentos, destinações e capacidades. Compartilhamento: art. 4º, § 1º, e art. 43, parágrafo único. |
| V.d | Embarcação-tipo por berço: tipo, comprimento, boca, calado e TPB. |
| V.e | Equipamentos/dispositivos de carga, descarga e movimentação, quantidade, capacidade e utilização quando couber. |
| V.f | Cronograma físico-financeiro; `Não se aplica` se instalação construída, com evidência e motivação. |
| V.g | Estimativa de movimentação de cargas/passageiros, incluindo perfil novo em alteração. |
| V.h | Valor global do investimento e ART/RRT específica com responsável, identificação, assinatura e registro; incluir infraestrutura, superestrutura, terrenos e, se construída, valor comercial (art. 4º, § 2º). |
| VI | Planta de locação de instalações existentes/projetadas, berços, armazenagem, circulação e instalações gerais/suprimentos; áreas conforme título, escala/cotas e ART/RRT. |
| VII | Título de propriedade, inscrição de ocupação, aforamento, cessão sob direito real ou instrumento de uso/fruição. Área da União: art. 4º, §§ 4º–5º. Comparar título, planta e áreas; não confundir com Item XIII complementar. |
| VIII | Consulta à autoridade aduaneira; indicar se consta consulta, resposta ou ambas. |
| IX | Consulta ao poder público municipal. Diferimento à vistoria de TLO somente se documentado, aplicável e motivado; não inventar dispensa. |
| X | Termo de referência ambiental, licença cabível ou dispensa do órgão competente; registrar fase, validade impressa e compatibilidade com perfil alterado. |
| XI | Regularidade perante Fazendas Estadual e Municipal da sede e, quando aplicável, da localidade da instalação; considerar art. 4º, §§ 6º–7º. Não inclui Fazenda Nacional nem FGTS. |
| XII | Parecer favorável da autoridade marítima quanto à NORMAM-11/DPC, quando couber. Se aplicabilidade indeterminada, `A conferir`, motivadamente. |

### 7.3 Art. 6º — Fazenda Nacional e FGTS

Verifique separadamente regularidade perante Fazenda Nacional e FGTS. O art. 6º prevê certidão pela ANTAQ, sem prejuízo de juntada; irregularidade enseja notificação para normalização em 30 dias (§ 1º) e o não atendimento implica arquivamento (§ 2º). Encaminhe status, datas e evidências à S3. Não classifique como inciso XI.

### 7.4 Item XIII — documentação SPU complementar

- Linha complementar do formulário/setor, fora do art. 4º (incisos I–XII). Verifique certidão/declaração de disponibilidade, instrumento de cessão ou documentação SPU quando houver área/espelho d’água sob gestão da SPU.
- Diferencie do título do inciso VII e dos §§ 4º–5º; use remissão cruzada para evitar dupla contagem.
- Ausência/incompletude aplicável: `PENDENCIA_COMPLEMENTAR_SPU`. Não impede Fase 1 nem publicação no DOU; S3 incluirá a pendência em Notificação com aviso expresso não impeditivo.
- Sem área SPU: `Não se aplica`, com justificativa.

### 7.5 Art. 4º, § 3º — passageiros

Quando aplicável, verifique áreas dimensionadas; segregação de fluxos ou operação não simultânea; plataforma, guarda-corpo, piso e rampas seguros; venda de passagens/atendimento; espera abrigada e assentos; sanitários/lixeiras; acessibilidade/prioridade; projeto de iluminação, sinalização e comunicação. Registre evidência por elemento material.

### 7.6 Cálculos, validade e cruzamentos

- **Ficha 34+35 — sempre visível:** `34 = [X] m² + 35 = [Y] m² = [Soma] m² vs. Total declarado = [Z] m²` no Painel e na constatação do Check-List.
- Se a Ficha ou Petição declarar expressamente sobreposição de áreas (p.ex. aforamento/ocupação sobreposta à matrícula alodial para evitar dupla contagem), registre a explicação e classifique `Item atendido`; use `A conferir` apenas para batimento visual de plantas, se necessário. Não gere diligência automática por divergência aritmética aparente explicada pela sobreposição.
- Sem justificativa de sobreposição e com valores legíveis divergentes, indique diligência com cálculo. `A conferir` só para valores ilegíveis/mascarados ou cruzamento visual inacessível.
- **Áreas:** triangule título, Memorial e plantas com parcelas, somas e diferenças. Ignore valor mascarado e marque apenas o cruzamento afetado `A conferir`.
- **Cadastro:** compare razão social, CNPJ, endereço e instalação entre Ficha, CNPJ e ato societário; divergência material explícita pode ser `Diligência`.
- **Declaração:** 18 meses desde a emissão. Registre emissão e data-limite. Não use assinatura como marco alternativo.
- **Demais certidões/licenças:** validade impressa; sem prazo genérico de 18 meses. Considere art. 4º, § 6º, para certidões dos incisos XI/XII e outras obtidas pela ANTAQ, sem exigir atualização durante tramitação nas hipóteses abrangidas.
- Certidão positiva com efeitos de negativa: descreva como emitida; não converta automaticamente em irregularidade.
- Dados mascarados: não cruze valores ocultos nem tente inferi-los.
- Terminal construído: V.f pode ser `Não se aplica` com motivação; V.h considera valor comercial e ART/RRT conforme art. 4º, § 2º.

## 8. Busca conclusiva da Declaração e gatilho

1. Busque em toda a documentação relevante, incluindo interior de PDFs longos, anexos e nomes genéricos plausíveis.
2. Se encontrada, registre SEI/página, emissão, escopo e validade; não acione ausência.
3. Só emita `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA` se nenhum documento plausível contiver a Declaração e todos os documentos relevantes/genéricos tiverem final real atingido (ou não houver candidato plausível). Marque Item I `Item não atendido`.
4. Se PDF, pacote, arquivo externo, documento restrito ou conteúdo plausível não tiver final atingido, não confirme ausência; marque Item I `A conferir`, descreva a limitação e não emita gatilho.

## 9. Relatório estruturado obrigatório à S3

Use situação controlada por item. O log de paginação é granular por SEI.

```yaml
processo: "[protocolo]"
modo: "A | B | reanálise isolada"
linha_de_base:
  checklist: "[SEI/data | inexistente]"
  notificacao: "[SEI/data | inexistente]"
controle_temporal:
  data_notificacao: "[data | não localizada]"
  data_ciencia: "[data | não localizada]"
  prazo_e_data_limite: "[prazo, critério e data | não calculável]"
  ultimo_documento_requerente: "[SEI/data de inclusão | nenhum]"
  documento_novo_apos_notificacao: "sim | não | indeterminado"
  intempestividade: "[fato, sem impedir reanálise]"
declaracao_adequacao:
  status: "ATENDIDA | AUSENTE_CONFIRMADA | A_CONFERIR"
  referencia: "[SEI/página ou busca/limitação]"
  emissao: "[data | não localizada]"
  validade_ate: "[data calculada | não calculável]"
  calculo: "emissão + 18 meses = [data]"
  gatilho: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA"
requisitos:
  - item: "[I, II, III ...]"
    situacao: "Item atendido | Item não atendido | Diligência | A conferir | Não se aplica"
    constatacao: "[fato, cálculo e referência]"
    sei_paginas: "[SEI/página | paginação indisponível]"
calculos:
  ficha_34_35: "34 = [X] m² + 35 = [Y] m² = [soma] m² vs. total declarado = [Z] m²"
  sobreposicao: "[declaração e efeito | não declarada | não aplicável]"
  areas: "[parcelas, documentos e diferenças]"
artigo_6_fazenda_nacional_fgts: "[situação, datas e referências]"
item_xiii_spu:
  aplicabilidade: "sim | não | indeterminada"
  situacao: "[situação controlada]"
  evidencia: "[documentos e acompanhamento]"
  nao_impeditivo_fase_1_dou: "sim"
documentos_ignorados_filtro:
  - "[SEI — tipo — motivo]"
capas_zip_ou_externos:
  - "[SEI — retorno — requisito afetado]"
paginacao:
  - sei: "[número]"
    titulo: "[tipo/nome]"
    chamadas: "[número e offsets]"
    caracteres_efetivamente_lidos: "[total/faixas]"
    avisos_de_corte: "[sim/não; número]"
    final_real_atingido: "sim | não | indeterminado"
    paginas: "[faixas ou não fornecidas]"
limitacoes: "[nenhuma ou lista precisa]"
```

## 10. Autoverificação da S2

- Filtro de relevância executado e documentos ignorados registrados por nº SEI?
- Lotes de 1–5, documentos âncora individualizados quando necessário e `tamanho: 60000`?
- Todo corte seguido de continuação por offset real até o fim, ou limitação técnica concreta registrada?
- Máscaras/OCR parcial não interromperam paginação?
- Capas ZIP curtas registradas e não confundidas com conteúdo verificado?
- Ausência da Declaração confirmada apenas com final real dos documentos plausíveis?
- Item I contém emissão + 18 meses; Item II contém soma e explicação de sobreposição quando aplicável?
- XI restrito às Fazendas Estadual/Municipal; Art. 6º separado; Item XIII complementar e não impeditivo?
- Cada situação usa um dos cinco valores autorizados?