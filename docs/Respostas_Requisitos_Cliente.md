# Respostas aos Requisitos do Cliente

**Projeto:** Observatório do Ecossistema Industrial e de Serviços de São José dos Campos
**Cliente:** CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos
**Documento de referência:** Requisitos de Cliente 1LOG – CADI (API 2026-1, 1º semestre de Logística)
**Ponto de vista:** Logística (cadeia de suprimentos) · **Atualizado em:** 23/11/2026 · [voltar ao README](../README.md)

> O observatório responde as 7 questões de análise, atende as 8 funcionalidades e os 6 requisitos técnicos (RN.P.1 a RN.P.6). Este documento liga cada item do cliente à resposta, com os números da base e o lugar do painel onde ele aparece.

**Base dos números:** RAIS 2024 de São José dos Campos (47.339 estabelecimentos e 206.717 vínculos ativos em 31/12/2024), na base única [`dados/RAIS_SJC_2024_PowerBI.csv`](../dados/RAIS_SJC_2024_PowerBI.csv), e PIB dos Municípios do IBGE em [`dados/IBGE_PIB_SJC_Observatorio.xlsx`](../dados/IBGE_PIB_SJC_Observatorio.xlsx). Os percentuais de emprego são sobre os 206.717 vínculos ativos.

**Painel:** [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9). A página **Regiões e Tecnologia** e o mapa com 99,99% dos pontos estão no projeto `.pbip` e aparecem no link depois que o painel for republicado (ver [`powerbi/README.md`](../powerbi/README.md)).

## Índice

1. [Resumo: requisito → onde está](#1-resumo-requisito--onde-está)
2. [Questões para análise](#2-questões-para-análise)
3. [Funcionalidades da solução](#3-funcionalidades-da-solução)
4. [Resultados esperados](#4-resultados-esperados)
5. [Tecnologias exigidas (RN.P)](#5-tecnologias-exigidas-rnp)
6. [Limites das respostas](#6-limites-das-respostas)

---

## 1. Resumo: requisito → onde está

| Requisito do cliente | Situação | Onde está |
|---|---|---|
| Q1. Principais setores | Respondida | Painel: Setor de Atividades (CNAE) · seção 2.1 |
| Q2. Distribuição geográfica | Respondida | Painel: KPIs e Mapa, Regiões e Tecnologia · seção 2.2 |
| Q3. Tipos de atividade predominantes | Respondida | Painel: Regiões e Tecnologia · seção 2.3 |
| Q4. Macroprocessos produtivos | Respondida (classificação da equipe, DEC-024) | Painel: Regiões e Tecnologia · seção 2.4 |
| Q5. Indústria × desenvolvimento tecnológico | Respondida | Painel: Regiões e Tecnologia · seção 2.5 |
| Q6. Inovação, tecnologia e desenvolvimento econômico | Respondida | Painel: PIB e Emprego · seção 2.6 |
| Q7. Oportunidades profissionais | Respondida do ponto de vista da logística | Seção 2.7 |
| Funcionalidades (8) | 8 atendidas | Seção 3 |
| Resultados esperados (4) | 3 entregues; apresentação em 03/12/2026 | Seção 4 |
| RN.P.1 a RN.P.6 | 6 atendidos | Seção 5 |

---

## 2. Questões para análise

### 2.1 Quais são os principais setores industriais e de serviços de São José dos Campos?

**Resposta:** comércio, indústria de transformação e serviços administrativos são os maiores empregadores. Na indústria, o destaque é o aeroespacial.

| Seção CNAE | Estabelecimentos | Vínculos ativos | % dos vínculos |
|---|---:|---:|---:|
| G – Comércio e reparação de veículos | 11.826 | 46.228 | 22,4% |
| C – Indústrias de transformação | 1.980 | 36.989 | 17,9% |
| N – Atividades administrativas e serviços complementares | 5.579 | 31.396 | 15,2% |
| Q – Saúde humana e serviços sociais | 4.465 | 18.824 | 9,1% |
| F – Construção | 3.297 | 11.870 | 5,7% |
| P – Educação | 1.929 | 11.667 | 5,6% |

- **Maior atividade isolada:** fabricação de aeronaves, com 11.069 vínculos (5,4% de todos os empregos formais) em 10 estabelecimentos.
- **Outras atividades grandes:** atendimento hospitalar (10.137 vínculos), restaurantes (7.598), supermercados (7.121), teleatendimento (4.395) e fabricação de automóveis (3.415, em 3 estabelecimentos).
- **Setores em destaque do cliente:** aeroespacial 5,9% dos vínculos, automotivo 4,6% (fabricação 2,4% e comércio e reparação 2,2%) e químico e farmacêutico 1,3%.

**No painel:** página *Setor de Atividades (CNAE)*, com o Top 10 por empregos CLT e por estabelecimentos, a participação por seção e a indústria por setor.

### 2.2 Como esses setores estão distribuídos no município e na região?

**Resposta:** o emprego se concentra no Sul e no Centro (26% cada), mas a indústria fica no Leste e no Sudeste. Na região, São José dos Campos é o polo econômico.

| Região oficial | Vínculos ativos | % | Três maiores tipos de atividade na região |
|---|---:|---:|---|
| Sul | 54.800 | 26,5% | Comércio 31%, manufatura 16%, serviços administrativos 14% |
| Centro | 54.609 | 26,4% | Saúde e educação 27%, comércio 23%, serviços administrativos 18% |
| Oeste | 43.193 | 20,9% | Serviços administrativos 19%, comércio 16%, manufatura 14% |
| Leste | 33.161 | 16,0% | Manufatura 31%, comércio 19%, serviços administrativos 16% |
| Sudeste | 14.047 | 6,8% | Manufatura 70%, comércio 10%, construção 5% |
| Norte | 6.577 | 3,2% | Comércio 28%, manufatura 18%, saúde e educação 17% |

- **Indústria:** 54% dos empregos da indústria de transformação estão no Leste (28%) e no Sudeste (26%). No Sudeste, 70% dos empregos são industriais.
- **Logística:** o Sul concentra 52% dos empregos do comércio atacadista e 35% dos de transporte e armazenagem.
- **Na região:** São José dos Campos responde por 48,9% do PIB da microrregião e 31,7% do PIB da mesorregião do Vale do Paraíba (IBGE, 2023).

**No painel:** mapa e filtro de região na página *KPIs e Mapa*; gráficos por região na página *Regiões e Tecnologia*.

### 2.3 Quais tipos de atividade produtiva predominam?

**Resposta:** comércio e manufatura predominam no emprego. Tecnologia e logística são menores, mas concentradas em poucas regiões.

| Tipo de atividade | Estabelecimentos | Vínculos ativos | % dos vínculos |
|---|---:|---:|---:|
| Comércio | 11.826 | 46.228 | 22,4% |
| Manufatura (indústria de transformação) | 1.980 | 36.989 | 17,9% |
| Serviços administrativos e de apoio | 5.579 | 31.396 | 15,2% |
| Saúde e educação | 6.394 | 30.491 | 14,8% |
| Outros serviços | 6.718 | 17.939 | 8,7% |
| Serviços especializados | 7.020 | 13.284 | 6,4% |
| Construção | 3.297 | 11.870 | 5,7% |
| Logística e transporte | 1.418 | 9.137 | 4,4% |
| Tecnologia, informação e P&D | 2.691 | 6.249 | 3,0% |
| Extração e utilidades | 108 | 2.398 | 1,2% |
| Agropecuária | 295 | 624 | 0,3% |

- **Tamanho médio:** a manufatura tem 1.980 estabelecimentos e média de 19 vínculos por estabelecimento; o comércio tem 11.826 e média de 4.
- **Tecnologia, informação e P&D:** 38% dos vínculos estão no Oeste e 26% no Centro.

A classificação segue as categorias do próprio documento do cliente (manufatura, tecnologia, logística, serviços especializados), aplicada pela divisão CNAE (DEC-021).

**No painel:** página *Regiões e Tecnologia*, gráfico "Vínculos por tipo de atividade", que responde ao filtro de região.

### 2.4 Quais são os principais macroprocessos produtivos?

**Resposta:** pela lógica da cadeia de suprimentos, a produção (indústria e construção) e o varejo concentram 40% dos empregos. As etapas logísticas centrais, distribuição atacadista e transporte e armazenagem, somam 8,3%.

A RAIS não informa os processos internos de cada empresa. Por isso, a equipe classificou cada estabelecimento pela **etapa da cadeia de suprimentos** em que ele atua, a partir da divisão CNAE (DEC-024). É a leitura de macroprocessos do ponto de vista da logística: abastecer, produzir, distribuir, entregar ao consumidor, dar suporte pós-venda e fazer o retorno dos materiais.

| Macroprocesso logístico | Estabelecimentos | Vínculos ativos | % dos vínculos | Exemplos em SJC |
|---|---:|---:|---:|---|
| 1. Suprimento (agro, extração, energia e água) | 343 | 1.606 | 0,8% | Agropecuária, energia, captação de água |
| 2. Produção (indústria e construção) | 4.622 | 46.695 | 22,6% | Aeronaves, automóveis, construção de edifícios |
| 3. Distribuição atacadista | 1.732 | 8.115 | 3,9% | Atacado de alimentos e de materiais médicos |
| 4. Transporte e armazenagem | 1.418 | 9.137 | 4,4% | Transporte rodoviário de carga (843 estabelecimentos), armazenagem, carga e descarga |
| 5. Varejo (venda ao consumidor) | 9.475 | 36.978 | 17,9% | Supermercados, concessionárias, lojas |
| 6. Pós-venda, manutenção e reparação | 1.655 | 3.517 | 1,7% | Oficinas, manutenção de máquinas, manutenção de aeronaves |
| 7. Logística reversa (resíduos e reciclagem) | 60 | 1.416 | 0,7% | Coleta e tratamento de resíduos |
| 8. Serviços de apoio às empresas | 16.654 | 51.679 | 25,0% | Engenharia, escritório, teleatendimento, TI |
| 9. Serviços ao consumidor e públicos | 11.370 | 47.574 | 23,0% | Saúde, educação, alimentação |
| Não classificado (atividade não informada) | 10 | 0 | 0,0% | — |

**Leitura logística:**
- A cadeia é puxada por uma produção de alto valor (aeronaves e automóveis) e por um varejo grande.
- A distribuição e o transporte são feitos por muitas empresas pequenas: dos 557 estabelecimentos de transporte e armazenagem com empregados, 400 são micro.
- A logística reversa ainda é pequena: 60 estabelecimentos e 1.416 vínculos.

**No painel:** página *Regiões e Tecnologia*, gráfico "Vínculos por macroprocesso logístico".

### 2.5 Qual a relação entre a indústria presente e o desenvolvimento tecnológico regional?

**Resposta:** 69% dos empregos industriais estão em atividades de alta ou média-alta tecnologia. É uma indústria muito mais tecnológica que o resto da economia, e está concentrada em poucas empresas grandes do Leste e do Sudeste.

Usamos a classificação de intensidade tecnológica da OCDE (Galindo-Rueda e Verger, 2016), aplicada pela divisão e pelo grupo CNAE (DEC-021):

| Intensidade tecnológica | Estabelecimentos | Vínculos ativos | % de todos os vínculos | % dos vínculos da indústria |
|---|---:|---:|---:|---:|
| Alta | 138 | 14.398 | 7,0% | 37,4%* |
| Média-alta | 2.381 | 14.406 | 7,0% | 31,9%* |
| Média | 808 | 4.999 | 2,4% | 13,5% |
| Média-baixa | 864 | 6.328 | 3,1% | 17,1% |
| Não se aplica (fora da indústria e de TI/P&D) | 43.148 | 166.586 | 80,6% | — |

\* Na indústria de transformação (36.989 vínculos), alta = 13.846 e média-alta = 11.816. As linhas "Alta" e "Média-alta" da tabela também incluem P&D (alta) e serviços de TI (média-alta).

- **Quem puxa a alta tecnologia:** aeronaves (11.069 vínculos), turbinas e peças para aeronaves (1.187), instrumentos médicos e ópticos (2.259) e, na média-alta, automóveis (3.415).
- **Onde fica:** os empregos de alta e média-alta tecnologia estão no Sudeste (9.051), no Leste (8.131) e no Oeste (6.924). Centro e Norte quase não têm.
- **Concentração:** 38 estabelecimentos com 500 ou mais empregados reúnem 48.786 vínculos (23,6% do total).

**No painel:** página *Regiões e Tecnologia*, gráfico "Vínculos por intensidade tecnológica (OCDE)".

### 2.6 Como o ecossistema se conecta com inovação, tecnologia e desenvolvimento econômico?

**Resposta:** a indústria tecnológica gera muito mais valor do que o seu peso no emprego. Ela tem 24,7% do emprego privado e gera 45,8% do valor adicionado privado, um índice de produtividade relativa de 1,86.

- **Tamanho da economia:** PIB de R$ 61,4 bilhões em 2023, ou R$ 86.361 por habitante.
- **Crescimento:** o PIB cresceu 1,6% ao ano acima da inflação entre 2002 e 2023, e 2,0% ao ano na última década.
- **Peso da indústria:** 42,4% do valor adicionado vem da indústria (2021, último dado por setor). Esse peso chegou a 59% em 2004, caiu até 32% em 2013 e voltou a subir a partir de 2016.
- **Peso no estado:** SJC é 1,78% do PIB paulista. A participação caiu 0,79 ponto desde 2002, porque o estado cresceu mais rápido, não porque SJC encolheu.
- **Pesquisa e tecnologia na RAIS:** 6.249 vínculos em tecnologia, informação e P&D, dos quais 552 em pesquisa e desenvolvimento científico (68 estabelecimentos).

**Ligação com a logística:** a inovação de SJC está na manufatura de alto valor, e ela depende de cadeias de suprimentos longas e exigentes: componentes importados, rastreabilidade, estoques de alto valor e manutenção (MRO). É aí que o desenvolvimento tecnológico encontra a logística.

> Limite: os institutos públicos de pesquisa da cidade (DCTA, ITA, INPE) são administração pública e não entram nesta base (DEC-013). O peso da pesquisa em SJC é maior do que os 552 vínculos de P&D privado mostram.

**No painel:** página *PIB e Emprego*, com o peso de cada setor no emprego e no valor adicionado, a produtividade relativa e o PIB de 2002 a 2023.

### 2.7 Quais oportunidades de atuação profissional existem? (ponto de vista da logística)

O documento do cliente fala em "engenheiro de produção". Como o projeto é do curso de Logística, a resposta é dada para o **profissional de logística**. Cada oportunidade abaixo sai de um número da base.

| Onde | Tamanho em SJC | O que o profissional de logística faz |
|---|---|---|
| Indústria aeroespacial e automotiva | 11.069 vínculos em aeronaves, 1.187 em peças e turbinas, 3.415 em automóveis; Leste e Sudeste | Planejamento de materiais (PCP e MRP), compras e importação de componentes, controle de estoques de alto valor, rastreabilidade de peças |
| Transporte rodoviário de carga | 843 estabelecimentos e 3.552 vínculos, a maioria micro e pequenas empresas | Gestão de frota, roteirização, custos de frete, operação e indicadores de entrega |
| Atacado e armazenagem | 8.115 vínculos no atacado (52% no Sul), 530 em armazenamento, 374 em organização do transporte de carga, 363 em carga e descarga | Centros de distribuição, gestão de armazém (WMS), recebimento e expedição, agenciamento de carga |
| Varejo | 36.978 vínculos; supermercados com 7.121 | Abastecimento de lojas, gestão de estoque, entrega ao consumidor (última milha) |
| Saúde | 10.137 vínculos em hospitais, 778 no atacado de materiais médicos, 2.259 na fabricação de instrumentos médicos | Logística hospitalar: suprimentos, controle de validade, rastreabilidade de medicamentos e materiais |
| Pós-venda e manutenção | 3.517 vínculos, incluindo 235 em manutenção de aeronaves | Logística de peças de reposição e de manutenção (MRO) |
| Logística reversa | 60 estabelecimentos e 1.416 vínculos em resíduos e reciclagem | Coleta, triagem e retorno de materiais, em linha com a Política Nacional de Resíduos Sólidos (Lei 12.305/2010) |

**Leitura:** a maior oportunidade está na **indústria de alta tecnologia**, que tem poucos empregadores grandes, cadeias complexas e alto valor por peça. O maior número de vagas de entrada está no **varejo** e no **transporte de carga**. As áreas que podem crescer, por serem pequenas hoje, são a **logística reversa** e a **logística hospitalar**.

**Confirmar com o cliente:** se a pergunta deve ser respondida para o profissional de logística, como fizemos, ou para o engenheiro de produção, como está escrito no documento.

---

## 3. Funcionalidades da solução

| Funcionalidade pedida | Atendida | Onde |
|---|---|---|
| Visualização dos principais setores industriais e de serviços | Sim | Setor de Atividades (CNAE): Top 10 e participação por seção |
| Identificação e classificação das atividades econômicas predominantes | Sim | Setor de Atividades (CNAE, 673 classes com nome oficial); Regiões e Tecnologia (tipo de atividade, macroprocesso, OCDE) |
| Representação geográfica das empresas ou setores | Sim | KPIs e Mapa (mapa por CEP, 99,99% com ponto após republicar); Regiões e Tecnologia (vínculos por região) |
| Indicadores econômicos e produtivos | Sim | KPIs e Mapa (estabelecimentos, vínculos, % com vínculo); PIB e Emprego (PIB, valor adicionado, produtividade relativa) |
| Participação dos setores na economia regional | Sim | PIB e Emprego: peso de cada setor no emprego e no valor adicionado |
| Comparações entre segmentos industriais e de serviços | Sim | Setor de Atividades (indústria por setor, tabela por porte); PIB e Emprego (produtividade relativa) |
| Gráficos e painéis analíticos | Sim | 5 páginas com filtros por setor, porte, tipo de estabelecimento e região |
| Interface clara e intuitiva | Sim | Navegação entre páginas, textos "o que isso mostra", página de Notas Metodológicas |

## 4. Resultados esperados

| Resultado | Situação | Onde |
|---|---|---|
| Visualizações e dashboards sobre o perfil produtivo regional | Entregue | [Painel publicado](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) e [`powerbi/`](../powerbi/) |
| Relatório técnico (fontes, metodologia e análises) | Entregue | [Relatório Técnico final](11-Relatorio-Tecnico-Sprint-3.docx), [Anexo 8 final](Relatorio_Sprint3_Anexo8.docx), relatórios técnicos das Sprints 1 e 2, [Relatório da Sprint 3](RELATORIO_SPRINT_3.md), [Log de Decisões](06-Decisoes-de-Dados.md) e este documento (análises) |
| Repositório com dados organizados e documentação | Entregue | Este repositório: [`dados/`](../dados/), [`notebooks/`](../notebooks/), [`docs/`](./), [`evidencias/`](../evidencias/) |
| Apresentação em evento acadêmico (Feira de Soluções) | 03/12/2026 | Vídeo no canal [LogMulti](https://www.youtube.com/@LogMulti) |

## 5. Tecnologias exigidas (RN.P)

| Requisito | Atendido | Evidência |
|---|---|---|
| RN.P.1 – Bases públicas organizadas no Google Colab | Sim | Notebooks 01 (ETL da RAIS), 01b (geocodificação) e 02 (base única), com links para abrir no Colab em [`evidencias/link-google-colab.md`](../evidencias/link-google-colab.md). O notebook de tratamento do PIB não está no repositório; só a planilha que ele gerou |
| RN.P.2 – Tratamento em Python 3+ | Sim | [`evidencias/codigos-tratamento-dados.md`](../evidencias/codigos-tratamento-dados.md) |
| RN.P.3 – Visualização em Power BI | Sim | [`powerbi/pbip/Observatorio_SJC.pbip`](../powerbi/pbip/) e painel publicado |
| RN.P.4 – Versionamento e documentação no GitHub | Sim | Este repositório, com histórico de commits por sprint |
| RN.P.5 – Visualizações claras e navegação intuitiva | Sim | Navegador de páginas, títulos e subtítulos explicativos, filtros no topo de cada página |
| RN.P.6 – Organização dos dados e documentação técnica | Sim | Dicionário de dados em [`dados/README.md`](../dados/README.md), Log de Decisões com 24 decisões, relatórios das sprints |

## 6. Limites das respostas

- **Um único ano (2024):** a RAIS disponível não permite medir quais setores crescem. A evolução no tempo vem só do PIB (2002–2023).
- **Sem nome das empresas (DEC-004):** os rankings são por setor e por atividade, não por empresa.
- **Administração pública fora da base (DEC-013):** institutos de pesquisa públicos, prefeitura e hospitais públicos não aparecem nos números da RAIS.
- **Região no painel × base única:** a região dos gráficos do painel vem da planilha `CEP x Região`, que deixa 603 estabelecimentos sem região; os números deste documento usam a base única, que deixa 5. Por isso o painel pode mostrar valores por região um pouco diferentes (DEC-022).
- **Macroprocessos (DEC-024):** é uma classificação da equipe pela atividade principal de cada estabelecimento. Uma fábrica com transporte próprio, por exemplo, conta só em "Produção".
