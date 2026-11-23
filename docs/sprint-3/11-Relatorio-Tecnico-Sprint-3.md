> Versão em Markdown de [`11-Relatorio-Tecnico-Sprint-3.docx`](11-Relatorio-Tecnico-Sprint-3.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao índice da documentação](../README.md)

# Relatório Técnico — Sprint 3 (versão final)

**Período:** 27/out a 23/nov · Meta da Sprint: consolidar o observatório como entrega final — mapa completo da cidade, painel com as respostas aos requisitos do cliente, documentação final e preparação da Feira de Soluções (03/12/2026).

## O que foi entregue

O mapa passou a usar as coordenadas do CNEFE 2022 do IBGE, já calculadas no notebook de geocodificação da equipe (01b) e até então não aproveitadas. Com isso, 47.334 dos 47.339 estabelecimentos (99,99%) têm ponto no mapa, no nível do CEP, contra 78,3% na Sprint 2, e 329 dos 331 pontos que caíam em bairros homônimos foram corrigidos (DEC-023).

O painel ganhou a página Regiões e Tecnologia, com vínculos por região, por tipo de atividade, por intensidade tecnológica (OCDE) e por macroprocesso logístico, uma nova classificação de cada estabelecimento pela etapa da cadeia de suprimentos (DEC-024). A página 1 recebeu ajustes de leitura (cartões sem "Mil", título e subtítulos corrigidos), e o projeto foi renomeado para Observatorio_SJC.pbip, com um parâmetro de pasta que permite a qualquer integrante atualizar as 6 tabelas a partir do repositório.

Cada pergunta, funcionalidade, resultado esperado e requisito técnico do documento do cliente foi ligado a uma resposta, com números da base e o lugar do painel onde aparece (Respostas_Requisitos_Cliente.md), do ponto de vista da logística. O repositório recebeu também o notebook de geocodificação, a evidência com os códigos de tratamento de dados e o canal do projeto no YouTube (LogMulti).

## Indicadores finais da base

| **Indicador**                                                            | **Valor**                              | **Referência**       |
|--------------------------------------------------------------------------|----------------------------------------|----------------------|
| Estabelecimentos (RAIS 2024)                                             | 47.339                                 | DEC-002, DEC-003     |
| Com vínculos ativos em 31/12/2024                                        | 15.058 (31,8%)                         | DEC-019              |
| RAIS negativa                                                            | 30.470 (64,4%)                         | DEC-001              |
| Vínculos ativos em 31/12/2024                                            | 206.717                                | —                    |
| Estabelecimentos com região oficial                                      | 47.334 (99,99%)                        | DEC-015              |
| Estabelecimentos com ponto no mapa                                       | 47.334 (99,99%); antes, 37.084 (78,3%) | DEC-023              |
| Vínculos em atividades de alta e média-alta tecnologia                   | 28.804 (13,9%)                         | DEC-021              |
| Vínculos em distribuição atacadista e em transporte e armazenagem        | 17.252 (8,3%)                          | DEC-024              |
| PIB de São José dos Campos em 2023                                       | R\$ 61,4 bilhões                       | IBGE                 |
| Indústria: participação no emprego privado × no valor adicionado privado | 24,7% × 45,8% (índice 1,86)            | DEC-006/009, DEC-013 |
| Decisões de dados registradas                                            | 24 (DEC-001 a DEC-024)                 | Log de Decisões      |

## Metodologia e tecnologias utilizadas

- **Fontes de dados:** RAIS Estabelecimentos 2024 (MTE); PIB dos Municípios do IBGE (PIB 2002–2023, valor adicionado por setor até 2021); CNAE 2.3 (IBGE/CONCLA); Cadastro Nacional de Endereços para Fins Estatísticos (CNEFE) do Censo 2022 (IBGE); divisão regional do Plano Diretor de São José dos Campos.

- **Ferramentas:** Google Colab + Python (pandas) para tratamento e validação (notebooks 01, 01b e 02); Power BI para modelagem e visualização, com colunas calculadas em DAX; GitHub para versionamento e documentação.

- **Geocodificação:** ponto médio dos endereços do CNEFE com o mesmo CEP; quando o CEP não aparece no cadastro, centro dos CEPs com os mesmos 5 primeiros dígitos. A região continua sendo atribuída pelo bairro.

- **Macroprocessos:** cada estabelecimento é classificado pela etapa da cadeia de suprimentos em que atua (suprimento, produção, distribuição atacadista, transporte e armazenagem, varejo, pós-venda, logística reversa, serviços de apoio e serviços ao consumidor), pela classe CNAE. A mesma regra está no notebook 02 e no painel, e as duas foram conferidas registro a registro.

## Respostas aos requisitos do cliente

As 7 questões de análise do documento de requisitos têm resposta no repositório. Os principais resultados: comércio (22,4%), indústria de transformação (17,9%) e serviços administrativos (15,2%) são os maiores empregadores; a indústria fica no Leste e no Sudeste (54% dos empregos industriais); 69% dos empregos da indústria são de alta ou média-alta tecnologia, puxados pela fabricação de aeronaves (11.069 vínculos em 10 estabelecimentos); e produção e varejo concentram 40,5% dos empregos, enquanto as etapas logísticas centrais (atacado e transporte e armazenagem) somam 8,3%.

A pergunta sobre oportunidades profissionais foi respondida para o profissional de logística, com sete áreas tiradas dos números da base: indústria aeroespacial e automotiva, transporte de carga, atacado e armazenagem, varejo, saúde, pós-venda e logística reversa. As 8 funcionalidades e os 6 requisitos técnicos (RN.P.1 a RN.P.6) estão atendidos.

## Dificuldades encontradas

A RAIS não informa os processos internos das empresas, e a pergunta do cliente sobre macroprocessos exigiu uma classificação própria da equipe pela atividade principal (DEC-024). A RAIS disponível tem um único ano e não traz data de admissão, o que impede mostrar a evolução dos setores (US08) e as contratações recentes (US10).

No painel, o cache de dados do Power BI não vai para o GitHub, então quem baixa o projeto precisa atualizar todas as tabelas. A tabela PIB anual lia uma aba que só existia no computador de uma integrante; a aba foi remontada a partir dos dados do IBGE já tratados no repositório e conferida com a série calculada pela equipe. As mudanças do painel foram feitas no projeto .pbip e só aparecem no link publicado depois de atualizar e republicar no Power BI Desktop.

## Decisões técnicas relevantes

As decisões da Sprint 3 foram registradas no Log de Decisões de Dados (06-Decisoes-de-Dados): DEC-023 (coordenadas do mapa pelo CNEFE 2022, que fechou a DEC-017 dos bairros homônimos) e DEC-024 (macroprocessos pela etapa da cadeia de suprimentos). Seguem abertas a DEC-004 (sem identificação nominal das empresas), a DEC-015 (tabela oficial bairro → região da Prefeitura, que falta para a Região Norte) e a DEC-022 (troca da fonte da tabela RAIS_SJC do painel pela base única). As DEC-007, 010 e 012, citadas pela equipe, ainda precisam ser transcritas para o log.

## Status final das User Stories

| **ID** | **Situação na entrega final**                                                                                          | **Status**   |
|--------|------------------------------------------------------------------------------------------------------------------------|--------------|
| US01   | Pipeline de ETL no Google Colab (notebook 01)                                                                          | Concluído    |
| US02   | Base filtrada e padronizada para o município 354990                                                                    | Concluído    |
| US03   | Inconsistências da RAIS tratadas e registradas (DEC-001 a DEC-005)                                                     | Concluído    |
| US04   | Documentação Scrum (Visão e Escopo, backlogs, DoR, DoD, Log de Decisões)                                               | Concluído    |
| US05   | Repositório no GitHub organizado e versionado                                                                          | Concluído    |
| US06   | Mapa por coordenadas com 99,99% dos estabelecimentos e filtro por região; link publicado será atualizado ao republicar | Concluído    |
| US07   | Rankings de setores por estabelecimentos e por empregos (agregado, DEC-004)                                            | Concluído    |
| US08   | Setores predominantes e participação no emprego; falta série histórica da RAIS para mostrar evolução                   | Parcial      |
| US09   | PIB 2002–2023, valor adicionado por setor e produtividade relativa                                                     | Concluído    |
| US10   | A RAIS Estabelecimentos não tem data de admissão; critério a revisar com o cliente                                     | Não atendida |
| US11   | Painel consolidado de 5 páginas, relatórios finais e respostas aos requisitos; apresentação na Feira em 03/12/2026     | Parcial      |

## Próximos passos (até a Feira de Soluções, 03/12/2026)

Abrir o projeto no Power BI Desktop, atualizar todas as tabelas e republicar no mesmo workspace, para o link mostrar o mapa completo, a página Regiões e Tecnologia e os ajustes da página 1. Publicar o vídeo do projeto no canal LogMulti e preparar a apresentação. Na Feira, levar ao cliente três decisões: a fonte ou o critério revisado para US08 e US10, a confirmação de que a pergunta sobre oportunidades pode ser respondida do ponto de vista da logística, e o pedido à Prefeitura da tabela oficial de bairros por região (DEC-015).
