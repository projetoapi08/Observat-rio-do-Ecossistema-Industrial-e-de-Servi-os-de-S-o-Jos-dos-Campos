> Versão em Markdown de [`03-Backlog-Sprint-1.docx`](03-Backlog-Sprint-1.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Backlog da Sprint 1

**CONCLUÍDA — entregue em 28/09/2026**

Capacidade estimada da equipe por sprint: (preencher — nº de integrantes × horas/semana × semanas da sprint)

Meta da Sprint 1: Ter os microdados da RAIS filtrados para o município de São José dos Campos, o dicionário de dados definido, os dados do PIB dos Municípios (IBGE) levantados, e uma primeira visualização simples (nº total de contratações em SJC) publicada no Power BI.

Resultado: meta cumprida — pipeline de ETL rodou de ponta a ponta, as 4 inconsistências dos dados foram identificadas e tratadas (DEC-001 a DEC-004, ver 06-Decisoes-de-Dados), e a suíte de documentação da Sprint 1 foi concluída. A primeira visualização no Power BI e a modelagem de relacionamento entre tabelas ficaram para o início da Sprint 2, junto com a geocodificação.

## User Stories da Sprint 1

| **ID** | **User Story (resumo)**                                                                | **Estimativa** | **Status** |
|--------|----------------------------------------------------------------------------------------|----------------|------------|
| US01   | Pipeline de ETL no Google Colab para extrair e preparar os dados brutos da RAIS        | 6h             | Concluído  |
| US02   | Filtrar e padronizar os dados para o município de SJC (354990)                         | —              | Concluído  |
| US03   | Identificar e tratar as inconsistências dos dados da RAIS                              | —              | Concluído  |
| US04   | Produzir a documentação formal do projeto (Visão, Backlogs, DoR, DoD, Log de Decisões) | —              | Concluído  |
| US05   | Estruturar o repositório no GitHub (docs/, notebooks/, powerbi/)                       | —              | Concluído  |

## Tarefas de apoio (compuseram o DoR da Sprint 1)

☑ Validação do documento de Visão e Escopo com o professor P2/M2

☑ Download e exploração dos microdados da RAIS (RAIS_ESTAB_PUB, ano-base 2024)

☑ Filtragem inicial dos dados por município (código 354990 — São José dos Campos)

☑ Levantamento dos dados de PIB dos Municípios (IBGE) por setor de atividade (CNAE)

☑ Definição do dicionário de dados (campos da RAIS utilizados)

☑ Estrutura inicial do arquivo/modelo no Power BI (conexão com as fontes) — concluída no início da Sprint 2

☑ Primeira visualização simples e demonstrável (ex.: nº total de contratações em SJC) — concluída no início da Sprint 2

*Ver checklist completo de Definition of Ready em 04-DoR-Checklist, Definition of Done em 05-DoD, e as decisões técnicas sobre tratamento dos dados em 06-Decisoes-de-Dados.*

## Entregáveis

☑ Notebook de ETL no Google Colab (ETL_RAIS_SJC.ipynb) — link: adicionar

☑ Arquivo Power BI inicial — entregue na Sprint 2 (powerbi/PowerbiATT_Api_Sprint2.pbix)

☑ Relatório técnico da Sprint 1 (07-Relatorio-Tecnico-Sprint-1)

☑ Relatório de Desenvolvimento — Anexo 8 (docs/sprint-1/Relatorio_Sprint1_Anexo8) — rascunho concluído, pendente revisão final
