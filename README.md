# Aprendizado por Projeto Integrado (API) - Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Projeto baseado na metodologia ágil SCRUM, procurando desenvolver a Proatividade, Autonomia, Colaboração e Entrega de Resultados dos estudantes envolvidos.

> Status do projeto: **Sprint 3 entregue (23/11/2026)** · próxima etapa: Feira de Soluções (03/12/2026) · [MVP da Sprint 3](MVP/sp3.md) · [Relatório da Sprint 3](docs/sprint-3/RELATORIO_SPRINT_3.md)
>
> Painel publicado: [🌐 abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) (abre no navegador, sem login). O link ainda mostra a versão de 26/10/2026; a versão final, com 5 páginas, entra ao republicar ([guia passo a passo](docs/final/Guia_Atualizar_PowerBI.md))
>
> Respostas aos requisitos do cliente: [✅ cada pergunta e critério, com números e onde ver no painel](docs/final/Respostas_Requisitos_Cliente.md)
>
> Vídeos do projeto: [▶️ canal LogMulti no YouTube](https://www.youtube.com/@LogMulti)
>
> Documentação: [📖 índice da pasta docs/](docs/README.md)
>
> Como refazer o projeto do zero: [🛠️ Manual de Replicação](docs/final/Manual_Replicacao.md) (códigos e construção do painel, passo a passo)

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
| Team Member | João Pedro Faria Vital de Souza | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/joao-pedro-a2b6122b7) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/Joao-pedro67) |
| Team Member | Milena Silva Nogueira | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/milenasnogueira) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/milenanogueira) |
| Team Member | Thalya Awany Berti | [![Linkedin Badge](https://img.shields.io/badge/Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/thalya-awany-berti-773923266) [![GitHub Badge](https://img.shields.io/badge/GitHub-111217?style=flat-square&logo=github&logoColor=white)](https://github.com/ThalyaAwany) |


# Objetivo do Projeto

São José dos Campos é um polo industrial, tecnológico e de serviços do Vale do Paraíba, mas não tem uma ferramenta pública e centralizada que reúna indicadores do seu ecossistema produtivo. Os dados públicos existem, mas têm inconsistências e não mostram de forma consolidada quem emprega, onde e em quais setores. Os objetivos estabelecidos para este projeto são:

* Desenvolver um pipeline de tratamento de dados (ETL) em Python, no Google Colab, que filtre e trate a RAIS 2024 para São José dos Campos (código IBGE 354990);
* Identificar e documentar formalmente cada inconsistência da base no [Log de Decisões de Dados](docs/final/06-Decisoes-de-Dados.md), garantindo a confiabilidade dos indicadores;
* Construir um painel em Power BI com indicadores de emprego, setores de atividade (CNAE), porte e distribuição geográfica dos estabelecimentos pelas regiões oficiais do município;
* Cruzar o emprego formal com o PIB dos Municípios (IBGE) para medir o peso de cada setor na economia local e apoiar decisões de desenvolvimento econômico.


# Tecnologias Utilizadas

* Python 3 (Google Colab)
* Power BI
* Microsoft Excel
* GitHub
* YouTube (canal [LogMulti](https://www.youtube.com/@LogMulti), vídeos do projeto)
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
| 01                | 28/09/2026 | Concluída | [MVP](MVP/sp1.md) · [Relatório](docs/sprint-1/RELATORIO_SPRINT_1.md) |
| 02                | 26/10/2026 | Concluída | [MVP](MVP/sp2.md) · [Relatório](docs/sprint-2/RELATORIO_SPRINT_2.md) |
| 03                | 23/11/2026 | Entregue  | [MVP](MVP/sp3.md) · [Relatório](docs/sprint-3/RELATORIO_SPRINT_3.md) |
| Feira de Soluções | 03/12/2026 | A fazer   | [Vídeo](https://www.youtube.com/@LogMulti) |

---

Projeto acadêmico desenvolvido na Fatec São José dos Campos.
