> Versão em Markdown de [`Manual_Replicacao.docx`](Manual_Replicacao.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Manual de Replicação do Observatório SJC

Como refazer o projeto do zero: dos dados públicos ao painel Power BI · versão de 23/11/2026

Este manual mostra como outra pessoa (o cliente, uma nova equipe ou a própria Secretaria) pode refazer o Observatório do Ecossistema Industrial e de Serviços de São José dos Campos a partir das fontes públicas: baixar os dados, rodar os códigos no Google Colab, preparar as planilhas e montar o painel no Power BI. Também mostra como atualizar o observatório com um novo ano da RAIS.

Todos os arquivos citados estão no repositório do projeto no GitHub:

<https://github.com/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos>

## Visão geral

O projeto tem duas partes. A primeira transforma os dados públicos em bases tratadas, com três notebooks Python rodados no Google Colab. A segunda monta o painel no Power BI a partir dessas bases.

| **Etapa**               | **Entrada**                                     | **Ferramenta**                | **Saída**                                         |
|-------------------------|-------------------------------------------------|-------------------------------|---------------------------------------------------|
| 1\. Baixar a RAIS       | Site do Ministério do Trabalho (PDET)           | Navegador ou Windows Explorer | Arquivo de estabelecimentos da RAIS 2024          |
| 2\. ETL da RAIS         | RAIS nacional (cerca de 12,6 milhões de linhas) | Notebook 01 (Colab)           | `RAIS_SJC_completo.csv` (47.339 estabelecimentos) |
| 3\. Geocodificação      | CEPs da RAIS de SJC + CNEFE 2022 (IBGE)         | Notebook 01b (Colab)          | `geo_ceps_sjc_cnefe.csv` (coordenadas por CEP)    |
| 4\. Base única          | Saídas anteriores + CNAE 2.3 + regiões          | Notebook 02 (Colab)           | `RAIS_SJC_2024_PowerBI.csv` (47 colunas)          |
| 5\. Planilhas do painel | Saídas anteriores + PIB do IBGE                 | Python ou Excel               | 4 arquivos em `powerbi/fontes/`                   |
| 6\. Painel              | Planilhas do painel                             | Power BI Desktop              | Painel de 5 páginas, publicado na web             |

> **Atalho:** se o objetivo é só abrir e atualizar o painel que já existe, não é preciso refazer tudo. Use o projeto pronto em `powerbi/pbip/` e siga o Guia de atualização do painel (`docs/final/Guia_Atualizar_PowerBI`).

## Antes de começar

- **Conta Google**, para usar o Google Colab (gratuito).

- **Power BI Desktop** atualizado (gratuito, para Windows).

- **7-Zip** (gratuito), para descompactar o arquivo da RAIS se ele vier em .7z.

- **Espaço em disco:** cerca de 4 GB livres para o arquivo nacional da RAIS.

- **Tempo estimado:** 2 a 3 horas para a parte de dados e 3 a 4 horas para montar o painel do zero.

## Parte 1 — Dados

### Fontes de dados

| **Fonte**                        | **Onde obter**                                                                                            | **Para que serve**                  | **No repositório**                                           |
|----------------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------|
| RAIS Estabelecimentos 2024 (MTE) | FTP do PDET: `ftp://ftp.mtps.gov.br/pdet/microdados/`, pasta da RAIS de 2024, arquivo de estabelecimentos | Estabelecimentos e vínculos formais | `dados/entrada/RAIS_SJC_completo.csv` (já filtrado para SJC) |
| CNEFE 2022 (IBGE)                | FTP do IBGE, Censo 2022, Arquivos CNEFE, município 3549904. O notebook 01b baixa sozinho                  | Coordenadas de cada CEP             | `dados/entrada/geo_ceps_sjc_cnefe.csv`                       |
| PIB dos Municípios (IBGE)        | Sidra, tabela 5938: `https://sidra.ibge.gov.br/tabela/5938`                                               | PIB e valor adicionado por setor    | `dados/IBGE_PIB_SJC_Observatorio.xlsx`                       |
| CNAE 2.3 (IBGE/CONCLA)           | `https://concla.ibge.gov.br`                                                                              | Nomes oficiais das atividades       | `dados/referencia/CNAE_Subclasses_2_3.xlsx`                  |
| Regiões da cidade (Prefeitura)   | Plano Diretor, estudo "Regiões Urbanas"                                                                   | Região oficial de cada bairro       | `dados/referencia/bairros_regiao_sjc.csv`                    |

### Passo 1 — Baixar a RAIS

1.  Pressione **Windows + E** para abrir o Windows Explorer e digite na barra de endereço: `ftp://ftp.mtps.gov.br/pdet/microdados/`. Os navegadores atuais nem sempre abrem endereços FTP; por isso o Windows Explorer ou um programa de FTP (como o FileZilla) é o caminho mais seguro.

2.  Entre na pasta da RAIS e no ano 2024 e baixe o arquivo de **estabelecimentos** (o nome começa com `RAIS_ESTAB_PUB`).

3.  O notebook 01 lê um arquivo **.zip** com o .txt dentro. Se o arquivo vier em **.7z**, abra com o 7-Zip, extraia o .txt e compacte de novo como .zip (botão direito → Enviar para → Pasta compactada).

### Passo 2 — Notebook 01: filtrar a RAIS para São José dos Campos

Abrir no Colab: https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/01_ETL_RAIS_SJC.ipynb

1.  No Colab, clique em **Ambiente de execução → Executar tudo**.

2.  Quando aparecer o botão de envio, selecione o .zip da RAIS. O envio do arquivo é a etapa mais demorada.

3.  O notebook lê o arquivo linha a linha (sem abrir tudo na memória), guarda só o município **354990** (São José dos Campos) e separa os arquivos por situação (DEC-001) e por tipo de estabelecimento (DEC-002).

4.  No fim, ele baixa `RAIS_SJC_tratado.zip`. O arquivo principal é `RAIS_SJC_completo.csv`.

**Confira:** 47.339 estabelecimentos no total, dos quais 30.470 com RAIS negativa (sem empregados formais).

### Passo 3 — Notebook 01b: coordenadas dos CEPs

Abrir no Colab: https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/01b_Geocodificacao_CEPs_SJC.ipynb

1.  Envie o `RAIS_SJC_completo.csv` para o Colab (ícone de pasta à esquerda → Enviar) e rode as **Células 1 a 3**. A Célula 3 confere 47.339 estabelecimentos e 3.677 CEPs distintos.

2.  Rode a célula do **CNEFE 2022**, logo depois da Célula 3. Ela baixa o cadastro de endereços do IBGE para São José dos Campos e calcula o ponto médio dos endereços de cada CEP. Essa é a fonte das coordenadas usada no painel (DEC-023).

3.  Baixe o arquivo gerado (`geo_ceps_sjc.csv`) e renomeie para `geo_ceps_sjc_cnefe.csv`.

**Confira:** 3.379 CEPs com coordenada exata, 297 aproximados pelos 5 primeiros dígitos e 1 não localizado.

> As Células 4 a 8 consultam serviços de CEP na internet (AwesomeAPI, BrasilAPI, ViaCEP e Nominatim) e levam de 30 a 60 minutos. Elas geraram o bairro de cada CEP, usado para a região oficial. Não é preciso rodá-las de novo: os arquivos resultantes (`rais_sjc_geo_v2.csv` e `ceps_sjc_geo_v2.csv`) estão em `dados/entrada/`.

### Passo 4 — Notebook 02: base única

Abrir no Colab: https://colab.research.google.com/github/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/blob/main/notebooks/02_Base_PowerBI_SJC.ipynb

1.  Clique em **Ambiente de execução → Executar tudo**. A primeira célula copia o repositório para dentro do Colab, com todos os arquivos de entrada.

2.  Se você refez o Passo 3, substitua `dados/entrada/geo_ceps_sjc_cnefe.csv` pelo seu arquivo antes de rodar (na pasta `/content/repo` do Colab).

3.  O notebook lê também `dados/CNAE_RAIS_SJC_2024.xlsx` (aba Base_RAIS): a mesma RAIS de SJC com a hierarquia CNAE em cada linha, na mesma ordem de `RAIS_SJC_completo.csv`. Ele confere as duas e para com erro se não baterem.

4.  O notebook junta a RAIS com as coordenadas, classifica a região oficial pelo bairro, aplica os nomes da CNAE 2.3 e cria as classificações do cliente (tipo de atividade, intensidade tecnológica, porte SEBRAE e macroprocesso logístico).

5.  Baixe o arquivo `dados/RAIS_SJC_2024_PowerBI.csv`.

**Confira:** o próprio notebook verifica 47.339 linhas, 47 colunas e 206.717 vínculos ativos, e mostra 99,99% dos estabelecimentos com região oficial e com ponto no mapa.

> Para tornar a classificação regional 100% oficial, troque `dados/referencia/bairros_regiao_sjc.csv` pela tabela de bairros por região da Prefeitura e rode o notebook 02 de novo (DEC-015).

### Passo 5 — Preparar as planilhas do painel

O painel lê 4 arquivos da pasta `powerbi/fontes/`. Abaixo está como cada um é feito. Os trechos de código rodam no Colab ou em qualquer Python com a biblioteca pandas; foram testados e reproduzem os arquivos do repositório.

| **Arquivo**                                  | **Abas usadas**                     | **Como é feito**                                                                                                                                       |
|----------------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `RAIS_SJC.csv`                               | —                                   | Saída do notebook 01 com os nomes de coluna originais da RAIS, separador ";" e codificação Windows-1252 (trecho A)                                     |
| `dCNAE_classes.xlsx`                         | dCNAE                               | As 673 classes da CNAE 2.3 com o nome oficial (trecho B)                                                                                               |
| `Cruzamento_RAIS_IBGE_Observatorio_SJC.xlsx` | Cruzamento, VAB setorial, PIB anual | VAB setorial = aba `fato_VAB_setorial` da planilha do IBGE; PIB anual = trecho C; Cruzamento = emprego RAIS × valor adicionado por setor (veja a nota) |
| `Regioes_SJC_filtro_por_regiao.xlsx`         | CEP x Região                        | Uma linha por CEP com região, bairro e coordenadas do CNEFE; planilha da equipe (veja a nota)                                                          |

#### Trecho A — RAIS_SJC.csv a partir do notebook 01

```python
import pandas as pd
NOMES = ["Bairros SP", "Bairros Fortaleza", "Bairros RJ", "CNAE 2.0 Classe", "CNAE 95 Classe",
         "Distritos SP", "Qtd Vínculos CLT", "Qtd Vínculos Ativos", "Qtd Vínculos Estatutários",
         "Ind Atividade Ano", "Ind CEI Vinculado", "Ind Estab Participa PAT", "Ind Rais Negativa",
         "Ind Simples", "Município", "Natureza Jurídica", "Regiões Adm DF", "CNAE 2.0 Subclasse",
         "Tamanho Estabelecimento", "Tipo Estab", "Tipo Estab_1", "UF", "IBGE Subsetor", "CEP Estab"]
rais = pd.read_csv("RAIS_SJC_completo.csv", dtype=str)
rais.columns = NOMES
for col in NOMES:
    if col != "Tipo Estab_1":
        rais[col] = rais[col].str.strip().str.lstrip("0").replace("", "0")
rais.to_csv("RAIS_SJC.csv", sep=";", index=False, encoding="cp1252")
```

#### Trecho B — dCNAE_classes.xlsx a partir da CNAE 2.3

```python
import re, pandas as pd
raw = pd.read_excel("CNAE_Subclasses_2_3.xlsx", header=None, dtype=str).iloc[4:]
linhas = []
for r in raw.itertuples(index=False):
    c, nome = r[3], r[5]
    if isinstance(c, str) and re.fullmatch(r"\d{2}\.\d{2}-\d", c.strip()):
        linhas.append({"Classe": re.sub(r"\D", "", c), "Classe_Descricao": re.sub(r"\s+", " ", str(nome)).strip()})
pd.DataFrame(linhas).to_excel("dCNAE_classes.xlsx", sheet_name="dCNAE", index=False)
```

O trecho usa a grafia atual da CNAE 2.3. Em 45 das 673 classes o nome sai um pouco diferente do arquivo do repositório (por exemplo, "Aquicultura" em vez de "Aqüicultura"); os códigos são os mesmos.

#### Trecho C — aba PIB anual a partir da planilha do IBGE

```python
import pandas as pd
X = "IBGE_PIB_SJC_Observatorio.xlsx"
fp = pd.read_excel(X, sheet_name="fato_PIB")
part = pd.read_excel(X, sheet_name="fato_Participacoes")
sp = part[part.indicador.str.contains("estado", case=False)].set_index("ano").valor_pct
p = pd.DataFrame({"ano": fp.ano, "pib": fp.pib, "pib_real_2023": fp.pib_real_2023})
p["cresc_real_pct"] = (p.pib_real_2023 / p.pib_real_2023.shift(1) - 1) * 100
p["indice_pib_real_2010_100"] = p.pib_real_2023 / p.loc[p.ano == 2010, "pib_real_2023"].iloc[0] * 100
p["pib_per_capita"] = fp.pib / fp.populacao
p["pib_per_capita_real_2023"] = fp.pib_real_2023 / fp.populacao
p["part_pib_estado_sp_pct"] = p.ano.map(sp)
p["populacao"] = fp.populacao
p["fonte_populacao"] = fp.fonte_populacao
p.round(4).to_excel("PIB_anual.xlsx", sheet_name="PIB anual", index=False)
```

> **Arquivos feitos fora dos notebooks do repositório.** A aba Cruzamento e a planilha de regiões foram montadas pela equipe na Sprint 2 (Colab e Excel), a planilha `dados/CNAE_RAIS_SJC_2024.xlsx` (análise da Sprint 1, com a aba Base_RAIS) foi feita em Colab e Excel, e a planilha `dados/IBGE_PIB_SJC_Observatorio.xlsx` veio de um notebook do PIB que não está no repositório. Para replicar o painel como está, use as versões do repositório. A aba Cruzamento soma os vínculos da RAIS de estabelecimentos com CNPJ, sem administração pública, por setor do IBGE (Agropecuária, Indústria e Serviços, pela aba "Mapa Seção x Setor") e compara com o valor adicionado de 2021: produtividade relativa = % do valor adicionado ÷ % do emprego (DEC-006, DEC-009 e DEC-013).

## Parte 2 — Painel Power BI

Há dois caminhos. O mais rápido é abrir o projeto pronto (`powerbi/pbip/Observatorio_SJC.pbip`) e só atualizar os dados, como no Guia de atualização. Os passos abaixo mostram como montar o mesmo painel do zero, para entender cada parte ou adaptar para outra cidade.

### Passo 6 — Criar o arquivo e o parâmetro da pasta

1.  Abra o Power BI Desktop e crie um relatório em branco.

2.  Em **Exibição → Temas → Procurar temas**, aplique o tema do projeto: `powerbi/pbip/Observatorio_SJC.Report/StaticResources/RegisteredResources/LogMulti___Clean_Blue8566195012392886.json`.

3.  Em **Página Inicial → Transformar dados → Gerenciar parâmetros → Novo**, crie o parâmetro **PastaFontes**, do tipo Texto, com o caminho da pasta das planilhas, terminado em barra invertida (por exemplo, `C:\Observatorio-SJC\powerbi\fontes\`).

### Passo 7 — Importar as 6 tabelas

| **Tabela no modelo** | **Arquivo**                                  | **Aba**      | **Como importar**                                                                         |
|----------------------|----------------------------------------------|--------------|-------------------------------------------------------------------------------------------|
| RAIS_SJC             | `RAIS_SJC.csv`                               | —            | Obter dados → Texto/CSV; delimitador ponto e vírgula; codificação 1252 (Europa Ocidental) |
| dCNAE                | `dCNAE_classes.xlsx`                         | dCNAE        | Obter dados → Excel                                                                       |
| Cruzamento           | `Cruzamento_RAIS_IBGE_Observatorio_SJC.xlsx` | Cruzamento   | Obter dados → Excel                                                                       |
| VAB setorial         | mesmo arquivo                                | VAB setorial | Obter dados → Excel                                                                       |
| PIB anual            | mesmo arquivo                                | PIB anual    | Obter dados → Excel                                                                       |
| CEP x Região         | `Regioes_SJC_filtro_por_regiao.xlsx`         | CEP x Região | Obter dados → Excel; coluna CEP como Texto                                                |

Depois de importar, em cada consulta abra o **Editor Avançado** e troque o caminho fixo do arquivo por `PastaFontes & "nome do arquivo"`. Exemplo para a RAIS:

```powerquery
Fonte = Csv.Document(File.Contents(PastaFontes & "RAIS_SJC.csv"),
    [Delimiter=";", Columns=24, Encoding=1252, QuoteStyle=QuoteStyle.None])
```

### Passo 8 — Etapas do Power Query na tabela RAIS_SJC

A tabela RAIS_SJC recebe estas etapas, nesta ordem (o código completo está em `powerbi/pbip/Observatorio_SJC.SemanticModel/definition/tables/RAIS_SJC.tmdl` e no documento de fórmulas):

1.  Promover a primeira linha a cabeçalho e ajustar os tipos (códigos como texto, quantidades como número inteiro).

2.  Remover as colunas sem uso em SJC: Bairros SP, Bairros Fortaleza, Bairros RJ, Distritos SP e Regiões Adm DF.

3.  **Situação Vínculo:** "Com Vínculo" quando Ind Rais Negativa = 0; senão, "Sem Vínculo" (DEC-001, DEC-011).

4.  **Setor:** nome curto para as 16 atividades mais frequentes; nas demais, o próprio código.

5.  **Categoria Automotiva** e **Atividade Automotiva:** recorte das divisões 29 (fabricação) e 45 (comércio e reparação).

6.  **Faixa de Porte** e **Ordem Porte:** faixa de empregados a partir de Tamanho Estabelecimento (1 = Zero até 10 = 1000 ou mais).

7.  **Natureza Nome:** nome da natureza jurídica mais comum.

8.  **Seção CNAE:** letra e nome da seção (A a U) pelos dois primeiros dígitos da classe.

9.  **Classe Chave:** classe CNAE com 5 dígitos (completa os zeros à esquerda).

10. Mesclar com a tabela **dCNAE** pela Classe Chave e expandir **Classe Descrição**; criar **Setor Completo** (nome oficial quando o Setor ficou só com o código).

### Passo 9 — Relação entre as tabelas

| **De**                | **Para**              | **Tipo**                                                                                            |
|-----------------------|-----------------------|-----------------------------------------------------------------------------------------------------|
| RAIS_SJC\[CEP Estab\] | 'CEP x Região'\[CEP\] | Muitos para um, filtro em direção única. Dá a região e a latitude/longitude de cada estabelecimento |

As tabelas do IBGE (Cruzamento, VAB setorial e PIB anual) não precisam de relação: cada gráfico da página PIB e Emprego usa uma só delas. Se o Power BI criar sozinho uma relação entre Cruzamento e VAB setorial pela coluna vab_real_2023, ela pode ser excluída.

### Passo 10 — Medidas

Crie as medidas na tabela RAIS_SJC (**Página Inicial → Nova medida**):

```dax
Total de Estabelecimentos = COUNTROWS('RAIS_SJC')
Estabelecimentos Com Vínculo = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Situação Vínculo] = "Com Vínculo")
Estabelecimentos Sem Vínculo = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Situação Vínculo] = "Sem Vínculo")
% Com Vínculo = DIVIDE([Estabelecimentos Com Vínculo], [Total de Estabelecimentos])
% Sem Vínculo = DIVIDE([Estabelecimentos Sem Vínculo], [Total de Estabelecimentos])
Total Vínculos Ativos = SUM('RAIS_SJC'[Qtd Vínculos Ativos])
Total Vínculos CLT = SUM('RAIS_SJC'[Qtd Vínculos CLT])
Total Vínculos Estatutários = SUM('RAIS_SJC'[Qtd Vínculos Estatutários])
% Participação Estab = DIVIDE([Total de Estabelecimentos], CALCULATE([Total de Estabelecimentos], ALL('RAIS_SJC'[Seção CNAE])))
% Participação Vínculos = DIVIDE([Total Vínculos Ativos], CALCULATE([Total Vínculos Ativos], ALL('RAIS_SJC'[Seção CNAE])))
```

O modelo tem também 8 medidas do recorte automotivo e do transporte de carga (Estab Fábricas, Vínculos Fábricas, Estab Comércio e Reparação, Vínculos Comércio e Reparação, as duas médias e as duas de Transporte de Carga). Elas estão no documento de fórmulas e não aparecem nas páginas atuais.

### Passo 11 — Colunas calculadas da página Regiões e Tecnologia

Crie as três colunas na tabela RAIS_SJC (**Ferramentas de tabela → Nova coluna**). Elas seguem a mesma regra da base única (notebook 02).

```dax
Tipo de Atividade =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
RETURN
    SWITCH (
        TRUE (),
        d = 0, "Não informado",
        d >= 10 && d <= 33, "Manufatura (indústria de transformação)",
        ( d >= 58 && d <= 63 ) || d = 72, "Tecnologia, informação e P&D",
        d >= 49 && d <= 53, "Logística e transporte",
        ( d >= 64 && d <= 66 ) || ( d >= 69 && d <= 75 ), "Serviços especializados",
        d >= 45 && d <= 47, "Comércio",
        d >= 41 && d <= 43, "Construção",
        d >= 77 && d <= 82, "Serviços administrativos e de apoio",
        d >= 85 && d <= 88, "Saúde e educação",
        ( d >= 5 && d <= 9 ) || ( d >= 35 && d <= 39 ), "Extração e utilidades",
        d <= 3, "Agropecuária",
        d = 84, "Administração pública",
        "Outros serviços"
    )
```

```dax
Intensidade Tecnológica OCDE =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
VAR g = LEFT ( 'RAIS_SJC'[Classe Chave], 3 )
RETURN
    IF (
        d >= 10 && d <= 33,
        SWITCH (
            TRUE (),
            d IN { 21, 26 } || g = "304", "Alta",
            d IN { 20, 27, 28, 29 } || g IN { "255", "325" } || ( d = 30 && NOT ( g IN { "301", "304" } ) ), "Média-alta",
            d IN { 22, 23, 24, 32, 33 } || g = "301", "Média",
            "Média-baixa"
        ),
        SWITCH (
            TRUE (),
            d = 72, "Alta",
            d IN { 62, 63 }, "Média-alta",
            "Não se aplica"
        )
    )
```

```dax
Macroprocesso Logístico =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
VAR cl = 'RAIS_SJC'[Classe Chave]
RETURN
    SWITCH (
        TRUE (),
        d = 0, "Não classificado",
        cl IN { "45200", "45439" } || d IN { 33, 95 }, "6. Pós-venda, manutenção e reparação",
        d <= 9 || d IN { 35, 36, 37 }, "1. Suprimento (agro, extração, energia e água)",
        ( d >= 10 && d <= 32 ) || ( d >= 41 && d <= 43 ), "2. Produção (indústria e construção)",
        d = 46, "3. Distribuição atacadista",
        d >= 49 && d <= 53, "4. Transporte e armazenagem",
        d IN { 45, 47 }, "5. Varejo (venda ao consumidor)",
        d IN { 38, 39 }, "7. Logística reversa (resíduos e reciclagem)",
        d >= 58 && d <= 82, "8. Serviços de apoio às empresas",
        ( d >= 55 && d <= 56 ) || ( d >= 84 && d <= 99 ), "9. Serviços ao consumidor e públicos",
        "Não classificado"
    )
```

### Passo 12 — Montar as páginas

Em cada página, ajuste o tamanho da tela em **Formatar página → Configurações da tela → Tipo: Personalizado, 1920 × 1080**. No topo de todas as páginas há o logo, o título, a linha de fontes e o **Navegador de páginas** (Inserir → Botões → Navegador → Navegador de páginas).

#### Página 1 — KPIs e Mapa

| **Visual**              | **Campos**                                                                                                                                                       |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 4 cartões               | Total de Estabelecimentos · Estabelecimentos Sem Vínculo · Estabelecimentos Com Vínculo · Total Vínculos Ativos (unidade de exibição: Nenhum)                    |
| 2 cartões de percentual | % Sem Vínculo · % Com Vínculo                                                                                                                                    |
| Pizza                   | % Com Vínculo e % Sem Vínculo nos Valores                                                                                                                        |
| Mapa (Azure Maps)       | Latitude = Média de CEP x Região\[Latitude\] · Longitude = Média de CEP x Região\[Longitude\] · Legenda = Situação Vínculo · Tamanho = Total de Estabelecimentos |
| Segmentações (filtros)  | Seção CNAE · Faixa de Porte · Tipo Estab_1 (tipo de estabelecimento) · CEP x Região\[Região\] · lista de Situação Vínculo                                        |

#### Página 2 — Setor de Atividades (CNAE)

| **Visual**                          | **Campos**                                                                           |
|-------------------------------------|--------------------------------------------------------------------------------------|
| Barras: Top 10 por empregos         | Eixo = Setor · Valor = Total Vínculos CLT · filtro Top N = 10 por Total Vínculos CLT |
| Barras: Top 10 por estabelecimentos | Eixo = Setor · Valor = Total de Estabelecimentos · filtro Top N = 10                 |
| Barras: peso de cada Seção          | Eixo = Seção CNAE · Valores = % Participação Vínculos e % Participação Estab         |
| Barras: indústria por setor         | Eixo = Setor Completo · Valor = Total Vínculos CLT · filtro Seção CNAE = C           |
| Tabela por porte                    | Faixa de Porte · Setor Completo · Total Vínculos CLT                                 |

#### Página 3 — PIB e Emprego

| **Visual**                                     | **Campos**                                                                         |
|------------------------------------------------|------------------------------------------------------------------------------------|
| Colunas empilhadas: valor adicionado por setor | Eixo = VAB setorial\[ano\] · Legenda = setor · Valor = Soma de vab_real_2023       |
| Linha: PIB 2002–2023                           | Eixo = PIB anual\[ano\] · Valor = Soma de pib_real_2023 (unidade: bilhões)         |
| Barras: variação anual do PIB                  | Eixo = PIB anual\[ano\] · Valor = Soma de cresc_real_pct                           |
| Colunas: peso no emprego × no valor adicionado | Eixo = Cruzamento\[setor\] · Valores = part_emprego_pct e part_vab_pct             |
| Tabela de produtividade relativa               | setor · vinculos_ativos · part_emprego_pct · part_vab_pct · produtividade_relativa |
| Caixa de texto                                 | "O que isso mostra para a gestão", com a leitura dos números                       |

#### Página 4 — Regiões e Tecnologia

| **Visual**                                   | **Campos**                                                                                                 |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------|
| Segmentação de região                        | CEP x Região\[Região\]                                                                                     |
| Barras: vínculos por região oficial          | Eixo = CEP x Região\[Região\] · Valor = Total Vínculos Ativos                                              |
| Barras: vínculos por tipo de atividade       | Eixo = Tipo de Atividade · Valor = Total Vínculos Ativos                                                   |
| Barras: vínculos por intensidade tecnológica | Eixo = Intensidade Tecnológica OCDE · Valor = Total Vínculos Ativos                                        |
| Barras: vínculos por macroprocesso logístico | Eixo = Macroprocesso Logístico · Valor = Total Vínculos Ativos · classificar pelo eixo, em ordem crescente |
| Caixa de texto                               | "O que isso mostra para a gestão"                                                                          |

#### Página 5 — Notas Metodológicas

Caixas de texto com: limites dos dados, regras do cruzamento com o PIB, decisões do grupo, ferramentas usadas e definições (com vínculo, sem vínculo, vínculo ativo, Seção CNAE e porte). O texto está no Relatório do painel Power BI (`docs/final/Relatorio_PowerBI_Final`).

### Passo 13 — Conferir e publicar

1.  Compare os números de cada página com a tabela de valores esperados do Guia de atualização (Passo 5 do guia). Por exemplo: 47.339 estabelecimentos, 206.717 vínculos ativos e PIB de R\$ 61 bilhões em 2023.

2.  Publique em **Página Inicial → Publicar** e, para um link aberto ao público, use **Arquivo → Inserir → Publicar na Web** no Power BI Service.

## Parte 3 — Atualizar com um novo ano da RAIS

1.  Baixe o arquivo de estabelecimentos do novo ano (Passo 1) e rode o notebook 01 com ele.

2.  Rode a célula do CNEFE no notebook 01b. Se aparecerem CEPs novos sem bairro, rode também as Células 4 a 8 para eles.

3.  Monte a aba Base_RAIS do novo ano: uma linha por estabelecimento, na mesma ordem do `RAIS_SJC_completo.csv`, com as colunas da aba atual (ID, situação, vínculos, faixa de tamanho e a hierarquia da CNAE 2.3: seção, divisão, grupo, classe e subclasse com seus nomes).

4.  No notebook 02, troque o ano 2024 pelo novo ano (nomes de arquivo e coluna Ano Base) e os totais conferidos (47.339 estabelecimentos e 206.717 vínculos ativos). Rode o notebook e gere as planilhas do painel (Passo 5).

5.  Atualize a planilha do IBGE com o PIB mais recente (Sidra 5938) e refaça a aba PIB anual (trecho C).

6.  No Power BI, clique em Atualizar e confira os totais novos.

7.  Registre no Log de Decisões (`docs/final/06-Decisoes-de-Dados`) cada mudança de regra ou de fonte, com uma nova entrada DEC.

## Onde está cada coisa

| **Pasta ou arquivo**                     | **O que é**                                                                                                             |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `notebooks/`                             | Códigos Python: 01 (ETL da RAIS), 01b (geocodificação dos CEPs) e 02 (base única)                                       |
| `evidencias/codigos-tratamento-dados.md` | O código dos três notebooks explicado etapa por etapa                                                                   |
| `dados/`                                 | Bases tratadas, arquivos de entrada e de referência, com dicionário de dados em `dados/README.md`                       |
| `powerbi/pbip/`                          | Projeto do painel Power BI (versão final)                                                                               |
| `powerbi/fontes/`                        | As 4 planilhas que o painel lê                                                                                          |
| `docs/final/`                            | Log de Decisões, fórmulas e relatório do painel, guia de atualização, respostas aos requisitos do cliente e este manual |
