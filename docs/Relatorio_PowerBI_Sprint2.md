# Relatório do Power BI — Sprint 2

> Versão em Markdown de [`Relatorio_PowerBI_Sprint2.docx`](Relatorio_PowerBI_Sprint2.docx). Painel descrito: [`powerbi/Powerbi_API_Sprint2.pbix`](../powerbi/Powerbi_API_Sprint2.pbix) ([PDF](../powerbi/Powerbi_API_Sprint2.pdf)).

## 1. De onde vêm os dados

Os dados vêm da base **RAIS Estabelecimentos 2024**, do Ministério do Trabalho. Cada linha é um estabelecimento. Tudo está na tabela `RAIS_SJC`, que já contém o CEP, o setor CNAE, o porte, o tipo de estabelecimento e a quantidade de vínculos.

Como agrupador foi usada a **Seção CNAE 2.0**, que tem 21 letras (G, C, N, Q…). Ela vem dos dois primeiros dígitos do CNAE (a divisão); onde a divisão não cai em nenhuma seção, vira "Não classificado".

**Por que Seção:** ela dá a visão geral. Para ver cada cadeia produtiva (aeronaves, automóveis, química), abre-se por setor — a Seção C junta várias cadeias diferentes, então ela sozinha não basta.

## 2. Medidas (fórmulas DAX)

Medida é uma conta que o Power BI refaz toda vez que você mexe num filtro.

| Medida | O que faz | Resultado |
|---|---|---|
| Total de Estabelecimentos | Conta as linhas da tabela (cada estabelecimento vale 1) | 47.339 |
| Estabelecimentos Com Vínculo | Conta as linhas com situação "Com Vínculo" | 16.816 |
| Estabelecimentos Sem Vínculo | Conta as linhas com situação "Sem Vínculo" | 30.523 |
| % Com Vínculo / % Sem Vínculo | Divide cada contagem pelo total | 35,52% / 64,48% |
| Total Vínculos Ativos | Soma os vínculos ativos em 31/12 | 206.717 |
| Total Vínculos CLT | Soma só os vínculos CLT (a diferença de 91 são os estatutários) | 206.626 |
| % Participação Estab / % Participação Vínculos | Valor de cada Seção ÷ total de todas as Seções | por Seção |

```dax
Total de Estabelecimentos = COUNTROWS ( 'RAIS_SJC' )
Estabelecimentos Com Vínculo = CALCULATE ( COUNTROWS ( 'RAIS_SJC' ), 'RAIS_SJC'[Situação Vínculo] = "Com Vínculo" )
Estabelecimentos Sem Vínculo = CALCULATE ( COUNTROWS ( 'RAIS_SJC' ), 'RAIS_SJC'[Situação Vínculo] = "Sem Vínculo" )
% Com Vínculo = DIVIDE ( [Estabelecimentos Com Vínculo], [Total de Estabelecimentos] )
% Sem Vínculo = DIVIDE ( [Estabelecimentos Sem Vínculo], [Total de Estabelecimentos] )
```

## 3. Como os estabelecimentos são somados

Cada linha representa 1 estabelecimento, e o filtro define quais entram na contagem: se um setor é selecionado, o total considera só os estabelecimentos daquele setor.

- **"Sem vínculo"** não quer dizer desempregados: o estabelecimento declarou na RAIS que não tinha empregados formais. Dos 30.523 sem vínculo, 30.470 declararam não ter empregados (RAIS negativa) e 53 aparecem com valor 2, que não tem significado definido no dicionário.
- **"Com vínculo"** (16.816) inclui 1.758 estabelecimentos que tiveram algum vínculo no ano, mas nenhum funcionário ativo em 31/12. De fato, **15.058** tinham funcionário ativo no fim do ano.
- Por isso a faixa de porte **"Zero"** tem **32.281** estabelecimentos: os 30.523 sem vínculo + os 1.758 que terminaram o ano sem funcionário ativo.

## 4. Página 1 — KPIs e Mapa

![Página KPIs e Mapa](../evidencias/sprint2/painel_kpis_mapa.png)

- **Cartões:** total, sem vínculo, com vínculo e total de vínculos ativos.
- **Pizza:** 64,48% sem vínculo × 35,52% com vínculo.
- **Mapa:** cada ponto é um CEP, colorido por situação. Muitos estabelecimentos no mesmo CEP caem no mesmo ponto, então a localização é aproximada.
- **Filtros:** setor (Seção CNAE), porte e tipo de estabelecimento.

## 5. Página 2 — Setor de Atividades (CNAE)

![Página Setor de Atividades](../evidencias/sprint2/painel_setor_atividades.png)

- **Top 10 por empregos:** as 10 classes CNAE com mais vínculos, agrupadas pelo nome do setor. Na frente: aeronaves, atendimento hospitalar e restaurantes.
- **Top 10 por estabelecimentos:** na frente, atenção ambulatorial, restaurantes e serviços de escritório.
- **% de participação por Seção:** barra escura = peso em empregos; barra clara = peso em estabelecimentos. Onde a escura é maior, o setor emprega mais do que o número de estabelecimentos sugere (a indústria, por exemplo).
- **Tabela:** faixa de porte, setor e vínculos CLT. O total é 67.837 (não 206.717) porque a tabela tem um filtro que mostra só as 16 classes CNAE dos rankings.

## 6. O que ainda falta (backlog da Sprint 2)

- **Cruzamento com o PIB:** a tabela do IBGE ainda não está neste modelo. *(A página "PIB e Emprego" existe na versão anterior do painel, [`PowerbiATT_Api_Sprint2.pbix`](../powerbi/PowerbiATT_Api_Sprint2.pbix), e precisa ser trazida para esta.)*
- **Região:** a classificação por região oficial está pronta na base `dados/RAIS_SJC_2024_PowerBI.csv`, mas ainda não entrou no painel.
- **Setores em alta:** a tabela só tem 2024, então não dá para falar em tendência; o painel mostra "setores com mais vínculos em 2024".

## 7. Perguntas que o cliente pode fazer

| Pergunta | Resposta |
|---|---|
| O que é "sem vínculo"? | Estabelecimentos que declararam não ter empregados formais. Não são pessoas desempregadas. |
| Por que Seção CNAE? | É a visão geral. Para ver cada cadeia, abrimos por setor. |
| Por que 64,48% e não 64,37%? | A diferença são os 53 estabelecimentos com valor 2 no indicador de RAIS negativa: eles foram contados como "sem vínculo" (DEC-011). 64,37% é só a RAIS negativa (30.470 ÷ 47.339). |
