> Versão em Markdown de [`Relatorio_Sprint2_Anexo8.docx`](Relatorio_Sprint2_Anexo8.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

**FATEC SÃO JOSÉ DOS CAMPOS**

**API — Aprendizagem por Projetos Integrados · Curso de Logística**

# Relatório de Desenvolvimento — Sprint 2

**Observatório do Ecossistema Industrial e de Serviços de São José dos Campos**

**Entrega da Sprint 2: 26/10/2026**

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

Na segunda sprint, o painel recebeu as análises centrais: setores de atividade pela CNAE, porte e situação dos estabelecimentos e o cruzamento entre emprego formal e valor adicionado por setor. A base de 47.339 estabelecimentos foi geocodificada a partir do CEP e classificada pelas regiões oficiais do município, alcançando 99,99% dos estabelecimentos com região e 78% com ponto no mapa, e foi validada pela CNAE 2.3. Os resultados indicam que a indústria responde por 24,7% do emprego formal privado e por 45,8% do valor adicionado privado, e que as atividades de alta e média-alta tecnologia reúnem cerca de 14% do emprego formal. As novas decisões de tratamento foram registradas no Log de Decisões de Dados (DEC-006 a DEC-022).

**Palavras-Chave: Observatório Econômico; RAIS; Geocodificação; Business Intelligence; Desenvolvimento Regional.**

## Abstract

This project develops the Observatory of the Industrial and Services Ecosystem of São José dos Campos, a data intelligence tool built in partnership with CADI and the city's Secretariat of Economic Development. The project aims to consolidate, treat, and make available public indicators on the city's industrial and services establishments, using as data sources the Annual Social Information Report (RAIS) from the Brazilian Ministry of Labor and Employment and the Municipal Gross Domestic Product from the Brazilian Institute of Geography and Statistics (IBGE). The methodology adopts an Extract, Transform, Load (ETL) process executed in Python within Google Colab, followed by data modeling and visualization in Microsoft Power BI, under the Scrum agile methodology organized into 3 sprints.

In the second sprint, the dashboard received its core analyses: economic sectors by CNAE, establishment size and status, and the comparison between formal employment and value added by sector. The base of 47,339 establishments was geocoded from postal codes (CEP) and classified by the city's official regions, reaching 99.99% of establishments with a region and 78% with a map point, and was validated against CNAE 2.3. The results show that manufacturing accounts for 24.7% of private formal employment and 45.8% of private value added, and that high and medium-high technology activities concentrate about 14% of formal employment. New data treatment decisions were recorded in the Data Decision Log (DEC-006 to DEC-022).

***Keywords: Economic Observatory; RAIS; Geocoding; Business Intelligence; Regional Development.***

## 1. Contextualização do projeto

São José dos Campos ocupa posição de destaque no Vale do Paraíba como polo industrial, tecnológico e de serviços, concentrando um número expressivo de estabelecimentos formais nos setores aeroespacial, automotivo e de tecnologia da informação. Apesar dessa relevância econômica, o município carece de uma ferramenta pública e centralizada que consolide indicadores sobre o seu ecossistema produtivo, dificultando o acompanhamento de políticas de desenvolvimento econômico local.

Esse cenário motivou o CADI e a Secretaria de Desenvolvimento Econômico de São José dos Campos a propor, em parceria com a Fatec São José dos Campos, o desenvolvimento de um observatório de dados nos moldes do Observatório da Inovação RS, iniciativa do governo do Rio Grande do Sul que reúne, em um painel público construído em Microsoft Power BI, indicadores sobre o ecossistema de inovação, ciência e tecnologia gaúcho (SICT, 2025). Adaptando essa referência para a realidade de São José dos Campos, o projeto se propõe a mapear o ecossistema industrial e de serviços do município a partir de bases de dados públicas, entregando um painel equivalente que sirva de apoio à tomada de decisão do poder público local.

## 2. Objetivos do projeto

Os objetivos estabelecidos para esse projeto consistem em:

- Desenvolver um pipeline de extração, tratamento e carga (ETL) em Python, no ambiente Google Colab, capaz de filtrar e tratar os dados públicos da RAIS especificamente para o município de São José dos Campos;

- Identificar e documentar formalmente as inconsistências estruturais presentes na base de dados bruta, de modo a garantir a confiabilidade dos indicadores gerados;

- Construir um painel interativo em Microsoft Power BI que reúna indicadores de emprego, natureza dos estabelecimentos e distribuição geográfica do ecossistema industrial e de serviços do município;

- Integrar os dados do Produto Interno Bruto dos Municípios (IBGE) ao painel, comparando a participação de cada setor no emprego e no valor adicionado do município;

- Representar a distribuição geográfica dos estabelecimentos por bairro e pelas regiões oficiais de São José dos Campos.

## 3. Fundamentação dos métodos analíticos e das tecnologias utilizadas

### 3.1 Métodos analíticos utilizados

O desenvolvimento do observatório se apoia primordialmente em métodos de estatística descritiva e em técnicas de tratamento e segmentação de microdados administrativos, aplicados sobre a base da RAIS. A literatura brasileira que utiliza microdados da RAIS para estudos de mercado de trabalho reforça a robustez dessa fonte, ao mesmo tempo em que aponta a necessidade de tratamento cuidadoso de suas particularidades antes de qualquer análise (Silva; Lima, 2018; De Negri et al., 2001). Para o desafio específico do mapeamento geográfico dos estabelecimentos — que não possuem coordenadas diretas na base pública, o projeto adota a técnica de geocodificação a partir do campo de CEP, seguindo abordagem já validada na literatura de geolocalização de empregos formais em cidades brasileiras (Morelli; Fiedler; Cunha, 2023).

Na segunda sprint, os estabelecimentos foram classificados por regras fixas a partir da CNAE: as seções foram agrupadas nos tipos de atividade citados pelo cliente (manufatura, tecnologia, logística, serviços especializados e outros), e as divisões foram ordenadas pela taxonomia de intensidade de pesquisa e desenvolvimento da OCDE (GALINDO-RUEDA; VERGER, 2016). Os códigos e descrições foram validados pela estrutura oficial da CNAE 2.3 (IBGE, \[s.d.\]), e a região de cada estabelecimento foi atribuída pelo bairro, segundo a lista de bairros por região do Plano Diretor do município (SÃO JOSÉ DOS CAMPOS, \[2018\]), com conferência pelo setor do CEP.

A Tabela 1 a seguir apresenta a lista de referências que auxiliam no entendimento dos métodos analíticos utilizados nesse projeto.

**Tabela 1 — Tabela de referências**

| **Autor(es)**                  | **Métodos de análise**                                         | **Dados utilizados**                                             | **Principais conclusões**                                                                                                                                             |
|--------------------------------|----------------------------------------------------------------|------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Silva; Lima (2018)             | Revisão integrativa de estudos com microdados RAIS             | 10 artigos analisados, publicados entre 2006 e 2015              | A RAIS é um instrumento relevante de análise do mercado de trabalho formal, mesmo sendo pouco explorada, contribuindo para políticas públicas de emprego.             |
| De Negri et al. (2001)         | Análise estatística comparativa entre bases administrativas    | Microdados RAIS e PNAD                                           | As duas bases convergem em variáveis como idade e gênero, mas apresentam diferenças relevantes no conceito de rendimento.                                             |
| Morelli; Fiedler; Cunha (2023) | Geocodificação por CEP combinada com faces de logradouro       | Base RAIS + CNEFE (IBGE)                                         | É possível localizar geograficamente empregos formais a partir do CEP com boa precisão em cidades médias e grandes, e de forma aproximada em municípios de CEP único. |
| Galindo-Rueda; Verger (2016)   | Classificação de atividades econômicas pela intensidade de P&D | Gastos em P&D e valor adicionado por atividade em países da OCDE | As atividades podem ser agrupadas em níveis de intensidade tecnológica (de alta a baixa), aplicáveis à indústria e aos serviços.                                      |

### 3.2 Tecnologias da Informação

O projeto utiliza três tecnologias principais, definidas em conjunto com o professor orientador. O Google Colab, executando Python 3, foi escolhido para a etapa de ETL por permitir o processamento do arquivo bruto da RAIS com mais de 12,6 milhões de registros nacionais e cerca de 3,27 GB descompactados em ambiente gratuito e colaborativo, sem necessidade de infraestrutura local. A biblioteca padrão csv foi utilizada em modo de leitura sequencial (streaming), evitando o carregamento integral do arquivo em memória.

O GitHub foi adotado como repositório central de versionamento (usuário projetoapi08, projeto observatorio-sjc), organizado em pastas docs/ (documentação do projeto: Visão e Escopo, Backlogs, Log de Decisões de Dados, relatórios técnicos), notebooks/ (notebooks de ETL produzidos no Google Colab), dados/ (bases tratadas, incluindo a base única para o Power BI), powerbi/ (arquivos do painel), MVP/ e evidencias/. Por fim, o Microsoft Power BI foi definido como ferramenta de visualização final, por ser a mesma tecnologia empregada no painel do Observatório da Inovação RS, referência direta do projeto (SICT, 2025).

Na segunda sprint, as principais dificuldades foram de qualidade de dados: o arquivo de CEPs geocodificados teve as coordenadas corrompidas ao ser salvo no Excel em português (o ponto decimal virou separador de milhar), alguns bairros foram localizados em homônimos de outra parte da cidade, e a lista oficial de bairros da Região Norte não está disponível no documento do Plano Diretor.

## 4. Coleta e descrição dos dados utilizados

Os dados da segunda sprint partiram da base de 47.339 estabelecimentos de São José dos Campos (RAIS 2024) e incorporaram três novas fontes: a série do PIB dos Municípios do IBGE (PIB de 2002 a 2023 e valor adicionado por setor até 2021), a estrutura oficial da CNAE 2.3 e a lista de bairros por região do Plano Diretor. Os 3.677 CEPs da base foram geocodificados no nível de bairro, e o resultado foi reunido numa base única para o Power BI, com 46 colunas.

O orientador pediu, na avaliação da Sprint 1, que se esclarecesse se os 64,37% de RAIS negativa poderiam ser erro de filtragem. A verificação mostrou que não: o extrato contém apenas o município 354990, e 13.604 desses estabelecimentos declararam atividade no ano, ou seja, funcionavam sem empregados formais.

As novas decisões de tratamento foram registradas no Log de Decisões de Dados:

DEC-006/009 e DEC-013 — o valor adicionado por setor de 2021 é comparado com o emprego de 2024, último ano com detalhe setorial do IBGE, sem a administração pública, que não está na base RAIS do extrato;

DEC-008 e DEC-014 — valores do PIB corrigidos pelo IPCA para reais de 2023 e setores classificados pela Seção CNAE 2.0, padrão do IBGE;

DEC-011 e DEC-019 — os 53 registros com indicador de RAIS negativa igual a 2 ficam no grupo sem vínculo, e uma situação detalhada separa os 1.758 estabelecimentos que fecharam o ano sem empregados;

DEC-015 a DEC-018 — região oficial atribuída pelo bairro (99,99% da base), coordenadas corrompidas substituídas, pontos em bairros homônimos marcados e CEPs de avenida mantidos sem ponto no mapa;

DEC-020 a DEC-022 — descrições da CNAE 2.3 oficiais, classificações derivadas (tipo de atividade, intensidade tecnológica, porte e setor destaque) e base única para o Power BI com mapa por coordenadas.

## 5. Resultados obtidos e esperados

Ao fim da segunda sprint, o painel apresenta os indicadores gerais da base, os setores de atividade, o porte e a situação dos estabelecimentos e o cruzamento entre emprego e valor adicionado. Os dados mostram que a indústria gera 45,8% do valor adicionado privado com 24,7% do emprego privado (índice de produtividade relativa de 1,86), que a indústria de transformação se concentra nas regiões Leste, Sudeste e Sul, e que o comércio e os serviços predominam no Centro e no Oeste. Para a terceira sprint, espera-se concluir o mapa por coordenadas, tornar oficial a classificação da Região Norte com dados da Prefeitura, definir com o cliente a fonte para a evolução dos setores e consolidar o painel, o relatório final e a apresentação na Feira de Soluções.

## Referências

DE NEGRI, João Alberto; CASTRO, Paulo Furtado de; SOUZA, Natalia Ribeiro de; ARBACHE, Jorge Saba. Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD. Texto para Discussão nº 840. Brasília: IPEA, 2001. Disponível em: \<https://repositorio.ipea.gov.br/handle/11058/2155\>. Acesso em: 14 set. 2026.

GALINDO-RUEDA, Fernando; VERGER, Fabien. OECD taxonomy of economic activities based on R&D intensity. Paris: OECD Publishing, 2016. (OECD Science, Technology and Industry Working Papers, n. 2016/04).

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Classificação Nacional de Atividades Econômicas – CNAE Subclasses 2.3: estrutura detalhada. Rio de Janeiro: IBGE/CONCLA, \[s.d.\]. Disponível em: \<https://concla.ibge.gov.br\>. Acesso em: 26 out. 2026.

MORELLI, André Borgato; FIEDLER, André de Carvalho; CUNHA, André Luiz. Um banco de dados de empregos formais georreferenciados em cidades brasileiras. arXiv:2303.09602, 2023. Disponível em: \<https://arxiv.org/pdf/2303.09602\>. Acesso em: 14 set. 2026.

SÃO JOSÉ DOS CAMPOS (Município). Plano Diretor: estudo técnico — Regiões Urbanas. São José dos Campos: Prefeitura Municipal, \[2018\]. Disponível em: \<https://www.sjc.sp.gov.br/media/1ascp0it/7_regioes_urbanas.pdf\>. Acesso em: 26 out. 2026.

SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RIO GRANDE DO SUL (SICT). Observatório da Inovação RS. Porto Alegre, 2025. Disponível em: \<https://sict.rs.gov.br/observatorio\>. Acesso em: 14 set. 2026.

SILVA, Valdenice Portela; LIMA, Marcus Eugênio Oliveira. Microdados RAIS e estudos sobre o mercado de trabalho no Brasil. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. Disponível em: \<https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244\>. Acesso em: 14 set. 2026.
