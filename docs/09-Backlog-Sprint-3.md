> Versão em Markdown de `docs/09-Backlog-Sprint-3.docx`, para leitura direta no GitHub. Em caso de diferença, vale o .docx.

# Backlog da Sprint 3

**A detalhar na Sprint Planning — entrega estimada 23/11/2026**

User Stories previstas (ver 02-Backlog-do-Produto), incluindo as herdadas da Sprint 2:

| ID | User Story (resumo) | Prior. |
|---|---|---|
| US06 | Distribuição geográfica das empresas — restante da Sprint 2: mapa por latitude/longitude, região oficial da Prefeitura e pontos ainda não geocodificados | 2 |
| US08 | Setores em alta — replanejar com o cliente a fonte da série histórica ou o critério de aceite | 8 |
| US10 | Contratações mais recentes registradas na RAIS | 10 |
| US11 | Dashboard consolidado, relatório técnico final e apresentação ao cliente | 11 |

Meta da Sprint 3: (definir na Sprint Planning, com base no que foi aprendido nas Sprints 1 e 2)

Estrutura a seguir o mesmo modelo da Sprint 1. Esta é a última sprint de desenvolvimento antes da Feira de Soluções (03/dez), que é o marco de apresentação final ao cliente — não uma sprint adicional.

## Riscos e pontos de atenção

- US10 pede contratações “ordenadas por data”, mas a RAIS Estabelecimentos não traz datas de admissão. Opções: RAIS Vínculos (microdados por vínculo) ou revisão do critério com o cliente.
- US08 depende da RAIS de anos anteriores (2022 e 2023) filtrada pelo mesmo pipeline da Sprint 1.
- A classificação regional só fica 100% oficial com a tabela bairro → região ou o shapefile da Prefeitura (DEC-015).
- A Sprint 3 termina em 23/11/2026, a 10 dias da Feira de Soluções (03/12/2026): reservar tempo para a apresentação.
