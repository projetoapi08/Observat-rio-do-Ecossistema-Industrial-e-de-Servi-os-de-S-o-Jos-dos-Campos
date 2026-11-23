> Versão em Markdown de [`07-Relatorio-Tecnico-Sprint-1.docx`](07-Relatorio-Tecnico-Sprint-1.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Relatório Técnico — Sprint 1

Período: 24/ago a 28/set · Meta da Sprint: Ter os microdados da RAIS filtrados para o município de São José dos Campos, o dicionário de dados definido, os dados do PIB dos Municípios (IBGE) levantados, e uma primeira visualização simples (nº total de contratações em SJC) publicada no Power BI.

## O que foi entregue

O notebook de ETL no Google Colab (ETL_RAIS_SJC.ipynb) rodou com sucesso em modo streaming, processando o arquivo nacional RAIS_ESTAB_PUB (12.643.067 registros, ~3,27 GB) e gerando o extrato filtrado para São José dos Campos, 100% restrito ao código de município 354990 (47.339 estabelecimentos). Foi produzida a suíte completa de documentos da Sprint 1 — Visão e Escopo, Backlog do Produto, Backlog da Sprint 1, Checklist de DoR, DoD, Log de Decisões de Dados (DEC-001 a DEC-005) e este Relatório Técnico — além do Checklist de Erros e Inconsistências enviado ao cliente e do Relatório de Desenvolvimento no modelo Anexo 8. O repositório GitHub observatorio-sjc/ foi estruturado com as pastas docs/, notebooks/ e powerbi/. Foi produzida ainda uma pré-visualização inicial no Power BI.

## Metodologia e tecnologias utilizadas

- Fonte de dados: RAIS (ano-base 2024, confirmado pelo cliente — DEC-003), PIB dos Municípios IBGE (ano 2023 — série mais recente publicada; defasagem de 1 ano em relação à RAIS, documentada na DEC-005)

- Ferramentas: Google Colab + Python (leitura em streaming, sem carregar o arquivo integral em memória), Power BI

- Etapas do tratamento de dados: filtragem do extrato pelo código de município 354990 (SJC); manutenção dos estabelecimentos com “RAIS negativa” (zero vínculos ativos) na base, sinalizados por indicador próprio e usados como métrica separada (DEC-001); segmentação por natureza de estabelecimento, restringindo o recorte padrão a registros do tipo CNPJ (DEC-002)

## Dificuldades encontradas

Durante o tratamento dos dados, identificamos quatro problemas estruturais na base RAIS: (1) 64,37% dos estabelecimentos (30.470 de 47.339) sem nenhum vínculo ativo, exigindo decisão sobre como reportar esse dado; (2) mistura de três naturezas de estabelecimento (CNPJ, CAEPF, CNO) numa mesma coluna; (3) ausência de um campo explícito de ano/competência no arquivo; (4) ausência de identificação nominal (razão social/CNPJ) das empresas. Ao confirmar o ano-base da RAIS (2024) junto ao cliente, identificamos ainda que o PIB dos Municípios (IBGE) mais recente publicado é da série 2022–2023, criando uma defasagem de 1 ano em relação à RAIS que precisou ser tratada como limitação metodológica documentada (DEC-005).

## Decisões técnicas relevantes

Todas as decisões de tratamento de dados foram formalizadas no Log de Decisões de Dados (06-Decisoes-de-Dados), seguindo o modelo ADR: DEC-001 (manutenção da RAIS negativa na base, como indicador próprio — orientação do cliente), DEC-002 (segmentação por natureza de estabelecimento, restrita a CNPJ), DEC-003 (confirmação do ano-base RAIS 2024 pelo cliente), DEC-004 (ausência de identificação nominal das empresas — ranking agregado por setor/região, em aberto quanto a uma eventual base identificada) e DEC-005 (adoção do PIB 2023 como cruzamento válido, dada a defasagem do IBGE).

## Próximos passos (Sprint 2)

Aguardar retorno do cliente sobre a pendência em aberto (fornecimento de base RAIS identificada — DEC-004). Filtrar e tratar a série do PIB dos Municípios 2022–2023 (IBGE) para São José dos Campos. Implementar a geocodificação por CEP dos estabelecimentos no Colab, viabilizando o mapeamento geográfico (US06). Iniciar a modelagem no Power BI com os dados tratados e montar uma página de Notas Metodológicas, formalizando visualmente DEC-001 (RAIS negativa como indicador próprio) para o cliente e para a banca. Planejar o backlog detalhado da Sprint 2.
