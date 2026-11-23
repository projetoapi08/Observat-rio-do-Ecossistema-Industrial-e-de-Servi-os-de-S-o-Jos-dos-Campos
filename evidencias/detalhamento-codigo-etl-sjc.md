> Versão em Markdown de [`detalhamento-codigo-etl-sjc.docx`](detalhamento-codigo-etl-sjc.docx), para leitura direta no GitHub. Em caso de diferença, vale o .docx. · [voltar ao README](../README.md)

**Observatório do Ecossistema Industrial e de Serviços de SJC**

**Manual Técnico e Detalhamento Completo do Pipeline de ETL em Python (RAIS / Colab)**

# 1. Visão Geral e Contexto do Pipeline de Dados

**O desenvolvimento do Observatório do Ecossistema Industrial e de Serviços de São José dos Campos exigiu a construção de uma infraestrutura robusta de engenharia de dados. A fonte primária empregada para o mapeamento de empregos formais e estabelecimentos produtivos é a base nacional da Relação Anual de Informações Sociais (RAIS), disponibilizada publicamente pelo Ministério do Trabalho e Emprego (MTE).t**

**Trabalhar com dados governamentais brutos em escala nacional apresenta gargalos de desempenho severos:**

- **Volume Massivo de Dados: A base nacional de estabelecimentos (RAIS_ESTAB_PUB) possui 12.643.067 de registros e um tamanho de aproximadamente 3,27 GB no formato texto descompactado.**

- **Limitação de Memória RAM: Tentativas de carregar o arquivo integral diretamente na memória via ferramentas convencionais (como Excel ou funções padrão do Pandas como pd.read_csv()) provocam estouro de memória (Out-Of-Memory) no ambiente gratuito do Google Colab (limitado a 12 GB RAM).**

- **Inconsistências e Ruídos Estruturais: Presença de 64,37% de registros com vínculos zerados (RAIS Negativa), falta de identificação nominativa de empresas por sigilo legal e mistura de cadastros jurídicos (CNPJ, CAEPF e CNO).**

| **📌 SOLUÇÃO DE ARQUITETURA: Para contornar o problema da memória RAM, a equipe desenvolveu uma estratégia baseada em leitura por streaming (processamento sequencial linha por linha), permitindo filtrar com precisão os 47.339 estabelecimentos do município de São José dos Campos (código IBGE 354990) em poucos segundos, utilizando apenas pacotes nativos do Python.** |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

# 2. Arquitetura do Pipeline de ETL (Extract, Transform, Load)

**O pipeline foi dividido estritamente nas três fases fundamentais da engenharia de dados, garantindo rastreabilidade e reprodutibilidade acadêmica:**

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 35%" />
<col style="width: 46%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Etapa ETL</strong></th>
<th><strong>Operação Realizada</strong></th>
<th><strong>Resultado / Métricas</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>EXTRACT<br />
(Extração)</strong></td>
<td><strong>Abertura direta do pacote compactado .zip no Google Colab, lendo o arquivo texto .txt via streaming com a biblioteca csv e io.TextIOWrapper.</strong></td>
<td><strong>12.643.067 registros nacionais varridos sem necessidade de descompactar o arquivo no disco rígido.</strong></td>
</tr>
<tr class="even">
<td><strong>TRANSFORM<br />
(Transformação)</strong></td>
<td><strong>1. Filtro estrito do município de SJC (IBGE 354990).<br />
2. Tratamento do padding e codificação Latin-1.<br />
3. Classificação de vínculos (DEC-001).<br />
4. Segmentação jurídica (CNPJ/CAEPF/CNO - DEC-002).<br />
5. Inserção do ano-base 2024 (DEC-003).</strong></td>
<td><strong>Isolamento de 47.339 estabelecimentos em SJC:<br />
• 16.869 Ativos (35,63%)<br />
• 30.470 RAIS Negativa (64,37%)<br />
• 46.244 Pessoas Jurídicas (CNPJ)</strong></td>
</tr>
<tr class="odd">
<td><strong>LOAD<br />
(Carga)</strong></td>
<td><strong>Exportação dos dados limpos em arquivos .csv estruturados para ingestão no Power BI e gravação do relatório estatístico em estatisticas_etl.json.</strong></td>
<td><strong>Arquivos gerados:<br />
• RAIS_SJC_completo.csv<br />
• RAIS_SJC_ativos.csv<br />
• RAIS_SJC_Cnpj.csv<br />
• estatisticas_etl.json</strong></td>
</tr>
</tbody>
</table>

# 3. Detalhamento Linha a Linha do Código Python (ETL_RAIS_SJC.ipynb)

**Abaixo está a decomposição didática dos quatro blocos de código que compõem o notebook de ETL, ideal para revisão acadêmica e apresentação técnica.**

## Bloco 1: Importação de Módulos Nativos e Parâmetros globais

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>import zipfile</strong><br />
<strong>import io</strong><br />
<strong>import csv</strong><br />
<strong>import json</strong><br />
<strong># Definição de parâmetros estruturais do pipeline</strong><br />
<strong>ARQUIVO_ZIP = 'RAIS_ESTAB_PUB.zip'</strong><br />
<strong>CODIGO_MUNICIPIO_SJC = '354990' # Código oficial IBGE para São José dos Campos</strong><br />
<strong>ENCODING_ORIGEM = 'latin-1' # Encodagem padrão dos arquivos governamentais do MTE</strong><br />
<strong>DELIMITADOR = ';' # Separador de colunas utilizado na RAIS</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

***Análise do trecho: Utilização exclusiva de bibliotecas nativas do Python (zipfile, io, csv, json). Isso elimina a necessidade de instalação de dependências pesadas e garante execução instantânea em qualquer ambiente Python 3.***

## Bloco 2: Configuração de Contadores e Leitura por Streaming

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong># Dicionário de métricas em tempo real para auditoria</strong><br />
<strong>contadores = {</strong><br />
<strong>'total_nacional': 0,</strong><br />
<strong>'total_sjc': 0,</strong><br />
<strong>'ativos_sjc': 0,</strong><br />
<strong>'rais_negativa_sjc': 0,</strong><br />
<strong>'cnpj': 0,</strong><br />
<strong>'caepf': 0,</strong><br />
<strong>'cno': 0</strong><br />
<strong>}</strong><br />
<strong>registros_sjc = []</strong><br />
<strong># Abertura do arquivo zip sem extração para o disco</strong><br />
<strong>with zipfile.ZipFile(ARQUIVO_ZIP, 'r') as z:</strong><br />
<strong>nome_arquivo_txt = z.namelist()[0]</strong><br />
<strong>with z.open(nome_arquivo_txt) as f_binario:</strong><br />
<strong># Conversão de fluxo binário para texto via io.TextIOWrapper</strong><br />
<strong>f_texto = io.TextIOWrapper(f_binario, encoding=ENCODING_ORIGEM)</strong><br />
<strong>leitor = csv.DictReader(f_texto, delimiter=DELIMITADOR)</strong><br />
<strong>for linha in leitor:</strong><br />
<strong>contadores['total_nacional'] += 1</strong><br />
<strong># FILTRO CRÍTICO: Isola apenas os dados de São José dos Campos</strong><br />
<strong>if linha.get('Município', '').strip() == CODIGO_MUNICIPIO_SJC:</strong><br />
<strong>contadores['total_sjc'] += 1</strong><br />
<strong># ... [continua no Bloco 3]</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

***Análise do trecho: A combinação de zipfile.open + io.TextIOWrapper + csv.DictReader cria um ponteiro de leitura sequencial. O Python processa linha por linha e descarta o registro nacional da memória RAM imediatamente após verificar que ele não pertence a SJC.***

## Bloco 3: Aplicação de Regras de Negócio e Decisões de Dados (DEC-001 a DEC-003)

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong># Limpeza de caracteres e espaços de padding em chaves e valores</strong><br />
<strong>linha_limpa = {k.strip(): v.strip() for k, v in linha.items()}</strong><br />
<strong># Regra DEC-001: Classificação da RAIS Negativa (vínculos zerados)</strong><br />
<strong>qtd_vinculos = int(linha_limpa.get('Qtd Vínculos Ativos', 0))</strong><br />
<strong>if qtd_vinculos &gt; 0:</strong><br />
<strong>linha_limpa['possui_vinculo_ativo'] = '1'</strong><br />
<strong>contadores['ativos_sjc'] += 1</strong><br />
<strong>else:</strong><br />
<strong>linha_limpa['possui_vinculo_ativo'] = '0'</strong><br />
<strong>contadores['rais_negativa_sjc'] += 1</strong><br />
<strong># Regra DEC-002: Segmentação por Natureza Jurídica</strong><br />
<strong>tipo_estab = linha_limpa.get('Tipo Estab', '').strip().upper()</strong><br />
<strong>if 'CNPJ' in tipo_estab or tipo_estab == '1':</strong><br />
<strong>linha_limpa['tipo_estabelecimento'] = 'CNPJ'</strong><br />
<strong>contadores['cnpj'] += 1</strong><br />
<strong>elif 'CAEPF' in tipo_estab or tipo_estab == '2':</strong><br />
<strong>linha_limpa['tipo_estabelecimento'] = 'CAEPF'</strong><br />
<strong>contadores['caepf'] += 1</strong><br />
<strong>elif 'CNO' in tipo_estab or tipo_estab == '3':</strong><br />
<strong>linha_limpa['tipo_estabelecimento'] = 'CNO'</strong><br />
<strong>contadores['cno'] += 1</strong><br />
<strong># Regra DEC-003: Fixação explícita do Ano-Base de referência</strong><br />
<strong>linha_limpa['Ano_Base'] = '2024'</strong><br />
<strong>registros_sjc.append(linha_limpa)</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

***Análise do trecho: Aplica as transformações das Decisões de Dados registradas oficialmente no projeto: cria indicadores binários para filtrar estabelecimentos ativos versus inativos e normaliza a tipologia jurídica para evitar misturar empresas formais com produtores rurais ou obras.***

## Bloco 4: Exportação dos Arquivos CSV e Relatório JSON

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>colunas_saida = list(registros_sjc[0].keys())</strong><br />
<strong># 1. Exportação da Base Completa (47.339 registros)</strong><br />
<strong>with open('RAIS_SJC_completo.csv', 'w', newline='', encoding='utf-8') as f:</strong><br />
<strong>writer = csv.DictWriter(f, fieldnames=colunas_saida)</strong><br />
<strong>writer.writeheader()</strong><br />
<strong>writer.writerows(registros_sjc)</strong><br />
<strong># 2. Exportação da Base de Ativos (16.869 registros - Padrão para Emprego)</strong><br />
<strong>with open('RAIS_SJC_ativos.csv', 'w', newline='', encoding='utf-8') as f:</strong><br />
<strong>writer = csv.DictWriter(f, fieldnames=colunas_saida)</strong><br />
<strong>writer.writeheader()</strong><br />
<strong>writer.writerows([r for r in registros_sjc if r['possui_vinculo_ativo'] == '1'])</strong><br />
<strong># 3. Exportação da Base de Pessoas Jurídicas (46.244 CNPJs)</strong><br />
<strong>with open('RAIS_SJC_Cnpj.csv', 'w', newline='', encoding='utf-8') as f:</strong><br />
<strong>writer = csv.DictWriter(f, fieldnames=colunas_saida)</strong><br />
<strong>writer.writeheader()</strong><br />
<strong>writer.writerows([r for r in registros_sjc if r['tipo_estabelecimento'] == 'CNPJ'])</strong><br />
<strong># 4. Gravação das Estatísticas de Auditoria em JSON</strong><br />
<strong>with open('estatisticas_etl.json', 'w', encoding='utf-8') as f_json:</strong><br />
<strong>json.dump(contadores, f_json, indent=4, ensure_ascii=False)</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

***Análise do trecho: A gravação em múltiplos arquivos otimiza a performance no Power BI. O analista pode carregar apenas a tabela de estabelecimentos ativos para painéis de emprego, reduzindo o tempo de atualização do dashboard.***

# 4. Log de Decisões de Dados (DEC-001 a DEC-005)

**Para assegurar a transparência metodológica exigida pela Fatec e pelo cliente (CADI / Prefeitura de SJC), todas as escolhas de tratamento de dados foram registradas no Log de Decisões de Dados (inspirado no padrão Architecture Decision Records - ADR):**

| **Código ADR** | **Problema Identificado na RAIS**                                                                        | **Decisão Técnica e Impacto no Painel**                                                                                                                                           |
|----------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DEC-001**    | **64,37% dos registros (30.470) possuem zero vínculos empregatícios ativos (RAIS Negativa).**            | **Manter os registros no banco para servir como indicador de 'densidade empresarial', mas separar em uma flag (possui_vinculo_ativo) para não distorcer as análises de emprego.** |
| **DEC-002**    | **A base mistura empresas (CNPJ), pessoas físicas autônomas (CAEPF) e obras de construção civil (CNO).** | **Segmentar a base por tipo. O recorte padrão do Observatório utiliza exclusivamente Pessoas Jurídicas (46.244 CNPJs), mantendo filtros opcionais para CAEPF e CNO.**             |
| **DEC-003**    | **A base pública da RAIS não traz o campo de ano na estrutura das colunas.**                             | **Fixar o ano-base de referência como 2024 de forma explícita na transformação do Python para permitir análises temporais futuras.**                                              |
| **DEC-004**    | **Por sigilo legal, a RAIS pública omite a Razão Social e o CNPJ completo dos estabelecimentos.**        | **Apresentar rankings de contratantes de forma agregada por setor econômico (CNAE) e região geográfica, sem expor nomes individuais de empresas.**                                |
| **DEC-005**    | **Defasagem temporal entre a RAIS (2024) e o PIB dos Municípios do IBGE (série mais recente 2023).**     | **Declarar formalmente a defasagem de 1 ano nas notas metodológicas do painel ao cruzar dados de emprego com produtividade econômica.**                                           |

# 5. Modelagem em Estrela (Star Schema) e Geocodificação no Power BI

**Os arquivos \`.csv\` gerados pelo Python são importados no Power BI e organizados sob um modelo relacional Star Schema (Esquema em Estrela), garantindo performance de consulta e simplicidade na navegação por gestores públicos:**

- **Tabela Fato (Fato_RAIS): Contém os 47.339 registros e as métricas numéricas (soma de vínculos ativos, contagem de estabelecimentos, indicadores de RAIS negativa).**

- **Tabela Fato Auxiliar (Fato_PIB_IBGE): Armazena os dados de Valor Adicionado Bruto e PIB de SJC (2023).**

- **Tabela Dimensão (Dim_Setor_CNAE): Conecta-se à fato via código CNAE_2_0 em relacionamento 1:N, permitindo agrupar por Seção, Divisão e Atividade Econômica.**

- **Tabela Dimensão (Dim_Geografia_CEP): Conecta-se à fato via CEP_Estab para plotagem espacial. Fundamentada na literatura científica de geolocalização de empregos no Brasil (Morelli, Fiedler & Cunha, 2023), permitindo identificar polos industriais, distritos comerciais e vazios logísticos no município.**

# 6. Guia Prático para Apresentação Acadêmica e Feira de Soluções

**Ao defender o projeto perante a banca avaliadora da Fatec ou na Feira de Soluções (03/dez), os estudantes de Logística devem enfatizar as seguintes respostas técnicas:**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>📌 PERGUNTA FREQUENTE DA BANCA #1: Pergunta da Banca: 'Por que utilizaram Python e não importaram o arquivo da RAIS direto no Power BI?'<br />
Resposta Recomendada: 'O arquivo bruto nacional da RAIS possui 12,6 milhões de linhas e 3,27 GB. Importar diretamente no Power BI causaria travamento por limite de RAM. O Python atuou no pré-processamento via streaming no Colab, filtrando apenas os 47.339 registros de SJC e reduzindo o tamanho do arquivo para poucos megabytes, tornando a atualização do Power BI instantânea.'</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>📌 PERGUNTA FREQUENTE DA BANCA #2: Pergunta da Banca: 'Como lidaram com os 64% de empresas sem funcionários?'<br />
Resposta Recomendada: 'Registramos a decisão DEC-001 no nosso Log de Decisões de Dados. A pedido do cliente (CADI/Prefeitura), mantivemos esses 30.470 registros como um indicador de densidade empresarial na cidade. No entanto, criamos um filtro lógico que isola os 16.869 estabelecimentos ativos para garantir que os rankings de emprego reflitam a realidade de contratações.'</strong></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

**Documento gerado automaticamente para o repositório técnico do Observatório do Ecossistema Industrial e de Serviços de SJC — Fatec São José dos Campos (2026).**
