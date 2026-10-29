> Versão em Markdown de `docs/02-Backlog-do-Produto.docx`, para leitura direta no GitHub. Em caso de diferença, vale o .docx.

# Backlog do Produto

**Observatório do Ecossistema Industrial e de Serviços de São José dos Campos**

**Disciplina API — Fatec São José dos Campos, curso de logística**

**Cliente: CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos /** Fonte dos dados: RAIS (Ministério do Trabalho e Emprego) e PIB dos Municípios (IBGE)

## Visão geral das sprints

| Sprint | Objetivo | Data de entrega | Status |
|---|---|---|---|
| Sprint 1 | Fundação técnica: pipeline de dados, tratamento de inconsistências e documentação de metodologia | 28/09/2026 | Concluída |
| Sprint 2 | Construção das análises centrais e mapeamento geográfico no Power BI | 26/10/2026 | Entregue — 2 US concluídas, 2 parciais |
| Sprint 3 | Consolidação do dashboard, relatório técnico final e apresentação ao cliente | 23/11/2026 | A iniciar |

## 2. Backlog detalhado

### Sprint 1 — Fundação técnica (entrega 28/09/2026) — CONCLUÍDA

| ID | User Story | Prior. | Status |
|---|---|---|---|
| US01 | Como equipe do projeto, quero um pipeline de ETL no Google Colab (Python) que extraia e prepare os dados brutos da RAIS, para que os dados estejam prontos para análise no Power BI.<br>Critério de aceite: notebook executa de ponta a ponta e gera os CSVs de saída sem erros. | 1 | Concluído |
| US02 | Como equipe do projeto, quero filtrar e padronizar os dados para o município de São José dos Campos (código 354990), para que a análise reflita exclusivamente o ecossistema local.<br>Critério de aceite: 100% dos registros no CSV final pertencem ao município 354990. | 3 | Concluído |
| US03 | Como equipe do projeto, quero identificar e tratar as inconsistências dos dados da RAIS (vínculos zerados, mistura de tipos de estabelecimento, ausência de ano e de identificação), para que o dashboard não apresente conclusões distorcidas.<br>Critério de aceite: cada inconsistência encontrada está registrada no Log de Decisões (DEC-XXX) com o tratamento adotado. | 4 | Concluído |
| US04 | Como equipe do projeto, quero produzir a documentação formal do projeto (Visão e Escopo, DoR, DoD, Log de Decisões), para que o trabalho siga a metodologia Scrum/API exigida pela disciplina.<br>Critério de aceite: todos os documentos da Sprint 1 aprovados pelo orientador. | 5 | Concluído |
| US05 | Como equipe do projeto, quero estruturar o repositório no GitHub (docs/, notebooks/, powerbi/), para que o código, os dados e a documentação fiquem organizados e versionados.<br>Critério de aceite: repositório publicado com as três pastas e README inicial. | 6 | Concluído |

### Sprint 2 — Análises centrais e mapeamento geográfico (entrega 26/10/2026) — ENTREGUE

| ID | User Story | Prior. | Status |
|---|---|---|---|
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade.<br>Critério de aceite: mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP com taxa de acerto acima de 90%.<br>Situação: 99,99% dos estabelecimentos com região oficial e 78% com ponto no mapa (nível de bairro); o mapa do painel já usa latitude/longitude e tem filtro por região ([painel online](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9)). | 2 | Parcial — restante na Sprint 3 |
| US07 | Como gestor público, quero ver um ranking das empresas que mais contratam em SJC, para que eu possa direcionar políticas de fomento ao emprego.<br>Critério de aceite: visual no Power BI lista os estabelecimentos ordenados por número de vínculos ativos, com filtro por setor (agregado, sem identificação nominal — ver DEC-004).<br>Situação: rankings Top 10 de setores por estabelecimentos e por empregos CLT na página Setor de Atividades. | 7 | Concluído (agregado — DEC-004) |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra.<br>Critério de aceite: visual mostra a evolução de contratações por setor (CNAE agrupado).<br>Situação: a base tem só a RAIS 2024, sem série histórica; o painel mostra os setores predominantes e a participação de cada um, mas não a evolução. | 8 | Parcial — replanejar na Sprint 3 |
| US09 | Como gestor público, quero visualizar o impacto do ecossistema de empresas no PIB municipal (dados do IBGE), para que eu possa avaliar a relevância econômica de cada setor.<br>Critério de aceite: dashboard cruza dados RAIS 2024 e PIB dos Municípios (IBGE) por setor, com fonte, ano e defasagem indicados (DEC-005).<br>Situação: página PIB e Emprego com PIB 2002–2023, valor adicionado por setor e produtividade relativa (VAB 2021 × emprego 2024). | 9 | Concluído |

### Sprint 3 — Consolidação e entrega final (entrega 23/11/2026)

| ID | User Story | Prior. | Status |
|---|---|---|---|
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local.<br>Critério de aceite: painel exibe as contratações do período mais recente disponível nos dados, ordenadas por data.<br>Atenção: a RAIS Estabelecimentos não traz datas de admissão — exige outra fonte (RAIS Vínculos) ou revisão do critério com o cliente. | 10 | A fazer — risco de dados |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão.<br>Critério de aceite: dashboard publicado reúne todos os visuais das sprints anteriores; relatório técnico e apresentação entregues e aprovados pelos orientadores. | 11 | A fazer |

Itens herdados da Sprint 2: US06 (mapa por latitude/longitude, região Norte oficial e pontos restantes) e US08 (fonte para a evolução dos setores). Ver 09-Backlog-Sprint-3.
