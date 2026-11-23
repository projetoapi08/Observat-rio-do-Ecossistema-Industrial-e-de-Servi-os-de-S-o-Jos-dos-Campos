> Versão em Markdown de [`Relatorio_Sprint3_Anexo8.docx`](Relatorio_Sprint3_Anexo8.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

**FATEC SÃO JOSÉ DOS CAMPOS**

**API — Aprendizagem por Projetos Integrados · Curso de Logística**

# Relatório de Desenvolvimento — Sprint 3 (versão final)

**Observatório do Ecossistema Industrial e de Serviços de São José dos Campos**

**Entrega da Sprint 3: 23/11/2026 · Feira de Soluções: 03/12/2026**

**Autor 1 (LinkedIn):** Beatriz Oliveira Sepulvida — <https://www.linkedin.com/in/beatriz-sepulvida?utm_source=share_via&utm_content=profile&utm_medium=member_ios>

**Autor 2 (LinkedIn):** Caio Moreira — <https://www.linkedin.com/in/caiomoreiradearaujo>

**Autor 3 (LinkedIn):** Hemilly Christiny da Silva Freitas — <https://www.linkedin.com/in/hemilly-freitas-31a509269?utm_source=share_via&utm_content=profile&utm_medium=member_android>

**Autor 4 (LinkedIn):** João Pedro Faria Vital de Souza — <https://www.linkedin.com/in/joao-pedro-a2b6122b7?utm_source=share_via&utm_content=profile&utm_medium=member_android>

**Autor 5 (LinkedIn):** Juliano Souza Santana – <https://www.linkedin.com/in/juliano-santana-776992249?utm_source=share_via&utm_content=profile&utm_medium=member_android>

**Autor 6 (LinkedIn):** Milena Silva Nogueira - <https://www.linkedin.com/in/milenasnogueira>

**Autor 7 (LinkedIn):** Pedro Henrique Oliveira de Carvalho - <https://www.linkedin.com/in/pedro-henrique-oliveira-de-carvalho-75bb07427?utm_source=share_via&utm_content=profile&utm_medium=member_ios>

**Autor 8 (LinkedIn):** Thalya Awany Berti - <https://www.linkedin.com/in/thalya-awany-berti-773923266>

**Professor M2 (Orientador):** José Jaétis

**Professor P2:** Marcus Nascimento

## Resumo do projeto

O presente projeto desenvolve o Observatório do Ecossistema Industrial e de Serviços de São José dos Campos, uma ferramenta de inteligência de dados construída em parceria com o CADI e a Secretaria de Desenvolvimento Econômico do município. O projeto tem como objetivo consolidar, tratar e disponibilizar indicadores públicos sobre os estabelecimentos industriais e de serviços da cidade, utilizando como fontes de dados a Relação Anual de Informações Sociais (RAIS) do Ministério do Trabalho e Emprego e o Produto Interno Bruto dos Municípios do Instituto Brasileiro de Geografia e Estatística (IBGE). A metodologia adota o processo de Extração, Transformação e Carga (ETL) executado em linguagem Python no ambiente Google Colab, seguido da modelagem e visualização dos dados na ferramenta Microsoft Power BI, segundo a metodologia ágil Scrum, organizada em 3 sprints.

Ao final das três sprints, o observatório reúne, num painel de cinco páginas, os indicadores gerais da base, os setores de atividade, o cruzamento entre emprego e valor adicionado e uma página sobre regiões e tecnologia. A base de 47.339 estabelecimentos e 206.717 vínculos ativos foi geocodificada pelo Cadastro Nacional de Endereços para Fins Estatísticos (CNEFE) do IBGE, com 99,99% dos estabelecimentos no mapa, e classificada por região oficial, tipo de atividade, intensidade tecnológica e etapa da cadeia de suprimentos. Os resultados indicam que a indústria responde por 24,7% do emprego formal privado e por 45,8% do valor adicionado privado, que 69% dos empregos industriais estão em atividades de alta ou média-alta tecnologia, concentradas nas regiões Leste e Sudeste, e que a distribuição atacadista e o transporte e armazenagem reúnem 8,3% do emprego formal. As 24 decisões de tratamento estão registradas no Log de Decisões de Dados (DEC-001 a DEC-024).

**Palavras-Chave: Observatório Econômico; RAIS; Geocodificação; Business Intelligence; Cadeia de Suprimentos.**

## Abstract

This project develops the Observatory of the Industrial and Services Ecosystem of São José dos Campos, a data intelligence tool built in partnership with CADI and the city's Secretariat of Economic Development. The project aims to consolidate, treat, and make available public indicators on the city's industrial and services establishments, using as data sources the Annual Social Information Report (RAIS) from the Brazilian Ministry of Labor and Employment and the Municipal Gross Domestic Product from the Brazilian Institute of Geography and Statistics (IBGE). The methodology adopts an Extract, Transform, Load (ETL) process executed in Python within Google Colab, followed by data modeling and visualization in Microsoft Power BI, under the Scrum agile methodology organized into 3 sprints.

At the end of the three sprints, the observatory brings together, in a five-page dashboard, the general indicators of the base, economic sectors, the comparison between employment and value added, and a page on regions and technology. The base of 47,339 establishments and 206,717 active jobs was geocoded with the IBGE National Address Register for Statistical Purposes (CNEFE), placing 99.99% of establishments on the map, and classified by official region, type of activity, technological intensity, and supply chain stage. The results show that manufacturing accounts for 24.7% of private formal employment and 45.8% of private value added, that 69% of industrial jobs are in high or medium-high technology activities, concentrated in the East and Southeast regions, and that wholesale distribution and transport and storage account for 8.3% of formal employment. The 24 data treatment decisions are recorded in the Data Decision Log (DEC-001 to DEC-024).

***Keywords: Economic Observatory; RAIS; Geocoding; Business Intelligence; Supply Chain.***

## 1. Contextualização do projeto

São José dos Campos ocupa posição de destaque no Vale do Paraíba como polo industrial, tecnológico e de serviços, concentrando um número expressivo de estabelecimentos formais nos setores aeroespacial, automotivo e de tecnologia da informação. Apesar dessa relevância econômica, o município carece de uma ferramenta pública e centralizada que consolide indicadores sobre o seu ecossistema produtivo, dificultando o acompanhamento de políticas de desenvolvimento econômico local.

Esse cenário motivou o CADI e a Secretaria de Desenvolvimento Econômico de São José dos Campos a propor, em parceria com a Fatec São José dos Campos, o desenvolvimento de um observatório de dados nos moldes do Observatório da Inovação RS, iniciativa do governo do Rio Grande do Sul que reúne, em um painel público construído em Microsoft Power BI, indicadores sobre o ecossistema de inovação, ciência e tecnologia gaúcho (SICT, 2025). Adaptando essa referência para a realidade de São José dos Campos, o projeto se propõe a mapear o ecossistema industrial e de serviços do município a partir de bases de dados públicas, entregando um painel equivalente que sirva de apoio à tomada de decisão do poder público local.

O documento de requisitos do cliente definiu sete questões de análise, sobre os principais setores, sua distribuição geográfica, os tipos de atividade, os macroprocessos produtivos, a relação com o desenvolvimento tecnológico e com a inovação, e as oportunidades de atuação profissional. Este relatório apresenta a versão final do projeto, entregue ao fim da terceira sprint, e as respostas a essas questões do ponto de vista da logística.

## 2. Objetivos do projeto

Os objetivos estabelecidos para esse projeto consistem em:

- Desenvolver um pipeline de extração, tratamento e carga (ETL) em Python, no ambiente Google Colab, capaz de filtrar e tratar os dados públicos da RAIS especificamente para o município de São José dos Campos;

- Identificar e documentar formalmente as inconsistências estruturais presentes na base de dados bruta, de modo a garantir a confiabilidade dos indicadores gerados;

- Construir um painel interativo em Microsoft Power BI que reúna indicadores de emprego, natureza dos estabelecimentos e distribuição geográfica do ecossistema industrial e de serviços do município;

- Integrar os dados do Produto Interno Bruto dos Municípios (IBGE) ao painel, comparando a participação de cada setor no emprego e no valor adicionado do município;

- Representar a distribuição geográfica dos estabelecimentos por bairro e pelas regiões oficiais de São José dos Campos;

- Classificar os estabelecimentos pela etapa da cadeia de suprimentos em que atuam e responder às questões de análise do cliente do ponto de vista da logística.

## 3. Fundamentação dos métodos analíticos e das tecnologias utilizadas

### 3.1 Métodos analíticos utilizados

O desenvolvimento do observatório se apoia primordialmente em métodos de estatística descritiva e em técnicas de tratamento e segmentação de microdados administrativos, aplicados sobre a base da RAIS. A literatura brasileira que utiliza microdados da RAIS para estudos de mercado de trabalho reforça a robustez dessa fonte, ao mesmo tempo em que aponta a necessidade de tratamento cuidadoso de suas particularidades antes de qualquer análise (Silva; Lima, 2018; De Negri et al., 2001). Para o desafio específico do mapeamento geográfico dos estabelecimentos — que não possuem coordenadas diretas na base pública, o projeto adota a técnica de geocodificação a partir do campo de CEP, seguindo abordagem já validada na literatura de geolocalização de empregos formais em cidades brasileiras (Morelli; Fiedler; Cunha, 2023).

Os estabelecimentos foram classificados por regras fixas a partir da CNAE: as seções foram agrupadas nos tipos de atividade citados pelo cliente (manufatura, tecnologia, logística, serviços especializados e outros), e as divisões foram ordenadas pela taxonomia de intensidade de pesquisa e desenvolvimento da OCDE (GALINDO-RUEDA; VERGER, 2016). Os códigos e descrições foram validados pela estrutura oficial da CNAE 2.3 (IBGE, \[s.d.\]), e a região de cada estabelecimento foi atribuída pelo bairro, segundo a lista de bairros por região do Plano Diretor do município (SÃO JOSÉ DOS CAMPOS, \[2018\]), com conferência pelo setor do CEP.

Na terceira sprint, dois métodos completaram a análise. A geocodificação passou a usar o CNEFE do Censo 2022 (IBGE, \[s.d.\]): cada CEP recebe o ponto médio dos endereços do cadastro com aquele CEP, a mesma base usada por Morelli, Fiedler e Cunha (2023) para localizar empregos formais. Para responder à questão sobre macroprocessos produtivos, que a RAIS não informa, cada estabelecimento foi classificado pela etapa da cadeia de suprimentos em que atua (suprimento, produção, distribuição, transporte e armazenagem, varejo, pós-venda e logística reversa), seguindo a visão integrada da logística empresarial de Ballou (2006).

A Tabela 1 a seguir apresenta a lista de referências que auxiliam no entendimento dos métodos analíticos utilizados nesse projeto.

**Tabela 1 — Tabela de referências**

| **Autor(es)**                  | **Métodos de análise**                                           | **Dados utilizados**                                             | **Principais conclusões**                                                                                                                                              |
|--------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Silva; Lima (2018)             | Revisão integrativa de estudos com microdados RAIS               | 10 artigos analisados, publicados entre 2006 e 2015              | A RAIS é um instrumento relevante de análise do mercado de trabalho formal, mesmo sendo pouco explorada, contribuindo para políticas públicas de emprego.              |
| De Negri et al. (2001)         | Análise estatística comparativa entre bases administrativas      | Microdados RAIS e PNAD                                           | As duas bases convergem em variáveis como idade e gênero, mas apresentam diferenças relevantes no conceito de rendimento.                                              |
| Morelli; Fiedler; Cunha (2023) | Geocodificação por CEP combinada com faces de logradouro         | Base RAIS + CNEFE (IBGE)                                         | É possível localizar geograficamente empregos formais a partir do CEP com boa precisão em cidades médias e grandes, e de forma aproximada em municípios de CEP único.  |
| Galindo-Rueda; Verger (2016)   | Classificação de atividades econômicas pela intensidade de P&D   | Gastos em P&D e valor adicionado por atividade em países da OCDE | As atividades podem ser agrupadas em níveis de intensidade tecnológica (de alta a baixa), aplicáveis à indústria e aos serviços.                                       |
| Ballou (2006)                  | Conceituação da logística empresarial e da cadeia de suprimentos | Revisão conceitual (livro-texto)                                 | A logística integra o fluxo de materiais do suprimento à produção, à distribuição física e ao pós-venda, o que permite classificar as atividades pela etapa da cadeia. |

### 3.2 Tecnologias da Informação

O projeto utiliza três tecnologias principais, definidas em conjunto com o professor orientador. O Google Colab, executando Python 3, foi escolhido para a etapa de ETL por permitir o processamento do arquivo bruto da RAIS com mais de 12,6 milhões de registros nacionais e cerca de 3,27 GB descompactados em ambiente gratuito e colaborativo, sem necessidade de infraestrutura local. A biblioteca padrão csv foi utilizada em modo de leitura sequencial (streaming), evitando o carregamento integral do arquivo em memória.

O GitHub foi adotado como repositório central de versionamento e documentação (usuário projetoapi08), organizado em pastas: docs/ (Visão e Escopo, backlogs, Log de Decisões de Dados, relatórios técnicos e de desenvolvimento e as respostas aos requisitos do cliente), notebooks/ (01: ETL da RAIS; 01b: geocodificação dos CEPs; 02: base única do Power BI), dados/ (bases tratadas e dicionário de dados), powerbi/ (projeto Observatorio_SJC.pbip, planilhas-fonte e versões anteriores), MVP/ e evidencias/. Por fim, o Microsoft Power BI foi definido como ferramenta de visualização final, por ser a mesma tecnologia empregada no painel do Observatório da Inovação RS, referência direta do projeto (SICT, 2025).

As principais dificuldades do projeto foram de qualidade e de disponibilidade dos dados: a RAIS pública não identifica as empresas nem traz data de admissão, o arquivo de CEPs teve as coordenadas corrompidas ao ser salvo no Excel em português, e a lista oficial de bairros da Região Norte não está no documento do Plano Diretor. Na terceira sprint, o painel passou a ler as planilhas por um parâmetro de pasta, para que qualquer integrante atualize os dados a partir do repositório.

## 4. Coleta e descrição dos dados utilizados

Os dados partiram da RAIS Estabelecimentos 2024, filtrada para São José dos Campos (código 354990), com 47.339 estabelecimentos e 206.717 vínculos ativos em 31/12/2024. Foram incorporados a série do PIB dos Municípios do IBGE (PIB de 2002 a 2023 e valor adicionado por setor até 2021), a estrutura oficial da CNAE 2.3, a lista de bairros por região do Plano Diretor e, na terceira sprint, o CNEFE do Censo 2022, com 320.850 endereços georreferenciados no município. Tudo foi reunido numa base única para o Power BI, com 47 colunas.

O orientador pediu, na avaliação da Sprint 1, que se esclarecesse se os 64,37% de RAIS negativa poderiam ser erro de filtragem. A verificação mostrou que não: o extrato contém apenas o município 354990, e 13.604 desses estabelecimentos declararam atividade no ano, ou seja, funcionavam sem empregados formais.

As decisões de tratamento foram registradas no Log de Decisões de Dados:

DEC-001 a DEC-005 (Sprint 1) — estabelecimentos com RAIS negativa mantidos com indicador próprio, recorte padrão pelos estabelecimentos com CNPJ, ano-base 2024 confirmado pelo cliente, rankings agregados por setor na falta de identificação nominal e defasagem documentada entre a RAIS 2024 e o PIB dos Municípios;

DEC-006/009 e DEC-013 — o valor adicionado por setor de 2021 é comparado com o emprego de 2024, último ano com detalhe setorial do IBGE, sem a administração pública, que não está na base RAIS do extrato;

DEC-008 e DEC-014 — valores do PIB corrigidos pelo IPCA para reais de 2023 e setores classificados pela Seção CNAE 2.0, padrão do IBGE;

DEC-011 e DEC-019 — os 53 registros com indicador de RAIS negativa igual a 2 ficam no grupo sem vínculo, e uma situação detalhada separa os 1.758 estabelecimentos que fecharam o ano sem empregados;

DEC-015 a DEC-018 — região oficial atribuída pelo bairro (99,99% da base), coordenadas corrompidas substituídas e pontos em bairros homônimos marcados para correção;

DEC-020 a DEC-022 — descrições da CNAE 2.3 oficiais, classificações derivadas (tipo de atividade, intensidade tecnológica, porte e setor destaque) e base única para o Power BI com mapa por coordenadas.

DEC-023 (Sprint 3) — coordenadas do mapa pelo CNEFE 2022, com 99,99% dos estabelecimentos no mapa e 329 dos 331 pontos em bairros homônimos corrigidos;

DEC-024 (Sprint 3) — macroprocessos produtivos classificados pela etapa da cadeia de suprimentos, a partir da classe CNAE, com a mesma regra na base única e no painel.

## 5. Resultados obtidos e esperados

O painel final tem cinco páginas: KPIs e Mapa, Setor de Atividades (CNAE), PIB e Emprego, Regiões e Tecnologia e Notas Metodológicas. Os dados mostram que comércio (22,4%), indústria de transformação (17,9%) e serviços administrativos (15,2%) são os maiores empregadores do município. A fabricação de aeronaves é a maior atividade isolada, com 11.069 vínculos (5,4% do emprego formal) em apenas 10 estabelecimentos.

A indústria gera 45,8% do valor adicionado privado com 24,7% do emprego privado (índice de produtividade relativa de 1,86) e se concentra nas regiões Leste e Sudeste, que reúnem 54% dos empregos industriais; 69% desses empregos estão em atividades de alta ou média-alta tecnologia. Pela cadeia de suprimentos, produção e varejo concentram 40,5% do emprego formal, e a distribuição atacadista e o transporte e armazenagem, 8,3%, com o Sul reunindo 52% dos empregos do atacado e 35% dos de transporte.

Do ponto de vista da logística, as maiores oportunidades profissionais estão no planejamento de materiais e nos suprimentos da indústria aeroespacial e automotiva, no transporte rodoviário de carga (843 estabelecimentos, a maioria micro e pequenas empresas), nos centros de distribuição do atacado, no abastecimento do varejo e na logística hospitalar. A logística reversa e a manutenção de aeronaves são áreas menores, com espaço para crescer.

Como limites, a RAIS disponível tem um único ano, o que impede medir quais setores crescem e acompanhar contratações recentes, e não inclui a administração pública, onde estão os institutos públicos de pesquisa da cidade. Até a Feira de Soluções, espera-se republicar o painel com a versão final, apresentar o trabalho ao cliente e registrar suas decisões sobre a série histórica da RAIS e a tabela oficial de bairros por região.

## Referências

BALLOU, Ronald H. Gerenciamento da cadeia de suprimentos/logística empresarial. 5. ed. Porto Alegre: Bookman, 2006.

DE NEGRI, João Alberto; CASTRO, Paulo Furtado de; SOUZA, Natalia Ribeiro de; ARBACHE, Jorge Saba. Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD. Texto para Discussão nº 840. Brasília: IPEA, 2001. Disponível em: \<https://repositorio.ipea.gov.br/handle/11058/2155\>. Acesso em: 14 set. 2026.

GALINDO-RUEDA, Fernando; VERGER, Fabien. OECD taxonomy of economic activities based on R&D intensity. Paris: OECD Publishing, 2016. (OECD Science, Technology and Industry Working Papers, n. 2016/04).

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Cadastro Nacional de Endereços para Fins Estatísticos – CNEFE: Censo Demográfico 2022. Rio de Janeiro: IBGE, \[s.d.\]. Disponível em: \<https://ftp.ibge.gov.br/Cadastro_Nacional_de_Enderecos_para_Fins_Estatisticos/Censo_Demografico_2022/\>. Acesso em: 17 out. 2026.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Classificação Nacional de Atividades Econômicas – CNAE Subclasses 2.3: estrutura detalhada. Rio de Janeiro: IBGE/CONCLA, \[s.d.\]. Disponível em: \<https://concla.ibge.gov.br\>. Acesso em: 26 out. 2026.

MORELLI, André Borgato; FIEDLER, André de Carvalho; CUNHA, André Luiz. Um banco de dados de empregos formais georreferenciados em cidades brasileiras. arXiv:2303.09602, 2023. Disponível em: \<https://arxiv.org/pdf/2303.09602\>. Acesso em: 14 set. 2026.

SÃO JOSÉ DOS CAMPOS (Município). Plano Diretor: estudo técnico — Regiões Urbanas. São José dos Campos: Prefeitura Municipal, \[2018\]. Disponível em: \<https://www.sjc.sp.gov.br/media/1ascp0it/7_regioes_urbanas.pdf\>. Acesso em: 26 out. 2026.

SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RIO GRANDE DO SUL (SICT). Observatório da Inovação RS. Porto Alegre, 2025. Disponível em: \<https://sict.rs.gov.br/observatorio\>. Acesso em: 14 set. 2026.

SILVA, Valdenice Portela; LIMA, Marcus Eugênio Oliveira. Microdados RAIS e estudos sobre o mercado de trabalho no Brasil. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. Disponível em: \<https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244\>. Acesso em: 14 set. 2026.
