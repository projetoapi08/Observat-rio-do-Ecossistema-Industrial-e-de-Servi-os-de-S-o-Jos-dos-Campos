> Versão em Markdown de [`00-README.docx`](00-README.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Projeto da metodologia API — Aprendizagem por Projetos Integrados (Fatec São José dos Campos), curso de Logística, 1º semestre de 2026.

Documento atualizado em 23/11/2026 — entrega final da Sprint 3 (mapa com 99,99% dos estabelecimentos, página Regiões e Tecnologia, respostas aos requisitos do cliente e relatórios finais).

## 📌 Sobre o projeto

Painel de Business Intelligence (Power BI), inspirado no modelo do Observatório da Inovação RS, que mapeia o ecossistema industrial e de serviços de São José dos Campos a partir dos estabelecimentos e empregos formais (RAIS 2024) e do PIB municipal (IBGE). Mostra os setores predominantes, o porte e a situação dos estabelecimentos, o peso de cada setor no emprego e no valor adicionado a distribuição das empresas pelas regiões oficiais da cidade e, na versão final, o tipo de atividade, a intensidade tecnológica e a etapa da cadeia de suprimentos de cada setor.

## 🎯 Desafio

Cliente: CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos. Tema oficial: Mapeamento do Ecossistema Industrial e de Serviços da Região de São José dos Campos.

Detalhes completos em docs/final/01-Visao-e-Escopo.docx.

## 👥 Equipe

| **Nome**                            | **Papel / função**                                  | **GitHub**          |
|-------------------------------------|-----------------------------------------------------|---------------------|
| Pedro Henrique Oliveira de Carvalho | Product Owner · apoio geral                         | @po032953-dev       |
| Juliano Souza Santana               | Scrum Master · dados e documentação                 | @projetoapi08       |
| Beatriz Oliveira Sepulvida          | Scrum Team · CSV e Excel; vídeo do projeto          | @beatrizsepulvida08 |
| Caio Moreira                        | Scrum Team · Power BI e dados                       | @CaioMoreiraujo     |
| Hemilly Christiny da Silva Freitas  | Scrum Team · documentação                           | @hemillyfreitas     |
| João Pedro Faria Vital de Souza     | Scrum Team · apoio geral; vídeo do projeto          | @Joao-pedro67       |
| Milena Silva Nogueira               | Scrum Team · dados e documentação; vídeo do projeto | @milenanogueira     |
| Thalya Awany Berti                  | Scrum Team · Power BI                               | @ThalyaAwany        |

Professor M2 (orientador): José Jaétis · Professor P2: Marcus Nascimento (contato do cliente via grupo do WhatsApp)

*Nota: funções conforme a distribuição de tarefas da Sprint 3 (vídeo do projeto: Beatriz, Milena e João Pedro).*

## 🛠️ Tecnologias utilizadas

- Google Colab + Python 3+ — coleta e tratamento dos microdados

- Power BI — modelagem e visualização

- GitHub — versionamento e documentação

## 📂 Documentação

- 01 — Visão e Escopo

- 02 — Backlog do Produto

- Sprints:

- 03 — Backlog da Sprint 1 · 07 — Relatório Técnico Sprint 1 (concluída em 28/09/2026)

- 08 — Backlog da Sprint 2 · 10 — Relatório Técnico Sprint 2 (entregue em 26/10/2026)

- 09 — Backlog da Sprint 3 · 11 — Relatório Técnico Sprint 3, versão final (entregue em 23/11/2026)

- Válidos para todas as sprints: 04 — DoR · 05 — DoD · 06 — Log de Decisões de Dados (DEC-001 a DEC-024)

- Relatórios de Desenvolvimento — Anexo 8 das Sprints 1, 2 e 3 (a da Sprint 3 é a versão final) (pasta docs/); guia de importação no Power BI, gráficos, prints e Passo a Passo do Desenvolvimento (pasta evidencias/); MVP de cada sprint (pasta MVP/)

- Respostas aos Requisitos do Cliente (docs/final/Respostas_Requisitos_Cliente.md): cada pergunta, funcionalidade, resultado esperado e requisito técnico do cliente ligado à resposta e ao lugar do painel onde aparece, do ponto de vista da logística

- Dados tratados (pasta dados/): RAIS_SJC_2024_PowerBI.csv (base única, 47.339 estabelecimentos, 47 colunas), CNAE_RAIS_SJC_2024.xlsx, IBGE_PIB_SJC_Observatorio.xlsx

## 🔗 Links

- Painel Power BI: https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9

- Canal do projeto no YouTube (LogMulti): https://www.youtube.com/@LogMulti

## 📊 Fontes de dados

- RAIS Estabelecimentos — Ministério do Trabalho e Emprego (ano-base 2024, confirmado pelo cliente)

- PIB dos Municípios — IBGE (PIB até 2023; valor adicionado por setor até 2021)

- CNAE 2.3 — IBGE/CONCLA (estrutura oficial usada para validar códigos e descrições)

- Divisão regional — Prefeitura de São José dos Campos, Plano Diretor 2018 (estudo “Regiões Urbanas”)

- CNEFE 2022 — IBGE, Cadastro Nacional de Endereços para Fins Estatísticos (coordenadas dos CEPs para o mapa, DEC-023)

## 📅 Cronograma

| **Data** | **Evento**                                                          |
|----------|---------------------------------------------------------------------|
| 24/ago   | Kick-off do projeto                                                 |
| 31/ago   | Validação do entendimento                                           |
| 28/set   | Entrega 1 — encerramento da Sprint 1 (Fundação dos dados)           |
| 26/out   | Entrega 2 — encerramento da Sprint 2 (Funcionalidades centrais)     |
| 23/nov   | Entrega 3 — encerramento da Sprint 3 (Consolidação e entrega final) |
| 03/dez   | Feira de Soluções — apresentação final ao cliente                   |

*Nota: o projeto está organizado em 3 sprints de desenvolvimento (Sprint 1, 2 e 3), alinhadas às Entregas 1, 2 e 3 do cronograma da disciplina. A Feira de Soluções (03/dez) é o marco de apresentação final, não uma sprint adicional de desenvolvimento — isso substitui o plano inicial de 4 sprints que constava nos primeiros rascunhos do projeto.*
