# Fórmulas do painel Power BI — versão final

> Versão em Markdown de [`Formulas_PowerBI_Sprint2.docx`](Formulas_PowerBI_Sprint2.docx). O código abaixo foi copiado do próprio modelo publicado ([`powerbi/pbip/`](../powerbi/pbip/), tabela `RAIS_SJC`), então é exatamente o que o painel usa. Painel online: [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9).

## 1. Colunas criadas no Power Query (linguagem M)

**Situação Vínculo** — separa "com vínculo" e "sem vínculo" (DEC-011):

```m
Table.AddColumn(#"Tipo Alterado1", "Situação Vínculo",
    each if [Ind Rais Negativa] = "0" then "Com Vínculo" else "Sem Vínculo")
```

Se o estabelecimento declarou 0 na "RAIS negativa", ele tem vínculo. Qualquer outro valor (1 ou 2) vira "Sem Vínculo". Por isso os 53 registros com valor 2 entram em "Sem Vínculo".

**Seção CNAE** — sai dos 2 primeiros dígitos da classe CNAE (a divisão), comparados com o limite de cada Seção (DEC-014):

```m
Table.AddColumn(#"Tipo Alterado6", "Seção CNAE", each let
  d = try Number.From(Text.Start(Text.PadStart(Text.From([CNAE 2.0 Classe]), 5, "0"), 2)) otherwise 0,
  lim = {3,9,33,35,39,43,47,53,56,63,66,68,75,82,84,85,88,93,96,97,99},
  nomes = {"A - Agricultura e pecuária", "B - Indústrias extrativas", "C - Indústrias de transformação", ... , "U - Organismos internacionais"},
  pos = List.PositionOf(List.Transform(lim, each d <= _), true)
in
  if d = 0 or pos = -1 then "Não classificado" else nomes{pos})
```

Exemplo: a classe 30415 (aeronaves) tem divisão 30; o primeiro limite maior ou igual a 30 é 33, que é a Seção C.

**Setor Completo** — usa o nome curto escolhido pelo grupo quando existe; senão, o nome oficial do IBGE da tabela `dCNAE`:

```m
Chave        = Table.AddColumn(#"Tipo Alterado7", "Classe Chave", each Text.PadStart(Text.From([CNAE 2.0 Classe]), 5, "0"), type text),
Mesclar      = Table.NestedJoin(Chave, {"Classe Chave"}, dCNAE, {"Classe"}, "dCNAE", JoinKind.LeftOuter),
Expandir     = Table.ExpandTableColumn(Mesclar, "dCNAE", {"Classe_Descricao"}, {"Classe Descrição"}),
SetorCompleto = Table.AddColumn(Expandir, "Setor Completo", each if [Setor] = [CNAE 2.0 Classe] then [Classe Descrição] else [Setor], type text)
```

**Faixa de Porte** — traduz o código `Tamanho Estabelecimento` da RAIS (1 = "Zero", 2 = "1 a 4", ... , 10 = "1000 ou mais"), com a coluna `Ordem Porte` para ordenar as faixas.

## 2. Medidas DAX

Pasta **📊 Medidas**:

```dax
Total de Estabelecimentos    = COUNTROWS('RAIS_SJC')
Estabelecimentos Com Vínculo = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Situação Vínculo] = "Com Vínculo")
Estabelecimentos Sem Vínculo = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Situação Vínculo] = "Sem Vínculo")
% Com Vínculo                = DIVIDE([Estabelecimentos Com Vínculo], [Total de Estabelecimentos])
% Sem Vínculo                = DIVIDE([Estabelecimentos Sem Vínculo], [Total de Estabelecimentos])
Total Vínculos Ativos        = SUM('RAIS_SJC'[Qtd Vínculos Ativos])
Total Vínculos CLT           = SUM('RAIS_SJC'[Qtd Vínculos CLT])
Total Vínculos Estatutários  = SUM('RAIS_SJC'[Qtd Vínculos Estatutários])
% Participação Estab         = DIVIDE([Total de Estabelecimentos], CALCULATE([Total de Estabelecimentos], ALL('RAIS_SJC'[Seção CNAE])))
% Participação Vínculos      = DIVIDE([Total Vínculos Ativos], CALCULATE([Total Vínculos Ativos], ALL('RAIS_SJC'[Seção CNAE])))
```

| Medida | Resultado (sem filtro) | Onde aparece |
|---|---|---|
| Total de Estabelecimentos | 47.339 | Cartão da página 1 |
| Estabelecimentos Com Vínculo | 16.816 | Cartão da página 1 |
| Estabelecimentos Sem Vínculo | 30.523 | Cartão da página 1 |
| % Com Vínculo / % Sem Vínculo | 35,52% / 64,48% | Cartões e pizza da página 1 |
| Total Vínculos Ativos | 206.717 | Cartão da página 1 e % de participação por Seção |
| Total Vínculos CLT | 206.626 (a diferença de 91 são estatutários) | Gráficos e tabela da página 2 |
| % Participação Estab / Vínculos | por Seção | Gráfico "Peso de cada Seção" da página 2 |

O `DIVIDE` evita erro se o total for zero. Nas medidas de participação, o `ALL('RAIS_SJC'[Seção CNAE])` tira o filtro da Seção só no denominador, então cada Seção é comparada com o total geral.

Pasta **🚗 Automotivo** (estão no modelo, mas ainda não aparecem em nenhum visual):

```dax
Estab Fábricas                 = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Categoria Automotiva] = "Fabricação de Veículos (Fábricas)")
Vínculos Fábricas              = CALCULATE([Total Vínculos CLT], 'RAIS_SJC'[Categoria Automotiva] = "Fabricação de Veículos (Fábricas)")
Estab Comércio e Reparação     = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[Categoria Automotiva] = "Comércio/Reparação de Veículos")
Vínculos Comércio e Reparação  = CALCULATE([Total Vínculos CLT], 'RAIS_SJC'[Categoria Automotiva] = "Comércio/Reparação de Veículos")
Média Vínculos por Fábrica     = DIVIDE([Vínculos Fábricas], [Estab Fábricas])
Média Vínculos por Comércio e Reparação = DIVIDE([Vínculos Comércio e Reparação], [Estab Comércio e Reparação])
Estab Transporte de Carga      = CALCULATE(COUNTROWS('RAIS_SJC'), 'RAIS_SJC'[CNAE 2.0 Classe] = "49302", REMOVEFILTERS('RAIS_SJC'[Categoria Automotiva]))
Vínculos Transporte de Carga   = CALCULATE([Total Vínculos CLT], 'RAIS_SJC'[CNAE 2.0 Classe] = "49302", REMOVEFILTERS('RAIS_SJC'[Categoria Automotiva]))
```

`Categoria Automotiva` é uma coluna do Power Query: classes que começam com 29 = fábricas; com 45 = comércio e reparação de veículos.

## 3. Página PIB e Emprego

Não há medidas novas. Os visuais usam colunas prontas da planilha do IBGE (`fontes/Cruzamento_RAIS_IBGE_Observatorio_SJC.xlsx`): `part_emprego_pct`, `part_vab_pct`, `produtividade_relativa`, `pib_real_2023`, `cresc_real_pct` e `vab_real_2023`.

```
produtividade_relativa = part_vab_pct / part_emprego_pct
```

Acima de 1, o setor gera mais valor do que a sua fatia de empregos. Resultados: Indústria 1,86, Agropecuária 1,65 e Serviços 0,72.

## 4. Relações do modelo

| De | Para | Tipo |
|---|---|---|
| `RAIS_SJC[CEP Estab]` | `CEP x Região[CEP]` | Muitos para um — dá a região e a latitude/longitude de cada estabelecimento |
| `Cruzamento[vab_real_2023]` | `VAB setorial[vab_real_2023]` | Criada automaticamente pelo Power BI sobre uma coluna de valor; conferir na Sprint 3 |

## 5. Sprint 3: colunas da página Regiões e Tecnologia

São colunas calculadas em DAX na tabela RAIS_SJC. Elas partem da coluna Classe Chave (classe CNAE com 5 dígitos) e seguem a mesma regra da base única (notebook 02). As duas versões foram conferidas: dão a mesma categoria para todos os 47.339 estabelecimentos.

**Tipo de Atividade**

```
Tipo de Atividade =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
RETURN
    SWITCH (
        TRUE (),
        d = 0, "Não informado",
        d >= 10 && d <= 33, "Manufatura (indústria de transformação)",
        ( d >= 58 && d <= 63 ) || d = 72, "Tecnologia, informação e P&D",
        d >= 49 && d <= 53, "Logística e transporte",
        ( d >= 64 && d <= 66 ) || ( d >= 69 && d <= 75 ), "Serviços especializados",
        d >= 45 && d <= 47, "Comércio",
        d >= 41 && d <= 43, "Construção",
        d >= 77 && d <= 82, "Serviços administrativos e de apoio",
        d >= 85 && d <= 88, "Saúde e educação",
        ( d >= 5 && d <= 9 ) || ( d >= 35 && d <= 39 ), "Extração e utilidades",
        d <= 3, "Agropecuária",
        d = 84, "Administração pública",
        "Outros serviços"
    )
```

Pega os dois primeiros dígitos da classe CNAE (a divisão) e aplica as categorias do documento de requisitos do cliente. Exemplo: divisões 10 a 33 viram "Manufatura (indústria de transformação)". A classe 00999 (atividade não informada) fica como "Não informado".

**Intensidade Tecnológica OCDE**

```
Intensidade Tecnológica OCDE =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
VAR g = LEFT ( 'RAIS_SJC'[Classe Chave], 3 )
RETURN
    IF (
        d >= 10 && d <= 33,
        SWITCH (
            TRUE (),
            d IN { 21, 26 } || g = "304", "Alta",
            d IN { 20, 27, 28, 29 } || g IN { "255", "325" } || ( d = 30 && NOT ( g IN { "301", "304" } ) ), "Média-alta",
            d IN { 22, 23, 24, 32, 33 } || g = "301", "Média",
            "Média-baixa"
        ),
        SWITCH (
            TRUE (),
            d = 72, "Alta",
            d IN { 62, 63 }, "Média-alta",
            "Não se aplica"
        )
    )
```

Usa a divisão e o grupo (três primeiros dígitos) da classe CNAE e a taxonomia da OCDE (Galindo-Rueda e Verger, 2016). Só a indústria e os serviços de TI e P&D recebem um nível; os demais ficam em "Não se aplica". Resultado: alta e média-alta somam 28.804 vínculos (13,9%).

**Macroprocesso Logístico**

```
Macroprocesso Logístico =
VAR d = IFERROR ( VALUE ( LEFT ( 'RAIS_SJC'[Classe Chave], 2 ) ), 0 )
VAR cl = 'RAIS_SJC'[Classe Chave]
RETURN
    SWITCH (
        TRUE (),
        d = 0, "Não classificado",
        cl IN { "45200", "45439" } || d IN { 33, 95 }, "6. Pós-venda, manutenção e reparação",
        d <= 9 || d IN { 35, 36, 37 }, "1. Suprimento (agro, extração, energia e água)",
        ( d >= 10 && d <= 32 ) || ( d >= 41 && d <= 43 ), "2. Produção (indústria e construção)",
        d = 46, "3. Distribuição atacadista",
        d >= 49 && d <= 53, "4. Transporte e armazenagem",
        d IN { 45, 47 }, "5. Varejo (venda ao consumidor)",
        d IN { 38, 39 }, "7. Logística reversa (resíduos e reciclagem)",
        d >= 58 && d <= 82, "8. Serviços de apoio às empresas",
        ( d >= 55 && d <= 56 ) || ( d >= 84 && d <= 99 ), "9. Serviços ao consumidor e públicos",
        "Não classificado"
    )
```

Classifica cada estabelecimento pela etapa da cadeia de suprimentos (DEC-024). A ordem das linhas importa: a pós-venda (divisões 33 e 95 e as classes de reparação de veículos) é testada antes da produção e do varejo. O número na frente de cada etapa mantém a ordem da cadeia nos gráficos.

## 6. Sprint 3: parâmetro de pasta das fontes

```
PastaFontes = "C:\Observatorio-SJC\powerbi\fontes\"

Fonte = Csv.Document(File.Contents(PastaFontes & "RAIS_SJC.csv"), ...)
```

O parâmetro guarda a pasta das planilhas, e as 6 consultas do Power Query montam o caminho com PastaFontes & "nome do arquivo". Quem baixar o repositório em outra pasta muda só o parâmetro, em Página Inicial → Transformar dados → Editar parâmetros.

## 7. Sprint 3: coordenadas do mapa

O mapa usa as colunas Latitude e Longitude da tabela CEP x Região. Desde a Sprint 3 elas vêm do CNEFE 2022 do IBGE (DEC-023); não há fórmula no painel, só os valores da planilha.

## Resumo

O painel conta estabelecimentos (1 linha = 1 estabelecimento), separa quem declarou ter empregados formais de quem não declarou, soma os empregos ativos e CLT, e divide tudo pelo total para mostrar o peso de cada setor. "Sem vínculo" quer dizer que o estabelecimento não tinha empregados formais, não que as pessoas estão desempregadas.
