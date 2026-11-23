> Versão em Markdown de [`Relatorio_Sprint1_Anexo8.docx`](Relatorio_Sprint1_Anexo8.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

**FATEC SÃO JOSÉ DOS CAMPOS**

**API — Aprendizagem por Projetos Integrados · Curso de Logística**

# Relatório de Desenvolvimento — Sprint 1

**Observatório do Ecossistema Industrial e de Serviços de São José dos Campos**

**Entrega da Sprint 1: 28/09/2026**

**Autor 1 (LinkedIn):** Beatriz Oliveira Sepulvida — <https://www.linkedin.com/in/beatriz-sepulvida>

**Autor 2 (LinkedIn):** Caio Moreira — <https://www.linkedin.com/in/caiomoreiradearaujo>

**Autor 3 (LinkedIn):** Hemilly Christiny da Silva Freitas — <https://www.linkedin.com/in/hemilly-freitas-31a509269>

**Autor 4 (LinkedIn):** João Pedro Faria Vital de Souza — <https://www.linkedin.com/in/joao-pedro-a2b6122b7>

**Autor 5 (LinkedIn):** Juliano Souza Santana – <https://www.linkedin.com/in/juliano-santana-776992249>

**Autor 6 (LinkedIn):** Milena Silva Nogueira - <https://www.linkedin.com/in/milenasnogueira>

**Autor 7 (LinkedIn):** Pedro Henrique Oliveira de Carvalho - <https://www.linkedin.com/in/pedro-henrique-oliveira-de-carvalho-75bb07427>

**Autor 8 (LinkedIn):** Thalya Awany Berti - <https://www.linkedin.com/in/thalya-awany-berti-773923266>

**Professor M2 (Orientador):** José Jaétis

**Professor P2:** Marcus Nascimento

## Resumo do projeto

O presente projeto desenvolve o Observatório do Ecossistema Industrial e de Serviços de São José dos Campos, uma ferramenta de inteligência de dados construída em parceria com o CADI e a Secretaria de Desenvolvimento Econômico do município. O projeto tem como objetivo consolidar, tratar e disponibilizar indicadores públicos sobre os estabelecimentos industriais e de serviços da cidade, utilizando como fontes de dados a Relação Anual de Informações Sociais (RAIS) do Ministério do Trabalho e Emprego e o Produto Interno Bruto dos Municípios do Instituto Brasileiro de Geografia e Estatística (IBGE). A metodologia adota o processo de Extração, Transformação e Carga (ETL) executado em linguagem Python no ambiente Google Colab, seguido da modelagem e visualização dos dados na ferramenta Microsoft Power BI. O desenvolvimento segue a metodologia ágil Scrum, organizado em 3 sprints com backlogs, critérios de Definição de Preparado (DoR) e Definição de Pronto (DoD) devidamente documentados.

Na primeira sprint, o projeto passou por um pivô de escopo, migrando de um relatório voltado à contratação de mão de obra para um observatório abrangente do ecossistema municipal, inspirado no modelo do Observatório da Inovação RS. Como resultado da etapa de tratamento de dados, identificaram-se quatro inconsistências estruturais na base RAIS bruta: a ausência de campo de ano de referência, a ausência de identificação nominal dos estabelecimentos, a alta proporção de estabelecimentos sem vínculos empregatícios ativos e a mistura de diferentes naturezas de estabelecimento em um mesmo arquivo, além de uma quinta decisão decorrente da confirmação do ano-base junto ao cliente; todas as cinco registradas formalmente em um Log de Decisões de Dados (DEC-001 a DEC-005). Espera-se, ao final do projeto, entregar um painel interativo que apoie a tomada de decisão pública sobre o desenvolvimento econômico de São José dos Campos.

**Palavras-Chave:** Observatório Econômico; RAIS; Indicadores Municipais; Business Intelligence; Extração, Transformação e Carga (ETL).

## Abstract

*This project develops the Observatory of the Industrial and Services Ecosystem of São José dos Campos, a data intelligence tool built in partnership with CADI and the city's Secretariat of Economic Development. The project aims to consolidate, treat, and make available public indicators on the city's industrial and services establishments, using as data sources the Annual Social Information Report (RAIS) from the Brazilian Ministry of Labor and Employment and the Municipal Gross Domestic Product from the Brazilian Institute of Geography and Statistics (IBGE). The methodology adopts an Extract, Transform, Load (ETL) process executed in Python within the Google Colab environment, followed by data modeling and visualization in Microsoft Power BI. Development follows the Scrum agile methodology, organized into 3 sprints with documented backlogs, Definition of Ready (DoR), and Definition of Done (DoD) criteria.*

*During the first sprint, the project underwent a scope pivot, shifting from a hiring-focused report to a comprehensive observatory of the municipal ecosystem, inspired by the Observatório da Inovação RS model. As a result of the data treatment stage, four structural inconsistencies were identified in the raw RAIS database: the absence of a reference-year field, the absence of establishment-level identification, a high proportion of establishments with no active employment links, and the mixing of different establishment types in a single file, plus a fifth decision arising from the confirmation of the reference year with the client; all five formally recorded in a Data Decision Log (DEC-001 to DEC-005). By the end of the project, an interactive dashboard is expected to be delivered to support public decision-making on the economic development of São José dos Campos.*

***Keywords:** Economic Observatory; RAIS; Municipal Indicators; Business Intelligence; Extract, Transform, Load (ETL).*

## 1. Contextualização do projeto

São José dos Campos ocupa posição de destaque no Vale do Paraíba como polo industrial, tecnológico e de serviços, concentrando um número expressivo de estabelecimentos formais nos setores aeroespacial, automotivo e de tecnologia da informação. Apesar dessa relevância econômica, o município carece de uma ferramenta pública e centralizada que consolide indicadores sobre o seu ecossistema produtivo, dificultando o acompanhamento de políticas de desenvolvimento econômico local.

Esse cenário motivou o CADI e a Secretaria de Desenvolvimento Econômico de São José dos Campos a propor, em parceria com a Fatec São José dos Campos, o desenvolvimento de um observatório de dados nos moldes do Observatório da Inovação RS, iniciativa do governo do Rio Grande do Sul que reúne, em um painel público construído em Microsoft Power BI, indicadores sobre o ecossistema de inovação, ciência e tecnologia gaúcho (SICT, 2025). Adaptando essa referência para a realidade de São José dos Campos, o projeto se propõe a mapear o ecossistema industrial e de serviços do município a partir de bases de dados públicas, entregando um painel equivalente que sirva de apoio à tomada de decisão do poder público local.

## 2. Objetivos do projeto

Os objetivos estabelecidos para esse projeto consistem em:

- Desenvolver um pipeline de extração, tratamento e carga (ETL) em Python, no ambiente Google Colab, capaz de filtrar e tratar os dados públicos da RAIS especificamente para o município de São José dos Campos;

- Identificar e documentar formalmente as inconsistências estruturais presentes na base de dados bruta, de modo a garantir a confiabilidade dos indicadores gerados;

- Construir um painel interativo em Microsoft Power BI que reúna indicadores de emprego, natureza dos estabelecimentos e distribuição geográfica do ecossistema industrial e de serviços do município;

- Integrar, em etapa futura, os dados do Produto Interno Bruto dos Municípios (IBGE) como segunda fonte de dados do observatório.

## 3. Fundamentação dos métodos analíticos e das tecnologias utilizadas

### 3.1 Métodos analíticos utilizados

O desenvolvimento do observatório se apoia primordialmente em métodos de estatística descritiva e em técnicas de tratamento e segmentação de microdados administrativos, aplicados sobre a base da RAIS. A literatura brasileira que utiliza microdados da RAIS para estudos de mercado de trabalho reforça a robustez dessa fonte, ao mesmo tempo em que aponta a necessidade de tratamento cuidadoso de suas particularidades antes de qualquer análise (Silva; Lima, 2018; De Negri et al., 2001). Para o desafio específico do mapeamento geográfico dos estabelecimentos — que não possuem coordenadas diretas na base pública, o projeto adota a técnica de geocodificação a partir do campo de CEP, seguindo abordagem já validada na literatura de geolocalização de empregos formais em cidades brasileiras (Morelli; Fiedler; Cunha, 2023).

A Tabela 1 a seguir apresenta a lista de referências que auxiliam no entendimento dos métodos analíticos utilizados nesse projeto.

**Tabela 1 — Tabela de referências**

| **Autor(es)**                      | **Métodos de análise**                                      | **Dados utilizados**                                | **Principais conclusões**                                                                                                                                             |
|------------------------------------|-------------------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Silva; Lima (2018)**             | Revisão integrativa de estudos com microdados RAIS          | 10 artigos analisados, publicados entre 2006 e 2015 | A RAIS é um instrumento relevante de análise do mercado de trabalho formal, mesmo sendo pouco explorada, contribuindo para políticas públicas de emprego.             |
| **De Negri et al. (2001)**         | Análise estatística comparativa entre bases administrativas | Microdados RAIS e PNAD                              | As duas bases convergem em variáveis como idade e gênero, mas apresentam diferenças relevantes no conceito de rendimento.                                             |
| **Morelli; Fiedler; Cunha (2023)** | Geocodificação por CEP combinada com faces de logradouro    | Base RAIS + CNEFE (IBGE)                            | É possível localizar geograficamente empregos formais a partir do CEP com boa precisão em cidades médias e grandes, e de forma aproximada em municípios de CEP único. |

### 3.2 Tecnologias da Informação

O projeto utiliza três tecnologias principais, definidas em conjunto com o professor orientador. O Google Colab, executando Python 3, foi escolhido para a etapa de ETL por permitir o processamento do arquivo bruto da RAIS com mais de 12,6 milhões de registros nacionais e cerca de 3,27 GB descompactados em ambiente gratuito e colaborativo, sem necessidade de infraestrutura local. A biblioteca padrão csv foi utilizada em modo de leitura sequencial (streaming), evitando o carregamento integral do arquivo em memória.

O GitHub foi adotado como repositório central de versionamento (usuário projetoapi08, projeto observatorio-sjc), organizado em pastas docs/ (documentação do projeto: Visão e Escopo, Backlogs, Log de Decisões de Dados), notebooks/ (notebooks de ETL produzidos no Google Colab) e powerbi/ (arquivos do painel). Por fim, o Microsoft Power BI foi definido como ferramenta de visualização final, por ser a mesma tecnologia empregada no painel do Observatório da Inovação RS, referência direta do projeto (SICT, 2025), o que facilita a comparação de resultados e a adoção de boas práticas já validadas nesse benchmark.

A principal dificuldade enfrentada até o momento foi o volume do arquivo bruto da RAIS, que inviabiliza sua abertura direta em ferramentas como Excel, sem tratamento prévio, exigindo leitura em streaming linha a linha.

## 4. Coleta e descrição dos dados utilizados

Os dados utilizados nesta primeira sprint foram extraídos do arquivo público RAIS_ESTAB_PUB, disponibilizado pelo Ministério do Trabalho e Emprego, contendo o total de 12.643.067 registros de estabelecimentos em todo o território nacional. O tratamento consistiu em um processo de ETL que filtrou exclusivamente os registros do município de São José dos Campos, identificado pelo código IBGE 354990, resultando em uma base de 47.339 estabelecimentos.

Durante o tratamento dos dados, foram identificadas e documentadas quatro inconsistências estruturais na base bruta, além de uma quinta decisão decorrente da confirmação do ano-base, registradas formalmente no Log de Decisões de Dados do projeto (DEC-001 a DEC-005):

**DEC-001 —** 30.470 estabelecimentos (64,37% do total) apresentam RAIS negativa, ou seja, não possuem vínculos empregatícios ativos. O cliente esclareceu que esse dado não deve ser tratado como um erro a ser descartado, podendo refletir uma característica real do tecido econômico do município; por essa razão, a equipe decidiu manter esses registros na base, sinalizados por um indicador próprio, e exibir esse percentual como métrica separada do painel; as análises de contratação usam por padrão os 16.869 estabelecimentos com vínculo ativo.

**DEC-002 —** a base mistura três naturezas distintas de estabelecimento (CNPJ, CAEPF e CNO), o que exigiu a segmentação dos dados em subconjuntos antes de qualquer agregação, resultando em 46.244 registros do tipo CNPJ, 708 do tipo CAEPF e 387 do tipo CNO. O recorte padrão do projeto adota os registros do tipo CNPJ.

**DEC-003 —** o arquivo bruto não possui nenhum campo indicando o ano ou a competência de referência dos dados; o cliente confirmou o ano-base 2024 para o extrato utilizado.

**DEC-004 —** a base pública não disponibiliza razão social, CNPJ ou CPF dos estabelecimentos, o que impede análises que dependam da identificação nominal; decisão em aberto, a equipe aguarda posicionamento do cliente sobre a eventual disponibilização de uma base identificada, mediante acordo de uso de dados. Como contingência, caso a base identificada não seja disponibilizada, o painel apresentará os indicadores agregados por setor e por região, sem identificação nominal dos estabelecimentos.

**DEC-005 —** com o ano-base confirmado, verificou-se que o PIB dos Municípios (IBGE) mais recente publicado é a série 2022–2023; o cruzamento com a RAIS 2024 adota o PIB 2023, com a defasagem de 1 ano documentada como limitação metodológica.

O campo de CEP do estabelecimento, presente na base, foi identificado como o caminho viável para a próxima etapa do projeto: o mapeamento geográfico dos estabelecimentos via geocodificação, conforme metodologia descrita na Seção 3.1.

## 5. Resultados esperados

Ao final do projeto, espera-se entregar um painel interativo em Power BI, hospedado nos moldes do Observatório da Inovação RS, que disponibilize ao CADI e à Secretaria de Desenvolvimento Econômico de São José dos Campos indicadores atualizados e confiáveis sobre o ecossistema industrial e de serviços do município, incluindo distribuição geográfica dos estabelecimentos, segmentação por natureza jurídica e indicadores de vínculos empregatícios. Como contribuição técnica, o projeto entrega um pipeline de ETL documentado e reprodutível, capaz de ser reaplicado a versões futuras da base RAIS, além de um Log de Decisões de Dados que registra formalmente as inconsistências identificadas e os critérios adotados para tratá-las. Como contribuição acadêmica, o trabalho reforça, para a área de Logística, a importância do tratamento crítico de dados públicos administrativos como insumo para políticas de desenvolvimento econômico municipal.

## Referências

DE NEGRI, João Alberto; CASTRO, Paulo Furtado de; SOUZA, Natalia Ribeiro de; ARBACHE, Jorge Saba. Mercado formal de trabalho: comparação entre os microdados da RAIS e da PNAD. Texto para Discussão nº 840. Brasília: IPEA, 2001. Disponível em: \<https://repositorio.ipea.gov.br/handle/11058/2155\>. Acesso em: 14 set. 2026.

MORELLI, André Borgato; FIEDLER, André de Carvalho; CUNHA, André Luiz. Um banco de dados de empregos formais georreferenciados em cidades brasileiras. arXiv:2303.09602, 2023. Disponível em: \<https://arxiv.org/pdf/2303.09602\>. Acesso em: 14 set. 2026.

SECRETARIA DE INOVAÇÃO, CIÊNCIA E TECNOLOGIA DO RIO GRANDE DO SUL (SICT). Observatório da Inovação RS. Porto Alegre, 2025. Disponível em: \<https://sict.rs.gov.br/observatorio\>. Acesso em: 14 set. 2026.

SILVA, Valdenice Portela; LIMA, Marcus Eugênio Oliveira. Microdados RAIS e estudos sobre o mercado de trabalho no Brasil. Revista de Políticas Públicas, São Luís, v. 22, n. 1, p. 523-544, 2018. Disponível em: \<https://periodicoseletronicos.ufma.br/index.php/rppublica/article/view/9244\>. Acesso em: 14 set. 2026.
