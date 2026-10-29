# Relatório do Power BI — Sprint 2

> Versão em Markdown de [`Relatorio_PowerBI_Sprint2.docx`](Relatorio_PowerBI_Sprint2.docx). Painel LogMulti, Observatório de São José dos Campos, versão de 26/10/2026.
>
> **Painel online:** [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) · Arquivo: [`powerbi/pbip/`](../powerbi/pbip/) · [PDF](../powerbi/Powerbi_API_Sprint2.pdf) · Código das medidas: [`Formulas_PowerBI_Sprint2.md`](Formulas_PowerBI_Sprint2.md)

O painel tem 4 páginas: **KPIs e Mapa**, **Setor de Atividades (CNAE)**, **PIB e Emprego** e **Notas Metodológicas**.

## 1. De onde vêm os dados

A base principal é a **RAIS Estabelecimentos 2024**, do Ministério do Trabalho e Emprego. Cada linha é um estabelecimento: 47.339 em São José dos Campos.

| Tabela | Conteúdo |
|---|---|
| `RAIS_SJC` | Base da RAIS, com CEP, setor, porte, tipo de estabelecimento e quantidade de vínculos |
| `Cruzamento`, `PIB anual`, `VAB setorial` | Dados do IBGE (PIB dos Municípios), tratados pelo grupo em Excel |
| `CEP x Região` | Região oficial de cada CEP e a latitude e a longitude usadas no mapa |
| `dCNAE` | As 673 classes da CNAE 2.0 com o nome de cada uma, para dar nome aos setores |

- **Seção CNAE:** agrupador de 21 letras (G, C, N, Q…), calculado a partir dos dois primeiros dígitos do código CNAE (a divisão). Se a divisão não cai em nenhuma Seção, o estabelecimento fica como "Não classificado". A Seção dá a visão geral; para ver cada cadeia produtiva (aeronaves, automóveis, química) abre-se por setor, porque a Seção C junta cadeias diferentes. É a mesma lógica do IBGE (DEC-014).
- **Setor:** nome da atividade (classe CNAE). Alguns nomes foram encurtados pelo grupo; os demais vêm da tabela `dCNAE`. Agora todas as atividades aparecem com nome (coluna `Setor Completo`).
- **Situação Vínculo:** criada no Power Query. RAIS negativa = 0 → "Com Vínculo"; qualquer outro valor (1 ou 2) → "Sem Vínculo". Os 53 registros com valor 2 entram em "Sem Vínculo" (DEC-011).

## 2. As medidas

Medida é uma conta que o Power BI refaz toda vez que você mexe num filtro. O código DAX está em [`Formulas_PowerBI_Sprint2.md`](Formulas_PowerBI_Sprint2.md).

| Medida | O que faz | Resultado |
|---|---|---|
| Total de Estabelecimentos | Conta as linhas da tabela | 47.339 |
| Estabelecimentos Com Vínculo | Conta só os "Com Vínculo" | 16.816 |
| Estabelecimentos Sem Vínculo | Conta só os "Sem Vínculo" | 30.523 |
| % Com Vínculo / % Sem Vínculo | Cada contagem dividida pelo total | 35,52% / 64,48% |
| Total Vínculos Ativos | Soma os vínculos ativos em 31/12 (cartões e % por Seção) | 206.717 |
| Total Vínculos CLT | Soma só os CLT (gráficos e tabela da página 2); a diferença de 91 são estatutários | 206.626 |
| % Participação Estab / Vínculos | Valor de cada Seção dividido pelo total de todas as Seções | por Seção |

A página PIB e Emprego não tem medidas novas: usa colunas prontas da planilha do IBGE. O modelo tem ainda medidas do recorte automotivo e de vínculos estatutários (pastas "Medidas" e "Automotivo"), que por enquanto não aparecem em nenhum visual.

## 3. Como os estabelecimentos são somados

Cada linha da base é 1 estabelecimento, e o filtro define quais entram na conta.

- **"Sem vínculo" não quer dizer desempregados:** o estabelecimento declarou na RAIS que não tinha empregados formais. Dos 30.523 sem vínculo, 30.470 declararam não ter empregados e 53 têm valor 2, sem significado definido.
- Os 16.816 **com vínculo** incluem 1.758 que tiveram vínculo no ano mas nenhum funcionário ativo em 31/12. Então **15.058** tinham funcionário ativo no fim do ano.
- Por isso a faixa de porte **"Zero"** tem **32.281** estabelecimentos: 30.523 sem vínculo + 1.758 que terminaram o ano sem funcionário ativo.

## 4. Página 1 — KPIs e Mapa

![Página KPIs e Mapa](../evidencias/sprint2/painel_kpis_mapa.png)

- **Cartões:** total de estabelecimentos (47.339), sem vínculo (30.523), com vínculo (16.816) e total de vínculos ativos (206.717), cada um com uma frase dizendo o que mede.
- **Percentuais e pizza:** 64,48% sem vínculo e 35,52% com vínculo.
- **Mapa:** cada ponto é o local de um CEP, colorido pela situação do vínculo, usando a latitude e a longitude da geocodificação do grupo. Muitos estabelecimentos dividem o mesmo CEP e alguns CEPs são genéricos, por isso a localização é aproximada. Estabelecimentos sem coordenadas não aparecem no mapa.
- **Filtros:** setor (Seção CNAE), porte (vínculos ativos), tipo de estabelecimento e região. Ao lado do mapa, uma lista para escolher entre "Com vínculo" e "Sem vínculo".
- **Rodapé:** Base: RAIS Estabelecimentos 2024 (linha) · Setor: Seção CNAE 2.0.

## 5. Página 2 — Setor de Atividades (CNAE)

![Página Setor de Atividades](../evidencias/sprint2/painel_setor_atividades.png)

Subtítulo: "Comparação entre estabelecimentos e vínculos CLT".

- **Top 10 por empregos:** setores com mais vínculos CLT em 31/12/2024. Na frente: fabricação de aeronaves, atendimento hospitalar e restaurantes.
- **Top 10 por estabelecimentos:** na frente, atenção ambulatorial, restaurantes e serviços de escritório.
- **% de participação por Seção:** barra escura = peso nos empregos; barra clara = peso nos estabelecimentos. Onde a escura é maior, o setor emprega mais do que o número de estabelecimentos faz parecer (a indústria, por exemplo).
- **Indústria (Seção C), empregos CLT por setor:** abre a Seção C atividade por atividade e responde "o que tem dentro da indústria?". Na frente: aeronaves, automóveis e instrumentos e materiais de uso médico e odontológico.
- **Tabela:** faixa de porte, setor e vínculos CLT, sem filtro de classe, com o total da base inteira (206.626). As faixas vão de "1000 ou mais" para a menor.

## 6. Página 3 — PIB e Emprego

![Página PIB e Emprego](../evidencias/sprint2/painel_pib_emprego.png)

Compara o emprego formal da RAIS 2024 com o valor adicionado do IBGE (PIB dos Municípios, Sidra tabela 5938, extração de 08/10/2026).

- A Administração pública fica fora (DEC-013).
- Valores reais em R$ de 2023, corrigidos pelo IPCA (DEC-008).
- O IBGE só detalha o setor até 2021, por isso o valor adicionado de 2021 é comparado com o emprego de 2024 (DEC-006 e DEC-009).

| Visual | O que mostra |
|---|---|
| Peso de cada setor (colunas) | % do emprego (RAIS 2024) × % do valor adicionado (IBGE 2021). Indústria 24,68% × 45,79%; Serviços 75,28% × 54,14%; Agropecuária 0,04% × 0,07% |
| Tabela de produtividade relativa | Vínculos, % do emprego, % do valor e produtividade relativa: Indústria 1,86, Agropecuária 1,65 e Serviços 0,72. Total desligado, porque somar índices não faz sentido |
| PIB de 2002 a 2023 (linha) | Em R$ de 2023. O PIB de SJC chegou a R$ 61,4 bilhões em 2023 (1,78% do PIB de São Paulo) |
| Variação anual do PIB (barras) | Crescimento ou queda em relação ao ano anterior, como a queda de 13,5% em 2020 |
| Valor adicionado por setor, 2002–2021 | Indústria perdendo peso (52,7% em 2002 e 42,4% em 2021) e serviços ganhando (40,6% e 50,1%) |
| Caixa "O que isso mostra para a gestão" | Os serviços concentram a maior parte dos empregos; a indústria gera mais valor em proporção ao número de empregos |

A tabela soma **204.331** vínculos (só CNPJ, sem Administração pública), diferente dos **206.717** do cartão da página 1, que inclui também CAEPF (1.419), CNO (855) e Administração pública (112).

## 7. Filtro de região

A tabela `CEP x Região` (planilha [`Regioes_SJC_filtro_por_regiao.xlsx`](../powerbi/fontes/Regioes_SJC_filtro_por_regiao.xlsx)) liga-se à `RAIS_SJC` pela coluna `CEP Estab` (muitos para um). O filtro é a lista suspensa "Região" da página 1.

As regiões seguem a divisão oficial da Prefeitura (Plano Diretor, "Leitura técnica do Município"): o bairro de cada CEP, vindo da geocodificação do grupo, foi comparado com a lista de bairros por região desse documento.

| Região | Estabelecimentos | % |
|---|---:|---:|
| Sul | 13.698 | 28,9% |
| Centro | 13.331 | 28,2% |
| Oeste | 10.137 | 21,4% |
| Leste | 5.921 | 12,5% |
| Norte | 1.893 | 4,0% |
| Sudeste | 1.756 | 3,7% |
| Sem região | 603 | 1,3% |
| **Total** | **47.339** | **100%** |

A soma fecha nos mesmos totais do painel (47.339 estabelecimentos e 206.717 vínculos). Como cada região foi decidida: 75,8% estão na lista da Prefeitura; 10,7% estão na lista com grafia um pouco diferente ("Eugênio de Mello" × "Eugênio de Melo"); 11,4% têm CEP genérico e recebem a região do bairro de referência (aproximada); 0,8% (16 bairros) não estão na lista e foram classificados pelos vizinhos mais próximos; 1,3% ficam sem região (sem bairro, sem coordenadas ou sem CEP). A planilha tem uma aba "Revisar" com os casos duvidosos.

> Esta classificação do painel é a da planilha do grupo. A base única do notebook 02 ([`dados/RAIS_SJC_2024_PowerBI.csv`](../dados/RAIS_SJC_2024_PowerBI.csv)) chega a 99,99% com região; unificar as duas fica para a Sprint 3 (DEC-015).

## 8. Página 4 — Notas Metodológicas

![Página Notas Metodológicas](../evidencias/sprint2/painel_notas_metodologicas.png)

Reúne as regras do painel em cinco blocos:

1. **Limites:** só emprego formal; CEP genérico no mapa; linhas idênticas mantidas; diferença entre 204.331 e 206.717.
2. **Cruzamento PIB:** anos diferentes, valores reais, Administração pública e produtividade relativa.
3. **Decisões do grupo:** DEC-011 e DEC-014.
4. **Ferramentas:** uso de IA, Power Query, Excel e validação.
5. **Definições:** com vínculo, sem vínculo, vínculo ativo, Seção CNAE e porte.

Traz também uma linha com a base e a fonte dos dados.

## 9. Perguntas que podem aparecer

| Pergunta | Resposta |
|---|---|
| O que é "sem vínculo"? | Estabelecimentos que declararam não ter empregados formais. Não são pessoas desempregadas. |
| Por que Seção CNAE? | Porque dá a visão geral. Para ver cada cadeia, abrimos por setor — por isso a página 2 tem a indústria (Seção C) aberta por setor. |
| Por que 64,48% e não 64,37%? | O painel usa 64,48% (30.523 de 47.339), que inclui os 53 com valor 2 (DEC-011). Os 64,37% contam só os 30.470 que declararam não ter empregados. |
| Por que o PIB é de 2021 e o emprego de 2024? | O IBGE só detalha o valor adicionado por setor até 2021. Comparamos a estrutura de cada setor, sem cálculo de causa e efeito. |
| O que é produtividade relativa? | % do valor adicionado do setor ÷ % do emprego do setor. Acima de 1, o setor gera mais valor do que a sua fatia de empregos. |
| Por que a Administração pública ficou fora? | Porque a RAIS pública não traz esses órgãos (DEC-013). O emprego do cruzamento é privado. |
| Por que 204.331 na página 3 e 206.717 na página 1? | O cruzamento usa só CNPJ e sem Administração pública. O cartão inclui CAEPF (1.419), CNO (855) e Administração pública (112). |
| Como foram definidas as regiões? | Pela divisão oficial da Prefeitura, usando o bairro do CEP de cada estabelecimento. Parte dos CEPs é genérica, por isso a região é aproximada. |
| Dá para falar em setores em alta? | Não. A base só tem 2024, então não há tendência. Falamos em "setores com mais vínculos em 2024". |
