# Aprendizado por Projeto Integrado (API) - Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Projeto baseado na metodologia ágil SCRUM, procurando desenvolver a Proatividade, Autonomia, Colaboração e Entrega de Resultados dos estudantes envolvidos.

> Status do projeto: **Sprint 3 em andamento** · [MVP da Sprint 3](MVP/sp3.md)
>
> Painel publicado: [🌐 abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) (abre no navegador, sem login)
>
> Documentação: [📖 pasta docs/](docs/)

# Índice
* [Projeto (API)](#projeto-api)
* [Equipe](#equipe)
* [Objetivo do Projeto](#objetivo-do-projeto)
* [Tecnologias Utilizadas](#tecnologias-utilizadas)
* [Product Backlog](#product-backlog)
* [Competências desenvolvidas](#competências-desenvolvidas)
* [Registro das Sprints](#registro-das-sprints)
* [Documentação e estrutura do repositório](#documentação-e-estrutura-do-repositório)


# Projeto (API)
Projeto pedagógico alicerçado na Metodologia API para ensino-aprendizado focado no desenvolvimento de competências e fundamentada nos pilares de aprendizado com problemas reais (RPBL), validação externa e mentalidade ágil.
Uso de estratégias para entender o problema, conceber uma solução viável ao desenvolver e implementar o MVP seguido de sua operação (CDIO).
Os resultados dos projetos devem obedecer ao Aviso Legal disponível no site da Fatec SJC com definição das datas do kickoff e das sprints.

O projeto é desenvolvido no curso de **Logística** da **Fatec São José dos Campos**, em parceria com o **CADI** e a **Secretaria de Desenvolvimento Econômico de São José dos Campos**. É uma ferramenta de Business Intelligence em **Power BI** que mapeia o ecossistema industrial e de serviços do município a partir dos dados de emprego formal da **RAIS** (Ministério do Trabalho e Emprego) e do **PIB dos Municípios** (IBGE), nos moldes do [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio).

**Orientador (M2):** Prof. José Jaétis · **Professor (P2):** Prof. Marcus Nascimento


# Equipe

| Função | Nome | LinkedIn & GitHub |
| :---: | :--- | :---: |
| Product Owner | Pedro Henrique Oliveira de Carvalho | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/pedro-henrique-oliveira-de-carvalho-75bb07427) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/po032953-dev) |
| Scrum Master | Juliano Souza Santana | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/juliano-santana-776992249) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/santanajuliano997-beep) |
| Team Member | Beatriz Oliveira Sepulvida | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/beatriz-sepulvida) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/beatrizsepulvida08) |
| Team Member | Caio Moreira | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/caiomoreiradearaujo) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/CaioMoreiraujo) |
| Team Member | Hemilly Christiny da Silva Freitas | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/hemilly-freitas-31a509269) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/hemillyfreitas) |
| Team Member | João Pedro Faria Vital de Souza | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/joao-pedro-a2b6122b7) |
| Team Member | Milena Silva Nogueira | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/milenasnogueira) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/milenanogueira) |
| Team Member | Thalya Awany Berti | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/thalya-awany-berti-773923266) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/ThalyaAwany) |


# Objetivo do Projeto

São José dos Campos é um polo industrial, tecnológico e de serviços do Vale do Paraíba, mas não tem uma ferramenta pública e centralizada que reúna indicadores do seu ecossistema produtivo. Os dados públicos existem, mas têm inconsistências e não mostram de forma consolidada quem emprega, onde e em quais setores. Os objetivos estabelecidos para este projeto são:

* Desenvolver um pipeline de tratamento de dados (ETL) em Python, no Google Colab, que filtre e trate a RAIS 2024 para São José dos Campos (código IBGE 354990);
* Identificar e documentar formalmente cada inconsistência da base no [Log de Decisões de Dados](docs/06-Decisoes-de-Dados.md), garantindo a confiabilidade dos indicadores;
* Construir um painel em Power BI com indicadores de emprego, setores de atividade (CNAE), porte e distribuição geográfica dos estabelecimentos pelas regiões oficiais do município;
* Cruzar o emprego formal com o PIB dos Municípios (IBGE) para medir o peso de cada setor na economia local e apoiar decisões de desenvolvimento econômico.


# Tecnologias Utilizadas

* Python 3 (Google Colab)
* Power BI
* Microsoft Excel
* GitHub
* BrasilAPI e Nominatim (OpenStreetMap), para geocodificar os CEPs
* Microsoft Word e Microsoft Teams
* WhatsApp (comunicação com o cliente e a equipe)


# Product Backlog

| Rank | Prioridade | User Story | Estimativa | Sprint |
| :---: | :---: | :--- | :---: | :---: |
| 1 | Alta | **US01** — Como equipe do projeto, quero um pipeline de ETL no Google Colab (Python) que extraia e prepare os dados brutos da RAIS, para que os dados estejam prontos para análise no Power BI. | 8 | 1 |
| 2 | Alta | **US06** — Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. | 13 | 2 e 3 |
| 3 | Alta | **US02** — Como equipe do projeto, quero filtrar e padronizar os dados para o município de São José dos Campos (código 354990), para que a análise reflita exclusivamente o ecossistema local. | 3 | 1 |
| 4 | Alta | **US03** — Como equipe do projeto, quero identificar e tratar as inconsistências dos dados da RAIS (vínculos zerados, mistura de tipos de estabelecimento, ausência de ano e de identificação), para que o dashboard não apresente conclusões distorcidas. | 8 | 1 |
| 5 | Média | **US04** — Como equipe do projeto, quero produzir a documentação formal do projeto (Visão e Escopo, DoR, DoD, Log de Decisões), para que o trabalho siga a metodologia Scrum/API exigida pela disciplina. | 5 | 1 |
| 6 | Média | **US05** — Como equipe do projeto, quero estruturar o repositório no GitHub, para que o código, os dados e a documentação fiquem organizados e versionados. | 3 | 1 |
| 7 | Média | **US07** — Como gestor público, quero ver um ranking das empresas que mais contratam em SJC, para que eu possa direcionar políticas de fomento ao emprego. | 5 | 2 |
| 8 | Média | **US08** — Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. | 8 | 2 e 3 |
| 9 | Média | **US09** — Como gestor público, quero visualizar o impacto do ecossistema de empresas no PIB municipal (dados do IBGE), para que eu possa avaliar a relevância econômica de cada setor. | 8 | 2 |
| 10 | Baixa | **US10** — Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | 5 | 3 |
| 11 | Alta | **US11** — Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | 13 | 3 |

> Estimativa em story points (escala de Fibonacci). Critérios de aceite e situação de cada User Story no [Backlog do Produto](docs/02-Backlog-do-Produto.md).


# Competências desenvolvidas

* Documentação de projeto ágil (backlog do produto e das sprints, DoR, DoD, log de decisões);
* Processo de desenvolvimento ágil com Scrum (papéis, cerimônias e entregas incrementais);
* Tratamento e análise de dados públicos com Python (leitura em streaming de um arquivo de 3,27 GB, filtragem, padronização e validação);
* Visualização de dados e Business Intelligence com Power BI (modelagem, medidas DAX e painéis interativos);
* Leitura de indicadores econômicos e do mercado de trabalho (RAIS, CNAE e PIB dos Municípios) aplicada à logística e ao desenvolvimento regional;
* Versionamento de código e documentação com GitHub;
* Soft skills: proatividade, autonomia, colaboração, comunicação com o cliente e entrega de resultados.


# Registro das Sprints

| Sprint            | Previsão   | Status    | Histórico |
|-------------------|------------|-----------|-----------|
| 01                | 28/09/2026 | Concluída | [MVP](MVP/sp1.md) · [Relatório](docs/RELATORIO_SPRINT_1.md) |
| 02                | 26/10/2026 | Concluída | [MVP](MVP/sp2.md) · [Relatório](docs/RELATORIO_SPRINT_2.md) |
| 03                | 23/11/2026 | Em andamento | [MVP](MVP/sp3.md) |
| Feira de Soluções | 03/12/2026 | A fazer   | [MVP](#) |


# Documentação e estrutura do repositório

```
.
├── README.md
├── MVP/          MVP de cada sprint (sp1.md, sp2.md, sp3.md)
├── docs/         Documentação Scrum, relatórios das sprints e relatórios técnicos (.docx e .md)
├── dados/        Bases tratadas prontas para o Power BI, com dicionário de dados
│   ├── entrada/      arquivos de entrada do notebook 02
│   └── referencia/   tabela bairro → região e CNAE 2.3
├── notebooks/    01: ETL da RAIS (Sprint 1) · 02: base única do Power BI (Sprint 2)
├── powerbi/      Painel: projeto .pbip (versão publicada), planilhas-fonte, PDF e versões anteriores
└── evidencias/   Prints, gráficos, guias e comprovações de cada sprint
```

| Documento | Word | Ler no GitHub |
|---|---|---|
| Visão e Escopo | [01-Visao-e-Escopo.docx](docs/01-Visao-e-Escopo.docx) | — |
| Backlog do Produto | [02-Backlog-do-Produto.docx](docs/02-Backlog-do-Produto.docx) | [02-Backlog-do-Produto.md](docs/02-Backlog-do-Produto.md) |
| Backlog das Sprints 1, 2 e 3 | [03](docs/03-Backlog-Sprint-1.docx) · [08](docs/08-Backlog-Sprint-2.docx) · [09](docs/09-Backlog-Sprint-3.docx) | [Sprint 2](docs/08-Backlog-Sprint-2.md) · [Sprint 3](docs/09-Backlog-Sprint-3.md) |
| DoR e DoD | [04-DoR-Checklist.docx](docs/04-DoR-Checklist.docx) · [05-DoD.docx](docs/05-DoD.docx) | — |
| Log de Decisões de Dados (DEC-001 a DEC-022) | [06-Decisoes-de-Dados.docx](docs/06-Decisoes-de-Dados.docx) | [06-Decisoes-de-Dados.md](docs/06-Decisoes-de-Dados.md) |
| Relatórios das Sprints | — | [Sprint 1](docs/RELATORIO_SPRINT_1.md) · [Sprint 2](docs/RELATORIO_SPRINT_2.md) |
| Relatórios Técnicos | [Sprint 1](docs/07-Relatorio-Tecnico-Sprint-1.docx) · [Sprint 2](docs/10-Relatorio-Tecnico-Sprint-2.docx) | — |
| Relatórios de Desenvolvimento (Anexo 8) | [Sprint 1](docs/Relatorio_Sprint1_Anexo8.docx) · [Sprint 2](docs/Relatorio_Sprint2_Anexo8.docx) | — |
| Relatório e fórmulas do Power BI (Sprint 2) | [Relatório](docs/Relatorio_PowerBI_Sprint2.docx) · [Fórmulas](docs/Formulas_PowerBI_Sprint2.docx) | [Relatório](docs/Relatorio_PowerBI_Sprint2.md) · [Fórmulas](docs/Formulas_PowerBI_Sprint2.md) |

**Como reproduzir:** o [notebook 01](notebooks/01_ETL_RAIS_SJC.ipynb) filtra o arquivo público `RAIS_ESTAB_PUB` para o município 354990; o [notebook 02](notebooks/02_Base_PowerBI_SJC.ipynb) abre no Google Colab (*Arquivo → Abrir notebook → GitHub*), roda com *Executar tudo* e gera a base única [`dados/RAIS_SJC_2024_PowerBI.csv`](dados/RAIS_SJC_2024_PowerBI.csv). O passo a passo para abrir e editar o painel está no [README do Power BI](powerbi/README.md) e o dicionário de dados no [README dos dados](dados/README.md).

**Fontes de dados:** RAIS 2024 (MTE) · PIB dos Municípios 2002–2023 (IBGE) · CNAE 2.3 (IBGE/CONCLA) · Plano Diretor de São José dos Campos, estudo "Regiões Urbanas" · referência de modelo: [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio).

### Referências

- DE NEGRI, J. A. et al. *Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD*. Texto para Discussão nº 840. Brasília: IPEA, 2001. [Link](https://repositorio.ipea.gov.br/handle/11058/2155)
- GALINDO-RUEDA, F.; VERGER, F. *OECD taxonomy of economic activities based on R&D intensity*. OECD Science, Technology and Industry Working Papers, n. 2016/04. Paris: OECD Publishing, 2016.
- IBGE. *Classificação Nacional de Atividades Econômicas – CNAE Subclasses 2.3*. Rio de Janeiro: IBGE/CONCLA. [Link](https://concla.ibge.gov.br)
- MORELLI, A. B.; FIEDLER, A. C.; CUNHA, A. L. *Um banco de dados de empregos formais georreferenciados em cidades brasileiras*. arXiv:2303.09602, 2023. [Link](https://arxiv.org/pdf/2303.09602)
- SÃO JOSÉ DOS CAMPOS (Município). *Plano Diretor: estudo técnico — Regiões Urbanas*. Prefeitura Municipal. [Link](https://www.sjc.sp.gov.br/media/1ascp0it/7_regioes_urbanas.pdf)
- SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RS (SICT). *Observatório da Inovação RS*. Porto Alegre, 2025. [Link](https://sict.rs.gov.br/observatorio)
- SILVA, V. P.; LIMA, M. E. O. *Microdados RAIS e estudos sobre o mercado de trabalho no Brasil*. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. [Link](https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244)

---

Projeto acadêmico desenvolvido na Fatec São José dos Campos.
