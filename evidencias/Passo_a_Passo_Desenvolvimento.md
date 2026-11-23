> Versão em Markdown de [`Passo_a_Passo_Desenvolvimento.docx`](Passo_a_Passo_Desenvolvimento.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao README](../README.md)

# Passo a Passo do Desenvolvimento

**Registro cronológico para catalogação no GitHub**

Este documento consolida, em ordem cronológica, tudo que foi feito no projeto até o momento — servindo de complemento ao Log de Decisões de Dados e ao Relatório de Desenvolvimento da Sprint 1 (Anexo 8). Pode ser usado como base para a catalogação da pasta docs/ no repositório GitHub.

## 1. Definição inicial do escopo

O projeto começou com escopo voltado a um relatório de RH / contratação, analisando dados de vínculos empregatícios.

**Status: Concluído — superado pelo pivô descrito a seguir**

## 2. Pivô de escopo para Observatório completo

O cliente apresentou o Observatório da Inovação RS como referência de modelo a ser seguido. O escopo foi ampliado: de um relatório de RH para um observatório completo do ecossistema industrial e de serviços do município. Essa mudança elevou a prioridade da User Story de mapeamento geográfico para Rank 2 no Backlog do Produto.

**Status: Concluído**

## 3. Documentação da Sprint 1 (metodologia Scrum/API)

Produção do conjunto de documentos formais que estruturam o projeto:

| **Documento**                | **O que contém**                                      |
|------------------------------|-------------------------------------------------------|
| Visão e Escopo               | Objetivo, escopo e diretrizes gerais do projeto       |
| Backlog do Produto           | 11 User Stories priorizadas, organizadas em 3 sprints |
| Backlog da Sprint 1          | Recorte das User Stories da primeira sprint           |
| DoR Checklist                | Critérios de “Definition of Ready”                    |
| DoD                          | Critérios de “Definition of Done”                     |
| Log de Decisões de Dados     | Registro formal DEC-001 a DEC-005                     |
| Relatório Técnico (Sprint 1) | Metodologia, dificuldades e resultados da sprint      |

**Status: Concluído**

## 4. Estruturação do repositório GitHub

Criação do repositório observatorio-sjc/ com pastas organizadas: docs/, notebooks/, powerbi/.

**Status: Concluído**

## 5. Identificação da fonte de dados bruta

Recebido o arquivo RAIS_ESTAB_PUB.zip — base nacional de estabelecimentos da RAIS (Ministério do Trabalho e Emprego). Estrutura identificada: 12.643.067 registros, 24 colunas, separador ';', encoding Latin-1, ~3,27 GB descompactado.

Colunas confirmadas: inclui Município, Ind Rais Negativa, Tipo Estab (Cnpj/Caepf/Cno), CEP Estab — mas sem campo de ano/competência (resolvido posteriormente via confirmação do cliente, DEC-003) e sem identificação nominal.

**Status: Concluído**

## 6. Desenvolvimento do pipeline de ETL

Script Python (Google Colab) construído para processar o arquivo bruto em streaming (sem carregar os 3,27 GB inteiros em memória). Etapas do pipeline:

- Extract — leitura do .txt de dentro do .zip, linha a linha.

- Transform — filtro por Município = 354990 (código de São José dos Campos), limpeza dos campos com padding fixo, segmentação por RAIS negativa e por tipo de estabelecimento.

- Load — gravação dos CSVs tratados.

Notebook final: ETL_RAIS_SJC.ipynb, pronto para subir em notebooks/ no GitHub.

**Status: Concluído**

## 7. Resultados do ETL — base de São José dos Campos

| **Métrica**                      | **Valor**       |
|----------------------------------|-----------------|
| Total de estabelecimentos em SJC | 47.339          |
| Com vínculos ativos              | 16.869          |
| RAIS negativa (sem vínculos)     | 30.470 (64,37%) |
| Tipo Cnpj                        | 46.244          |
| Tipo Caepf                       | 708             |
| Tipo Cno                         | 387             |

Arquivos gerados: RAIS_SJC_completo.csv, RAIS_SJC_ativos.csv, RAIS_SJC_rais_negativa.csv, RAIS_SJC_Cnpj.csv, RAIS_SJC_Caepf.csv, RAIS_SJC_Cno.csv, estatisticas_etl.json.

**Status: Concluído**

## 8. Identificação das inconsistências nos dados

Quatro problemas estruturais identificados e formalizados no Log de Decisões de Dados:

| **ID**  | **Problema identificado**                                                    | **Status (em 22/09)** |
|---------|------------------------------------------------------------------------------|-----------------------|
| DEC-001 | 64,37% dos estabelecimentos com RAIS negativa (zero vínculos ativos).        | Resolvido             |
| DEC-002 | Mistura de naturezas de estabelecimento (Cnpj, Caepf, Cno) no mesmo arquivo. | Resolvido             |
| DEC-003 | Ausência de campo de ano/competência no arquivo bruto.                       | Resolvido             |
| DEC-004 | Ausência de identificação nominal (razão social/CNPJ) nos dados públicos.    | Pendente              |

Documento de apoio: Checklist de Erros e Inconsistências nos Dados (RAIS).

**Status: Concluído — DEC-001, DEC-002 e DEC-003 resolvidos · DEC-004 pendente de resposta do cliente**

## 9. Esclarecimento do cliente sobre a RAIS negativa

Em áudio enviado ao PO (Pedro), o cliente esclareceu que a alta proporção de RAIS negativa não deve ser tratada como erro a ser descartado — pode refletir uma característica real da economia do município.

Orientação do cliente: reportar essa métrica como indicador próprio do dashboard, em vez de apenas excluí-la das análises de emprego. Isso respondeu a uma das perguntas pendentes e definiu o tratamento de DEC-001.

**Status: Concluído — decisão incorporada**

## 10. Orientações do Prof. Marcus sobre documentação e GitHub

Recebidas via áudio, com os seguintes pontos:

- Preencher a tela de MVP no GitHub (acessível pelo quadro de sprints do fork), com todos os detalhes indicados na própria tela.

- Produzir o Relatório de Desenvolvimento da Sprint usando o modelo Anexo 8 (padrão ABNT da Fatec), documentando: objetivo, tecnologias utilizadas, código Python comentado linha a linha (quando houver), e print screens do painel Power BI explicando seu funcionamento (quando houver).

- Alterar o texto de “objetivo” do repositório GitHub — não pode ficar o texto padrão do fork; deve refletir o objetivo real do projeto.

- Interagir semanalmente com o professor para mostrar evolução.

**Status: Em andamento — tela de MVP e texto de objetivo do GitHub ainda pendentes de confirmação**

## 11. Elaboração do Relatório de Desenvolvimento — Sprint 1 (Anexo 8)

Documento produzido seguindo a estrutura do Anexo 8: resumo, abstract, contextualização, objetivos, fundamentação dos métodos analíticos (com tabela de referências bibliográficas reais), tecnologias utilizadas, coleta e descrição dos dados, resultados esperados e referências em ABNT.

Pendências no próprio documento: nomes e LinkedIn dos demais integrantes da equipe; validação das citações da seção de métodos analíticos junto ao Professor Marcus.

**Status: Rascunho concluído — pendente revisão da equipe e do professor**

## 12. Fechamento formal da Sprint 1 e reconciliação da documentação

Em 20/09/2026, a Sprint 1 foi encerrada: as 5 User Stories (US01–US05) foram marcadas como Concluído no Backlog do Produto, e o Log de Decisões de Dados foi atualizado.

Em 22/09/2026, toda a documentação do projeto foi revisada e consolidada. Foi identificada e corrigida uma divergência entre duas versões do Log de Decisões (uma delas, na suíte inicial de documentos do GitHub, registrava incorretamente a exclusão da RAIS negativa e um ano-base por um caminho não confirmado pelo cliente). A versão corrigida mantém a RAIS negativa na base como indicador próprio e confirma o ano-base 2024, conforme validado com o autor do projeto — ver 06-Decisoes-de-Dados.

**Status: Concluído**

## 13. Próximos passos

☐ Preencher tela de MVP e atualizar texto de objetivo no GitHub.

☐ Obter resposta do cliente sobre DEC-004 (base identificada).

☐ Iniciar construção do painel no Power BI (Sprint 2).

☐ Implementar geocodificação a partir do campo CEP_Estab para o mapeamento geográfico (US06).

☐ Processar a segunda fonte de dados: PIB dos Municípios (IBGE) 2022–2023.

☐ Subir todos os artefatos (docs/, notebooks/, CSVs tratados) no repositório GitHub.

☐ Capturar print screens do Power BI assim que o painel for iniciado, para incluir no Relatório Anexo 8 atualizado.

☐ Completar nomes completos e links de LinkedIn dos integrantes no Relatório Anexo 8.

*Documento gerado para consolidar o histórico de desenvolvimento do projeto e facilitar a organização/catalogação no repositório GitHub observatorio-sjc/.*
