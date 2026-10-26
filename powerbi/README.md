# Painel Power BI

| Arquivo | O que é | Páginas |
|---|---|---|
| [`Powerbi_API_Sprint2.pbix`](Powerbi_API_Sprint2.pbix) | **Versão atual** do painel da Sprint 2, descrita no [relatório do Power BI](../docs/Relatorio_PowerBI_Sprint2.md) | KPIs e Mapa · Setor de Atividades (CNAE) |
| [`Powerbi_API_Sprint2.pbit`](Powerbi_API_Sprint2.pbit) | Modelo (template) da versão atual: abre o painel sem os dados, pedindo a fonte | — |
| [`Powerbi_API_Sprint2.pdf`](Powerbi_API_Sprint2.pdf) | Versão atual exportada em PDF, para ver sem o Power BI | 2 |
| [`PowerbiATT_Api_Sprint2.pbix`](PowerbiATT_Api_Sprint2.pbix) | Versão anterior da Sprint 2, com as páginas de PIB e de notas | Notas Metodológicas · KPIs e Mapa · Setor de Atividades (CNAE) · PIB e Emprego |

## Telas da versão atual

![KPIs e Mapa](../evidencias/sprint2/painel_kpis_mapa.png)

![Setor de Atividades](../evidencias/sprint2/painel_setor_atividades.png)

## Pendências para a Sprint 3

- Trazer as páginas **PIB e Emprego** e **Notas Metodológicas** da versão `PowerbiATT` para a versão atual (cruzamento com o IBGE — US09).
- Trocar a fonte da tabela `RAIS_SJC` pela base única [`dados/RAIS_SJC_2024_PowerBI.csv`](../dados/RAIS_SJC_2024_PowerBI.csv) e o mapa do texto do CEP para **latitude/longitude**, com legenda por região oficial (US06). Passo a passo em [`evidencias/Importacao_PowerBI_RAIS_SJC.txt`](../evidencias/Importacao_PowerBI_RAIS_SJC.txt).
- Corrigir os subtítulos dos cartões da página 1: "Unidades com CNPJ próprio" (o total inclui CAEPF e CNO), "Cadastrados, com RAIS positiva" (está sob o cartão de *sem* vínculo) e "Empregados com contrato formal" (o cartão conta estabelecimentos, não pessoas).
- Corrigir o título do gráfico de pizza ("Distruibuição" → "Distribuição").
- Mostrar os cartões sem a unidade "Mil" (hoje aparece "47,339 Mil" e "206,717 Mil", que se lê como decimal); em Formato → Valor, usar unidade de exibição "Nenhum" para mostrar 47.339 e 206.717.
