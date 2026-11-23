> Versão em Markdown de [`10-Relatorio-Tecnico-Sprint-2.docx`](10-Relatorio-Tecnico-Sprint-2.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Relatório Técnico — Sprint 2

**Período:** 29/set a 26/out · Meta da Sprint: construir as análises centrais no Power BI — setores de atividade, porte e situação dos estabelecimentos e cruzamento RAIS × PIB — e preparar a base geocodificada com a região oficial de cada estabelecimento para o mapa da cidade.

## O que foi entregue

O painel Power BI (PowerbiATT_Api_Sprint2.pbix) ganhou quatro páginas: Notas Metodológicas, KPIs e Mapa, Setor de Atividades (CNAE) e PIB e Emprego. A base RAIS de São José dos Campos (47.339 estabelecimentos) foi classificada pela CNAE de seção a subclasse (CNAE_RAIS_SJC_2024.xlsx) e a série do PIB dos Municípios foi tratada no Colab de 2002 a 2023 (IBGE_PIB_SJC_Observatorio.xlsx).

Os 3.677 CEPs da base foram geocodificados no nível de bairro e cada estabelecimento recebeu a região oficial do município. Tudo foi reunido numa base única para o Power BI (RAIS_SJC_2024_PowerBI.csv, 46 colunas), validada pela CNAE 2.3 oficial e acompanhada de um guia de importação e de um relatório da base.

## Indicadores da base

| **Indicador**                                                            | **Valor**                   | **Referência**       |
|--------------------------------------------------------------------------|-----------------------------|----------------------|
| Estabelecimentos (RAIS 2024)                                             | 47.339                      | DEC-002, DEC-003     |
| Com vínculos ativos em 31/12/2024                                        | 15.058 (31,8%)              | DEC-019              |
| RAIS negativa                                                            | 30.470 (64,4%)              | DEC-001              |
| Vínculos ativos em 31/12/2024                                            | 206.717                     | —                    |
| Estabelecimentos com região oficial                                      | 47.334 (99,99%)             | DEC-015              |
| Estabelecimentos com ponto no mapa                                       | 37.084 (78,3%)              | DEC-017, DEC-018     |
| Vínculos em atividades de alta e média-alta tecnologia                   | 28.804 (13,9%)              | DEC-021              |
| PIB de São José dos Campos em 2023                                       | R\$ 61,4 bilhões            | IBGE                 |
| Indústria: participação no emprego privado × no valor adicionado privado | 24,7% × 45,8% (índice 1,86) | DEC-006/009, DEC-013 |

## Metodologia e tecnologias utilizadas

- **Fontes de dados:** RAIS Estabelecimentos 2024 (MTE); PIB dos Municípios do IBGE (PIB 2002–2023, valor adicionado por setor até 2021); CNAE 2.3 (IBGE/CONCLA); divisão regional do Plano Diretor da Prefeitura de São José dos Campos.

- **Ferramentas:** Google Colab + Python (pandas) para tratamento, junções e validações; BrasilAPI e Nominatim (OpenStreetMap) para a geocodificação dos CEPs; Power BI para modelagem e visualização.

- **Etapas do tratamento:** junção da base RAIS com a geocodificação pelo CEP (muitos para um, sem duplicar linhas); classificação da região pelo bairro, validada pelo setor do CEP; verificação dos pontos contra o centro da região; substituição das descrições pela CNAE 2.3; criação das classificações de tipo de atividade, intensidade tecnológica (OCDE), porte (SEBRAE) e setor destaque; releitura do arquivo final para conferir totais.

## Resposta ao feedback da Sprint 1

O orientador pediu para esclarecer se os 64,37% de RAIS negativa poderiam ser erro de filtragem. Não são: o extrato contém apenas o município 354990 (100% das 47.339 linhas). Desses 30.470 estabelecimentos, 13.604 declararam atividade no ano — estavam funcionando, mas sem empregados formais. Outros 1.758 tiveram empregados no ano e fecharam 2024 com zero vínculos, e 53 têm um indicador (valor 2) fora do dicionário da RAIS (DEC-011, DEC-019).

## Dificuldades encontradas

O arquivo de CEPs geocodificados teve todas as coordenadas corrompidas ao ser salvo no Excel em português (o ponto decimal virou separador de milhar), o que exigiu usar outra fonte das coordenadas (DEC-016). Nove bairros foram geocodificados num homônimo em outra parte da cidade (DEC-017), e 10.255 estabelecimentos ficaram sem ponto no mapa por estarem em CEPs de avenida ou em bairros não encontrados (DEC-018).

A divisão regional oficial não existia em nenhum arquivo e o PDF do Plano Diretor não traz os bairros da Região Norte (DEC-015). A RAIS disponível tem um único ano e não traz datas de admissão, o que impede mostrar a evolução dos setores (US08) e limita a US10. Por fim, o IBGE só detalha o valor adicionado por setor até 2021, o que obrigou a comparar anos diferentes no cruzamento com o emprego (DEC-006/009).

## Decisões técnicas relevantes

As decisões da Sprint 2 foram registradas no Log de Decisões de Dados (06-Decisoes-de-Dados): DEC-006/009 (valor adicionado por setor até 2021 e cruzamento com o emprego de 2024), DEC-008 (correção pelo IPCA), DEC-011 (indicador 2 de RAIS negativa), DEC-013 (administração pública fora do cruzamento), DEC-014 (setores pela Seção CNAE), DEC-015 (região oficial), DEC-016 a DEC-018 (coordenadas e CEPs sem localização), DEC-019 (situação detalhada), DEC-020 (descrições da CNAE 2.3), DEC-021 (classificações derivadas) e DEC-022 (base única e mapa por coordenadas). As DEC-007, 010 e 012, citadas pela equipe, ainda precisam ser transcritas para o log.

## Status das User Stories

| **ID** | **Situação ao fim da Sprint 2**                                                                         | **Status** |
|--------|---------------------------------------------------------------------------------------------------------|------------|
| US06   | Base com região oficial (99,99%) e ponto no mapa (78%); mapa do painel ainda localiza pelo texto do CEP | Parcial    |
| US07   | Rankings Top 10 de setores por estabelecimentos e por empregos CLT (agregado — DEC-004)                 | Concluído  |
| US08   | Setores predominantes e participação; falta série histórica para mostrar evolução                       | Parcial    |
| US09   | Página PIB e Emprego com PIB 2002–2023, valor adicionado por setor e produtividade relativa             | Concluído  |

## Próximos passos (Sprint 3)

Importar a base única no painel e trocar o mapa para latitude/longitude, corrigindo os subtítulos dos cartões da página KPIs. Pedir ao cliente a tabela ou o shapefile oficial das regiões e a decisão sobre a fonte para a evolução dos setores (US08) e as contratações recentes (US10). Geocodificar os bairros restantes, criar os visuais por região, tipo de atividade e intensidade tecnológica e consolidar o dashboard, o relatório final e a apresentação da Feira de Soluções (US11).
