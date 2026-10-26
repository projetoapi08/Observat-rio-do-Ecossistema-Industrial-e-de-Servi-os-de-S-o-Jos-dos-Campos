# Dados do Observatório

Bases tratadas do projeto. A principal é **`RAIS_SJC_2024_PowerBI.csv`**, a base única que alimenta o painel: uma linha por estabelecimento de São José dos Campos (47.339 linhas, 46 colunas), gerada pelo notebook [`notebooks/02_Base_PowerBI_SJC.ipynb`](../notebooks/02_Base_PowerBI_SJC.ipynb).

## Arquivos

| Arquivo | Conteúdo | Origem |
|---|---|---|
| [`RAIS_SJC_2024_PowerBI.csv`](RAIS_SJC_2024_PowerBI.csv) | Base única para o Power BI: CEP, coordenadas, região oficial, CNAE 2.3, porte, tipo e situação | Notebook 02 (Sprint 2) |
| [`CNAE_RAIS_SJC_2024.xlsx`](CNAE_RAIS_SJC_2024.xlsx) | Base RAIS com a hierarquia CNAE (aba `Base_RAIS`), tabelas de setores, porte, RAIS negativa e legendas | Sprint 2 |
| [`IBGE_PIB_SJC_Observatorio.xlsx`](IBGE_PIB_SJC_Observatorio.xlsx) | PIB dos Municípios 2002–2023, valor adicionado por setor (até 2021) e cruzamento com a RAIS | Sprint 2 |
| [`entrada/RAIS_SJC_completo.csv`](entrada/RAIS_SJC_completo.csv) | Extrato da RAIS 2024 filtrado para o município 354990 | ETL da Sprint 1 (notebook 01) |
| [`entrada/rais_sjc_geo_v2.csv`](entrada/rais_sjc_geo_v2.csv) | RAIS com bairro e coordenadas de cada CEP | Geocodificação (BrasilAPI + Nominatim) |
| [`entrada/ceps_sjc_geo_v2.csv`](entrada/ceps_sjc_geo_v2.csv) | Uma linha por CEP com logradouro e marcação de CEP genérico. **Atenção:** as coordenadas deste arquivo estão corrompidas (DEC-016) | Geocodificação |
| [`referencia/bairros_regiao_sjc.csv`](referencia/bairros_regiao_sjc.csv) | Tabela bairro → região oficial, editável. Para tornar a classificação 100% oficial, substitua pela lista da Prefeitura e rode o notebook 02 | Plano Diretor PMSJC + lista secundária (Norte) |
| [`referencia/CNAE_Subclasses_2_3.xlsx`](referencia/CNAE_Subclasses_2_3.xlsx) | Estrutura oficial da CNAE 2.3 (1.332 subclasses) | IBGE/CONCLA |

## Como importar no Power BI

Siga [`evidencias/Importacao_PowerBI_RAIS_SJC.txt`](../evidencias/Importacao_PowerBI_RAIS_SJC.txt). Os dois cuidados principais:

- **CEP e códigos CNAE como texto**, senão o Power BI apaga o zero à esquerda (01113 vira 1113).
- **Latitude e longitude com a localidade "Inglês (EUA)"**, porque o arquivo usa ponto decimal.

## Dicionário da base única

Colunas marcadas com ⭐ já são usadas pelos visuais do painel e mantêm o nome original.

| Coluna | Tipo | Significado | Exemplo |
|---|---|---|---|
| ID Estab | inteiro | Número da linha do estabelecimento (igual ao ID da Base_RAIS); chave única | 1 |
| Ano Base | inteiro | Ano de referência da RAIS (DEC-003) | 2024 |
| CEP Estab ⭐ | texto | CEP com 8 dígitos; vazio quando o CEP original é zero | 12231675 |
| CEP Formatado | texto | CEP com hífen, para exibição | 12231-675 |
| CEP Genérico | texto | Sim = CEP terminado em 000, de grande avenida, sem ponto no mapa | Não |
| Logradouro | texto | Rua ou avenida do CEP (BrasilAPI) | Avenida Cidade Jardim |
| Bairro | texto | Bairro do CEP | Jardim Satélite |
| Região Oficial | texto | Centro, Norte, Sul, Leste, Oeste, Sudeste, São Francisco Xavier, Rural ou Não classificado (DEC-015) | Sul |
| Fonte Região | texto | Origem da região: lista oficial, fonte secundária, setor do CEP ou distrito/rural | Plano Diretor PMSJC 2018 |
| Confiabilidade Região | texto | Alta, Média, Baixa ou Não se aplica | Alta |
| Latitude | decimal | Latitude do centro do bairro; vazia quando não há ponto | -23.2280912 |
| Longitude | decimal | Longitude do centro do bairro | -45.8867116 |
| Precisão Geo | texto | bairro, bairro (aproximado), distrito, região (sem ponto no mapa), não localizado, sem CEP | bairro |
| Alerta Coordenada | texto | Preenchida quando o ponto caiu em outra região por bairro homônimo (DEC-017) | (vazio) |
| Seção Cód | texto | Letra da seção CNAE (A a U; NI = ignorada) | C |
| Seção CNAE ⭐ | texto | Letra + nome oficial IBGE da seção | C - Indústrias de transformação |
| Setor ⭐ | texto | Nome curto da seção CNAE | Indústria de transformação |
| Divisão CNAE | texto | Código de 2 dígitos | 30 |
| Divisão Descrição | texto | Nome da divisão | Fabricação de outros equipamentos de transporte, exceto veículos automotores |
| Grupo CNAE | texto | Código de 3 dígitos | 304 |
| Grupo Descrição | texto | Nome do grupo (CNAE 2.3) | Fabricação de aeronaves |
| CNAE 2.0 Classe ⭐ | texto | Código de 5 dígitos, com zero à esquerda | 30415 |
| Classe Descrição | texto | Nome da classe (CNAE 2.3) | Fabricação de aeronaves |
| CNAE 2.0 Subclasse | texto | Código de 7 dígitos | 3041500 |
| Subclasse Descrição | texto | Nome da subclasse (CNAE 2.3) | Fabricação de aeronaves |
| Subclasse na CNAE 2.3 | texto | Sim/Não: o código existe na CNAE 2.3 vigente (DEC-020) | Sim |
| Tipo de Atividade | texto | Categoria do cliente: manufatura, tecnologia, logística, serviços especializados, comércio etc. (DEC-021) | Manufatura (indústria de transformação) |
| Intensidade Tecnológica OCDE | texto | Alta, Média-alta, Média, Média-baixa ou Não se aplica | Alta |
| Setor Destaque | texto | Automotiva, aeroespacial, química e farmacêutica ou Demais setores | Aeroespacial |
| Tamanho Estabelecimento | inteiro | Código RAIS da faixa de vínculos (1 a 10); use para ordenar a Faixa de Porte | 2 |
| Faixa de Porte ⭐ | texto | Vínculos ativos em 31/12: Zero, 1 a 4, 5 a 9 … 1.000 ou mais | 1 a 4 |
| Porte SEBRAE | texto | Micro, Pequena, Média, Grande ou Sem vínculos | Micro |
| Tipo Estab_1 ⭐ | texto | Cnpj (empresa), Caepf (empregador pessoa física) ou Cno (obra) | Cnpj |
| Situação Vínculo ⭐ | texto | Com vínculo = RAIS positiva; Sem vínculo = RAIS negativa ou indicador 2 (DEC-011) | Com vínculo |
| Situação Detalhada | texto | Com vínculos em 31/12; Sem vínculos em 31/12 (não negativa); RAIS negativa; Indicador 2 (DEC-019) | Com vínculos em 31/12 |
| Ind Rais Negativa | inteiro | Código original: 0 = positiva, 1 = negativa, 2 = não documentado | 0 |
| Atividade no Ano | texto | Sim = teve atividade em algum momento de 2024 | Sim |
| Qtd Vínculos Ativos | inteiro | Empregos formais ativos em 31/12/2024 | 3 |
| Qtd Vínculos CLT | inteiro | Parte dos vínculos sob CLT | 3 |
| Qtd Vínculos Estatutários | inteiro | Parte dos vínculos de servidores estatutários | 0 |
| Natureza Jurídica | texto | Código CONCLA da forma jurídica | 2062 |
| Natureza Descrição | texto | Nome da forma jurídica | Sociedade Empresária Limitada |
| Natureza Grupo | texto | Entidades empresariais, sem fins lucrativos, pessoas físicas ou ignorado | Entidades empresariais |
| Simples | texto | Sim = optante pelo Simples Nacional | Sim |
| IBGE Subsetor | texto | Código da classificação antiga do IBGE (26 subsetores) | 21 |
| IBGE Subsetor Descrição | texto | Nome do subsetor IBGE | Alojamento, alimentação, reparação e manutenção |

## Totais de conferência

| Indicador | Valor |
|---|---|
| Estabelecimentos | 47.339 |
| Vínculos ativos em 31/12/2024 | 206.717 |
| Com vínculos em 31/12 / RAIS negativa | 15.058 / 30.470 |
| Com região oficial | 47.334 (99,99%) |
| Com ponto no mapa | 37.084 (78,3%) |
