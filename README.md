# 📊 Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Projeto da disciplina **API (Aprendizagem por Projetos Integrados)** do curso de **Logística** da **Fatec São José dos Campos**.

O projeto constrói uma ferramenta de inteligência de dados, em parceria com o **CADI** e a **Secretaria de Desenvolvimento Econômico** do município, que consolida e disponibiliza indicadores públicos sobre os estabelecimentos industriais e de serviços da cidade. O produto final é um painel interativo em **Power BI**, nos moldes do [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio) ([ver painel](https://sict.rs.gov.br/painel-do-observatorio)).

---

## 🎯 Contexto

| Item | Descrição |
|---|---|
| **Cliente** | CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos |
| **Orientadores** | Prof. José Jaétis (M2) e Prof. Marcus Nascimento (P2) |
| **Metodologia** | Scrum, em 3 sprints |
| **Entrega final** | Feira de Soluções, 03/12/2026 |

## 🧩 O problema

São José dos Campos é um polo industrial, tecnológico e de serviços do Vale do Paraíba, com destaque para os setores aeroespacial, automotivo e de tecnologia da informação. Apesar disso, o município não tem uma ferramenta pública e centralizada que reúna indicadores sobre o seu ecossistema produtivo, o que dificulta o acompanhamento de políticas de desenvolvimento econômico local.

Os dados públicos existem, mas não estão prontos para análise: têm inconsistências e não oferecem uma visão consolidada de quem emprega, onde e em quais setores. O projeto trata esses dados, documenta cada decisão tomada e entrega os resultados em um painel interativo.

> Na Sprint 1, o escopo mudou de um relatório voltado à contratação de mão de obra para um observatório abrangente do ecossistema municipal, inspirado no modelo do Observatório da Inovação RS.

## 🎯 Objetivos

- Desenvolver um pipeline de ETL em Python, no Google Colab, que filtre e trate os dados da RAIS para São José dos Campos.
- Identificar e documentar formalmente as inconsistências da base bruta, garantindo a confiabilidade dos indicadores.
- Construir um painel em Power BI com indicadores de emprego, natureza dos estabelecimentos e distribuição geográfica.
- Integrar os dados do PIB dos Municípios (IBGE) como segunda fonte do observatório.

---

## 🛠️ Tecnologias

- **Python 3+** no Google Colab, para extração e tratamento dos dados (ETL). O arquivo bruto tem cerca de 3,27 GB, por isso é lido em modo sequencial (streaming) com a biblioteca `csv`, sem carregá-lo inteiro na memória.
- **Power BI**, para o dashboard.
- **GitHub**, para versionamento do código e da documentação.

## 🗂️ Fontes de dados

| Fonte | Uso |
|---|---|
| **RAIS** (Ministério do Trabalho e Emprego), arquivo público `RAIS_ESTAB_PUB`, ano-base 2024 | Estabelecimentos e vínculos de emprego |
| **PIB dos Municípios** (IBGE), ano 2023 | Contexto econômico do município |
| [**Observatório da Inovação RS**](https://sict.rs.gov.br/observatorio) | Referência de modelo para o dashboard |

### Resultado do tratamento da RAIS

| Etapa | Registros |
|---|---|
| Estabelecimentos no arquivo nacional | 12.643.067 |
| Estabelecimentos de São José dos Campos (código IBGE 354990) | 47.339 |
| Do tipo Cnpj | 46.244 |
| Do tipo Caepf | 708 |
| Do tipo Cno | 387 |

---

## 📁 Estrutura do repositório

```
observatorio-sjc/
├── README.md
├── MVP/            MVP de cada sprint
├── docs/           Documentação Scrum e relatório técnico
├── notebooks/      ETL em Google Colab (Python)
├── powerbi/        Dashboard
└── evidencias/     Prints e comprovações de cada sprint
```

## 📚 Documentação

- [MVP da Sprint 1](MVP/sp1.md)
- [Relatório da Sprint 1](RELATORIO_SPRINT_1.md)
- Visão e Escopo, Backlog do Produto, Backlog das Sprints, DoR, DoD e Log de Decisões de Dados: pasta [`docs/`](docs/)

---

## ▶️ Como reproduzir o tratamento dos dados

1. Baixe o arquivo público `RAIS_ESTAB_PUB` no site do Ministério do Trabalho e Emprego.
2. Abra o notebook da pasta `notebooks/` no Google Colab e carregue o arquivo.
3. Execute todas as células. O notebook lê o arquivo linha a linha e mantém apenas os registros do município 354990.
4. Os arquivos CSV tratados são gerados ao final.

---

## 🗓️ Sprints

| Sprint | Objetivo | Entrega | Status |
|---|---|---|---|
| 01 | Fundação técnica: pipeline de dados, tratamento de inconsistências e documentação de metodologia | 28/09/2026 (confirmada) | Concluída |
| 02 | Análises centrais e mapeamento geográfico no Power BI | 26/10/2026 (detalhamento a confirmar) | A iniciar |
| 03 | Consolidação do dashboard, relatório técnico final e apresentação ao cliente | 23/11/2026 (detalhamento a confirmar) | A iniciar |

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

### Sprint 2: Análises centrais e mapeamento geográfico

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. | O mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%. | 2 | A fazer |
| US07 | Como gestor público, quero ver um ranking das empresas que mais contratam em SJC, para que eu possa direcionar políticas de fomento ao emprego. | Visual no Power BI lista os estabelecimentos ordenados por número de vínculos ativos, com filtro por setor (agregado, sem identificação nominal; ver DEC-004). | 7 | A fazer |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. | Visual mostra a evolução de contratações por setor (CNAE agrupado). | 8 | A fazer |
| US09 | Como gestor público, quero visualizar o impacto do ecossistema de empresas no PIB municipal (dados do IBGE), para que eu possa avaliar a relevância econômica de cada setor. | O dashboard cruza dados RAIS 2024 e PIB dos Municípios (IBGE) 2023 por setor, com fonte, ano e defasagem indicados (DEC-005). | 9 | A fazer |

### Sprint 3: Consolidação e entrega final

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | O painel exibe as contratações do período mais recente disponível nos dados, ordenadas por data. | 10 | A fazer |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | O dashboard publicado reúne todos os visuais das sprints anteriores. Relatório técnico e apresentação entregues e aprovados pelos orientadores. | 11 | A fazer |

---

## 🔍 Log de Decisões de Dados

Os problemas encontrados na RAIS e o tratamento de cada um estão registrados no Log de Decisões de Dados.

| ID | Problema | Decisão | Status |
|---|---|---|---|
| DEC-001 | 30.470 estabelecimentos (64,37%) com RAIS negativa, ou seja, sem vínculos ativos | Manter na base e tratar como indicador próprio do painel, pois o cliente esclareceu que não é um erro a descartar | Fechada |
| DEC-002 | A base mistura três tipos de estabelecimento (Cnpj, Caepf e Cno) | Segmentar os dados, com recorte padrão em Cnpj | Fechada |
| DEC-003 | O arquivo não tem campo de ano ou competência | Ano-base 2024, confirmado pelo cliente | Fechada |
| DEC-004 | A base pública não traz razão social, CNPJ ou CPF dos estabelecimentos | Em aberto, aguardando o cliente sobre uma base identificada. Contingência: indicadores agregados por setor e região | **Aberta** |
| DEC-005 | O PIB dos Municípios mais recente publicado é a série 2022–2023 | Cruzar a RAIS 2024 com o PIB 2023, documentando a defasagem de 1 ano | Fechada |

---

## 👥 Equipe

| Integrante | Papel | LinkedIn |
|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Product Owner | [pedro-henrique-oliveira-de-carvalho-75bb07427](https://www.linkedin.com/in/pedro-henrique-oliveira-de-carvalho-75bb07427) |
| Juliano Souza Santana | Scrum Master | [juliano-santana-776992249](https://www.linkedin.com/in/juliano-santana-776992249) |
| Beatriz Oliveira Sepulvida | Scrum Team | [beatriz-sepulvida](https://www.linkedin.com/in/beatriz-sepulvida) |
| Caio Moreira | Scrum Team | [caiomoreiradearaujo](https://www.linkedin.com/in/caiomoreiradearaujo) |
| Hemilly Christiny da Silva Freitas | Scrum Team | [hemilly-freitas-31a509269](https://www.linkedin.com/in/hemilly-freitas-31a509269) |
| João Pedro Faria Vital de Souza | Scrum Team | [joao-pedro-a2b6122b7](https://www.linkedin.com/in/joao-pedro-a2b6122b7) |
| Milena Silva Nogueira | Scrum Team | [milenasnogueira](https://www.linkedin.com/in/milenasnogueira) |
| Thalya Awany Berti | Scrum Team | [thalya-awany-berti-773923266](https://www.linkedin.com/in/thalya-awany-berti-773923266) |

**Orientador (M2):** José Jaétis · **Professor (P2):** Marcus Nascimento

---

## 📖 Referências

- DE NEGRI, J. A. et al. *Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD*. Texto para Discussão nº 840. Brasília: IPEA, 2001. [Link](https://repositorio.ipea.gov.br/handle/11058/2155)
- MORELLI, A. B.; FIEDLER, A. C.; CUNHA, A. L. *Um banco de dados de empregos formais georreferenciados em cidades brasileiras*. arXiv:2303.09602, 2023. [Link](https://arxiv.org/pdf/2303.09602)
- SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RS (SICT). *Observatório da Inovação RS*. Porto Alegre, 2025. [Link](https://sict.rs.gov.br/observatorio)
- SILVA, V. P.; LIMA, M. E. O. *Microdados RAIS e estudos sobre o mercado de trabalho no Brasil*. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. [Link](https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244)

---

## 📄 Licença

Projeto acadêmico desenvolvido na Fatec São José dos Campos.
