# SUBSKILL 2 — LEITURA INTEGRAL, PAGINAÇÃO E ANÁLISE DE MÉRITO

> Responsável pela leitura completa da faixa acessível dos documentos relevantes e pelo enquadramento fático-normativo de TUP, ETC, IP4, IPTur e alterações de perfil.

## 1. Ferramentas e parâmetro de corte

- Use `documentos_listar` e `documento_ler`.
- **Parâmetro obrigatório de tamanho:** Use **`tamanho: 15000`** (abaixo do teto de corte de ~18.000 caracteres da ferramenta) e lotes de **1 a 3 documentos curtos** ou **1 documento longo por chamada**.
- Nunca escreva, assine ou tramite no SEI.

## 2. Controle temporal e Reanálise (Modo B)

1. Identifique a última Notificação/Ofício, ciência, prazo e eventuais pedidos/decisões de prorrogação.
2. Identifique o último Check-List como **linha de base**.
3. Identifique documentos juntados pelo requerente após a linha de base/notificação pela **data de inclusão SEI** (não pela data impressa no PDF).
4. Recibos de protocolo e termos de encaminhamento não são resposta documental; petições de resposta e anexos técnicos são obrigatórios.
5. Documento novo juntado após o prazo deve ser reanalisado normalmente; intempestividade isolada não gera alerta nem arquivamento.

## 3. Filtro de relevância pré-leitura

Classifique todos os itens da árvore antes de ler:
- **Ler para mérito:** requerimento/petição, Ficha Cadastral, CNPJ, atos societários, Declaração, Memorial, plantas, títulos/contratos, licenças/pareceres ambientais, consultas (aduana, município, Marinha), certidões fiscais, documentos SPU, anexos técnicos.
- **Ler para prazo/contexto:** Notificação/Ofício, prova de ciência, pedido/decisão de prorrogação, resposta do requerente, Check-List anterior.
- **Ignorar no mérito:** Recibo Eletrônico de Protocolo, Termo de Encaminhamento, despacho de mero expediente sem decisão, comprovante de ciência quando desnecessário à contagem.
  - **Regra de integridade:** Documento listado como ignorado **não pode** ser citado como evidência de requisito. Se contiver informação útil (ex.: ciência ou dado SPU), reclassifique-o e leia-o.

## 4. Algoritmo de paginação exaustiva

1. Inicie cada documento relevante com `inicio: 0, tamanho: 15000`.
2. Conte os **caracteres efetivamente recebidos do texto do documento** (descontando metadados do envelope e eventual aviso de corte).
3. Se houver aviso de corte (`[..., resultado cortado: X caracteres omitidos...]`), faça nova chamada para o mesmo SEI com `inicio = offset_anterior + caracteres_efetivamente_recebidos` e `tamanho: 15000`.
4. **Critério de fim real:** Só marque `final_real_atingido: sim` quando: (a) a resposta vier **sem aviso de corte** e com conteúdo menor que 15.000 caracteres, ou (b) o offset seguinte retornar vazio/EOF.
5. **Trava de loop:** Se dois offsets consecutivos retornarem exatamente o mesmo bloco sem aviso de fim, interrompa aquele SEI, registre a limitação técnica e marque `final_real_atingido: indeterminado`.
6. **Capas ZIP e arquivos externos:** Se o retorno tiver < 300 caracteres indicando apenas capa/link de `.zip` ou arquivo externo não suportado, **não tente ler novamente**; registre o SEI e marque o requisito dependente como `A conferir`.
7. **Mascaramento e OCR parcial:** Nunca interrompa a paginação por marcadores (`[PESSOA_1]`, `[TELEFONE_1]`) ou falha de OCR em páginas intermediárias. Continue até o fim real e delimite o `A conferir` apenas ao dado/página afetados.
8. **Regra de declaração de leitura:** Só use a expressão **"leitura integral"** se todos os documentos relevantes tiverem `final_real_atingido: sim`. Caso contrário, registre **"leitura parcial"** e liste os SEIs incompletos.

## 5. Situações permitidas e lista fechada de `A conferir`

Use exclusivamente: `Item atendido`, `Item não atendido`, `Diligência`, `A conferir`, `Não se aplica`.

- **`A conferir` (lista fechada de motivos):** Só é admitido por:
  1. Conteúdo inacessível, sigiloso/restrito ou erro técnico de extração;
  2. Capa de `.zip` ou arquivo externo não extraível;
  3. Planta, mapa, assinatura ou imagem que exija conferência visual;
  4. OCR parcial ou ilegibilidade de trecho específico;
  5. Dado específico oculto por mascaramento que impeça cruzamento.
- **Proibição expressa:** É **proibido** usar `A conferir` com justificativas como *"conferir compatibilidade"* ou *"verificar suficiência"* quando o texto foi lido e está legível. Nesses casos, decida objetivamente entre `Item atendido` e `Diligência`.

## 6. Regras específicas por requisito (Matriz S0 § 2)

- **Item I (Declaração):** Validade = **18 meses desde a data de emissão** (Portaria nº 1.064/2020, art. 6º, § 2º; alteração, art. 29, § 2º). Calcule e registre mesmo se houver ressalva de escopo/razão social. Só emita `DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA` se todos os documentos plausíveis tiverem `final_real_atingido: sim`.
- **Item II (Ficha Cadastral):** Extraia todos os dados de identificação (sede, instalação, endereço, CEP, contatos, e-mail, coordenadas) para a S3. Exiba `34 = [X] m² + 35 = [Y] m² = [Soma] m² vs. Total declarado = [Z] m²`. Se houver sobreposição expressamente declarada para evitar dupla contagem, explique e classifique `Item atendido` (sem diligência aritmética).
- **Item III (Ato Constitutivo):** Verifique registro vigente; em S.A., ata de eleição e mandato. Registre como observação complementar eventual restrição de poderes do signatário.
- **Itens V.a–V.h:** Em terminal já construído, V.f pode ser `Não se aplica` (motivado) e V.h exige valor comercial + ART/RRT (art. 4º, § 2º).
- **Item VII vs. Item XIII (SPU):** VII trata do título de propriedade/posse/cessão de direito real (art. 4º, VII e §§ 4º–5º). **Item XIII** é linha complementar fora do art. 4º para documentação/disponibilidade SPU (terra ou espelho d'água da União); sua pendência **não impede Fase 1/DOU**.
- **Item IX vs. Item XII:** **IX** = consulta/alvará ao **Poder Público Municipal** (verifique se o endereço do alvará corresponde ao terminal e não apenas ao escritório). **XII** = parecer da **Autoridade Marítima** (NORMAM-11/DPC).
- **Item X (Ambiental):** Registre fase (LP/LI/LO/TR/dispensa), validade impressa, condicionantes pendentes e compatibilidade do objeto licenciado com o pedido.
- **Item XI vs. Art. 6º:** **XI** = apenas Fazendas **Estadual e Municipal**. **Art. 6º** = **Fazenda Nacional e FGTS** (linha própria).
- **Art. 4º, § 3º:** Requisitos de passageiros (`Não se aplica` motivado para TUP/ETC exclusivamente de carga).
- **Triangulação de áreas e validades:** Registre divergências de área entre título, Ficha Cadastral e plantas (ex.: área de acostagem/espelho d'água) e alerte certidões/licenças que vencem em até **30 dias** da data da análise.

## 7. Relatório estruturado obrigatório à S3

```yaml
processo: "[protocolo]"
modo: "A | B"
coerencia_inicial:
  assunto_vs_objeto: "[compatível | divergente: detalhar]"
  empreendimento_nas_licencas: "[compatível | divergente: detalhar]"
identificacao_ficha:
  requerente: "[razão social]"
  sede_endereco_cep: "[endereço e CEP completos ou a preencher]"
  sede_contato_email: "[nome/cargo, tel e e-mail ou a preencher]"
  instalacao_nome: "[nome]"
  instalacao_endereco_cep: "[endereço e CEP completos ou a preencher]"
  instalacao_contato_email: "[nome/cargo, tel e e-mail ou a preencher]"
  coordenadas_2_pontos: "[coordenadas ou situação]"
controle_temporal:
  linha_de_base: "[SEI/data | inexistente]"
  notificacao_ciencia_prazo: "[SEI, datas e prazo | não localizada]"
  documento_novo_apos_notificacao: "sim (SEI/data) | não"
declaracao_adequacao:
  status: "ATENDIDA | AUSENTE_CONFIRMADA | A_CONFERIR"
  referencia: "[SEI/página]"
  emissao: "[data]"
  validade_ate: "[data = emissão + 18 meses]"
  gatilho: "nenhum | DECLARACAO_AUSENTE_CONFIRMADA_POR_LEITURA"
requisitos_22_linhas:
  - item: "[I até XIII — complementar]"
    situacao: "Item atendido | Item não atendido | Diligência | A conferir | Não se aplica"
    motivo_a_conferir: "[somente se A conferir: item da lista fechada da §5]"
    constatacao: "[fato, cálculo e referência]"
    sei_paginas: "[SEI/página]"
calculos_e_alertas:
  ficha_34_35: "34 = [X] m² + 35 = [Y] m² = [soma] m² vs. total declarado = [Z] m²"
  sobreposicao: "[explicação | não declarada]"
  triangulacao_areas: "[comparação título x Ficha x plantas]"
  alertas_validade_30_dias: "[certidões/licenças a vencer em <= 30 dias | nenhum]"
documentos_ignorados_filtro:
  - "[SEI — tipo — motivo]"
documentos_nao_extraidos_ou_zip:
  - "[SEI — motivo técnico/ZIP — requisito afetado]"
log_paginacao:
  - sei: "[número]"
    titulo: "[título]"
    chamadas_e_faixas: "[ex.: 2 chamadas: 0–14980, 14980–23100]"
    caracteres_lidos: "[total]"
    corte: "sim | não"
    final_real_atingido: "sim | não | indeterminado"
```
