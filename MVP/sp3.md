# 📌 MVP - Sprint 3 · Consolidação do Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

> **Entrega:** 23/11/2026 · **Status:** Em andamento · Apresentação final na Feira de Soluções (03/12/2026) · [voltar ao README](../README.md)

## 🎯 Objetivo do MVP

> O MVP da Sprint 3 fecha o observatório: um painel único no Power BI, nos moldes do [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio), que reúne todos os indicadores das sprints anteriores, completa o mapa da cidade por região oficial e vem acompanhado do relatório técnico final e da apresentação ao cliente.

- Qual problema resolve? Ao fim da Sprint 2, os indicadores já existiam, mas o mapa cobria 78,3% dos estabelecimentos, a evolução dos setores e as contratações recentes dependiam de fontes que a base não tem, e não havia uma versão final que o CADI e a Secretaria pudessem usar sozinhos.

- Qual hipótese será validada? A hipótese de que um painel consolidado, com fontes e limites explicados, é suficiente para que a Secretaria de Desenvolvimento Econômico acompanhe o ecossistema produtivo do município e use o observatório na tomada de decisão.

- Qual valor será entregue ao usuário final? Uma ferramenta pronta para uso: painel publicado com todas as páginas, mapa por região oficial, relatório técnico final que documenta método, decisões e limitações, e uma apresentação para a Feira de Soluções.

---

## 📝 Descrição da Solução

> Consolidação do painel Power BI sobre a base única `dados/RAIS_SJC_2024_PowerBI.csv`, com o mapa por latitude/longitude, os visuais por região e tipo de atividade, a revisão das User Stories que dependem de série histórica e a documentação final.

- Funcionalidades principais incluídas:
  - **Mapa por região oficial (US06):** trocar a fonte do mapa pela base única (DEC-022), aumentar a cobertura de pontos e corrigir os bairros homônimos (DEC-017).
  - **Visuais por região, tipo de atividade, intensidade tecnológica (OCDE) e porte SEBRAE**, com as colunas já preparadas na Sprint 2 (DEC-021).
  - **Setores em alta (US08):** série histórica com a RAIS 2022–2023 pelo mesmo pipeline da Sprint 1, ou critério de aceite revisado com o cliente.
  - **Contratações recentes (US10):** RAIS Vínculos como nova fonte, ou critério de aceite revisado com o cliente.
  - **Dashboard consolidado (US11):** todas as páginas num só painel publicado, relatório técnico final e apresentação.

- Limitações conhecidas:
  - A RAIS Estabelecimentos não tem data de admissão: a US10 depende de outra fonte ou de novo critério.
  - A Região Norte não tem lista oficial de bairros no Plano Diretor (DEC-015 aberta até a Prefeitura enviar a tabela ou o shapefile).
  - Os pontos do mapa ficam no centro do bairro, não no endereço da empresa.
  - Sem identificação nominal das empresas (DEC-004): os rankings continuam por setor.

- Escopo reduzido: sem novas fontes além das já mapeadas (RAIS e PIB dos Municípios) e sem atualização automática dos dados; o foco é consolidar, validar e documentar.

---

## 👥 Personas / Usuários-Alvo

- **Persona 1:** Gestor público (usuário do observatório): quer ver no mapa onde estão os polos e vazios produtivos da cidade e quais setores crescem, para direcionar fomento, investimento e qualificação.
- **Persona 2:** Cliente (CADI e Secretaria de Desenvolvimento Econômico): quer receber uma ferramenta final, documentada e pronta para uso, com o relatório técnico e a apresentação.
- **Persona 3:** Analista de mercado: quer comparar regiões, tipos de atividade e intensidade tecnológica dos estabelecimentos de São José dos Campos.

---

## 🔑 User Stories (Backlog do MVP)

| ID   | User Story | Prioridade | Estimativa | Status |
| ---- | ---------- | ---------- | ---------- | ------ |
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. *(restante da Sprint 2)* | Alta | 13 pontos | Em andamento |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. *(restante da Sprint 2)* | Média | 8 pontos | Em andamento |
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | Baixa | 5 pontos | A fazer |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | Alta | 13 pontos | A fazer |

> Detalhamento no [Backlog da Sprint 3](../docs/09-Backlog-Sprint-3.md).

---

## 📅 Sprint(s) Relacionadas

| Sprint | Entregas Principais | Entrega | Status |
| ------ | ------------------- | ------- | ------ |
| 01 | US01 a US05: ETL em Colab, CSVs tratados, Log de Decisões (DEC-001 a DEC-005), documentação Scrum e repositório no GitHub | 28/09/2026 | Concluído ([MVP](sp1.md)) |
| 02 | US06 a US09: painel com KPIs, setores (CNAE), PIB e emprego; base geocodificada com região oficial; Log de Decisões até DEC-022 | 26/10/2026 | Concluído, 2 parciais ([MVP](sp2.md)) |
| 03 | Restante de US06 e US08, US10 e US11: mapa por região oficial, dashboard consolidado, relatório técnico final e apresentação | 23/11/2026 | Em andamento |
| Feira de Soluções | Apresentação final do observatório ao cliente | 03/12/2026 | A fazer |

---

## 📊 Critérios de Aceitação

| US | Critério |
| -- | -------- |
| US06 | O mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%, e filtra pelas regiões oficiais do município. |
| US08 | Visual mostra a evolução de contratações por setor (CNAE agrupado), ou o critério revisado com o cliente está registrado no Log de Decisões. |
| US10 | O painel exibe as contratações do período mais recente disponível, ordenadas por data, ou o critério revisado com o cliente está registrado no Log de Decisões. |
| US11 | O dashboard publicado reúne todos os visuais das sprints anteriores; relatório técnico final e apresentação entregues e aprovados pelos orientadores. |

---

## 📈 Métricas de Validação

| Métrica | Meta | Resultado |
| ------- | ---- | --------- |
| Estabelecimentos com ponto no mapa | acima de 90% (hoje 78,3%) | *a preencher* |
| Estabelecimentos com região oficial | 100% (hoje 99,99%) | *a preencher* |
| Decisões de dados em aberto | DEC-015, DEC-017 e DEC-022 resolvidas ou com encaminhamento registrado | *a preencher* |
| Usuários que testaram o MVP | equipe, orientadores e cliente | *a preencher* |
| Feedback qualitativo do cliente | aprovação do painel final | *a preencher* |

---

## 🚀 Próximos Passos

- Registrar o resultado de cada User Story ao fechar a sprint (23/11/2026).
- Preparar a apresentação e o vídeo da Feira de Soluções (03/12/2026).
- Entregar ao cliente o painel publicado, o relatório técnico final e o guia para atualizar os dados com uma nova RAIS.

---

## 📂 Anexos / Evidências

- Backlog da Sprint 3: [`docs/09-Backlog-Sprint-3.md`](../docs/09-Backlog-Sprint-3.md)
- Log de Decisões de Dados: [`docs/06-Decisoes-de-Dados.md`](../docs/06-Decisoes-de-Dados.md)
- Painel publicado: [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9)
- Prints de tela do painel final: *(adicionar em `evidencias/sprint3/`)*
- Relatório técnico final: *(adicionar em `docs/`)*
- Vídeo do MVP: *(adicionar link do YouTube)*
