# 📌 MVP - [Tratamento dos dados da RAIS para o Observatório do Ecossistema Industrial e de Serviços de São José dos Campos no Power BI]

## 🎯 Objetivo do MVP

> O MVP visa preparar e tratar, em Python, os dados da RAIS de São José dos Campos para alimentar um dashboard no Power BI que apoie decisões sobre o ecossistema industrial e de serviços do município.

- Qual problema resolve? A Secretaria de Desenvolvimento Econômico e o CADI não têm uma visão consolidada e atualizada de quem emprega, onde e em quais setores no município. Os dados públicos da RAIS têm inconsistências que impedem o uso direto.

- Qual hipótese será validada? A hipótese de que o tratamento automatizado da RAIS, aliado a um painel de BI inspirado no [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio), permite mapear o ecossistema industrial e de serviços de São José dos Campos de forma confiável.

- Qual valor será entregue ao usuário final? Dados limpos e documentados, com decisões de tratamento registradas, e uma base pronta para visualizações que ajudem a acompanhar emprego, setores, localização das empresas e relação com o PIB do município.

---

## 📝 Descrição da Solução

> Pipeline de dados em Python (Google Colab) que filtra e trata a RAIS do município 354990, integrado a um dashboard em Power BI, com versionamento da documentação e do código no GitHub.

- Funcionalidades principais incluídas: Filtragem e tratamento da RAIS em Python, geração de CSVs tratados, Log de Decisões de Dados, documentação formal (Visão e Escopo, DoR e DoD) e uma pré-visualização inicial no Power BI. O dashboard interativo completo vem nas sprints seguintes.

- Limitações conhecidas: A RAIS pública não traz identificação nominal das empresas (DEC-004, ainda aberta com o cliente). Há defasagem de 1 ano entre RAIS (2024) e PIB dos Municípios (2023). A atualização depende da execução dos scripts. O arquivo bruto tem cerca de 3,27 GB e precisa ser lido em streaming.

- Escopo reduzido: Foco no tratamento dos dados, na documentação das decisões e na estrutura do repositório. O mapa e as análises ficam para a Sprint 2, e a consolidação do dashboard para a Sprint 3.

---

## 👥 Personas / Usuários-Alvo

- **Persona 1:** Gestor público (usuário do observatório): precisa de indicadores confiáveis sobre empresas, emprego e setores de São José dos Campos para direcionar políticas de fomento, investimento e qualificação de mão de obra.
- **Persona 2:** Cliente (CADI e Secretaria de Desenvolvimento Econômico): precisa de um dashboard consolidado, nos moldes do Observatório da Inovação RS, para usar na tomada de decisão.
- **Persona 3:** Equipe do projeto: nas User Stories da Sprint 1, é quem precisa de dados prontos e bem documentados para construir o dashboard.

---

## 🔑 User Stories (Backlog do MVP)

| ID   | User Story | Prioridade | Status |
| ---- | ---------- | ---------- | ------ |
| US01 | Como equipe do projeto, quero um pipeline de ETL no Google Colab (Python) que extraia e prepare os dados brutos da RAIS, para que os dados estejam prontos para análise no Power BI. | 1 | Concluído |
| US02 | Como equipe do projeto, quero filtrar e padronizar os dados para o município de São José dos Campos (código 354990), para que a análise reflita exclusivamente o ecossistema local. | 3 | Concluído |
| US03 | Como equipe do projeto, quero identificar e tratar as inconsistências dos dados da RAIS (vínculos zerados, mistura de tipos de estabelecimento, ausência de ano e de identificação), para que o dashboard não apresente conclusões distorcidas. | 4 | Concluído |
| US04 | Como equipe do projeto, quero produzir a documentação formal do projeto (Visão e Escopo, DoR, DoD, Log de Decisões), para que o trabalho siga a metodologia Scrum/API exigida pela disciplina. | 5 | Concluído |
| US05 | Como equipe do projeto, quero estruturar o repositório no GitHub (docs/, notebooks/, powerbi/), para que o código, os dados e a documentação fiquem organizados e versionados. | 6 | Concluído |

> A prioridade é a ordem definida no Backlog do Produto (1 é a mais alta). A US06 (mapa, prioridade 2) fica na Sprint 2.

---

## 📅 Sprint(s) Relacionadas

| Sprint | Entregas Principais | Entrega | Status |
| ------ | ------------------- | ------- | ------ |
| 01 | US01 a US05: ETL em Colab, CSVs tratados, Log de Decisões (DEC-001 a DEC-005), documentação Scrum e repositório no GitHub | 28/09/2026 | Concluído |
| 02 | US06 a US09: mapa de distribuição geográfica (geocodificação via CEP), ranking de empresas que mais contratam, setores em alta e impacto no PIB municipal | 26/10/2026 (detalhamento a confirmar) | A fazer |
| 03 | US10 e US11: contratações mais recentes e dashboard consolidado com relatório técnico final e apresentação | 23/11/2026 (detalhamento a confirmar) | A fazer |

---

## 📊 Critérios de Aceitação

- **US01:** o notebook executa de ponta a ponta e gera os CSVs de saída sem erros.
- **US02:** 100% dos registros do CSV final pertencem ao município 354990.
- **US03:** cada inconsistência encontrada está registrada no Log de Decisões (DEC-XXX) com o tratamento adotado.
- **US04:** todos os documentos da Sprint 1 aprovados pelo orientador.
- **US05:** repositório publicado com as três pastas (docs/, notebooks/, powerbi/) e README inicial.

---

## 📈 Métricas de Validação

- Base tratada: 47.339 estabelecimentos de São José dos Campos, extraídos de 12.643.067 registros nacionais.
- Tipos de estabelecimento: 46.244 CNPJ, 708 CAEPF e 387 CNO.
- Estabelecimentos com RAIS negativa: 30.470 de 47.339 (64,37%), mantidos na base com indicador próprio (DEC-001).
- Decisões de dados: 4 fechadas e 1 aberta (DEC-004), das 5 registradas.
- User Stories da Sprint 1: 5 de 5 concluídas.
- Pré-visualização inicial no Power BI produzida (meta da Sprint 1 cumprida).

---

## 🚀 Próximos Passos

- Filtrar os dados do PIB dos Municípios (IBGE) para São José dos Campos e confirmar se a edição 2022–2023 traz a abertura por setor, necessária para a US09.
- Sprint 2 (26/10/2026): geocodificar os estabelecimentos via CEP e construir os visuais de mapa (US06), ranking (US07), setores em alta (US08) e impacto no PIB (US09).
- Resolver com o cliente a pendência do DEC-004 (dados nominais). Se negativo, o ranking da US07 usa indicadores agregados por setor e região.
- Confirmar o detalhamento das Entregas 2 e 3 com os professores.
- Sprint 3 (23/11/2026): consolidar o dashboard, entregar o relatório técnico final e a apresentação. A Feira de Soluções (03/12/2026) é o marco de apresentação final.

---

## 📂 Anexos / Evidências

- Repositório: <https://github.com/projetoapi08/observatorio-sjc>
- Documentação (Visão e Escopo, Backlog, DoR, DoD, Log de Decisões, Relatório Técnico): `docs/`
- Notebook de ETL (Google Colab): `notebooks/` *https://colab.research.google.com/drive/1zOZJ0oXUY7QJlAMfuiMbI5g9EcBWSnMz?usp=sharing*
- Dados tratados (CSVs): *(colar o link do Drive)*
- Pré-visualização inicial no Power BI: *(colar o link ou arrastar o print)*
- Vídeo ou prints da execução do ETL: *(arrastar o arquivo para este arquivo no GitHub)*
- Referência do projeto: [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio)

### Log de Decisões de Dados

| ID      | Problema | Decisão | Status |
| ------- | -------- | ------- | ------ |
| DEC-001 | 30.470 estabelecimentos (64,37%) com RAIS negativa, ou seja, sem vínculos ativos | Manter na base, com indicador próprio, pois o cliente esclareceu que não é um erro a descartar. As análises de contratação usam por padrão os 16.869 estabelecimentos com vínculo ativo | Fechada |
| DEC-002 | A base mistura três tipos de estabelecimento (CNPJ, CAEPF e CNO) | Segmentar os dados, com recorte padrão em CNPJ | Fechada |
| DEC-003 | O arquivo não tem campo de ano ou competência | Ano-base 2024, confirmado pelo cliente | Fechada |
| DEC-004 | A base pública não traz razão social, CNPJ ou CPF dos estabelecimentos | Em aberto, aguardando o cliente. Contingência: indicadores agregados por setor e região | Aberta |
| DEC-005 | O PIB dos Municípios mais recente publicado é a série 2022–2023 | Cruzar a RAIS 2024 com o PIB 2023, documentando a defasagem de 1 ano | Fechada |
