# Relatório da Sprint 2

**Projeto:** Observatório do Ecossistema Industrial e de Serviços de São José dos Campos
**Disciplina:** API (Aprendizagem por Projetos Integrados), curso de Logística, Fatec São José dos Campos
**Cliente:** CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos
**Orientadores:** Prof. José Jaétis (M2) e Prof. Marcus Nascimento (P2)
**Período:** 29/09/2026 a 26/10/2026 · **Entrega da Sprint 2:** 26/10/2026

---

## 1. Objetivo da Sprint

Construir as análises centrais no Power BI — setores de atividade, porte e situação dos estabelecimentos e cruzamento RAIS × PIB — e preparar a base geocodificada com a região oficial de cada estabelecimento para o mapa da cidade.

## 2. Resultado da Sprint

| Indicador | Resultado |
|---|---|
| User Stories planejadas / concluídas | 4 / 2 concluídas (US07, US09) e 2 parciais (US06, US08) |
| Painel Power BI | 4 páginas: Notas Metodológicas, KPIs e Mapa, Setor de Atividades (CNAE), PIB e Emprego |
| Base RAIS classificada pela CNAE | 47.339 estabelecimentos, de seção a subclasse; códigos validados pela CNAE 2.3 |
| Geocodificação | 3.677 CEPs; 37.084 estabelecimentos (78,3%) com ponto no mapa, no nível de bairro |
| Região oficial | 47.334 estabelecimentos (99,99%) classificados nas regiões da Prefeitura |
| PIB dos Municípios (IBGE) | PIB 2002–2023 corrigido pelo IPCA; valor adicionado por setor até 2021 |
| Cruzamento emprego × valor adicionado | Indústria: 24,7% do emprego privado e 45,8% do valor adicionado privado (índice 1,86) |
| Decisões de dados | 22 registradas no total (DEC-001 a DEC-022) |

## 3. Backlog da Sprint 2

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. | O mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%. | 2 | Parcial |
| US07 | Como gestor público, quero ver um ranking das empresas que mais contratam em SJC, para que eu possa direcionar políticas de fomento ao emprego. | Visual no Power BI lista os estabelecimentos ordenados por número de vínculos ativos, com filtro por setor (agregado, sem identificação nominal; ver DEC-004). | 7 | Concluído |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. | Visual mostra a evolução de contratações por setor (CNAE agrupado). | 8 | Parcial |
| US09 | Como gestor público, quero visualizar o impacto do ecossistema de empresas no PIB municipal (dados do IBGE), para que eu possa avaliar a relevância econômica de cada setor. | O dashboard cruza dados RAIS 2024 e PIB dos Municípios (IBGE) por setor, com fonte, ano e defasagem indicados. | 9 | Concluído |

## 4. Entregas e evidências

### 4.1 Documentação (Scrum)

Atualizados ou criados na pasta `docs/`: Visão e Escopo (restrições e riscos), Backlog do Produto, Backlog da Sprint 2, Backlog da Sprint 3, DoR, DoD, Log de Decisões de Dados (DEC-006 a DEC-022), Relatório Técnico da Sprint 2 e Relatório de Desenvolvimento da Sprint 2 (modelo Anexo 8 da Fatec).

### 4.2 Tratamento dos dados

- **Classificação CNAE:** hierarquia de seção a subclasse, com descrições oficiais da CNAE 2.3 (`dados/CNAE_RAIS_SJC_2024.xlsx`)
- **PIB dos Municípios:** série 2002–2023 tratada no Colab e conferida (`dados/IBGE_PIB_SJC_Observatorio.xlsx`)
- **Geocodificação:** CEP → bairro e coordenada, com BrasilAPI e Nominatim (OpenStreetMap)
- **Região oficial:** bairro → região pela lista do Plano Diretor da Prefeitura, conferida pelo setor do CEP (33 dos 37 setores caem inteiros numa só região; os outros 4 estão na divisa Centro–Oeste ou misturam área urbana e rural)
- **Base única:** `dados/RAIS_SJC_2024_PowerBI.csv` — 47.339 linhas e 46 colunas, com os nomes de colunas usados pelo painel; guia em `evidencias/Importacao_PowerBI_RAIS_SJC.txt`

### 4.3 Resposta ao feedback da Sprint 1

O orientador pediu para esclarecer se os 64,37% de RAIS negativa poderiam ser erro de filtragem. Não são: o extrato contém apenas o município 354990, e 13.604 desses 30.470 estabelecimentos declararam atividade no ano — funcionavam, mas sem empregados formais. Outros 1.758 tiveram empregados no ano e fecharam 2024 com zero vínculos.

### 4.4 Log de Decisões de Dados — Sprint 2

| ID | Problema | Decisão | Status |
|---|---|---|---|
| DEC-006 / 009 | IBGE só detalha o valor adicionado por setor até 2021 | Comparar VAB 2021 com o emprego de 2024, mostrando o ano de cada fonte | Fechada |
| DEC-008 | Valores do PIB de anos diferentes não são comparáveis | Corrigir pelo IPCA para reais de 2023 | Fechada |
| DEC-011 | 53 registros com indicador de RAIS negativa = 2 | Categoria própria, somada a "Sem vínculo" | Fechada |
| DEC-013 | Administração pública fora da base RAIS | Excluir do cruzamento com o PIB | Fechada |
| DEC-014 | Nível de agregação dos setores | Seção CNAE 2.0, padrão IBGE | Fechada |
| DEC-015 | Região oficial ausente dos arquivos | Bairro → região pelo Plano Diretor; setor do CEP para ambíguos | **Aberta** |
| DEC-016 | Coordenadas corrompidas no arquivo de CEPs | Usar as coordenadas corretas; importar com localidade en-US | Fechada |
| DEC-017 | 9 bairros geocodificados em homônimos | Coluna Alerta Coordenada; regeocodificar | **Aberta** |
| DEC-018 | CEPs de avenida e bairros não encontrados | Sem ponto no mapa; região pelo bairro | Fechada |
| DEC-019 | "Com vínculo" inclui quem fechou o ano sem empregados | Coluna Situação Detalhada | Fechada |
| DEC-020 | Descrições CNAE com grafia antiga | Texto oficial da CNAE 2.3 | Fechada |
| DEC-021 | Tipo de atividade e intensidade tecnológica pedidos pelo cliente | Colunas derivadas por regra fixa | Fechada |
| DEC-022 | Mapa localizava pelo texto do CEP | Base única com latitude/longitude | **Aberta** |

### 4.5 Evidências a anexar

Marque cada item depois de adicionar o print ou arquivo na pasta `evidencias/`.

- [ ] Print da página KPIs e Mapa
- [ ] Print da página Setor de Atividades (CNAE)
- [ ] Print da página PIB e Emprego
- [ ] Print da página Notas Metodológicas
- [x] Gráfico de vínculos por região oficial gerado da base (`evidencias/sprint2_vinculos_por_regiao.png`)
- [ ] Execução do notebook do PIB no Colab
- [ ] Vídeo de incremento da Sprint 2

## 5. Estrutura do repositório

```
.
├── README.md
├── RELATORIO_SPRINT_1.md
├── RELATORIO_SPRINT_2.md
├── MVP/           MVP de cada sprint (sp1.md, sp2.md)
├── docs/          documentação Scrum e relatórios técnicos
├── dados/         bases tratadas prontas para o Power BI
├── notebooks/     ETL em Google Colab
├── powerbi/       dashboard
└── evidencias/    prints, gráficos e guias de cada sprint
```

## 6. Pendências e riscos

| Pendência | Impacto | Encaminhamento |
|---|---|---|
| Lista oficial de bairros da Região Norte ou shapefile das regiões (DEC-015) | 1.024 estabelecimentos com região de confiabilidade média | Pedir à Prefeitura, via cliente |
| Série histórica da RAIS | US08 não mostra evolução | Baixar RAIS 2022–2023 ou ajustar o critério com o cliente |
| Datas de admissão | US10 pede contratações "ordenadas por data", mas a RAIS Estabelecimentos não tem esse campo | Avaliar a RAIS Vínculos ou revisar o critério |
| Troca da fonte e do mapa no painel (DEC-022) | Mapa atual pouco preciso | Seguir o guia de importação na Sprint 3 |
| DEC-007, DEC-010 e DEC-012 | Decisões citadas pela equipe sem registro no log | Transcrever para `docs/06-Decisoes-de-Dados.docx` |

## 7. Próximos passos

**Sprint 3 (entrega em 23/11/2026): consolidação e entrega final**

1. US06: importar a base única, trocar o mapa para latitude/longitude e criar os visuais por região.
2. US08: definir a fonte da série histórica com o cliente.
3. US10: contratações mais recentes (depende da fonte de dados).
4. US11: dashboard consolidado, relatório técnico final e apresentação.

A Feira de Soluções (03/12/2026) é o marco de apresentação final.

## 8. Equipe

| Integrante | Papel | Função na Sprint 2 |
|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Product Owner | Apoio geral e demais demandas |
| Juliano Souza Santana | Scrum Master | Dados e documentação |
| Beatriz Oliveira Sepulvida | Scrum Team | CSV e Excel |
| Caio Moreira | Scrum Team | Tratamento de dados |
| Hemilly Christiny da Silva Freitas | Scrum Team | Documentação |
| João Pedro Faria Vital de Souza | Scrum Team | Apoio geral e demais demandas |
| Milena Silva Nogueira | Scrum Team | Power BI |
| Thalya Awany Berti | Scrum Team | Power BI |

---

*Última atualização: 26/10/2026*
