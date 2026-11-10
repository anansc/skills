# SUBSKILL 2 — LEITURA INTEGRAL E ANÁLISE DE MÉRITO

> Pode ser executada isoladamente, inclusive para reanálise. Leia documentos do início ao fim; não decida mérito com base apenas nos metadados.

## 1. Papel, ferramentas e limites

- Analise documentalmente os requisitos aplicáveis à autorização de TUP, ETC, IP4, IPTur e pedidos relacionados, à luz da Res. ANTAQ nº 71/2022 e da Portaria nº 1.064/2020.
- Use `documentos_listar` e `documento_ler` conforme disponíveis. Limite cada chamada de `documento_ler` a no máximo 20 documentos, se esse for o limite da ferramenta.
- Não crie, edite, assine, tramite ou altere documentos no SEI. Produza constatações e relatório técnico para a Subskill 3.
- Distinga requisitos do art. 4º da Resolução, requisitos do art. 6º, requisitos complementares da Portaria e exigências complementares do setor, sem atribuir a uma norma dispositivo que ela não contém.

## 2. Reanálise isolada: comparação de datas obrigatória

1. Identifique a última notificação/ofício de diligência enviado ao requerente, a data do documento e, se disponível, a data de ciência.
2. Identifique a data de inclusão nos autos do documento mais recente juntado pelo requerente após essa notificação. Use data de inclusão no SEI, não a data escrita no arquivo, para estabelecer a ordem de juntada.
3. Compare e registre: (a) data da notificação/ofício; (b) ciência; (c) prazo indicado e data-limite, se calculável; (d) data de inclusão do último documento do requerente; e (e) nº SEI do documento.
4. Se não houver documento novo, retorne `SEM_NOVO_DOCUMENTO_DO_REQUERENTE` e indique as pendências anteriores preservadas para avaliação de prazo pela S3. Não considere recibos, despachos da Administração ou atos internos como resposta documental do requerente.
5. Se houver documento novo, analise-o mesmo que juntado após o prazo. Não emita alerta apenas por intempestividade e não deixe de realizar a reanálise por esse motivo. A decisão de arquivamento, quando cabível por falta de resposta, compete à S3.
6. Se não houver notificação anterior, classifique como primeira análise ou indique a limitação; não fabrique uma data de corte.

## 3. Leitura completa sem atalhos

1. Liste todos os documentos, suas datas de inclusão, nº SEI, nome/tipo, estado (cancelado/substituído), restrição e paginação disponível.
2. Identifique as peças administrativas que precisam ser lidas para prazo ou contexto (notificação/ofício, resposta do requerente, pedido/decisão de prorrogação, último Check-List). Não descarte documentos que possam alterar prazos ou identificar a resposta.
3. Leia cada documento relevante desde a primeira até a última página. Se a ferramenta só permitir lotes, processe faixas/páginas em sequência até a última página de cada arquivo. Continue os lotes até concluir todos os documentos relevantes.
4. É proibido: ler apenas páginas iniciais; interromper a leitura por extensão ou por exceder 30/80 páginas; presumir conformidade porque o documento se parece com outro; inferir conformidade pelo tamanho ou nome do arquivo; declarar ausente um requisito sem busca no processo e em anexos/pacotes plausíveis.
5. Se a ferramenta não disponibilizar paginação ou truncar o conteúdo, tente os mecanismos de continuação/faixas disponíveis. Registre quais páginas foram efetivamente lidas e quais não foram. Não presuma conteúdo não lido e use `A conferir` somente para a parte realmente inacessível.
6. Para arquivo ilegível, restrito ou com conteúdo mascarado, descreva a limitação e não faça inferência sobre os dados ilegíveis. Não exponha dados sensíveis além do estritamente necessário; reproduza marcadores mascarados como recebidos.
7. Antes de concluir ausência, examine nomes genéricos, anexos e pacotes que possam conter o requisito. Se não puder abrir/inspecionar um arquivo plausível, não declare ausência confirmada; passe à S3 como `A conferir`/limitação.

## 4. Fluxo de documentos e modo de análise

### Modo A — primeira análise

Leia o requerimento, Ficha Cadastral, documentos de identificação empresarial, Declaração de Adequação e documentos técnicos/administrativos aplicáveis. Em seguida, cubra todos os requisitos aplicáveis da matriz da seção 6. A ordem de lote pode priorizar documentos-âncora, mas não pode excluir nem abreviar os demais.

### Modo B — reanálise

1. Identifique o último Check-List e a última Notificação/Ofício. Use o último ciclo como linha de base e registre SEI/data.
2. Inclua documentos juntados depois do último Check-List, a petição de resposta e atos de prazo/prorrogação. Use data e ordem de inclusão, não a data impressa no documento, para o corte.
3. Reavalie itens pendentes e documentos novos. Revalide itens atendidos sujeitos a validade quando a base indicar vencimento ou não houver data-limite suficiente. Reveja item aprovado se documento novo o substituir ou afetar sua evidência.
4. Não reabra a leitura de documentos antigos sem necessidade, exceto para triangulação específica ou se o documento anterior for necessário para entender uma nova peça. Registre o fundamento de cada releitura.
5. Se processo arquivado recebeu novos documentos, trate a juntada como pedido de reanálise, conforme prática informada pelo setor. Não faça alteração de situação no SEI.

## 5. Status e evidências

- `Item atendido`: evidência lida integralmente, requisito satisfeito e referência ao nº SEI e página/folha. Se a ferramenta não fornece paginação, cite nº SEI e registre a limitação; não invente folha.
- `Item não atendido`: ausência confirmada após busca integral aplicável; documento comprovadamente vencido; ou desconformidade explícita.
- `Diligência`: documento presente e lido, mas com vício sanável que exige providência do requerente.
- `A conferir`: evidência parcialmente inacessível, arquivo restrito/ilegível/mascarado, pacote plausível que não pôde ser inspecionado ou falta de acesso a processo relacionado. Indique exatamente o que precisa de confirmação. Não use por conta aritmética que possa ser feita.
- `Não se aplica`: somente quando a exigência não incide no tipo de instalação/pedido; motive.
- Não declare documento ausente se a busca não foi integral ou se restar arquivo plausível sem inspeção. Encaminhe essa incerteza como `A conferir`.

## 6. Matriz de requisitos e regras técnicas

### Enquadramento

- **TUP:** movimentação e/ou armazenagem de cargas fora do porto organizado.
- **ETC:** exclusivamente transbordo de cargas em navegação interior ou cabotagem; requisitos incompatíveis com o tipo de instalação podem ser `Não se aplica`, com motivação.
- **IP4:** passageiros ou cargas em navegação interior; se houver passageiros, aplique o § 3º do art. 4º.
- **IPTur:** passageiros de turismo; aplique o § 3º do art. 4º.
- **Alteração/acréscimo de perfil:** avalie o art. 34 da Res. 71/2022 e os arts. 26 a 31 da Portaria nº 1.064/2020. Use os documentos de origem somente se acessíveis e pertinentes; a declaração para alteração de perfil tem validade de 18 meses desde a emissão, conforme art. 29, § 2º, da Portaria.

### Resolução ANTAQ nº 71/2022 — art. 4º, incisos I a XII

| Item | Requisito a verificar |
|---|---|
| I | Declaração de adequação às diretrizes de planejamento e políticas do setor portuário, emitida pelo poder concedente. Calcule validade de 18 meses desde a emissão conforme art. 6º, § 2º, da Portaria nº 1.064/2020; em alteração de perfil, art. 29, § 2º. Ausência confirmada deve ser encaminhada à S3 para arquivamento imediato conforme regra operacional do setor. |
| II | Ficha Cadastral conforme formulário ANTAQ: presença, preenchimento e cruzamentos pertinentes. Some os campos/itens 34+35, mostre cada operando e o resultado, e compare ao total declarado. |
| III | Ato constitutivo/estatuto/contrato social vigente e registrado; para sociedade por ações, eleição de administradores, registro e mandato vigente. Registre poderes do signatário quando verificáveis como informação complementar. |
| IV | Número de CNPJ da sede e da instalação requerida, conforme aplicável. Compare com os dados cadastrais e societários. |
| V.a | Planta de situação e poligonal georreferenciada separando área terrestre, sobre água, berços, bacia de evolução e canal de acesso; coordenadas decimais ou UTM/SIRGAS2000, planilha editável, formato gráfico aceito, acessos/adjacências, escala, legenda, cotas e ART/RRT com responsável, assinatura e registro profissional. |
| V.b | Descrição dos acessos aquaviários e terrestres existentes e a construir. |
| V.c | Descrição de acostagem, berços/finalidades, armazenagem, circulação, instalações gerais e suprimentos, destinações e capacidades. Para compartilhamento, ver art. 4º, § 1º, e art. 43, parágrafo único. |
| V.d | Embarcação-tipo por berço: tipo, comprimento, boca, calado e TPB. |
| V.e | Equipamentos/dispositivos de carga, descarga e movimentação, incluindo quantidade, capacidade e utilização quando couber. |
| V.f | Cronograma físico-financeiro de implantação; não se aplica quando a instalação já estiver construída, com motivação documental. |
| V.g | Estimativa de movimentação de cargas e/ou passageiros, abrangendo o perfil novo quando for alteração. |
| V.h | Valor global do investimento, com ART/RRT específica e identificação, assinatura e registro do responsável; considere infraestrutura, superestrutura, terrenos e, se construído, valor comercial (art. 4º, § 2º). |
| VI | Planta de locação das instalações existentes/projetadas, berços, armazenagem, circulação e instalações gerais/suprimentos; demarcação das áreas a outorgar conforme título, escala/cotas e ART/RRT. |
| VII | Título de propriedade, inscrição de ocupação, certidão de aforamento, cessão sob direito real ou instrumento de uso/fruição. Para área da União, considere art. 4º, §§ 4º e 5º, quanto à certidão SPU e condição suspensiva. Compare áreas com planta e consolide títulos. |
| VIII | Consulta à autoridade aduaneira. Registre se consta consulta, resposta ou ambas, conforme os autos. |
| IX | Consulta ao poder público municipal. Eventual diferimento à vistoria de TLO somente se motivado e aplicável conforme prática documentada; não invente dispensa normativa. |
| X | Termo de referência de estudos ambientais, licença cabível ou dispensa emitida pelo órgão competente. Registre fase e validade impressa; verifique abrangência do perfil alterado. |
| XI | Regularidade perante fazendas estadual e municipal da sede e, quando aplicável, da localidade da instalação, conforme redação do art. 4º, XI. Considere art. 4º, §§ 6º e 7º. Não atribua ao art. 4º a Fazenda Nacional/FGTS. |
| XII | Parecer favorável da autoridade marítima sobre NORMAM-11/DPC, quando couber. Se a aplicabilidade não puder ser determinada, use `A conferir`, motivando. |

### Art. 6º da Resolução — Fazenda Nacional e FGTS

Verifique separadamente a regularidade perante a Fazenda Nacional e o FGTS. O art. 6º prevê emissão de certidão pela ANTAQ, sem prejuízo de juntada pela requerente, e notificação para normalização em 30 dias se houver irregularidade (§ 1º); o não atendimento implica arquivamento (§ 2º). Encaminhe a conclusão, datas e evidências à S3 para controle e desfecho. Não classifique como inciso XI do art. 4º.

### Item XIII — exigência complementar relativa à SPU

- O item XIII é uma linha complementar do formulário/setor, **fora da Res. ANTAQ nº 71/2022, art. 4º**, que termina no inciso XII.
- Verifique certidão/declaração de disponibilidade, instrumento de cessão ou documentação SPU aplicável quando houver área terrestre ou espelho d’água sob gestão da SPU. Diferencie isso do título do art. 4º, VII e da hipótese dos §§ 4º–5º.
- Se aplicável e ausente, registre `PENDENCIA_COMPLEMENTAR_SPU` e o acompanhamento necessário. **Não trate a ausência como impedimento à fase 1 ou à publicação no Diário Oficial**, conforme regra do setor. Não a inclua como pendência impeditiva na conclusão oficial da fase 1.
- Se não houver área sob gestão da SPU, classifique como `Não se aplica` com justificativa.

### § 3º do art. 4º — instalações com passageiros

Quando aplicável, verifique áreas dimensionadas, segregação ou procedimento de operação não simultânea, plataforma/guarda-corpo/piso/rampas seguros, venda de passagens/atendimento, espera abrigada e assentos, sanitários/lixeiras, acessibilidade/prioridade e projeto de iluminação/sinalização/comunicação. Registre evidência para cada elemento material.

### Conferências aritméticas, cadastrais e de validade

- **Ficha 34+35:** calcule e registre `34 = [valor] m² + 35 = [valor] m² = [soma] m²; total declarado = [valor] m²`. Se divergir, use `Diligência`; se fechar, `Item atendido`. Só use `A conferir` se os números forem ilegíveis/mascarados.
- **Áreas:** triangule título, Memorial e plantas, discriminando parcelas/áreas comparadas e diferença. Ignore valores explicitamente mascarados; marque o cruzamento afetado `A conferir`.
- **Cadastro:** compare razão social, CNPJ, endereço e dados da instalação entre Ficha, CNPJ e ato societário. Divergência material explícita gera `Diligência`.
- **Declaração:** validade de 18 meses contados da **emissão** (não da assinatura), segundo Portaria, art. 6º, § 2º; alteração de perfil, art. 29, § 2º. Registre data de emissão e data-limite.
- **Demais certidões/licença:** use a validade impressa; não aplique prazo genérico de 18 meses. Considere art. 4º, § 6º, da Resolução para as certidões dos incisos XI e XII e outras obtidas pela ANTAQ: não exija atualização durante a tramitação quando abrangidas pela regra.
- Certidão positiva com efeitos de negativa: descreva exatamente e encaminhe eventual decisão interpretativa ao servidor; não converta automaticamente em irregularidade sem regra aplicável.
- Dados mascarados: reproduza marcadores sem tentar inferi-los e não faça cruzamento sobre valores ocultos.

## 7. Ausência da Declaração e roteamento

1. Faça busca por todo o conteúdo documental relevante e anexos/pacotes plausíveis, incluindo documentos com nomes genéricos.
2. Se a Declaração for encontrada, registre evidência e validade e não acione arquivamento por ausência.
3. Se a ausência estiver confirmada após busca integral, marque o inciso I como `Item não atendido` e emita o gatilho `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA` para a S3. A S3 emitirá imediatamente a minuta de arquivamento conforme regra do setor e modelo `arquivamento_declaracao.md`; não aguarde prazo de 30 dias nesse gatilho.
4. Se restar pacote plausível sem acesso, a ausência não está confirmada: marque `A conferir`, informe a limitação e não emita o gatilho de arquivamento.

## 8. Relatório obrigatório de saída

Entregue à S3 um relatório estruturado contendo:

```yaml
processo: "[protocolo]"
modo: "A | B | reanálise isolada"
linha_de_base: "[SEI/data do último Check-List e notificação, ou não há]"
controle_temporal:
  data_notificacao: "[data ou não localizada]"
  data_ciencia: "[data ou não localizada]"
  prazo_e_data_limite: "[prazo/datas ou não calculável]"
  ultimo_documento_requerente: "[SEI/data de inclusão ou nenhum]"
  documento_novo_apos_notificacao: "sim | não | indeterminado"
  observacao: "[reanalise mesmo se juntada após prazo; sem alerta apenas por intempestividade]"
declaracao_adequacao:
  status: "ATENDIDA | AUSENTE_CONFIRMADA | A_CONFERIR"
  referencia: "[SEI/página, ou buscas e motivo da incerteza]"
  emissao: "[data]"
  validade_ate: "[data calculada ou não calculável]"
  gatilho: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA"
requisitos: "[tabela completa dos itens aplicáveis com status, constatação, evidência SEI/página]"
aritmetica_e_areas: "[operandos, somas e cruzamentos]"
artigo_6_fazenda_nacional_fgts: "[status, datas e evidências]"
item_xiii_spu_complementar: "[aplicável/não aplicável, status e evidência; não impede fase 1/publicação]"
documentos_e_paginas_lidos: "[registro integral por documento; faixas lidas]"
limitacoes: "[nenhuma ou lista precisa]"
```

Use o identificador `PENDENCIA_COMPLEMENTAR_SPU` se precisar de código interno. Não converta status complementar da SPU em pendência impeditiva da fase 1.