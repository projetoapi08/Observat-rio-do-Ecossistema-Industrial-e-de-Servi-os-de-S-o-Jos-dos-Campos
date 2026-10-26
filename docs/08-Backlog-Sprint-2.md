> Versão em Markdown de `docs/08-Backlog-Sprint-2.docx`, para leitura direta no GitHub. Em caso de diferença, vale o .docx.

# Backlog da Sprint 2

**ENTREGUE em 26/10/2026**

**Período:** 29/09/2026 a 26/10/2026 · equipe de 8 integrantes (distribuição de funções abaixo).

**Meta da Sprint 2:** Construir as análises centrais no Power BI — setores de atividade, porte e situação dos estabelecimentos e cruzamento RAIS × PIB — e preparar a base geocodificada com a região oficial de cada estabelecimento para o mapa da cidade.

**Resultado:** meta cumprida em parte. O painel ganhou quatro páginas (Notas Metodológicas, KPIs e Mapa, Setor de Atividades, PIB e Emprego) e a base RAIS foi classificada pela CNAE 2.3, geocodificada e associada às regiões oficiais. Ficaram para a Sprint 3 a troca do mapa para coordenadas (US06) e a fonte para mostrar a evolução dos setores (US08).

## User Stories da Sprint 2

| ID | User Story (resumo) | Status |
|---|---|---|
| US06 | Distribuição geográfica e classificação das empresas (mapeamento por CEP)<br>Base pronta: 99,99% com região oficial e 78% com ponto no mapa. Falta trocar o mapa do painel do texto do CEP para latitude/longitude. | Parcial |
| US07 | Ranking das empresas que mais contratam em SJC (agregado por setor/região)<br>Top 10 de setores por estabelecimentos e por empregos CLT; tabela por porte e setor (DEC-004). | Concluído |
| US08 | Setores em alta em termos de contratação<br>O painel mostra os setores predominantes e a participação de cada um; a evolução exige RAIS de outros anos. | Parcial |
| US09 | Impacto de cada setor no PIB municipal<br>Página PIB e Emprego: PIB 2002–2023, valor adicionado por setor e produtividade relativa (VAB 2021 × emprego 2024). | Concluído |

## Distribuição de funções

| Integrante | Função na Sprint 2 | Papel |
|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Apoio geral e demais demandas | Product Owner |
| Juliano Souza Santana | Dados e documentação | Scrum Master |
| Beatriz Oliveira Sepulvida | CSV e Excel | Scrum Team |
| Caio Moreira | Tratamento de dados | Scrum Team |
| Hemilly Christiny da Silva Freitas | Documentação | Scrum Team |
| João Pedro Faria Vital de Souza | Apoio geral e demais demandas | Scrum Team |
| Milena Silva Nogueira | Power BI | Scrum Team |
| Thalya Awany Berti | Power BI | Scrum Team |

## Tarefas de apoio

- [x] Série do PIB dos Municípios (IBGE, 2002–2023) tratada no Colab e conferida (IBGE_PIB_SJC_Observatorio.xlsx)
- [x] Base RAIS classificada pela CNAE, de seção a subclasse, com descrições (CNAE_RAIS_SJC_2024.xlsx)
- [x] Resposta ao feedback da Sprint 1 sobre os 64,37% de RAIS negativa (aba RAIS_Negativa da planilha CNAE)
- [x] Geocodificação dos 3.677 CEPs (BrasilAPI + Nominatim), no nível de bairro
- [x] Classificação de cada estabelecimento pela região oficial do município (DEC-015)
- [x] Validação dos códigos e descrições pela CNAE 2.3 oficial (DEC-020)
- [x] Base única para o Power BI (RAIS_SJC_2024_PowerBI.csv) e guia de importação (DEC-022)
- [x] Painel com as páginas Notas Metodológicas, KPIs e Mapa, Setor de Atividades e PIB e Emprego
- [ ] Trocar a fonte da tabela RAIS_SJC pela base única e o mapa para latitude/longitude
- [ ] Corrigir os subtítulos de três cartões da página KPIs e o texto das Notas Metodológicas
- [ ] Receber do cliente a lista oficial de bairros da Região Norte

## Entregáveis

- [x] Painel Power BI — powerbi/PowerbiATT_Api_Sprint2.pbix
- [x] Planilhas tratadas — dados/CNAE_RAIS_SJC_2024.xlsx e dados/IBGE_PIB_SJC_Observatorio.xlsx
- [x] Base única — dados/RAIS_SJC_2024_PowerBI.csv e evidencias/Importacao_PowerBI_RAIS_SJC.txt
- [x] Relatório Técnico da Sprint 2 (10-Relatorio-Tecnico-Sprint-2) e Log de Decisões atualizado (06)
- [x] Relatório de Desenvolvimento — Anexo 8 da Sprint 2 (docs/Relatorio_Sprint2_Anexo8)
- [ ] Vídeo de incremento da Sprint 2 — link: adicionar

## Itens transferidos para a Sprint 3

- US06: importar a base única no painel, trocar o mapa para latitude/longitude e geocodificar os bairros não encontrados e os 9 bairros com ponto em homônimo (DEC-017, DEC-018).
- US06: substituir a classificação regional pela tabela ou shapefile oficial da Prefeitura, quando o cliente enviar (DEC-015).
- US08: definir com o cliente a fonte para a evolução dos setores (RAIS de anos anteriores) ou ajustar o critério de aceite.
- Visuais novos com as colunas da base: emprego por região, tipo de atividade, intensidade tecnológica e porte SEBRAE.
