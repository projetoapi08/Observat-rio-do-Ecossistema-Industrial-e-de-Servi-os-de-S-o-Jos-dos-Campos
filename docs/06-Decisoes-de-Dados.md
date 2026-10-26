> Versão em Markdown de `docs/06-Decisoes-de-Dados.docx`, para leitura direta no GitHub. Em caso de diferença, vale o .docx.

# Log de Decisões de Dados

## 1. Contexto

Durante a exploração dos dados brutos da RAIS filtrados para São José dos Campos, foram identificados problemas estruturais que exigiam uma decisão explícita antes de seguir com a modelagem. Este documento registra o problema, a decisão adotada, a justificativa e o impacto de cada um, atendendo ao critério de aceite da User Story US03 (“tratar as inconsistências dos dados da RAIS”). Técnica inspirada em ADR (Architecture Decision Record), adaptada para decisões sobre tratamento de dados: toda nova decisão ganha uma entrada DEC-00X nova; não se edita o histórico de uma decisão já tomada — se a decisão mudar, registra-se uma nova entrada referenciando a anterior.

## 2. Decisões

### DEC-001 — Estabelecimentos com vínculos ativos zerados (RAIS negativa)

| Campo | Descrição |
|---|---|
| Problema identificado | 30.470 dos 47.339 estabelecimentos do extrato de SJC (64,37%) apresentam Qtd Vínculos Ativos = 0 — declaração de “RAIS negativa”: o estabelecimento existe formalmente, mas não tinha nenhum vínculo empregatício ativo no ano de referência. |
| Decisão adotada | Os estabelecimentos com vínculos zerados permanecem na base (não são excluídos) e recebem um indicador próprio “possui_vinculo_ativo”. As visualizações de contratação e ranking de empregadores (US07, US08) usam por padrão apenas os 16.869 estabelecimentos com vínculo ativo; o total de estabelecimentos cadastrados é exibido à parte, como indicador de densidade empresarial do município. |
| Justificativa | Em orientação enviada por áudio ao Product Owner, o cliente esclareceu que a alta proporção de RAIS negativa não deve ser tratada como erro a ser descartado — pode refletir uma característica real da economia do município. A orientação foi reportar essa métrica como indicador próprio do dashboard, em vez de simplesmente excluí-la das análises de emprego. |
| Impacto | A base de análise de contratações usa por padrão 16.869 estabelecimentos ativos (dos 47.339 totais); o percentual de RAIS negativa (64,37%) é exibido como indicador próprio, não como dado descartado. |
| User Stories impactadas | US07, US08 |
| Status | Fechada — confirmada pelo cliente |

### DEC-002 — Mistura de tipos de estabelecimento (CNPJ, CAEPF, CNO)

| Campo | Descrição |
|---|---|
| Problema identificado | A coluna Tipo Estab mistura três naturezas diferentes de registro: CNPJ — pessoa jurídica (46.244 linhas), CAEPF — produtor rural/profissional autônomo pessoa física (708) e CNO — obra de construção civil (387). |
| Decisão adotada | Foi criado o campo categórico “tipo_estabelecimento”. O recorte padrão do dashboard usa apenas registros do tipo CNPJ, alinhado ao escopo de “ecossistema industrial e de serviços”; CAEPF e CNO ficam disponíveis como filtro opcional, fora do recorte padrão. |
| Justificativa | O requisito do cliente pede mapeamento de “empresas” — CAEPF (pessoa física autônoma) e CNO (obra temporária) não representam empresas no sentido solicitado. Sem essa separação, comparações entre setores e rankings misturariam naturezas jurídicas distintas, invalidando as comparações. |
| Impacto | Exclusão de 1.095 registros (708 + 387) do recorte principal — impacto pequeno no total, mas evita erro conceitual na apresentação. |
| User Stories impactadas | US02, US07, US08 |
| Status | Fechada — critério assumido pela equipe; validar formalmente com o cliente se possível |

### DEC-003 — Ano-base de referência da RAIS

| Campo | Descrição |
|---|---|
| Problema identificado | O arquivo fornecido (RAIS_ESTAB_PUB) não contém uma coluna explícita indicando o ano-base da declaração RAIS. |
| Decisão adotada | Adotar RAIS ano-base 2024 em todas as análises e visualizações do painel, com a informação indicada explicitamente em todo gráfico ou relatório publicado. |
| Justificativa | O cliente (CADI / Secretaria de Desenvolvimento Econômico) confirmou o ano-base 2024. O ano de referência é essencial para cruzar com o PIB dos Municípios (IBGE) no mesmo período (US09) e para qualquer comparação temporal futura. |
| Impacto | Desbloqueia a US09 (impacto no PIB) e fecha a pendência mais crítica do checklist de erros. Toda visualização temporal do painel deve indicar “RAIS 2024”. |
| User Stories impactadas | US08, US09, US10 |
| Status | Fechada — confirmada pelo cliente |

### DEC-004 — Ausência de identificação nominal (nome/CNPJ) nos dados públicos

| Campo | Descrição |
|---|---|
| Problema identificado | Os microdados públicos da RAIS não trazem nome ou CNPJ das empresas, apenas atributos agregados por estabelecimento (CNAE, porte, natureza jurídica, CEP). |
| Decisão adotada | Não tentar inferir/“adivinhar” nomes de empresa a partir de CNAE + porte. O ranking de “empresas que mais contratam” (US07) é apresentado de forma agregada — por setor (CNAE) e por região — em vez de por razão social, salvo se o cliente confirmar o fornecimento de uma base identificada. |
| Justificativa | Dados identificados da RAIS são sigilosos por lei (acesso restrito a órgãos públicos autorizados); usar a RAIS pública para supor identidade de empresas seria metodologicamente incorreto e não verificável/auditável. |
| Impacto | A camada de “nome de empresa” no produto final depende de fonte externa curada (ou de eventual base identificada do cliente), não da RAIS pública. |
| User Stories impactadas | US07 |
| Status | Aberta — aguardando resposta do cliente sobre eventual base identificada |

### DEC-005 — Defasagem entre RAIS (2024) e PIB dos Municípios/IBGE (2022–2023)

| Campo | Descrição |
|---|---|
| Problema identificado | Com o ano-base da RAIS confirmado em 2024 (DEC-003), verificou-se que o PIB dos Municípios (IBGE) mais recente disponível é a série 2022–2023 — não existe PIB 2024 publicado; a próxima divulgação está prevista apenas para o fim de 2026/2027. |
| Decisão adotada | Para a US09 (impacto no PIB), cruzar RAIS 2024 com o PIB municipal 2023 — o ano mais recente disponível — documentando explicitamente, no dashboard e no relatório técnico, a defasagem de 1 ano entre as duas fontes. |
| Justificativa | O prazo do projeto (1 semestre letivo, 3 sprints) não comporta aguardar a divulgação do PIB 2024 pelo IBGE. Cruzar com o dado mais recente disponível, com a defasagem declarada como limitação metodológica, é prática padrão em estudos municipais que combinam RAIS e Contas Nacionais. |
| Impacto | Todo gráfico que cruzar RAIS x PIB deve indicar os anos de cada fonte (RAIS 2024 / PIB 2023) para evitar leitura equivocada. |
| User Stories impactadas | US09 |
| Status | Fechada |

Decisões numeradas pela equipe durante a Sprint 2 sem registro neste log (DEC-007, DEC-010 e DEC-012): conteúdo não localizado nos arquivos do projeto — completar a partir do registro original da equipe. As DEC-006, 008, 009, 011, 013 e 014 abaixo foram transcritas das Notas Metodológicas do painel Power BI.

## 2.1 Decisões registradas na Sprint 2

### DEC-006 e DEC-009 — Valor adicionado por setor só até 2021; cruzamento com o emprego de 2024

| Campo | Descrição |
|---|---|
| Problema identificado | O IBGE não publicou o valor adicionado por setor de 2022 e 2023 (só o PIB total), por causa da mudança do ano de referência das Contas Nacionais. O último ano com detalhe setorial é 2021, enquanto a RAIS é de 2024. |
| Decisão adotada | O cruzamento RAIS × PIB por setor compara a estrutura do valor adicionado de 2021 com a do emprego de 2024. Os anos de 2022 e 2023 ficam vazios (não zero) na série setorial. |
| Justificativa | É o dado setorial mais recente publicado; comparar estruturas (participações) reduz o efeito da diferença de anos. Amplia a DEC-005. |
| Impacto | Toda visualização do cruzamento informa os anos de cada fonte (VAB 2021 / RAIS 2024). Texto registrado nas Notas Metodológicas do painel. |
| User Stories impactadas | US09 |
| Status | Fechada — registrada pela equipe no painel (as duas decisões aparecem juntas nas Notas Metodológicas; separar o texto conforme o registro original da equipe) |

### DEC-008 — Correção de valores pela inflação (IPCA)

| Campo | Descrição |
|---|---|
| Problema identificado | Valores do PIB de anos diferentes não são comparáveis em reais correntes. |
| Decisão adotada | Valores corrigidos pelo IPCA para reais de 2023 (colunas *_real_2023). |
| Justificativa | Permite comparar a evolução do PIB de 2002 a 2023 sem o efeito da inflação. |
| Impacto | O crescimento mostrado é “deflacionado pelo IPCA”, não o PIB real oficial (o IBGE não publica volume para municípios); usar esse rótulo no painel. |
| User Stories impactadas | US09 |
| Status | Fechada — registrada pela equipe no painel |

### DEC-011 — Registros com indicador de RAIS negativa igual a 2

| Campo | Descrição |
|---|---|
| Problema identificado | 53 estabelecimentos têm Ind Rais Negativa = 2, valor que não consta do dicionário da RAIS (só 0 e 1). Todos têm 0 vínculos. |
| Decisão adotada | Classificados como categoria própria (“Indicador 2 — não documentado”) e somados ao grupo “Sem vínculo” do painel. |
| Justificativa | Não há vínculos nesses registros; mantê-los evita perda de dado e deixa o caso rastreável. |
| Impacto | O painel passa a mostrar 16.816 estabelecimentos com vínculo e 30.523 sem vínculo (a DEC-001 citava 16.869 ativos, que incluíam esses 53). |
| User Stories impactadas | US07, US08 |
| Status | Fechada — significado do valor 2 ainda a confirmar com o cliente |

### DEC-013 — Administração pública fora do cruzamento com o PIB

| Campo | Descrição |
|---|---|
| Problema identificado | A base RAIS do extrato não traz órgãos da administração pública (natureza jurídica 1xxx) e só 91 vínculos estatutários, enquanto o valor adicionado do IBGE inclui a administração pública. |
| Decisão adotada | Excluir a administração pública do cruzamento RAIS × PIB; o cruzamento usa 204.331 vínculos (CNPJ, sem administração pública). |
| Justificativa | Comparar apenas os setores privados presentes nas duas fontes. |
| Impacto | O painel compara participação no emprego privado com participação no valor adicionado privado (produtividade relativa). |
| User Stories impactadas | US09 |
| Status | Fechada — registrada pela equipe no painel |

### DEC-014 — Setores classificados pela Seção CNAE 2.0

| Campo | Descrição |
|---|---|
| Problema identificado | Era preciso um nível único de agregação para setores no painel e no cruzamento com o IBGE. |
| Decisão adotada | Usar a Seção CNAE 2.0 (21 seções, letra + nome oficial do IBGE) como “setor” padrão do painel. |
| Justificativa | É o mesmo padrão usado pelo IBGE e permite ligar RAIS e PIB por setor. |
| Impacto | Visuais de setor e filtros usam a coluna Seção CNAE; divisões, grupos e classes ficam para detalhamento. |
| User Stories impactadas | US07, US08, US09 |
| Status | Fechada — registrada pela equipe no painel |

### DEC-015 — Classificação dos estabelecimentos pela região oficial do município

| Campo | Descrição |
|---|---|
| Problema identificado | Nenhum arquivo do projeto trazia a região oficial de São José dos Campos (Centro, Norte, Sul, Leste, Oeste, Sudeste, São Francisco Xavier e área rural). |
| Decisão adotada | Atribuir a região pelo bairro de cada CEP, usando a lista de bairros por região do Plano Diretor da Prefeitura (2018). Os bairros da Região Norte, ausentes do PDF oficial, vêm de lista secundária; bairros ambíguos ou fora das listas recebem a região predominante do setor do CEP (5 dígitos). A coluna Confiabilidade Região indica Alta, Média ou Baixa. |
| Justificativa | É a divisão usada pela Prefeitura (inclusive na divulgação do Censo 2022). A validação mostrou que 33 dos 37 setores de CEP caem inteiros numa só região (os outros 4 estão na divisa Centro–Oeste ou misturam área urbana e rural). |
| Impacto | 99,99% dos estabelecimentos com região (85% confiabilidade Alta, 13,4% Média, 1,6% Baixa); 5 sem região (CEP geral 12200-000 ou sem CEP). |
| User Stories impactadas | US06 |
| Status | Aberta — aguardando do cliente a tabela oficial bairro → região (com a Região Norte) ou o shapefile das regiões |

### DEC-016 — Coordenadas corrompidas no arquivo de CEPs

| Campo | Descrição |
|---|---|
| Problema identificado | No arquivo ceps_sjc_geo_v2, todas as coordenadas perderam o ponto decimal (ex.: -23.1772612 virou -231.772.612), efeito de salvar o CSV no Excel em português. |
| Decisão adotada | Não usar as coordenadas desse arquivo; usar as do rais_sjc_geo_v2, que estão corretas. Gravar os CSVs com ponto decimal e importar no Power BI com a localidade “Inglês (EUA)”. |
| Justificativa | Coordenadas corrompidas colocariam todos os pontos fora do mapa. |
| Impacto | Nenhuma perda: o mesmo CEP tem a coordenada correta no outro arquivo. |
| User Stories impactadas | US06 |
| Status | Fechada |

### DEC-017 — Pontos de bairro geocodificados em homônimos

| Campo | Descrição |
|---|---|
| Problema identificado | Nove bairros foram geocodificados num bairro de mesmo nome em outra parte da cidade (ex.: Jardim Paraíso, Sul, posto em Jardim Paraíso do Sol, Leste), afetando 331 estabelecimentos. |
| Decisão adotada | Manter a região pela lista oficial e marcar esses pontos na coluna Alerta Coordenada; o mapa filtra esses pontos até a correção. |
| Justificativa | A região está certa (confirmada pelo setor do CEP); só o ponto precisa ser refeito. |
| Impacto | 331 estabelecimentos fora do mapa de pontos, mas presentes nos gráficos por região. |
| User Stories impactadas | US06 |
| Status | Aberta — regeocodificar os 9 bairros na Sprint 3 |

### DEC-018 — CEPs genéricos e sem localização

| Campo | Descrição |
|---|---|
| Problema identificado | 5.259 estabelecimentos usam CEPs terminados em 000 (grandes avenidas, que atravessam vários bairros) e 4.994 têm bairro não encontrado pelo geocodificador; 5 têm o CEP geral da cidade ou CEP zero. |
| Decisão adotada | CEPs genéricos ficam sem ponto no mapa e recebem a região pelo bairro da avenida (confiabilidade Média). Os 5 sem localização ficam como “Não classificado”. |
| Justificativa | Um ponto no centro de uma avenida longa seria enganoso; a região, por outro lado, raramente muda ao longo dela. |
| Impacto | 10.255 estabelecimentos sem ponto no mapa, todos com região (exceto os 5). |
| User Stories impactadas | US06 |
| Status | Fechada — geocodificação dos bairros não encontrados fica na Sprint 3 |

### DEC-019 — Situação detalhada do estabelecimento

| Campo | Descrição |
|---|---|
| Problema identificado | A situação “Com vínculo” do painel (RAIS positiva, 16.816) inclui 1.758 estabelecimentos que tiveram empregados no ano, mas fecharam 2024 com zero vínculos ativos. |
| Decisão adotada | Manter a coluna Situação Vínculo como no painel (DEC-011) e criar a coluna Situação Detalhada com quatro categorias: com vínculos em 31/12 (15.058), sem vínculos em 31/12 não negativa (1.758), RAIS negativa (30.470) e indicador 2 (53). |
| Justificativa | Preserva os números atuais do painel e permite a leitura correta de “empregos em 31/12”. |
| Impacto | Novas medidas podem contar só quem tinha empregados em 31/12; textos do painel devem distinguir estabelecimentos de vínculos. |
| User Stories impactadas | US07, US08 |
| Status | Fechada |

### DEC-020 — Descrições oficiais da CNAE 2.3

| Campo | Descrição |
|---|---|
| Problema identificado | As descrições de grupo, classe e subclasse da base usavam grafias antigas e quebras de linha (ex.: “liqüefeito”, “glp”, “préescola”). Os códigos batem 100% com a CNAE 2.3. |
| Decisão adotada | Substituir as descrições pelo texto oficial da CNAE 2.3 (IBGE/CONCLA), mantendo os códigos. Subclasses inexistentes na CNAE 2.3 (8630505 e 9999999, 16 estabelecimentos) mantêm a descrição anterior e ficam marcadas na coluna Subclasse na CNAE 2.3. |
| Justificativa | Rótulos oficiais e uniformes no painel e nos relatórios. |
| Impacto | 2.869 estabelecimentos com descrição atualizada; nenhum código alterado. |
| User Stories impactadas | US07, US08 |
| Status | Fechada |

### DEC-021 — Classificações derivadas da CNAE e do porte

| Campo | Descrição |
|---|---|
| Problema identificado | Os requisitos do cliente pedem o tipo de atividade predominante (manufatura, tecnologia, logística, serviços especializados), a relação com o desenvolvimento tecnológico e os setores aeroespacial, automotivo e químico. |
| Decisão adotada | Criar quatro colunas por regra fixa: Tipo de Atividade (grupos de seções/divisões CNAE), Intensidade Tecnológica OCDE (taxonomia da OCDE de 2016), Porte SEBRAE (critério por número de empregados, indústria × comércio/serviços) e Setor Destaque (automotiva, aeroespacial e química e farmacêutica). |
| Justificativa | Responde diretamente às perguntas do documento de requisitos; regras fixas tornam a classificação reprodutível. |
| Impacto | Atividades de alta e média-alta tecnologia: cerca de 28,8 mil vínculos (14% do emprego formal) em 2.519 estabelecimentos. |
| User Stories impactadas | US07, US08, US11 |
| Status | Fechada |

### DEC-022 — Base única para o Power BI e mapa por coordenadas

| Campo | Descrição |
|---|---|
| Problema identificado | O painel lia a RAIS sem região nem coordenadas, e o mapa localizava os estabelecimentos pelo texto do CEP, que o Azure Maps não encontra com precisão. |
| Decisão adotada | Gerar uma base única (RAIS_SJC_2024_PowerBI.csv, 47.339 linhas, 46 colunas) que substitui a fonte da tabela RAIS_SJC mantendo os nomes de colunas usados pelos visuais; o mapa passa a usar Latitude e Longitude. |
| Justificativa | Evita retrabalho nos visuais e torna o mapa confiável. |
| Impacto | Troca de fonte e ajuste do mapa no Power BI, conforme o guia de importação (evidencias/). |
| User Stories impactadas | US06, US11 |
| Status | Aberta — troca no painel a concluir na Sprint 3 |

## 3. Fechamento da US03

Com as cinco decisões da Sprint 1 (DEC-001 a DEC-005), o critério de aceite da US03 (“cada inconsistência encontrada está registrada no Log de Decisões com o tratamento adotado”) foi atendido. Status da US03 no Backlog do Produto: Concluído.

## 4. Pendências que permanecem em aberto com o cliente

- Disponibilidade de dados identificados (nome/CNPJ dos estabelecimentos) — afeta DEC-004. Plano de contingência em uso: ranking agregado por setor (US07).
- Confirmação formal do critério de segmentação por natureza de estabelecimento (DEC-002).
- Significado do valor 2 no indicador de RAIS negativa (DEC-011).
- Tabela oficial de bairros por região, incluindo a Região Norte, ou shapefile das regiões (DEC-015).
- Fonte para a evolução dos setores (US08) e as contratações recentes (US10): RAIS de anos anteriores ou RAIS Vínculos.

Essas pendências não bloquearam a entrega da Sprint 2, mas afetam o fechamento da US06 e o replanejamento da US08 e da US10 na Sprint 3.

## Como usar este log

- Toda nova decisão sobre tratamento de dado ganha uma entrada DEC-00X nova, nunca se edita o histórico de uma decisão já tomada (se a decisão mudar, registra-se uma nova entrada referenciando a anterior).
- Este arquivo deve ser citado no relatório técnico de cada sprint sempre que uma decisão aqui registrada afetar o resultado apresentado.
