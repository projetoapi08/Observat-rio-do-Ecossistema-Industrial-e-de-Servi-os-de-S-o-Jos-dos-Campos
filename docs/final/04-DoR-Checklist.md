> Versão em Markdown de [`04-DoR-Checklist.docx`](04-DoR-Checklist.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Checklist de Definition of Ready (DoR)

**Modelo reutilizável para todas as sprints — Sprint 1 cumprida em 28/09/2026 · Sprint 2 cumprida em 26/10/2026**

Baseado no Anexo III do Guia de Avaliação API 2025-2. Preencher para cada item de trabalho antes de iniciar a execução. As marcações gerais abaixo valem para as Sprints 1 e 2; a cada nova sprint, desmarcar e reavaliar item a item na Sprint Planning.

## Sobre a User Story / tarefa

☑ Tem título claro, descrição bem definida e objetivo compreendido

☑ Tem critérios de aceitação escritos

☑ Tem regras de negócio claras

☑ Foi estimada pela equipe

☑ Sem dependências bloqueadoras

☑ Compreensão validada com o time

## Sobre artefatos correlatos

☑ Design/documentação disponível

☑ Regras de negócio detalhadas (texto ou diagrama)

☑ Modelo de dados disponível

☑ Estratégia de testes definida

## Itens específicos da Sprint 1 (cumpridos)

☑ Fonte de dados da RAIS identificada e acessível (RAIS_ESTAB_PUB)

☑ Código do município de São José dos Campos confirmado (354990)

☑ Ambiente do Google Colab configurado com as bibliotecas necessárias (pandas, csv)

☑ Acesso ao Power BI Desktop/Service configurado para todos os membros

## Itens específicos da Sprint 2 (cumpridos)

☑ Campo de CEP validado para geocodificação: 3.677 CEPs processados; 99,99% dos estabelecimentos com região oficial e 78% com ponto no mapa (o restante segue na Sprint 3 — US06)

☑ Série do PIB dos Municípios (IBGE 2002–2023) baixada, tratada no Colab e conferida (IBGE_PIB_SJC_Observatorio.xlsx)

☑ Acesso de todos os membros ao arquivo Power BI compartilhado (PowerbiATT_Api_Sprint2.pbix)

## Itens a confirmar para a Sprint 3

☐ Lista oficial de bairros por região (incluindo a Região Norte) ou shapefile das regiões, fornecido pelo cliente

☐ Fonte definida com o cliente para a evolução dos setores (US08) e as contratações recentes (US10): RAIS de anos anteriores ou RAIS Vínculos

☐ Base única RAIS_SJC_2024_PowerBI.csv importada no painel por todos os membros

☐ Resposta do cliente sobre a base identificada (DEC-004) e o indicador 2 de RAIS negativa
