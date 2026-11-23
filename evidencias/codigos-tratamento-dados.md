# Códigos de tratamento de dados (Google Colab)

> Evidência dos códigos em Python usados no Google Colab para tratar os dados do observatório. O código abaixo foi copiado dos notebooks versionados em [`notebooks/`](../notebooks/). Para rodar, abra o notebook no Colab e use *Ambiente de execução → Executar tudo*. · [voltar ao README](../README.md)

## Links para abrir no Colab

| Notebook | O que faz | Abrir |
|---|---|---|
| [`01_ETL_RAIS_SJC.ipynb`](../notebooks/01_ETL_RAIS_SJC.ipynb) | Lê o arquivo público `RAIS_ESTAB_PUB` (3,27 GB) em partes, filtra o município 354990 (São José dos Campos), padroniza os campos e gera os CSVs tratados. | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/01_ETL_RAIS_SJC.ipynb) |
| [`02_Base_PowerBI_SJC.ipynb`](../notebooks/02_Base_PowerBI_SJC.ipynb) | Junta a base RAIS tratada com a geocodificação do CEP, a região oficial, as descrições da CNAE 2.3 e as classificações pedidas pelo cliente, e gera `dados/RAIS_SJC_2024_PowerBI.csv`. | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/02_Base_PowerBI_SJC.ipynb) |

Notebook original da Sprint 1 no Google Drive da equipe: <https://colab.research.google.com/drive/1zOZJ0oXUY7QJlAMfuiMbI5g9EcBWSnMz?usp=sharing>

Os links "Abrir no Colab" carregam a versão do notebook que está no GitHub, então mostram sempre o código mais recente do repositório.

> Os textos explicativos de cada notebook são da sprint em que ele foi escrito. As pendências citadas no notebook 01 foram tratadas depois: o ano-base foi confirmado como 2024 (DEC-003, fechada) e a falta de identificação nominal segue registrada (DEC-004). Situação atual no [Log de Decisões](../docs/06-Decisoes-de-Dados.md).

## Índice

* [Notebook 01 — ETL da RAIS (Sprint 1)](#notebook-01--etl-da-rais-sprint-1)
* [Notebook 02 — Base única do Power BI (Sprint 2)](#notebook-02--base-única-do-power-bi-sprint-2)

---

## Notebook 01 — ETL da RAIS (Sprint 1)

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/01_ETL_RAIS_SJC.ipynb)

Lê o arquivo público `RAIS_ESTAB_PUB` (3,27 GB) em partes, filtra o município 354990 (São José dos Campos), padroniza os campos e gera os CSVs tratados.


**Projeto:** API — Fatec São José dos Campos · Curso de Logística
**Cliente:** CADI / Secretaria de Desenvolvimento Econômico de SJC
**Fonte de dados:** RAIS_ESTAB_PUB (Ministério do Trabalho e Emprego) — base nacional de estabelecimentos

Este notebook implementa o pipeline **ETL (Extract, Transform, Load)** que:

1. **Extract** — lê o arquivo bruto `RAIS_ESTAB_PUB.txt` de dentro do `.zip` nacional, em streaming (o arquivo tem ~3,27 GB descompactado e 12,6 milhões de linhas — não cabe inteiro na memória).
2. **Transform** — filtra apenas os estabelecimentos do município de São José dos Campos (código IBGE **354990**), limpa os campos (a base vem com espaçamento fixo) e segmenta os dados de acordo com os problemas já mapeados no Log de Decisões de Dados:
   - **DEC-001**: separa estabelecimentos com RAIS negativa (zero vínculos) dos ativos.
   - **DEC-002**: separa por tipo de estabelecimento (Cnpj, Caepf, Cno).
3. **Load** — grava os CSVs tratados, prontos para uso no Power BI.

> **Pendências conhecidas (não resolvidas pelo tratamento de dados):**
> - **DEC-003** — o arquivo bruto não possui nenhuma coluna de ano/competência. Aguardando confirmação do cliente.
> - **DEC-004** — o arquivo bruto não possui razão social nem CNPJ/CPF identificado. Aguardando decisão do cliente sobre fornecer base identificada.

### 0. Upload do arquivo bruto

Faça upload do arquivo `RAIS_ESTAB_PUB.zip` (baixado do portal da RAIS) quando solicitado abaixo.
Se preferir usar o Google Drive em vez do upload direto, comente a célula de upload e ajuste o caminho `INPUT_ZIP` manualmente.

```python
from google.colab import files

uploaded = files.upload()  # selecione o RAIS_ESTAB_PUB.zip
INPUT_ZIP = list(uploaded.keys())[0]
print(f"Arquivo carregado: {INPUT_ZIP}")
```

### 1. Configuração

```python
import zipfile
import csv
import io
import os
import json

# Código IBGE do município de São José dos Campos
SJC_CODE = "354990"

OUTPUT_DIR = "RAIS_SJC_tratado"
os.makedirs(OUTPUT_DIR, exist_ok=True)

# Índices (0-based) das colunas no arquivo bruto RAIS_ESTAB_PUB
IDX_MUNICIPIO = 14
IDX_RAIS_NEGATIVA = 12
IDX_QTD_VINC_ATIVOS = 7
IDX_TIPO_ESTAB_LABEL = 20

# Cabeçalho de saída (nomes de colunas normalizados, sem acento/espaço)
HEADER_OUT = [
    "Bairros_SP", "Bairros_Fortaleza", "Bairros_RJ", "CNAE20_Classe", "CNAE95_Classe",
    "Distritos_SP", "Qtd_Vinculos_CLT", "Qtd_Vinculos_Ativos", "Qtd_Vinculos_Estatutarios",
    "Ind_Atividade_Ano", "Ind_CEI_Vinculado", "Ind_Estab_Participa_PAT", "Ind_Rais_Negativa",
    "Ind_Simples", "Municipio", "Natureza_Juridica", "Regioes_Adm_DF", "CNAE20_Subclasse",
    "Tamanho_Estabelecimento", "Tipo_Estab_Codigo", "Tipo_Estab_Label", "UF", "IBGE_Subsetor",
    "CEP_Estab",
]
```

### 2. Extract + Transform + Load

O arquivo é processado **linha a linha em streaming** (sem descompactar tudo em disco e sem carregar tudo em memória), filtrando somente os registros de SJC e já gravando nos CSVs segmentados.

```python
paths = {
    "completo": os.path.join(OUTPUT_DIR, "RAIS_SJC_completo.csv"),
    "ativos": os.path.join(OUTPUT_DIR, "RAIS_SJC_ativos.csv"),
    "rais_negativa": os.path.join(OUTPUT_DIR, "RAIS_SJC_rais_negativa.csv"),
    "cnpj": os.path.join(OUTPUT_DIR, "RAIS_SJC_Cnpj.csv"),
    "caepf": os.path.join(OUTPUT_DIR, "RAIS_SJC_Caepf.csv"),
    "cno": os.path.join(OUTPUT_DIR, "RAIS_SJC_Cno.csv"),
}

files_out = {k: open(v, "w", encoding="utf-8", newline="") for k, v in paths.items()}
writers = {k: csv.writer(f) for k, f in files_out.items()}
for w in writers.values():
    w.writerow(HEADER_OUT)

stats = {
    "total_linhas_brutas": 0,
    "total_sjc": 0,
    "sjc_ativos": 0,
    "sjc_rais_negativa": 0,
    "sjc_cnpj": 0,
    "sjc_caepf": 0,
    "sjc_cno": 0,
    "sjc_outro_tipo": 0,
}

with zipfile.ZipFile(INPUT_ZIP) as zf:
    inner_name = zf.namelist()[0]
    with zf.open(inner_name) as raw:
        # A base pública da RAIS é distribuída em Latin-1 (ISO-8859-1), não em UTF-8
        text_stream = io.TextIOWrapper(raw, encoding="latin-1", newline="")
        reader = csv.reader(text_stream, delimiter=";")
        next(reader)  # descarta cabeçalho original

        for row in reader:
            stats["total_linhas_brutas"] += 1
            if len(row) < 24:
                continue

            municipio = row[IDX_MUNICIPIO].strip()
            if municipio != SJC_CODE:
                continue

            clean_row = [c.strip() for c in row]
            stats["total_sjc"] += 1
            writers["completo"].writerow(clean_row)

            # Segmentação DEC-001: RAIS negativa vs ativos
            rais_negativa = clean_row[IDX_RAIS_NEGATIVA]
            if rais_negativa == "1":
                writers["rais_negativa"].writerow(clean_row)
                stats["sjc_rais_negativa"] += 1
            else:
                writers["ativos"].writerow(clean_row)
                stats["sjc_ativos"] += 1

            # Segmentação DEC-002: tipo de estabelecimento
            tipo_label = clean_row[IDX_TIPO_ESTAB_LABEL]
            if tipo_label == "Cnpj":
                writers["cnpj"].writerow(clean_row)
                stats["sjc_cnpj"] += 1
            elif tipo_label == "Caepf":
                writers["caepf"].writerow(clean_row)
                stats["sjc_caepf"] += 1
            elif tipo_label == "Cno":
                writers["cno"].writerow(clean_row)
                stats["sjc_cno"] += 1
            else:
                stats["sjc_outro_tipo"] += 1

for f in files_out.values():
    f.close()

stats["pct_rais_negativa"] = round(100 * stats["sjc_rais_negativa"] / stats["total_sjc"], 2) if stats["total_sjc"] else 0

with open(os.path.join(OUTPUT_DIR, "estatisticas_etl.json"), "w", encoding="utf-8") as f:
    json.dump(stats, f, ensure_ascii=False, indent=2)

print(json.dumps(stats, ensure_ascii=False, indent=2))
```

### 3. Conferência rápida dos resultados

```python
import pandas as pd

df_completo = pd.read_csv(os.path.join(OUTPUT_DIR, "RAIS_SJC_completo.csv"))
print(f"Total de estabelecimentos em SJC: {len(df_completo)}")
df_completo.head()
```

### 4. Download dos CSVs tratados

Baixe os arquivos para subir na pasta `notebooks/` (ou `data/`) do repositório GitHub e usar como fonte no Power BI.

```python
import shutil

shutil.make_archive(OUTPUT_DIR, "zip", OUTPUT_DIR)
files.download(f"{OUTPUT_DIR}.zip")
```

### 5. Pendências para a próxima sprint

- **DEC-003** — confirmar com o cliente o ano/competência de referência deste arquivo (não presente nos dados).
- **DEC-004** — aguardar decisão do cliente sobre fornecimento de base identificada (razão social/CNPJ).
- Implementar geocodificação a partir do campo `CEP_Estab` para viabilizar o mapeamento geográfico (User Story Rank 2).


---

## Notebook 02 — Base única do Power BI (Sprint 2)

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/02_Base_PowerBI_SJC.ipynb)

Junta a base RAIS tratada com a geocodificação do CEP, a região oficial, as descrições da CNAE 2.3 e as classificações pedidas pelo cliente, e gera `dados/RAIS_SJC_2024_PowerBI.csv`.


**Observatório do Ecossistema Industrial e de Serviços de São José dos Campos** · Fatec SJC · API Logística

Este notebook gera `dados/RAIS_SJC_2024_PowerBI.csv`, a base usada pelo painel na Sprint 2: uma linha por estabelecimento (47.339), com CEP, coordenadas, **região oficial** do município, CNAE 2.3, porte, tipo e situação.

| Etapa | O que faz | Decisão |
|---|---|---|
| 1 | Carrega a base RAIS tratada e confere com o arquivo original | DEC-001 a DEC-003 |
| 2 | Junta a geocodificação pelo CEP | DEC-016, DEC-018 |
| 3 | Classifica a região oficial pelo bairro e pelo setor do CEP | DEC-015 |
| 4 | Marca pontos que caíram em bairros homônimos | DEC-017 |
| 5 | Aplica as descrições oficiais da CNAE 2.3 | DEC-020 |
| 6 | Cria tipo de atividade, intensidade tecnológica, porte SEBRAE e setor destaque | DEC-019, DEC-021 |
| 7 | Grava a base com os nomes de colunas do painel e confere os totais | DEC-022 |

**Como rodar no Google Colab:** *Ambiente de execução → Executar tudo*. A primeira célula baixa o repositório com os arquivos de entrada.

```python
# 0. Ambiente: no Colab, baixa o repositório; localmente, usa a pasta do projeto
import os, re
REPO = "https://github.com/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos.git"
if "BASE" not in globals():
    if os.path.exists("/content"):
        if not os.path.exists("/content/repo"):
            os.system(f"git clone --depth 1 {REPO} /content/repo")
        BASE = "/content/repo"
    else:
        BASE = os.path.abspath("..")  # rodando de dentro de notebooks/
DADOS = os.path.join(BASE, "dados")
ENTRADA = os.path.join(DADOS, "entrada")
REF = os.path.join(DADOS, "referencia")
SAIDA = os.path.join(DADOS, "RAIS_SJC_2024_PowerBI.csv")

import pandas as pd
import numpy as np
print("Pasta do projeto:", BASE)
```

### 1. Base RAIS tratada

A aba `Base_RAIS` da planilha `CNAE_RAIS_SJC_2024.xlsx` já tem a hierarquia CNAE, a situação e a faixa de tamanho. O arquivo original `RAIS_SJC_completo.csv` (saída do ETL da Sprint 1) está **na mesma ordem de linhas** e é usado para conferir e para pegar o CEP com 8 dígitos.

```python
base = pd.read_excel(os.path.join(DADOS, "CNAE_RAIS_SJC_2024.xlsx"), sheet_name="Base_RAIS", dtype=str)
comp = pd.read_csv(os.path.join(ENTRADA, "RAIS_SJC_completo.csv"), dtype=str)

assert len(base) == len(comp) == 47339, "a base deve ter 47.339 estabelecimentos"
assert (base.Vinculos_Ativos.astype(int) == comp.Qtd_Vinculos_Ativos.astype(int)).all()
assert (base.Subclasse.str.lstrip("0").fillna("") == comp.CNAE20_Subclasse.astype(int).astype(str).str.lstrip("0")).all()
base["cep8"] = comp.CEP_Estab.astype(int).astype(str).str.zfill(8)
print("Linhas conferidas com o arquivo original:", len(base))
```

### 2. Geocodificação pelo CEP

`rais_sjc_geo_v2.csv` traz bairro e coordenadas de cada CEP (BrasilAPI + Nominatim). Cada CEP tem **uma única** geocodificação, então a junção é *muitos para um* e não duplica linhas.

> As coordenadas de `ceps_sjc_geo_v2.csv` estão corrompidas (o Excel em português trocou o ponto decimal), por isso dele só usamos logradouro e a marcação de CEP genérico (DEC-016).

```python
geo = pd.read_csv(os.path.join(ENTRADA, "rais_sjc_geo_v2.csv"), dtype=str)
geo["cep8"] = geo["CEP Estab"].astype(int).astype(str).str.zfill(8)
gcols = ["bairro", "nivel_geo", "lat_mapa", "lng_mapa", "precisao_mapa"]
assert geo.groupby("cep8")[gcols].nunique(dropna=False).max().max() == 1, "um CEP com duas geocodificações"
gcep = geo.drop_duplicates("cep8")[["cep8"] + gcols]

ceps = pd.read_csv(os.path.join(ENTRADA, "ceps_sjc_geo_v2.csv"), sep=";", dtype=str)
ceps["cep8"] = ceps.CEP.str.zfill(8)
gcep = gcep.merge(ceps[["cep8", "logradouro", "cep_generico"]], on="cep8", how="left")

df = base.merge(gcep, on="cep8", how="left", validate="many_to_one")
assert len(df) == 47339
print("CEPs distintos:", gcep.cep8.nunique(), "| com ponto no mapa:", int(pd.to_numeric(df.lat_mapa).notna().sum()))
```

### 3. Região oficial

A tabela `dados/referencia/bairros_regiao_sjc.csv` liga cada bairro à sua região (fonte: lista de bairros por região do Plano Diretor da Prefeitura; Região Norte por lista secundária). **Para tornar a classificação 100% oficial, basta substituir essa tabela pela lista oficial da Prefeitura e rodar o notebook de novo.**

Bairros ambíguos (mesmo nome em duas regiões) ou fora da tabela recebem a região **predominante do setor do CEP** (5 primeiros dígitos), desde que ela tenha pelo menos 85% dos estabelecimentos do setor.

```python
FONTE = {
    "plano_diretor": "Plano Diretor PMSJC 2018 (lista oficial de bairros por região)",
    "lista_secundaria": "Lista de bairros por região da PMSJC (fonte secundária)",
    "distrito_rural": "Distrito / área rural (classificação PMSJC)",
    "setor_cep": "Inferido pelo setor do CEP (a confirmar)",
    "nao_classificado": "Não classificado",
}
tab = pd.read_csv(os.path.join(REF, "bairros_regiao_sjc.csv"), dtype=str).fillna("")
tab = tab[tab.regiao != ""]  # ambíguos ficam de fora e caem no setor do CEP
reg_de = dict(zip(tab.bairro, tab.regiao)); fonte_de = dict(zip(tab.bairro, tab.fonte))

df["set5"] = df.cep8.str[:5]
df["reg"] = df.bairro.map(reg_de)
df["src"] = df.bairro.map(fonte_de)

ok = df.reg.notna() & df.nivel_geo.eq("bairro")
t = df[ok].groupby(["set5", "reg"]).size().unstack(fill_value=0)
dom, share = t.idxmax(axis=1), t.max(axis=1) / t.sum(axis=1)
print(f"Setores de CEP: {len(t)} | com uma única região: {(share == 1).sum()}")

falta = df.reg.isna() & df.set5.isin(share[share >= 0.85].index)
df.loc[falta, "reg"] = df.loc[falta, "set5"].map(dom)
df.loc[falta, "src"] = "setor_cep"
df["reg"] = df.reg.fillna("Não classificado")
df["src"] = df.src.fillna("nao_classificado")

def conf(row):
    if row.src == "setor_cep": return "Baixa"
    if row.src == "nao_classificado": return "Não se aplica"
    if row.src == "lista_secundaria" or row.cep_generico == "True": return "Média"
    return "Alta"
df["confiabilidade_regiao"] = df.apply(conf, axis=1)
df.reg.value_counts()
```

### 4. Pontos em bairros homônimos

Cada ponto é comparado com o centro da própria região. Se cair bem mais perto de outra região (mais de 1,5 km de diferença), o geocodificador provavelmente achou um bairro de mesmo nome em outro lugar: a região é mantida e o ponto é marcado em **Alerta Coordenada**.

```python
lat = pd.to_numeric(df.lat_mapa); lng = pd.to_numeric(df.lng_mapa)
pts = df.assign(lat=lat, lng=lng).dropna(subset=["lat"])
cen = pts[pts.reg != "Não classificado"].groupby("reg")[["lat", "lng"]].mean()

def km(a, b, c, d):
    return np.hypot((a - c) * 111.0, (b - d) * 111.0 * np.cos(np.radians(23.2)))

has = lat.notna()
dist = pd.DataFrame({r: km(lat[has], lng[has], la, ln) for r, (la, ln) in cen.iterrows()})
d_own = pd.Series([dist.at[i, r] if r in dist.columns else np.nan for i, r in zip(dist.index, df.reg[has])], index=dist.index)
near, d_near = dist.idxmin(axis=1), dist.min(axis=1)
alerta = pd.Series(False, index=df.index)
alerta[has] = (near != df.reg[has]) & ((d_own - d_near) > 1.5) & df.reg[has].ne("Não classificado")
df["alerta_coordenada"] = np.where(alerta, "Ponto fora da região oficial (homônimo no geocodificador)", "")
df[alerta].groupby(["bairro", "reg"]).size()
```

### 5. Descrições oficiais da CNAE 2.3

A tabela oficial do IBGE/CONCLA (`dados/referencia/CNAE_Subclasses_2_3.xlsx`) é lida em hierarquia. Os códigos da base batem 100% com ela; trocamos só as descrições (grafia antiga, quebras de linha). Subclasses que não existem na CNAE 2.3 ficam marcadas.

```python
raw = pd.read_excel(os.path.join(REF, "CNAE_Subclasses_2_3.xlsx"), header=None, dtype=str).iloc[4:]
linhas, nomes = [], {}
sec = div = grp = cla = None
for r in raw.itertuples(index=False):
    s, dv, g, c, sb, nm = [None if pd.isna(v) else str(v).strip() for v in r[:6]]
    if s and len(s) == 1: sec = s; nomes["S" + s] = nm
    elif dv and re.fullmatch(r"\d{2}", dv): div = dv; nomes["D" + dv] = nm
    elif g and re.fullmatch(r"\d{2}\.\d", g): grp = g.replace(".", ""); nomes["G" + grp] = nm
    elif c and re.fullmatch(r"\d{2}\.\d{2}-\d", c): cla = re.sub(r"\D", "", c); nomes["C" + cla] = nm
    elif sb and re.fullmatch(r"\d{4}-\d/\d{2}", sb):
        linhas.append(dict(Subclasse=re.sub(r"\D", "", sb), Classe=cla, Grupo=grp, Sub_desc=nm))
c23 = pd.DataFrame(linhas)
c23["Classe_desc"] = c23.Classe.map(lambda v: nomes.get("C" + v))
c23["Grupo_desc"] = c23.Grupo.map(lambda v: nomes.get("G" + v))

clean = lambda s: s.str.replace(r"\s+", " ", regex=True).str.strip()
sub = c23.set_index("Subclasse")
cla_ = c23.drop_duplicates("Classe").set_index("Classe")
grp_ = c23.drop_duplicates("Grupo").set_index("Grupo")
n_sub = df.Subclasse.map(clean(sub.Sub_desc))
n_cla = df.Classe.map(clean(cla_.Classe_desc))
n_grp = df.Grupo.map(clean(grp_.Grupo_desc))
alteradas = (n_sub.notna() & (n_sub != df.Subclasse_Descricao)) | (n_cla.notna() & (n_cla != df.Classe_Descricao))
df["Subclasse_Descricao"] = n_sub.fillna(df.Subclasse_Descricao)
df["Classe_Descricao"] = n_cla.fillna(df.Classe_Descricao)
df["Grupo_Descricao"] = n_grp.fillna(df.Grupo_Descricao)
df["cnae23"] = np.where(df.Subclasse.isin(sub.index), "Sim", "Não")
print("Subclasses na CNAE 2.3:", len(c23), "| linhas com descrição atualizada:", int(alteradas.sum()),
      "| fora da CNAE 2.3:", int((df.cnae23 == "Não").sum()))
```

### 6. Classificações pedidas pelo cliente

- **Tipo de Atividade:** as categorias do documento de requisitos (manufatura, tecnologia, logística, serviços especializados…).
- **Intensidade Tecnológica OCDE:** taxonomia de intensidade de P&D da OCDE (Galindo-Rueda e Verger, 2016).
- **Porte SEBRAE:** micro, pequena, média e grande pelo número de empregados (indústria e construção × comércio e serviços).
- **Setor Destaque:** automotiva, aeroespacial e química e farmacêutica.
- **Situação Vínculo:** padrão do painel (DEC-011): com vínculo = RAIS positiva.

```python
dsec = pd.read_excel(os.path.join(DADOS, "CNAE_RAIS_SJC_2024.xlsx"), sheet_name="dSecao", dtype=str).set_index("Secao")
sec_ibge = df.Secao.map(dsec.Secao_Descricao_IBGE).fillna(df.Secao_Nome)
div = df.Divisao.astype(str); grp = df.Grupo.astype(str)

def tipo_ativ(sec, d):
    if sec == "C": return "Manufatura (indústria de transformação)"
    if d in ("58", "59", "60", "61", "62", "63", "72"): return "Tecnologia, informação e P&D"
    if sec == "H": return "Logística e transporte"
    if sec in ("K", "M"): return "Serviços especializados"
    if sec == "G": return "Comércio"
    if sec == "F": return "Construção"
    if sec == "N": return "Serviços administrativos e de apoio"
    if sec in ("P", "Q"): return "Saúde e educação"
    if sec in ("B", "D", "E"): return "Extração e utilidades"
    if sec == "A": return "Agropecuária"
    if sec == "O": return "Administração pública"
    if sec == "NI": return "Não informado"
    return "Outros serviços"

def ocde(sec, d, g):
    if sec == "C":
        if d in ("21", "26") or g == "304": return "Alta"
        if d in ("20", "27", "28", "29") or g in ("255", "325") or (d == "30" and g not in ("301", "304")): return "Média-alta"
        if d in ("22", "23", "24", "32", "33") or g == "301": return "Média"
        return "Média-baixa"
    if d == "72": return "Alta"
    if d in ("62", "63"): return "Média-alta"
    return "Não se aplica"

cod = df.Tamanho_Cod.astype(int)
industria = df.Secao.isin(list("BCDEF"))
def sebrae(c, ind):
    if c == 1: return "Sem vínculos"
    if ind: return "Micro" if c <= 4 else "Pequena" if c <= 6 else "Média" if c <= 8 else "Grande"
    return "Micro" if c <= 3 else "Pequena" if c <= 5 else "Média" if c == 6 else "Grande"

df["tipo_ativ"] = [tipo_ativ(a, b) for a, b in zip(df.Secao, div)]
df["ocde"] = [ocde(a, b, c) for a, b, c in zip(df.Secao, div, grp)]
df["porte_sebrae"] = [sebrae(c, i) for c, i in zip(cod, industria)]
destaque = df.Setor_Destaque.copy()
destaque[div.isin(["20", "21"])] = "Química e farmacêutica"
df["destaque"] = destaque.fillna("Demais setores")
df["sit2"] = np.where(df.Ind_Rais_Negativa.astype(int) == 0, "Com vínculo", "Sem vínculo")
df.groupby("tipo_ativ").Vinculos_Ativos.apply(lambda s: s.astype(int).sum()).sort_values(ascending=False)
```

### 7. Base final

As colunas que os visuais do painel já usam mantêm o nome original (`CEP Estab`, `CNAE 2.0 Classe`, `Seção CNAE`, `Setor`, `Faixa de Porte`, `Situação Vínculo`, `Tipo Estab_1`). O arquivo é gravado em UTF-8 com BOM, separador vírgula e ponto decimal. Para importar no Power BI, siga `evidencias/Importacao_PowerBI_RAIS_SJC.txt`.

```python
cep_ok = df.cep8 != "00000000"
out = pd.DataFrame({
    "ID Estab": df.ID.astype(int),
    "Ano Base": 2024,
    "CEP Estab": np.where(cep_ok, df.cep8, ""),
    "CEP Formatado": np.where(cep_ok, df.cep8.str[:5] + "-" + df.cep8.str[5:], "Não informado"),
    "CEP Genérico": np.where(df.cep_generico.eq("True"), "Sim", np.where(cep_ok, "Não", "")),
    "Logradouro": df.logradouro.fillna(""),
    "Bairro": df.bairro.fillna("Não identificado"),
    "Região Oficial": df.reg,
    "Fonte Região": df.src.map(FONTE),
    "Confiabilidade Região": df.confiabilidade_regiao,
    "Latitude": lat.round(7),
    "Longitude": lng.round(7),
    "Precisão Geo": df.precisao_mapa.fillna("sem CEP"),
    "Alerta Coordenada": df.alerta_coordenada,
    "Seção Cód": df.Secao,
    "Seção CNAE": df.Secao + " - " + sec_ibge,
    "Setor": df.Secao_Nome,
    "Divisão CNAE": div, "Divisão Descrição": df.Divisao_Descricao,
    "Grupo CNAE": grp, "Grupo Descrição": df.Grupo_Descricao,
    "CNAE 2.0 Classe": df.Classe, "Classe Descrição": df.Classe_Descricao,
    "CNAE 2.0 Subclasse": df.Subclasse, "Subclasse Descrição": df.Subclasse_Descricao,
    "Subclasse na CNAE 2.3": df.cnae23,
    "Tipo de Atividade": df.tipo_ativ,
    "Intensidade Tecnológica OCDE": df.ocde,
    "Setor Destaque": df.destaque,
    "Tamanho Estabelecimento": cod,
    "Faixa de Porte": df.Faixa_Tamanho,
    "Porte SEBRAE": df.porte_sebrae,
    "Tipo Estab_1": df.Tipo_Estab,
    "Situação Vínculo": df.sit2,
    "Situação Detalhada": df.Situacao,
    "Ind Rais Negativa": df.Ind_Rais_Negativa.astype(int),
    "Atividade no Ano": df.Atividade_no_Ano,
    "Qtd Vínculos Ativos": df.Vinculos_Ativos.astype(int),
    "Qtd Vínculos CLT": df.Vinculos_CLT.astype(int),
    "Qtd Vínculos Estatutários": df.Vinculos_Estatutarios.astype(int),
    "Natureza Jurídica": df.Natureza_Juridica, "Natureza Descrição": df.Natureza_Descricao,
    "Natureza Grupo": df.Natureza_Grupo,
    "Simples": df.Simples,
    "IBGE Subsetor": df.IBGE_Subsetor, "IBGE Subsetor Descrição": df.IBGE_Subsetor_Descricao,
})
out.to_csv(SAIDA, index=False, encoding="utf-8-sig")

# Conferências finais (os mesmos números do relatório da Sprint 2)
chk = pd.read_csv(SAIDA, dtype=str, encoding="utf-8-sig")
assert chk.shape == (47339, 46)
assert chk["ID Estab"].is_unique
assert chk["Qtd Vínculos Ativos"].astype(int).sum() == 206717
print("Arquivo gravado:", SAIDA, chk.shape)
print("Com região oficial: {:.2%}".format((chk["Região Oficial"] != "Não classificado").mean()))
print("Com ponto no mapa:  {:.2%}".format(chk["Latitude"].notna().mean()))
```

---

*Gerado a partir dos notebooks em 23/11/2026.*
