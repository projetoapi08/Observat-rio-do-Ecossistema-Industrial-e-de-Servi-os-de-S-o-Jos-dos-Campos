> Versão em Markdown de `docs/sprint-3/09-Backlog-Sprint-3.docx`, para leitura direta no GitHub. Em caso de diferença, vale o .docx.

# Backlog da Sprint 3

**ENTREGUE em 23/11/2026 — versão final**

**Período:** 27/10/2026 a 23/11/2026 · equipe de 8 integrantes (distribuição de funções abaixo).

**Meta da Sprint 3:** Consolidar o observatório como entrega final: completar o mapa da cidade, reunir no painel as respostas aos requisitos do cliente, produzir a documentação final e preparar a apresentação da Feira de Soluções (03/12/2026).

**Resultado:** meta cumprida em grande parte. O mapa passou a ter ponto para 99,99% dos estabelecimentos com as coordenadas do CNEFE 2022 (DEC-023), o painel ganhou a página Regiões e Tecnologia com a classificação por macroprocesso logístico (DEC-024), e cada requisito do cliente foi ligado a uma resposta. US08 e US10 dependem de dados que a RAIS disponível não tem e ficam para decisão do cliente.

## User Stories da Sprint 3

| ID | User Story (resumo) | Status |
|---|---|---|
| US06 | Distribuição geográfica das empresas (restante da Sprint 2)<br>Mapa com 99,99% dos estabelecimentos pelo CNEFE 2022 e filtro por região oficial; o link publicado mostra o mapa novo depois de republicar. | Concluído |
| US08 | Setores em alta em termos de contratação (restante da Sprint 2)<br>Setores predominantes, participação e página Regiões e Tecnologia; a evolução exige a RAIS de outros anos. | Parcial |
| US10 | Contratações mais recentes registradas na RAIS<br>A RAIS Estabelecimentos não tem data de admissão; critério a revisar com o cliente. | Não atendida |
| US11 | Dashboard consolidado, relatório técnico final e apresentação<br>Painel de 5 páginas, Relatório Técnico da Sprint 3, Anexo 8 final e respostas aos requisitos do cliente; apresentação em 03/12/2026. | Parcial |

## Distribuição de funções

| Integrante | Função na Sprint 3 | Papel |
|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Apoio geral e demais demandas | Product Owner |
| Juliano Souza Santana | Dados e documentação | Scrum Master |
| Beatriz Oliveira Sepulvida | CSV e Excel; vídeo do projeto | Scrum Team |
| Caio Moreira | Power BI e dados | Scrum Team |
| Hemilly Christiny da Silva Freitas | Documentação | Scrum Team |
| João Pedro Faria Vital de Souza | Apoio geral; vídeo do projeto | Scrum Team |
| Milena Silva Nogueira | Dados e documentação; vídeo do projeto | Scrum Team |
| Thalya Awany Berti | Power BI | Scrum Team |

## Tarefas de apoio

- [x] Coordenadas do mapa pelo CNEFE 2022 na base única e na planilha do painel (DEC-023)
- [x] Notebook de geocodificação dos CEPs incluído no repositório (notebooks/01b)
- [x] Classificação por macroprocesso logístico na base única e no painel (DEC-024)
- [x] Página Regiões e Tecnologia no projeto do painel
- [x] Ajustes da página KPIs e Mapa (cartões sem "Mil", título e subtítulos)
- [x] Parâmetro de pasta nas fontes do painel, projeto renomeado para Observatorio_SJC e aba PIB anual incluída
- [x] Respostas a cada requisito do cliente, do ponto de vista da logística
- [x] Evidência com os códigos de tratamento de dados e links do Colab
- [ ] Atualizar e republicar o painel no Power BI Desktop
- [ ] Receber do cliente a lista oficial de bairros da Região Norte (DEC-015)

## Entregáveis

- [x] Projeto do painel — powerbi/pbip/Observatorio_SJC.pbip (5 páginas)
- [x] Base única — dados/RAIS_SJC_2024_PowerBI.csv (47 colunas)
- [x] Relatório Técnico da Sprint 3 (11-Relatorio-Tecnico-Sprint-3) e Log de Decisões até a DEC-024
- [x] Relatório de Desenvolvimento — Anexo 8 da Sprint 3, versão final (docs/Relatorio_Sprint3_Anexo8)
- [x] Respostas aos requisitos do cliente (docs/final/Respostas_Requisitos_Cliente.md)
- [x] Canal do projeto no YouTube — https://www.youtube.com/@LogMulti
- [ ] Link direto do vídeo de apresentação
- [ ] Apresentação da Feira de Soluções (03/12/2026)

## Pendências para a Feira de Soluções (03/12/2026)

- US08: decidir com o cliente se a evolução dos setores usa a RAIS 2022–2023 ou se o critério de aceite é revisto.
- US10: decidir com o cliente entre a RAIS Vínculos (mês de admissão) e um critério revisado.
- Confirmar se a pergunta sobre oportunidades profissionais pode ser respondida para o profissional de logística.
- DEC-015 e DEC-022: tabela oficial de bairros por região e troca da fonte da tabela RAIS_SJC pela base única.
