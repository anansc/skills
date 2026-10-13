---
name: check-list-habilitacao-outorga
description: "Verifica a conformidade documental de processos de outorga de autorização e de alteração/acréscimo de perfil de carga de instalações portuárias (TUP, ETC, IP4 e IPTur) à luz do art. 4º da Resolução ANTAQ nº 71/2022 e gera o Check-List de Habilitação — Anexo II em .docx no padrão da GOA. USE ESTA SKILL sempre que o usuário pedir para \"verificar a documentação\", \"fazer/montar o check-list\", \"check-list de habilitação\", \"analisar o requerimento de outorga\", \"conferir se a documentação está completa\", \"habilitar/instruir o processo\", \"Anexo II\", ou tratar de acréscimo ou alteração de perfil de carga de TUP/ETC/IP4/IPTur — mesmo sem citar \"check-list\" — ou quando indicar uma pasta de processo com documentos SEI a conferir. NÃO use para redigir pareceres/notas técnicas com voz autoral (skill estilo-gabriel) nem para consultar dados do Estatístico Aquaviário."
---

---
name: check-list-habilitacao-outorga
description: >-
  Verifica a conformidade documental de processos de outorga de autorização e de
  alteração/acréscimo de perfil de carga de instalações portuárias (TUP, ETC, IP4 e
  IPTur) à luz do art. 4º da Resolução ANTAQ nº 71/2022, e gera o Check-List de
  Habilitação — Anexo II em .docx no padrão da GOA. USE ESTA SKILL sempre que o
  usuário pedir para "verificar a documentação", "fazer o check-list", "check-list
  de habilitação", "analisar o requerimento de outorga", "conferir se a documentação
  está completa", "habilitar/instruir o processo", "Anexo II", ou tratar de acréscimo
  ou alteração de perfil de carga de TUP/ETC/IP4/IPTur — mesmo que não cite "check-list"
  explicitamente. Também acione quando o usuário indicar uma pasta de processo com
  documentos SEI a conferir. NÃO use para redigir pareceres/notas técnicas com voz
  autoral (isso é da skill estilo-gabriel), nem para consultar dados do Estatístico
  Aquaviário.
---

# Check-List de Habilitação — Anexo II (Res. ANTAQ 71/2022)

## 1. O que esta skill faz

Instrui a fase de **habilitação documental** de um requerimento de outorga (ou de
alteração/acréscimo de perfil de carga) de instalação portuária privada, verificando
item a item a documentação do art. 4º da Resolução ANTAQ nº 71/2022 e produzindo o
**Check-List de Habilitação — Anexo II** em `.docx`, no mesmo padrão dos modelos da GOA.

O trabalho é de **verificação de conformidade documental objetiva** — presença/ausência,
legibilidade, campos obrigatórios (assinatura, nº CREA/CAU, validade, datas, datum) e
coerência entre documentos — não de análise de mérito de engenharia, capacidade ou
viabilidade locacional (que pertencem a fases posteriores).

## 2. Princípios que orientam a verificação

Estes princípios não são retóricos: eles definem *como* preencher cada item.

- **Ceticismo profissional.** A informação do requerente é ponto de partida, não de
  chegada. Confira o que a peça afirma contra o documento-fonte (ex.: se o memorial diz
  "coordenadas em SIRGAS2000", abra a planta e confirme; se a certidão é "válida", cheque
  a data). Registre "Item atendido" apenas quando a evidência corrobora.
- **Materialidade.** Calibre a profundidade ao peso do item. Título de propriedade,
  poligonal georreferenciada, ART/RRT e licença ambiental são de alta materialidade e
  merecem verificação minuciosa; itens formais (ficha cadastral, CNPJ) resolvem-se com
  checagem de presença.
- **Motivação e proporcionalidade.** Toda constatação de não atendimento deve dizer *o
  que* falta e *por quê* (âncora no inciso/alínea do art. 4º). A resposta — habilitar,
  ressalvar ou notificar — deve ser proporcional ao que efetivamente falta.
- **Objetividade e independência.** A manifestação representa o interesse público. Avalie
  pelo mérito documental, não pela conveniência do requerente.

## 3. Entrada: a pasta do processo

O usuário aponta uma **pasta** (tipicamente em *Projetos*) contendo os documentos do
processo. Os arquivos seguem a convenção de nome:

```
[N]-XXXXXXX_Descrição.ext
```

- `N` (entre colchetes) = ordem do documento na árvore do SEI;
- `XXXXXXX` = **número SEI de 7 dígitos do documento** — é este número que se cita;
- `Descrição` = rótulo curto do documento.

Exemplo: `[14]-2986097_Consulta.pdf` → documento **SEI 2986097**.

**Passos de leitura da pasta:**
1. Liste os arquivos e extraia de cada nome o nº SEI (os 7 dígitos após o colchete).
2. Leia o conteúdo de cada documento (PDF/imagem/planilha). Para PDFs, extraia o texto;
   para plantas, ARTs, certidões e tabelas em imagem, leia a imagem diretamente.
3. Monte um índice interno {nº SEI → tipo de documento → o que ele comprova}. Esse índice
   é a base para preencher a coluna direita do check-list.

## 4. Regras de citação e de tratamento de imagens

- **Sempre remeta ao nº SEI** ao referir qualquer documento (ex.: "consta no SEI 2843933").
  Quando o documento tiver paginação, acrescente a folha: "SEI 2843933, fls. 11". Se o
  documento estiver em processo distinto, cite também o processo (ex.: "processo SEI
  50300.001201/2015-11, doc. SEI 0056725").
- **Imagens nunca são coladas no check-list.** Quando um item depende de informação que
  está numa imagem (planta, ART, carimbo, tabela de coordenadas), **remeta ao documento
  SEI onde a imagem se encontra** e descreva a constatação objetiva por escrito.
- **Sinalize a confirmação humana.** Em itens de alta materialidade verificados por
  imagem (fechamento da poligonal, datum, legibilidade de ART, validade de certidão em
  digitalização ruim), registre a constatação e marque o item para conferência humana
  (campo `obs_humana` no JSON). A leitura de imagem apoia a triagem; não substitui perícia
  nem medição geodésica.
- **Números longos** (CNPJ, matrícula, coordenadas) são transcritos com cautela e
  sinalizados para conferência quando a fonte for imagem de baixa qualidade.

## 5. Fluxo de trabalho

1. **Identifique o tipo de instalação e o tipo de pedido** (ver seção 6). Isso define
   quais itens do art. 4º se aplicam e o texto do cabeçalho.
2. **Preencha o bloco de identificação** a partir do requerimento e da ficha cadastral
   (SEI de cada um citado).
3. **Percorra a matriz do art. 4º** (seção 7), item a item. Para cada um: localize o(s)
   documento(s)-fonte, verifique os critérios objetivos, redija a constatação com o nº SEI
   e atribua o veredito: **Item atendido** / **Item não atendido** / **Não se aplica**.
   Use **Diligência/Parcial** quando o documento existe mas falta um elemento sanável.
4. **Escreva a conclusão** (seção 8) de forma **enxuta**: abertura padrão seguida apenas da
   lista de pendências que enseja notificação (art. 5º; art. 6º quanto às certidões federais),
   **sem** relacionar itens atendidos nem acrescentar observações finais.
5. **Monte o Anexo I** (cadeia dominial) quando houver múltiplos títulos de propriedade
   (seção 9).
6. **Gere o `.docx`** com o gerador da seção 10 e salve na pasta do processo.

## 6. Modo adaptativo — tipo de instalação e tipo de pedido

Detecte, a partir do assunto/requerimento/ficha cadastral:

**Tipo de instalação** (art. 2º da Res. 71/2022):
- **TUP** — movimentação e/ou armazenagem de cargas; fora do porto organizado.
- **ETC** — **exclusivamente transbordo** de cargas (navegação interior/cabotagem); não há
  armazenagem — as alíneas de armazenagem do memorial tendem a "Não se aplica".
- **IP4** — passageiros ou cargas em navegação interior. Se movimentar passageiros, aplica-se
  o **§3º** do art. 4º (requisitos de terminal de passageiros).
- **IPTur** — embarque/desembarque/trânsito de passageiros de turismo; **sempre** aplica-se
  o **§3º** do art. 4º.

**Tipo de pedido:**
- **Autorização nova (construção/exploração)** — verifica-se o conjunto completo do art. 4º.
- **Alteração/acréscimo de perfil de carga** — a instalação já é autorizada. Documentos
  estruturais (atos constitutivos, CNPJ, título de propriedade, plantas, acessos) costumam
  ser **reaproveitados do processo de origem**: registre "consta no processo SEI …
  (reaproveitado)" e concentre a verificação no que muda com o novo perfil — **memorial
  descritivo do novo perfil, estimativa de movimentação atualizada, adequação da estrutura
  ao perfil, licença ambiental que abranja o novo perfil, e eventual investimento/ART** se
  houver obra. Quando não há obra nem ampliação, cronograma (alínea f) e valor/ART do
  investimento (alínea h) ficam "Não se aplica", com a devida motivação.

## 7. Matriz de verificação — art. 4º da Res. 71/2022

Para cada item, a coluna esquerda do check-list reproduz o texto do inciso/alínea; a
direita traz a constatação (com SEI) e o veredito. Critérios objetivos a verificar:

**I — Declaração de adequação** às diretrizes do planejamento e políticas do setor
portuário, emitida **pelo poder concedente** (SNPTA/MPor) — exigência do **art. 4º, I, da
Res. ANTAQ nº 71/2022**. Confira: emissor correto; e a **data de validade**, que é de **18
(dezoito) meses contados da emissão** (data de assinatura) da declaração, nos termos do
**art. 6º, §2º, da Portaria MINFRA nº 1.064/2020** (art. 29, §2º, no caso de alteração de
perfil de carga). **Calcule e registre expressamente a data-limite de validade** (data de
assinatura + 18 meses) e confronte-a com a data da análise: se já vencida, é não atendimento.
*Alta materialidade.*

**II — Ficha cadastral** preenchida conforme o modelo divulgado pela ANTAQ. Presença e
preenchimento completo.

**III — Ato constitutivo / estatuto / contrato social** em vigor, **registrado na junta
comercial**; em S.A., acompanhado da comprovação de eleição dos administradores com
**mandato vigente**, registrados no órgão competente. Confira registro e vigência.

**IV — CNPJ** da **sede** e da **instalação portuária**. Confira ambos (matriz e filial/
instalação, quando constituída sob forma de filial).

**V — Memorial descritivo**, contendo:
- **a) Planta de situação** com a poligonal georreferenciada, discriminando separadamente
  área em terra, área sobre a água, berços de atracação, bacia de evolução e canal de
  acesso; pontos em **graus decimais ou UTM — SIRGAS2000**; **planilha eletrônica editável**
  de coordenadas; formatos PDF/KML/KMZ/SHP; identificação das vias de acesso aquaviário e
  terrestre e dos empreendimentos adjacentes; escala, legendas e cotas; **com ART ou RRT**
  (nome, assinatura e nº de registro do responsável técnico no CREA/CAU). *Alta materialidade;
  imagem → remeter ao SEI da planta e sinalizar datum/fechamento para conferência.*
- **b) Descrição de todos os acessos** — aquaviário (marítimo/fluvial/lacustre) e terrestre
  (rodoviário/ferroviário/dutoviário), existentes e a construir.
- **c) Descrição do terminal** — instalações de acostagem, berços e finalidades, armazenagem,
  circulação, gerais e de suprimentos, com destinações e **capacidades**. (Em ETC, não há
  armazenagem. Em compartilhamento de acostagem, exigir também o contrato do art. 43,
  parágrafo único — §1º.)
- **d) Embarcação-tipo** por berço: tipo, comprimento, boca, calado e porte bruto (TPB).
- **e) Principais equipamentos e dispositivos** de carga/descarga e movimentação; quantidade,
  capacidade e utilização, quando couber.
- **f) Cronograma físico e financeiro** de implantação — **exceto quando a instalação já
  estiver construída** (nesse caso, "Não se aplica", motivando).
- **g) Estimativa de movimentação** de cargas e/ou passageiros. No acréscimo de perfil, deve
  contemplar o(s) novo(s) perfil(is).
- **h) Valor global do investimento**, **com ART ou RRT** do responsável pelo orçamento
  (nome, assinatura, nº CREA). Inclui infra e superestrutura, aquisição de terrenos e, se já
  construída, o valor comercial (§2º).

**VI — Planta de locação** (PDF/KML/KMZ/SHP) das instalações existentes e projetadas; escala
e cotas; **demarcação das áreas a outorgar** constantes da certidão de propriedade/posse;
**com ART ou RRT** (CREA/CAU). *Alta materialidade.*

**VII — Título de propriedade** / inscrição de ocupação / certidão de aforamento / contrato
de cessão sob regime de direito real / outro instrumento que assegure **uso e fruição do
terreno**. Para áreas da União, admite-se certidão da **SPU** de disponibilidade (§4º), caso
em que o contrato de adesão pode ter **cláusula suspensiva** (§5º). Havendo cadeia dominial
(vários títulos), consolide no **Anexo I**. *Alta materialidade; verifique o fechamento da
cadeia entre a área da certidão e a área demarcada na planta.*

**VIII — Consulta à autoridade aduaneira.**

**IX — Consulta ao poder público municipal.** (Pode ser diferida à vistoria de TLO em casos
específicos; motive.)

**X — Licenciamento ambiental**: termo de referência emitido pelo órgão licenciador, **ou**
licença ambiental cabível, **ou** dispensa de licença. Confira **validade** e, no acréscimo
de perfil, **se a licença abrange o novo perfil de carga**. *Alta materialidade.*

**XI — Regularidade fiscal e trabalhista.** O modelo da GOA desdobra este item em linhas
próprias; verifique e registre cada uma, **nesta ordem**, com **validade** e nº SEI:
- **a) Fazenda Nacional** — Certidão conjunta de débitos federais.
- **b) Fazenda Estadual** da sede (e da localidade da instalação, quando aplicável).
- **c) Fazenda Municipal** da sede (e da localidade da instalação, quando aplicável).
- **d) FGTS** — Certificado de Regularidade do FGTS (CRF).

As certidões de **Fazenda Nacional e FGTS** são as do **art. 6º**, **emitidas pela própria
ANTAQ** (sem prejuízo de juntada pela requerente); ainda assim devem figurar como linhas
explícitas no check-list. As certidões estadual/municipal podem ser substituídas por
**declaração do representante legal** (§7º) e não precisam ser atualizadas durante a
tramitação (§6º). Havendo irregularidade fiscal federal/FGTS, aplica-se o **art. 6º, §§1º e
2º** (notificação em 30 dias, sob pena de arquivamento).

**XII — Parecer favorável da autoridade marítima** quanto à **NORMAM-11/DPC** (obras sob,
sobre e às margens das águas jurisdicionais; ordenamento do espaço aquaviário e segurança da
navegação), **quando couber**.

**XIII — Certidão/Declaração de Disponibilidade da SPU** — Certidão/Declaração de
Disponibilidade ou contrato de cessão de uso onerosa emitido pela **SPU** em relação ao uso
das **áreas de propriedade da União** (espelho d'água e/ou terrenos da União). Aplica-se
**quando o empreendimento ocupar áreas/águas da União**; decorre dos **§§4º e 5º do art. 4º**
(admite-se a certidão da SPU no lugar do título, com possível cláusula suspensiva no contrato
de adesão) e do **§2º do art. 15** (certidão declaratória de disponibilidade do espaço físico
em águas públicas). Verifique a presença e a pertinência da área declarada; sua ausência é
não atendimento de alta materialidade quando há uso de área da União. Não confundir com o item
VII (uso e fruição do terreno em terra). *Alta materialidade.*

**§3º — Instalações de passageiros (IPTur e IP4 de passageiros).** O memorial deve ainda
contemplar: áreas dimensionadas para os fluxos; segregação (ou uso compartilhado com
separação física / operação não simultânea) entre passageiros e carga; plataforma com
guarda-corpo, piso antiderrapante e rampas/transição bordo-terra seguras; instalações de
venda de passagens e atendimento; áreas de espera abrigadas com assentos; sanitários e
lixeiras suficientes; **acessibilidade** (PcD, idosos, gestantes, lactantes e pessoas com
crianças de colo); e projeto de iluminação, sinalização e comunicação.

> Regra geral de veredito: **atendido** quando a evidência (com SEI) corrobora o requisito;
> **não atendido** quando o documento falta ou não cumpre o requisito (diga o que falta,
> ancorado no inciso/alínea); **não se aplica** quando o requisito é logicamente afastado
> pelo tipo de instalação/pedido (motive sempre); **diligência/parcial** quando existe, mas
> falta elemento sanável.

## 8. Conclusão

A conclusão é **enxuta e objetiva**: um parágrafo de abertura seguido **apenas** da lista de
**pendências / não atendimentos**. **Não** relacione os itens já atendidos nem acrescente
observações, ressalvas ou registros finais — por exemplo, pontos já sanados/esclarecidos no
curso da instrução, comentários sobre a competência da ANTAQ para emitir as certidões
federais/FGTS, as faculdades dos §§ do art. 6º ou a eventual cláusula suspensiva do contrato
de adesão. O que consta como atendido já está demonstrado na matriz item a item; a conclusão
existe para deflagrar o saneamento.

**Estrutura:**

1. **Abertura** (padrão): *"Da verificação da documentação apresentada, constata-se que o
   requerimento não atende integralmente aos requisitos do art. 4º da Resolução ANTAQ nº
   71/2022, devendo a requerente ser notificada a promover as adequações no prazo de 30
   (trinta) dias, sob pena de arquivamento (art. 5º, parágrafo único)."* Havendo
   irregularidade fiscal federal/FGTS entre as pendências, some a remissão ao **art. 6º, §§1º
   e 2º** (mesmo prazo de 30 dias, sob pena de arquivamento).

2. **Pendências / não atendimentos**: lista objetiva, uma por item, cada qual ancorada no
   inciso/alínea do art. 4º e com o nº SEI pertinente, dizendo *o que* falta. Nada além disso.

Caso **não haja pendências**, a abertura registra que a documentação está **habilitada/apta**
e a conclusão se encerra aí, sem observações adicionais.

## 9. Anexo I — cadeia dominial (quando aplicável)

Quando o item VII envolver vários títulos de propriedade, consolide-os em tabela com as
colunas: **Item · Tipo · Emissor · Data · Titular da propriedade · Matrícula/Registro nº ·
Validade · Área (m²) · SEI**. Verifique se a soma das áreas e a titularidade fecham com a área
demarcada na planta de locação (item VI).

## 10. Geração do `.docx`

O documento de saída é montado por um gerador Python que recebe um **JSON** com o conteúdo do
check-list e produz o `.docx` no padrão da GOA (título institucional, bloco de identificação,
tabela de itens com veredito colorido, conclusão e Anexo I). Isso garante formatação
consistente a cada uso.

**Esquema do JSON** (todos os campos ausentes viram vazio):

```json
{
  "cabecalho": {
    "data_analise": "", "protocolo": "SEI ....... de DD/MM/AAAA",
    "publicacao_sitio": "", "processo": "50300....../AAAA-XX", "assunto": "",
    "tipo_instalacao": "TUP|ETC|IP4|IPTur", "tipo_pedido": "",
    "requerente_nome": "", "requerente_endereco": "", "requerente_cep": "",
    "requerente_cnpj": "", "requerente_contato": "", "requerente_tel": "",
    "requerente_email": "", "instalacao_nome": "", "instalacao_endereco": "",
    "instalacao_cep": "", "instalacao_cnpj": "", "instalacao_contato": "",
    "instalacao_tel": "", "instalacao_email": "",
    "coordenadas": ""
  },
  "itens": [
    {"secao": true, "titulo": "V — Memorial descritivo (SEI .......)"},
    {"num": "I", "titulo": "texto do inciso", "analise": "constatação com SEI ......., fls. Y",
     "status": "Item atendido|Item não atendido|Não se aplica|Diligência",
     "obs_humana": "opcional — o que conferir manualmente"}
  ],
  "conclusao": {"resultado": "Documentação HABILITADA | Pendências — notificação (art. 5º)",
                "texto": "fundamentação"},
  "anexo_propriedade": {"incluir": false, "linhas": [
     {"item":"1","tipo":"","emissor":"","data":"","titular":"","registro":"","validade":"","area_m2":"","sei":""}
  ]}
}
```

> Itens com sub-alíneas (memorial descritivo; regularidade fiscal do inciso XI) são
> representados por uma linha `{"secao": true, ...}` de cabeçalho seguida das linhas
> `{"num": "XI.a", "titulo": "Fazenda Nacional — certidão conjunta de débitos federais", ...}`,
> `{"num": "XI.d", "titulo": "FGTS — CRF", ...}` etc. O item XIII
> (SPU) é uma linha `{"num": "XIII", ...}` incluída quando houver uso de áreas da União.

**Como gerar:** grave o script abaixo como `gerar_checklist_docx.py`, grave o JSON preenchido
como `dados.json` e execute `python3 gerar_checklist_docx.py dados.json "Check-List Habilitacao - <Processo>.docx"`.
Requer `python-docx` (instale com `pip install python-docx --break-system-packages` se necessário).
Salve o `.docx` na pasta do processo e apresente-o ao usuário.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""Gera o Check-List de Habilitacao (Anexo II) da GOA/ANTAQ em .docx a partir de JSON."""
import json, sys
from docx import Document
from docx.shared import Pt, RGBColor, Cm
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.table import WD_TABLE_ALIGNMENT
from docx.oxml.ns import qn
from docx.oxml import OxmlElement

VERDE=RGBColor(0x1F,0x6E,0x43); VERMELHO=RGBColor(0xB0,0x1C,0x2E)
LARANJA=RGBColor(0x9C,0x5A,0x00); CINZA=RGBColor(0x59,0x59,0x59); AZUL=RGBColor(0x1F,0x3B,0x73)

def _bg(cell,hexc):
    tcPr=cell._tc.get_or_add_tcPr(); shd=OxmlElement("w:shd")
    shd.set(qn("w:val"),"clear"); shd.set(qn("w:color"),"auto"); shd.set(qn("w:fill"),hexc)
    tcPr.append(shd)

def _txt(cell,text,bold=False,size=9,color=None,align=None):
    cell.text=""; p=cell.paragraphs[0]
    if align is not None: p.alignment=align
    for i,line in enumerate(str(text).split("\n")):
        if i>0: p.add_run().add_break()
        r=p.add_run(line); r.bold=bold; r.font.size=Pt(size)
        if color is not None: r.font.color.rgb=color
    return p

def _statuscolor(s):
    s=(s or "").lower()
    if "nao atendido" in s or "não atendido" in s: return VERMELHO
    if "nao se aplica" in s or "não se aplica" in s or "prejudicado" in s: return CINZA
    if "parcial" in s or "diligenc" in s or "diligênc" in s: return LARANJA
    return VERDE

def _larg(t,ws):
    t.autofit=False
    for row in t.rows:
        for i,w in enumerate(ws):
            if i<len(row.cells): row.cells[i].width=w

def titulo(doc,cab):
    tipo=cab.get("tipo_instalacao","TUP/ETC/IP4/IPTur")
    for txt,sz,b in [("AGÊNCIA NACIONAL DE TRANSPORTES AQUAVIÁRIOS",11,True),
        ("ANÁLISE DE REQUERIMENTO DE AUTORIZAÇÃO PARA INSTALAÇÃO PORTUÁRIA",11,True),
        (f"({tipo})",10,True),("CONSTRUÇÃO / EXPLORAÇÃO / ALTERAÇÃO",10,True),
        ("CHECK-LIST DE HABILITAÇÃO — ANEXO II",11,True)]:
        p=doc.add_paragraph(); p.alignment=WD_ALIGN_PARAGRAPH.CENTER
        r=p.add_run(txt); r.bold=b; r.font.size=Pt(sz)
    p=doc.add_paragraph(); p.alignment=WD_ALIGN_PARAGRAPH.CENTER
    r=p.add_run("Lei nº 12.815/2013 — Decreto nº 8.033/2013 — Resolução ANTAQ nº 71/2022 (arts. 4º a 6º)")
    r.italic=True; r.font.size=Pt(9); doc.add_paragraph()

def bloco(doc,cab):
    campos=[("Data da análise",cab.get("data_analise","")),
        ("Protocolo e data do requerimento",cab.get("protocolo","")),
        ("Publicação da íntegra no sítio da ANTAQ",cab.get("publicacao_sitio","")),
        ("Processo nº",cab.get("processo","")),("Assunto",cab.get("assunto","")),
        ("Nome da requerente",cab.get("requerente_nome","")),
        ("Endereço da sede",cab.get("requerente_endereco","")),
        ("CEP da sede",cab.get("requerente_cep","")),("CNPJ da sede",cab.get("requerente_cnpj","")),
        ("Contato na sede — cargo",cab.get("requerente_contato","")),
        ("Tel./Cel. do contato",cab.get("requerente_tel","")),
        ("E-mail do contato",cab.get("requerente_email","")),
        ("Nome da instalação",cab.get("instalacao_nome","")),
        ("Endereço da instalação",cab.get("instalacao_endereco","")),
        ("CEP da instalação",cab.get("instalacao_cep","")),
        ("CNPJ da instalação",cab.get("instalacao_cnpj","")),
        ("Contato na instalação — cargo",cab.get("instalacao_contato","")),
        ("Tel./Fax/Cel. do contato na instalação",cab.get("instalacao_tel","")),
        ("E-mail do contato na instalação",cab.get("instalacao_email","")),
        ("Coordenadas geográficas (2 pontos)",cab.get("coordenadas",""))]
    t=doc.add_table(rows=0,cols=2); t.style="Table Grid"; t.alignment=WD_TABLE_ALIGNMENT.CENTER
    for rot,val in campos:
        c=t.add_row().cells; _txt(c[0],rot,bold=True); _bg(c[0],"EEEEEE"); _txt(c[1],val)
    _larg(t,[Cm(6.5),Cm(10.5)]); doc.add_paragraph()

def itens(doc,its):
    t=doc.add_table(rows=0,cols=2); t.style="Table Grid"; t.alignment=WD_TABLE_ALIGNMENT.CENTER
    for it in its:
        if it.get("secao"):
            c=t.add_row().cells; a=c[0].merge(c[1])
            _txt(a,it.get("titulo",""),bold=True,size=9.5,color=AZUL); _bg(a,"DCE6F1"); continue
        c=t.add_row().cells; num=it.get("num",""); tit=it.get("titulo","")
        _txt(c[0], f"{num} — {tit}" if num else tit); _bg(c[0],"F5F5F5")
        c[1].text=""; p=c[1].paragraphs[0]; r=p.add_run(it.get("analise","")); r.font.size=Pt(9)
        st=it.get("status","")
        if st:
            p2=c[1].add_paragraph(); rr=p2.add_run(st); rr.bold=True; rr.font.size=Pt(9); rr.font.color.rgb=_statuscolor(st)
        if it.get("obs_humana"):
            p3=c[1].add_paragraph(); rr=p3.add_run("⚠ "+it["obs_humana"]); rr.italic=True; rr.font.size=Pt(8); rr.font.color.rgb=LARANJA
    _larg(t,[Cm(7.5),Cm(9.5)]); doc.add_paragraph()

def conclusao(doc,cc):
    p=doc.add_paragraph(); r=p.add_run("CONCLUSÃO"); r.bold=True; r.font.size=Pt(11)
    t=doc.add_table(rows=1,cols=1); t.style="Table Grid"; cell=t.rows[0].cells[0]
    res=cc.get("resultado",""); _txt(cell,res,bold=True,size=10,color=_statuscolor(res))
    if cc.get("texto"):
        for l in cc["texto"].split("\n"):
            pp=cell.add_paragraph(); rr=pp.add_run(l); rr.font.size=Pt(9)
    doc.add_paragraph()

def anexo(doc,ax):
    if not ax or not ax.get("incluir"): return
    p=doc.add_paragraph(); r=p.add_run("ANEXO I — CHECK-LIST DE DOCUMENTOS DE PROPRIEDADE APRESENTADOS")
    r.bold=True; r.font.size=Pt(10)
    cols=["Item","Tipo","Emissor","Data","Titular da propriedade","Matrícula/Registro nº","Validade","Área (m²)","SEI"]
    t=doc.add_table(rows=1,cols=len(cols)); t.style="Table Grid"
    for i,c in enumerate(cols): _txt(t.rows[0].cells[i],c,bold=True,size=8); _bg(t.rows[0].cells[i],"EEEEEE")
    for lin in ax.get("linhas",[]):
        cc=t.add_row().cells
        vals=[lin.get("item",""),lin.get("tipo",""),lin.get("emissor",""),lin.get("data",""),lin.get("titular",""),lin.get("registro",""),lin.get("validade",""),lin.get("area_m2",""),lin.get("sei","")]
        for i,v in enumerate(vals): _txt(cc[i],v,size=8)
    doc.add_paragraph()

def main():
    if len(sys.argv)<3: print("Uso: gerar_checklist_docx.py dados.json saida.docx"); sys.exit(1)
    dados=json.load(open(sys.argv[1],encoding="utf-8"))
    doc=Document(); doc.styles["Normal"].font.name="Calibri"; doc.styles["Normal"].font.size=Pt(9)
    cab=dados.get("cabecalho",{})
    titulo(doc,cab); bloco(doc,cab); itens(doc,dados.get("itens",[])); conclusao(doc,dados.get("conclusao",{})); anexo(doc,dados.get("anexo_propriedade"))
    p=doc.add_paragraph(); r=p.add_run("Minuta de trabalho — conferir e assinar no SEI."); r.italic=True; r.font.size=Pt(8); r.font.color.rgb=CINZA
    doc.save(sys.argv[2]); print("OK:",sys.argv[2])

if __name__=="__main__": main()
```

## 11. Verificação final (antes de entregar)

- Todo documento citado tem **nº SEI**; nenhuma imagem foi colada — apenas remissões.
- Os incisos I a XIII aplicáveis foram percorridos, incluindo o desdobramento fiscal do XI
  (**Fazenda Nacional**, Estadual, Municipal, **FGTS**) e o item **XIII (SPU)** quando houver
  uso de áreas da União.
- Cada "Item atendido" tem evidência que o corrobora; cada "não atendido"/"não se aplica"
  diz *o que falta e por quê*, ancorado no inciso/alínea do art. 4º.
- Itens de alta materialidade verificados por imagem estão sinalizados para conferência humana.
- A conclusão é coerente com os vereditos e, havendo pendência, invoca o art. 5º (e o art. 6º
  para o âmbito fiscal federal/FGTS).
- O `.docx` foi salvo na pasta do processo e apresentado ao usuário.

