# 📊 Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Projeto da disciplina **API (Aprendizagem por Projetos Integrados)** do curso de **Logística** da **Fatec São José dos Campos**.

O projeto constrói uma ferramenta de inteligência de dados, em parceria com o **CADI** e a **Secretaria de Desenvolvimento Econômico** do município, que consolida e disponibiliza indicadores públicos sobre os estabelecimentos industriais e de serviços da cidade. O produto final é um painel interativo em **Power BI**, nos moldes do [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio) ([ver painel](https://sict.rs.gov.br/painel-do-observatorio)).

**Acesso rápido:** [MVP da Sprint 2](MVP/sp2.md) · [Relatório da Sprint 2](RELATORIO_SPRINT_2.md) · [Log de Decisões](docs/06-Decisoes-de-Dados.md) · [Backlog do Produto](docs/02-Backlog-do-Produto.md) · [Dicionário de dados](dados/README.md) · [Painel (.pbix)](powerbi/PowerbiATT_Api_Sprint2.pbix)

---

## 🎯 Contexto

| Item | Descrição |
|---|---|
| **Cliente** | CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos |
| **Orientadores** | Prof. José Jaétis (M2) e Prof. Marcus Nascimento (P2) |
| **Metodologia** | Scrum, em 3 sprints |
| **Entrega final** | Feira de Soluções, 03/12/2026 |
| **Situação atual** | Sprint 2 entregue em 26/10/2026 · Sprint 3 em andamento |

## 🧩 O problema

São José dos Campos é um polo industrial, tecnológico e de serviços do Vale do Paraíba, com destaque para os setores aeroespacial, automotivo e de tecnologia da informação. Apesar disso, o município não tem uma ferramenta pública e centralizada que reúna indicadores sobre o seu ecossistema produtivo, o que dificulta o acompanhamento de políticas de desenvolvimento econômico local.

Os dados públicos existem, mas não estão prontos para análise: têm inconsistências e não oferecem uma visão consolidada de quem emprega, onde e em quais setores. O projeto trata esses dados, documenta cada decisão tomada e entrega os resultados em um painel interativo.

> Na Sprint 1, o escopo mudou de um relatório voltado à contratação de mão de obra para um observatório abrangente do ecossistema municipal, inspirado no modelo do Observatório da Inovação RS.

## 🎯 Objetivos

- Desenvolver um pipeline de ETL em Python, no Google Colab, que filtre e trate os dados da RAIS para São José dos Campos.
- Identificar e documentar formalmente as inconsistências da base bruta, garantindo a confiabilidade dos indicadores.
- Construir um painel em Power BI com indicadores de emprego, natureza dos estabelecimentos e distribuição geográfica.
- Integrar os dados do PIB dos Municípios (IBGE) como segunda fonte do observatório.
- Classificar os estabelecimentos pelas regiões oficiais do município e pelo tipo de atividade (manufatura, tecnologia, logística, serviços especializados).

---

## 🛠️ Tecnologias

- **Python 3+** no Google Colab, para extração e tratamento dos dados (ETL). O arquivo bruto tem cerca de 3,27 GB, por isso é lido em modo sequencial (streaming) com a biblioteca `csv`, sem carregá-lo inteiro na memória.
- **BrasilAPI** e **Nominatim (OpenStreetMap)**, para geocodificar os CEPs no nível de bairro.
- **Power BI**, para o dashboard.
- **GitHub**, para versionamento do código e da documentação.

## 🗂️ Fontes de dados

| Fonte | Uso |
|---|---|
| **RAIS** (Ministério do Trabalho e Emprego), arquivo público `RAIS_ESTAB_PUB`, ano-base 2024 | Estabelecimentos e vínculos de emprego |
| **PIB dos Municípios** (IBGE): PIB 2002–2023 e valor adicionado por setor até 2021 | Peso de cada setor na economia do município |
| **CNAE 2.3** (IBGE/CONCLA) | Validação dos códigos e descrições das atividades |
| **Plano Diretor** da Prefeitura de São José dos Campos (estudo "Regiões Urbanas") | Divisão regional oficial: bairros de cada região |
| [**Observatório da Inovação RS**](https://sict.rs.gov.br/observatorio) | Referência de modelo para o dashboard |

### Resultado do tratamento da RAIS

| Etapa | Registros |
|---|---|
| Estabelecimentos no arquivo nacional | 12.643.067 |
| Estabelecimentos de São José dos Campos (código IBGE 354990) | 47.339 |
| Do tipo CNPJ | 46.244 |
| Do tipo CAEPF | 708 |
| Do tipo CNO | 387 |

### Resultado da Sprint 2

| Indicador | Valor |
|---|---|
| Com vínculos ativos em 31/12/2024 | 15.058 estabelecimentos (31,8%) |
| Vínculos ativos em 31/12/2024 | 206.717 |
| Estabelecimentos com região oficial | 47.334 (99,99%) |
| Estabelecimentos com ponto no mapa | 37.084 (78,3%) |
| Vínculos em atividades de alta e média-alta tecnologia (OCDE) | 28.804 (13,9%) |
| Indústria: emprego privado × valor adicionado privado | 24,7% × 45,8% (índice 1,86) |
| PIB de São José dos Campos em 2023 | R$ 61,4 bilhões |

![Vínculos ativos por região oficial](evidencias/sprint2_vinculos_por_regiao.png)

---

## 📁 Estrutura do repositório

```
.
├── README.md
├── RELATORIO_SPRINT_1.md   Relatório da Sprint 1
├── RELATORIO_SPRINT_2.md   Relatório da Sprint 2
├── MVP/                    MVP de cada sprint (sp1.md, sp2.md)
├── docs/                   Documentação Scrum e relatórios técnicos (.docx e .md)
├── dados/                  Bases tratadas prontas para o Power BI (com dicionário)
│   ├── entrada/            Arquivos de entrada do notebook 02
│   └── referencia/         Tabela bairro → região e CNAE 2.3
├── notebooks/              01: ETL da RAIS (Sprint 1) · 02: base única do Power BI (Sprint 2)
├── powerbi/                Arquivo do painel (.pbix)
└── evidencias/             Prints, gráficos, guias e comprovações de cada sprint
```

## 📚 Documentação

- [MVP da Sprint 1](MVP/sp1.md)
- [Relatório da Sprint 1](RELATORIO_SPRINT_1.md)
- [MVP da Sprint 2](MVP/sp2.md)
- [Relatório da Sprint 2](RELATORIO_SPRINT_2.md)
- Base única para o Power BI: [`dados/RAIS_SJC_2024_PowerBI.csv`](dados/RAIS_SJC_2024_PowerBI.csv) (47.339 estabelecimentos, 46 colunas) e [guia de importação](evidencias/Importacao_PowerBI_RAIS_SJC.txt)

Documentos da pasta `docs/` (a coluna **Ler no GitHub** abre a versão em Markdown):

| Documento | Word | Ler no GitHub |
|---|---|---|
| Guia do repositório (README em Word) | [00-README.docx](docs/00-README.docx) | — |
| Visão e Escopo | [01-Visao-e-Escopo.docx](docs/01-Visao-e-Escopo.docx) | — |
| Backlog do Produto | [02-Backlog-do-Produto.docx](docs/02-Backlog-do-Produto.docx) | [02-Backlog-do-Produto.md](docs/02-Backlog-do-Produto.md) |
| Backlog da Sprint 1 | [03-Backlog-Sprint-1.docx](docs/03-Backlog-Sprint-1.docx) | — |
| Checklist DoR (Definition of Ready) | [04-DoR-Checklist.docx](docs/04-DoR-Checklist.docx) | — |
| DoD (Definition of Done) | [05-DoD.docx](docs/05-DoD.docx) | — |
| Log de Decisões de Dados (DEC-001 a DEC-022) | [06-Decisoes-de-Dados.docx](docs/06-Decisoes-de-Dados.docx) | [06-Decisoes-de-Dados.md](docs/06-Decisoes-de-Dados.md) |
| Relatório Técnico da Sprint 1 | [07-Relatorio-Tecnico-Sprint-1.docx](docs/07-Relatorio-Tecnico-Sprint-1.docx) | — |
| Backlog da Sprint 2 | [08-Backlog-Sprint-2.docx](docs/08-Backlog-Sprint-2.docx) | [08-Backlog-Sprint-2.md](docs/08-Backlog-Sprint-2.md) |
| Backlog da Sprint 3 | [09-Backlog-Sprint-3.docx](docs/09-Backlog-Sprint-3.docx) | [09-Backlog-Sprint-3.md](docs/09-Backlog-Sprint-3.md) |
| Relatório Técnico da Sprint 2 | [10-Relatorio-Tecnico-Sprint-2.docx](docs/10-Relatorio-Tecnico-Sprint-2.docx) | — |
| Relatório de Desenvolvimento, Anexo 8 — Sprint 1 | [Relatorio_Sprint1_Anexo8.docx](docs/Relatorio_Sprint1_Anexo8.docx) | — |
| Relatório de Desenvolvimento, Anexo 8 — Sprint 2 | [Relatorio_Sprint2_Anexo8.docx](docs/Relatorio_Sprint2_Anexo8.docx) | — |

---

## ▶️ Como reproduzir o tratamento dos dados

**Sprint 1 — ETL da RAIS** ([`notebooks/01_ETL_RAIS_SJC.ipynb`](notebooks/01_ETL_RAIS_SJC.ipynb))

1. Baixe o arquivo público `RAIS_ESTAB_PUB` no site do Ministério do Trabalho e Emprego.
2. Abra o notebook no Google Colab e carregue o arquivo.
3. Execute todas as células. O notebook lê o arquivo linha a linha e mantém apenas os registros do município 354990.
4. Os arquivos CSV tratados são gerados ao final (`dados/entrada/RAIS_SJC_completo.csv`).

**Sprint 2 — Base única do Power BI** ([`notebooks/02_Base_PowerBI_SJC.ipynb`](notebooks/02_Base_PowerBI_SJC.ipynb))

1. Abra o notebook no Google Colab (*Arquivo → Abrir notebook → GitHub* e cole o endereço deste repositório).
2. Clique em *Ambiente de execução → Executar tudo*. A primeira célula baixa o repositório com os arquivos de `dados/entrada/` e `dados/referencia/`.
3. O notebook gera `dados/RAIS_SJC_2024_PowerBI.csv` e confere os totais (47.339 estabelecimentos, 206.717 vínculos).
4. Para atualizar a região oficial, edite `dados/referencia/bairros_regiao_sjc.csv` e rode de novo.
5. No Power BI, importe a base seguindo [`evidencias/Importacao_PowerBI_RAIS_SJC.txt`](evidencias/Importacao_PowerBI_RAIS_SJC.txt) (CEP e CNAE como texto; latitude e longitude com localidade "Inglês (EUA)").

---

## 🗓️ Sprints

As entregas de cada sprint estão marcadas com tags no GitHub (`sprint-1`, `sprint-2`), na aba [Tags](https://github.com/projetoapi08/Observat-rio-do-Ecossistema-Industrial-e-de-Servi-os-de-S-o-Jos-dos-Campos/tags).

| Sprint | Objetivo | Entrega | Status |
|---|---|---|---|
| 01 | Fundação técnica: pipeline de dados, tratamento de inconsistências e documentação de metodologia | 28/09/2026 (confirmada) | Concluída |
| 02 | Análises centrais e mapeamento geográfico no Power BI | 26/10/2026 | Entregue: 2 concluídas, 2 parciais |
| 03 | Consolidação do dashboard, relatório técnico final e apresentação ao cliente | 23/11/2026 | Em andamento |

## 🔑 Backlog do Produto

A coluna **Prior.** é a ordem de prioridade definida no Backlog do Produto (1 é a mais alta).

### Sprint 1: Fundação técnica ✅

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US01 | Como equipe do projeto, quero um pipeline de ETL no Google Colab (Python) que extraia e prepare os dados brutos da RAIS, para que os dados estejam prontos para análise no Power BI. | O notebook executa de ponta a ponta e gera os CSVs de saída sem erros. | 1 | Concluído |
| US02 | Como equipe do projeto, quero filtrar e padronizar os dados para o município de São José dos Campos (código 354990), para que a análise reflita exclusivamente o ecossistema local. | 100% dos registros do CSV final pertencem ao município 354990. | 3 | Concluído |
| US03 | Como equipe do projeto, quero identificar e tratar as inconsistências dos dados da RAIS (vínculos zerados, mistura de tipos de estabelecimento, ausência de ano e de identificação), para que o dashboard não apresente conclusões distorcidas. | Cada inconsistência está registrada no Log de Decisões (DEC-XXX) com o tratamento adotado. | 4 | Concluído |
| US04 | Como equipe do projeto, quero produzir a documentação formal do projeto (Visão e Escopo, DoR, DoD, Log de Decisões), para que o trabalho siga a metodologia Scrum/API exigida pela disciplina. | Todos os documentos da Sprint 1 aprovados pelo orientador. | 5 | Concluído |
| US05 | Como equipe do projeto, quero estruturar o repositório no GitHub (docs/, notebooks/, powerbi/), para que o código, os dados e a documentação fiquem organizados e versionados. | Repositório publicado com as três pastas e README inicial. | 6 | Concluído |

### Sprint 2: Análises centrais e mapeamento geográfico 🟡

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. | O mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%. | 2 | Parcial: 99,99% com região e 78% com ponto; mapa por coordenadas na Sprint 3 |
| US07 | Como gestor público, quero ver um ranking das empresas que mais contratam em SJC, para que eu possa direcionar políticas de fomento ao emprego. | Visual no Power BI lista os estabelecimentos ordenados por número de vínculos ativos, com filtro por setor (agregado, sem identificação nominal; ver DEC-004). | 7 | Concluído (Top 10 de setores) |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. | Visual mostra a evolução de contratações por setor (CNAE agrupado). | 8 | Parcial: base de um só ano; série histórica na Sprint 3 |
| US09 | Como gestor público, quero visualizar o impacto do ecossistema de empresas no PIB municipal (dados do IBGE), para que eu possa avaliar a relevância econômica de cada setor. | O dashboard cruza dados RAIS 2024 e PIB dos Municípios (IBGE) 2023 por setor, com fonte, ano e defasagem indicados (DEC-005). | 9 | Concluído |

### Sprint 3: Consolidação e entrega final

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | O painel exibe as contratações do período mais recente disponível nos dados, ordenadas por data. | 10 | A fazer (a RAIS Estabelecimentos não tem data de admissão) |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | O dashboard publicado reúne todos os visuais das sprints anteriores. Relatório técnico e apresentação entregues e aprovados pelos orientadores. | 11 | A fazer |

---

## 🔍 Log de Decisões de Dados

Os problemas encontrados na RAIS e o tratamento de cada um estão registrados no Log de Decisões de Dados.

| ID | Problema | Decisão | Status |
|---|---|---|---|
| DEC-001 | 30.470 estabelecimentos (64,37%) com RAIS negativa, ou seja, sem vínculos ativos | Manter na base, com indicador próprio, pois o cliente esclareceu que não é um erro a descartar. As análises de contratação usam por padrão os 16.869 estabelecimentos com vínculo ativo | Fechada |
| DEC-002 | A base mistura três tipos de estabelecimento (CNPJ, CAEPF e CNO) | Segmentar os dados, com recorte padrão em CNPJ | Fechada |
| DEC-003 | O arquivo não tem campo de ano ou competência | Ano-base 2024, confirmado pelo cliente | Fechada |
| DEC-004 | A base pública não traz razão social, CNPJ ou CPF dos estabelecimentos | Em aberto, aguardando o cliente sobre uma base identificada. Contingência: indicadores agregados por setor e região | **Aberta** |
| DEC-005 | O PIB dos Municípios mais recente publicado é a série 2022–2023 | Cruzar a RAIS 2024 com o PIB 2023, documentando a defasagem de 1 ano | Fechada |
| DEC-006 / 009 | IBGE só detalha o valor adicionado por setor até 2021 | Comparar VAB 2021 com o emprego de 2024, mostrando o ano de cada fonte | Fechada |
| DEC-008 | Valores do PIB de anos diferentes | Corrigir pelo IPCA para reais de 2023 | Fechada |
| DEC-011 | 53 registros com indicador de RAIS negativa = 2 | Categoria própria, somada a "Sem vínculo" | Fechada |
| DEC-013 | Administração pública ausente da base RAIS | Excluir do cruzamento com o PIB | Fechada |
| DEC-014 | Nível de agregação dos setores | Seção CNAE 2.0, padrão IBGE | Fechada |
| DEC-015 | Região oficial ausente dos arquivos | Bairro → região pelo Plano Diretor; setor do CEP para ambíguos | **Aberta** |
| DEC-016 a 018 | Coordenadas corrompidas, bairros homônimos e CEPs sem localização | Coordenadas corretas, alerta no ponto e região pelo bairro | 016 e 018 fechadas · 017 **aberta** |
| DEC-019 a 021 | Situação detalhada, descrições CNAE 2.3 e classificações pedidas pelo cliente | Novas colunas na base única | Fechadas |
| DEC-022 | Mapa localizava pelo texto do CEP | Base única com latitude/longitude | **Aberta** |

> Detalhes de cada decisão em `docs/06-Decisoes-de-Dados.docx`. DEC-007, DEC-010 e DEC-012 ainda precisam ser transcritas para o log.

---

## 👥 Equipe

| Integrante | Papel | Função na Sprint 2 | LinkedIn |
|---|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Product Owner | Apoio geral | [pedro-henrique-oliveira-de-carvalho-75bb07427](https://www.linkedin.com/in/pedro-henrique-oliveira-de-carvalho-75bb07427) |
| Juliano Souza Santana | Scrum Master | Dados e documentação | [juliano-santana-776992249](https://www.linkedin.com/in/juliano-santana-776992249) |
| Beatriz Oliveira Sepulvida | Scrum Team | CSV e Excel | [beatriz-sepulvida](https://www.linkedin.com/in/beatriz-sepulvida) |
| Caio Moreira | Scrum Team | Tratamento de dados | [caiomoreiradearaujo](https://www.linkedin.com/in/caiomoreiradearaujo) |
| Hemilly Christiny da Silva Freitas | Scrum Team | Documentação | [hemilly-freitas-31a509269](https://www.linkedin.com/in/hemilly-freitas-31a509269) |
| João Pedro Faria Vital de Souza | Scrum Team | Apoio geral | [joao-pedro-a2b6122b7](https://www.linkedin.com/in/joao-pedro-a2b6122b7) |
| Milena Silva Nogueira | Scrum Team | Power BI | [milenasnogueira](https://www.linkedin.com/in/milenasnogueira) |
| Thalya Awany Berti | Scrum Team | Power BI | [thalya-awany-berti-773923266](https://www.linkedin.com/in/thalya-awany-berti-773923266) |

**Orientador (M2):** José Jaétis · **Professor (P2):** Marcus Nascimento

---

## 📖 Referências

- DE NEGRI, J. A. et al. *Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD*. Texto para Discussão nº 840. Brasília: IPEA, 2001. [Link](https://repositorio.ipea.gov.br/handle/11058/2155)
- GALINDO-RUEDA, F.; VERGER, F. *OECD taxonomy of economic activities based on R&D intensity*. OECD Science, Technology and Industry Working Papers, n. 2016/04. Paris: OECD Publishing, 2016.
- IBGE. *Classificação Nacional de Atividades Econômicas – CNAE Subclasses 2.3*. Rio de Janeiro: IBGE/CONCLA. [Link](https://concla.ibge.gov.br)
- MORELLI, A. B.; FIEDLER, A. C.; CUNHA, A. L. *Um banco de dados de empregos formais georreferenciados em cidades brasileiras*. arXiv:2303.09602, 2023. [Link](https://arxiv.org/pdf/2303.09602)
- SÃO JOSÉ DOS CAMPOS (Município). *Plano Diretor: estudo técnico — Regiões Urbanas*. Prefeitura Municipal. [Link](https://www.sjc.sp.gov.br/media/1ascp0it/7_regioes_urbanas.pdf)
- SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RS (SICT). *Observatório da Inovação RS*. Porto Alegre, 2025. [Link](https://sict.rs.gov.br/observatorio)
- SILVA, V. P.; LIMA, M. E. O. *Microdados RAIS e estudos sobre o mercado de trabalho no Brasil*. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. [Link](https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244)

---

## 📄 Licença

Projeto acadêmico desenvolvido na Fatec São José dos Campos.
