> Versão em Markdown de [`01-Visao-e-Escopo.docx`](01-Visao-e-Escopo.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Documento de Visão e Escopo do Projeto

## 1. Nome e descrição resumida do projeto

Nome: Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

Descrição: Ferramenta de Business Intelligence, desenvolvida em Power BI e inspirada no modelo do Observatório da Inovação RS (Secretaria de Inovação, Ciência e Tecnologia do Rio Grande do Sul), que mapeia o ecossistema industrial e de serviços de São José dos Campos a partir de dados de contratações formais (RAIS) e do PIB municipal (IBGE). O painel permite identificar os maiores empregadores, os setores em crescimento, a distribuição geográfica das empresas na cidade e a participação estimada de cada setor no PIB municipal.

## 2. Problema real identificado

Gestores, analistas de mercado e órgãos de fomento local não dispõem de uma visão consolidada e visual sobre o comportamento do mercado de trabalho formal e o ecossistema produtivo de São José dos Campos — quais empresas mais contratam, quais setores estão em expansão, onde essas empresas estão concentradas geograficamente e qual o peso econômico de cada segmento na cidade. Os dados existem (RAIS, IBGE), mas estão dispersos e não são analisados de forma integrada e acessível. Outras esferas de governo, como o Estado do Rio Grande do Sul, já desenvolveram ferramentas públicas semelhantes (o Observatório da Inovação RS), mas São José dos Campos ainda não conta com um instrumento equivalente em escala municipal.

## 3. Cliente, organização ou público interessado

Cliente: CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos.

- Professor M2: José Jaétis

- Professor P2: Marcus

- Contato do cliente: Marcus, via grupo do WhatsApp

- Público interessado: órgãos municipais de desenvolvimento econômico (Secretaria de Desenvolvimento Econômico), associações empresariais locais, estudantes e pesquisadores de economia regional

## 4. Justificativa do projeto

São José dos Campos é um polo industrial e tecnológico relevante no Vale do Paraíba, com forte presença dos setores aeroespacial, automotivo, químico e de serviços especializados, além de um ecossistema de inovação reconhecido (certificação internacional Platina em Smart City). Apesar dessa relevância, não existe um mapeamento estruturado e público da estrutura produtiva regional. O próprio cliente apresentou como referência o modelo de governança de hélice tríplice/quádrupla (Empresa, Academia, Sociedade, Governo) e o Observatório da Inovação RS como “modelo interessante” a ser seguido. Entender a dinâmica de contratação, a distribuição geográfica e o peso econômico das empresas locais apoia decisões de política pública, atração de investimentos e planejamento de mão de obra qualificada na região.

## 5. Objetivo geral

Desenvolver um painel analítico (observatório) em Power BI que consolide dados da RAIS e do PIB dos Municípios (IBGE) para apresentar indicadores sobre contratações, setores em alta, distribuição geográfica das empresas e impacto econômico das empresas de São José dos Campos, inspirado no formato do Observatório da Inovação RS.

## 6. Objetivos específicos

- Identificar as empresas com maior volume de contratações formais no município

- Apontar os setores/áreas (CNAE) com maior crescimento de contratações

- Estimar a participação de cada setor no PIB municipal, cruzando RAIS e dados do IBGE

- Mapear geograficamente a distribuição das empresas/setores no município, identificando concentrações (polos, distritos, hubs) quando os dados permitirem

- Exibir as contratações mais recentes registradas

- Permitir filtros por setor de atividade, porte, tipo de estabelecimento e região oficial do município (a RAIS disponível cobre só 2024; filtro por período depende de bases de outros anos)

- Classificar os estabelecimentos por tipo de atividade, intensidade tecnológica e etapa da cadeia de suprimentos, para responder às questões de análise do cliente do ponto de vista da logística (Sprint 3)

## 7. Público-alvo e personas

- Gestor público/econômico (Secretaria de Desenvolvimento Econômico): quer indicadores para embasar decisões sobre desenvolvimento econômico local

- Analista de mercado: quer identificar tendências de contratação por setor e por região da cidade

- Administrador do sistema: quer manter os dados atualizados e o painel funcionando

## 8. Escopo incluído

- Coleta e tratamento de microdados da RAIS para o município de São José dos Campos

- Cruzamento com dados de PIB dos Municípios (IBGE) por setor de atividade (CNAE)

- Construção de dashboard interativo em Power BI com os indicadores definidos

- Classificação e mapeamento geográfico das empresas por setor de atividade e, quando aplicável, por tipo de ambiente de inovação (polo, hub, distrito, núcleo), tomando como referência o modelo do Observatório da Inovação RS

- Filtros por setor, porte, tipo de estabelecimento e região (período: só 2024 nesta versão da base)

- Documentação técnica do processo de ETL e do modelo de dados

## 9. Escopo explicitamente excluído

- Dados de emprego informal (não capturados pela RAIS)

- Previsões ou modelos preditivos de contratação (fica como sugestão de trabalho futuro)

- Dados de empresas fora do município de São José dos Campos

- Aplicativo mobile ou sistema web próprio (entrega será via Power BI/relatório publicado)

- Réplica completa dos quatro eixos do Observatório da Inovação RS (indicadores de pesquisa, editais da Fapergs, programas estaduais) — fora do escopo por não haver fontes de dados municipais equivalentes disponíveis; o Observatório RS é usado apenas como inspiração de formato e experiência do usuário, não como escopo de dados

## 10. Restrições de prazo, tecnologia, dados ou infraestrutura

- Prazo: 1 semestre letivo, dividido em 3 sprints de desenvolvimento (Sprint 1, 2 e 3), seguidas da apresentação final na Feira de Soluções (03/dez)

- Tecnologias definidas pelo cliente: Google Colab + Python 3+ para tratamento dos dados; Power BI para visualização; GitHub para versionamento e documentação

- Dados limitados à granularidade e periodicidade de divulgação da RAIS — ano-base confirmado pelo cliente: 2024

- PIB municipal segue a periodicidade de divulgação do IBGE: o PIB total vai até 2023, mas o valor adicionado por setor só até 2021 (mudança de referência das Contas Nacionais). O cruzamento por setor compara valor adicionado de 2021 com emprego de 2024 (ver 06-Decisoes-de-Dados)

- A RAIS não fornece coordenadas das empresas: na Sprint 2 o CEP foi geocodificado no nível de bairro (78% dos estabelecimentos com ponto no mapa) e, na Sprint 3, pelas coordenadas do CNEFE 2022 do IBGE (99,99% com ponto, DEC-023). Cada estabelecimento recebeu a região oficial do município (99,99%); a lista oficial de bairros da Região Norte segue pendente com a Prefeitura (DEC-015).

## 11. Critérios gerais de sucesso

- Painel publicado e funcional, com todos os indicadores planejados

- Dados da RAIS corretamente filtrados para o município de SJC

- Cruzamento RAIS x PIB validado com uma metodologia clara e documentada

- Painel apresenta ao menos uma visualização geográfica das empresas/setores, alinhada ao modelo de referência apresentado pelo cliente

- Aprovação da equipe docente na entrega final

## 12. Tecnologias previstas

- Google Colab + Python 3+ (acesso, organização e tratamento inicial dos microdados)

- Power BI (modelagem e visualização)

- GitHub (versionamento e documentação do projeto)

- Fontes de dados: RAIS (Ministério do Trabalho e Emprego) e PIB dos Municípios (IBGE)

- Referência de formato/UX: Observatório da Inovação RS (Secretaria de Inovação, Ciência e Tecnologia do Rio Grande do Sul)

## 13. Riscos iniciais e estratégias de mitigação

| **Risco**                                                                                                                             | **Mitigação**                                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Volume grande de microdados da RAIS pode ser difícil de processar                                                                     | Filtrar por município (SJC) o quanto antes no processo de ETL, usando Google Colab/Python — feito via leitura em streaming (Sprint 1)                                                                                                             |
| Defasagem entre a divulgação da RAIS e do PIB municipal                                                                               | Usar o último ano disponível em cada base (RAIS 2024, PIB 2023, valor adicionado por setor 2021) e mostrar o ano de cada número no painel (DEC-005, DEC-006/009)                                                                                  |
| Dificuldade em estimar participação de empresa individual no PIB (dado é por setor, não por empresa)                                  | Deixar claro que a estimativa é por setor de atividade (CNAE), não por empresa isolada                                                                                                                                                            |
| Tentar replicar o escopo completo do Observatório da Inovação RS (equipe estadual dedicada, múltiplas fontes como editais da Fapergs) | Usar o Observatório RS apenas como inspiração de formato/UX; manter o escopo de dados restrito a RAIS + PIB dos Municípios (IBGE)                                                                                                                 |
| Falta de dado estruturado sobre localização exata (endereço/coordenadas) das empresas na RAIS                                         | Geocodificação por CEP no nível de bairro e classificação por região oficial (Sprint 2); pontos com problema marcados na base (DEC-015 a DEC-018). Na Sprint 3, coordenadas do CNEFE 2022 por CEP (99,99% dos estabelecimentos no mapa, DEC-023). |
| Divisão regional oficial incompleta nas fontes públicas (bairros da Região Norte fora do Plano Diretor)                               | Lista do Plano Diretor + setor do CEP, com coluna de confiabilidade; pedir ao cliente a tabela bairro → região ou o shapefile das regiões (DEC-015)                                                                                               |
| A RAIS disponível tem um só ano e não traz datas de admissão — limita “setores em alta” (US08) e “contratações recentes” (US10)       | Mostrar setores predominantes; avaliar com o cliente o uso da RAIS de anos anteriores ou da RAIS Vínculos na Sprint 3                                                                                                                             |

Revisão de 26/10/2026 (fechamento da Sprint 2): ajustados os objetivos e o escopo de filtros (base com um único ano), as restrições de dados (valor adicionado por setor até 2021; geocodificação e região oficial) e incluídos dois riscos novos.

Revisão de 23/11/2026 (entrega final, Sprint 3): atualizada a restrição de localização (coordenadas do CNEFE 2022, DEC-023) e incluído o objetivo de classificar as atividades pela etapa da cadeia de suprimentos (DEC-024). O ranking por empresa segue agregado por setor, por falta de identificação nominal na RAIS pública (DEC-004).
