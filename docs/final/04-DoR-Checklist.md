> Versão em Markdown de [`04-DoR-Checklist.docx`](04-DoR-Checklist.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Checklist de Definition of Ready (DoR)

**Modelo reutilizável para todas as sprints — Sprint 1 cumprida em 28/09/2026 · Sprint 2 cumprida em 26/10/2026 · Sprint 3 cumprida em 23/11/2026**

Baseado no Anexo III do Guia de Avaliação API 2025-2. Preencher para cada item de trabalho antes de iniciar a execução. As marcações gerais abaixo valem para as Sprints 1, 2 e 3; a cada nova sprint, desmarcar e reavaliar item a item na Sprint Planning.

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

## Itens específicos da Sprint 3

☑ Coordenadas dos CEPs disponíveis para o mapa: CNEFE 2022 do IBGE, com 99,99% dos estabelecimentos com ponto (DEC-023)

☑ Regra de classificação por macroprocesso logístico definida e registrada antes de montar a página Regiões e Tecnologia (DEC-024)

☑ Planilhas do painel no repositório, com a aba PIB anual, e caminho das fontes configurável (parâmetro PastaFontes)

☑ Requisitos do cliente revisados item a item (docs/final/Respostas_Requisitos_Cliente.md)

☐ Lista oficial de bairros por região (incluindo a Região Norte) ou shapefile das regiões, fornecido pelo cliente — segue pendente (DEC-015)

☐ Fonte para a evolução dos setores (US08) e as contratações recentes (US10): RAIS de anos anteriores ou RAIS Vínculos — decisão do cliente na Feira de Soluções

☐ Base única RAIS_SJC_2024_PowerBI.csv como fonte da tabela RAIS_SJC do painel — segue pendente (DEC-022); o painel usa as planilhas de powerbi/fontes/

☐ Resposta do cliente sobre a base identificada (DEC-004) e o indicador 2 de RAIS negativa — segue pendente
