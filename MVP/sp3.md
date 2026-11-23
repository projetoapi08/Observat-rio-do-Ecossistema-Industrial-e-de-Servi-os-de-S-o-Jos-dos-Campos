# 📌 MVP - Sprint 3 · Consolidação do Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

> **Entrega:** 23/11/2026 · **Status:** Entregue (painel consolidado publicado; US06 e US08 parciais, US10 sem fonte de dados) · Apresentação final na Feira de Soluções (03/12/2026) · [Relatório da Sprint 3](../docs/RELATORIO_SPRINT_3.md) · [voltar ao README](../README.md)

> 🌐 **Painel publicado:** [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) (abre no navegador, sem login)
>
> ▶️ **Vídeos do projeto:** [canal LogMulti no YouTube](https://www.youtube.com/@LogMulti)

## 🎯 Objetivo do MVP

> O MVP da Sprint 3 fecha o observatório: um painel único no Power BI, nos moldes do [Observatório da Inovação RS](https://sict.rs.gov.br/observatorio), que reúne os indicadores das sprints anteriores, mostra o mapa da cidade por região oficial e vem acompanhado da documentação final, do vídeo do projeto e da apresentação ao cliente.

- Qual problema resolve? A Secretaria de Desenvolvimento Econômico e o CADI não tinham uma versão final, publicada e documentada, que pudessem abrir e usar sozinhos para acompanhar o ecossistema produtivo do município.

- Qual hipótese será validada? A hipótese de que um painel consolidado, com fontes e limites explicados, é suficiente para que a Secretaria acompanhe o ecossistema produtivo do município e use o observatório na tomada de decisão. A validação com o cliente acontece na Feira de Soluções (03/12/2026).

- Qual valor será entregue ao usuário final? Uma ferramenta pronta para consulta: painel publicado com acesso pelo navegador, sem login, base única documentada, notebooks para refazer o tratamento com uma nova RAIS e um vídeo que mostra como usar o painel.

---

## 📝 Descrição da Solução

> Painel Power BI publicado com 4 páginas, sobre a RAIS 2024 de São José dos Campos classificada pela CNAE 2.3, geocodificada no nível de bairro e cruzada com o PIB dos Municípios (IBGE). A versão publicada é a mesma da Sprint 2: a Sprint 3 consolidou, validou e documentou essa versão como entrega final.

- Funcionalidades principais entregues:
  - **KPIs e Mapa:** total de estabelecimentos, com e sem vínculo, vínculos ativos; mapa por latitude e longitude; filtros por seção CNAE, porte, tipo de estabelecimento e **região oficial**.
  - **Setor de Atividades (CNAE):** Top 10 setores por estabelecimentos e por empregos CLT, participação de cada seção, indústria (Seção C) por setor e tabela por porte.
  - **PIB e Emprego:** PIB 2002–2023 corrigido pelo IPCA, variação anual, valor adicionado por setor e produtividade relativa.
  - **Notas Metodológicas:** fontes, definições, limites e decisões da equipe.
  - **Documentação de entrega:** relatório da Sprint 3, Log de Decisões (DEC-001 a DEC-022), notebooks 01 e 02 para reproduzir a base, dicionário de dados e guia para abrir e atualizar o painel.
  - **Canal LogMulti no YouTube**, para o vídeo de apresentação do projeto (gravação de tela do GitHub e do painel, até 5 minutos).

- Limitações conhecidas:
  - **Mapa:** 78,3% dos estabelecimentos têm ponto; a meta era acima de 90%. Os pontos ficam no centro do bairro, não no endereço da empresa.
  - **Um único ano de RAIS (2024):** não dá para mostrar a evolução dos setores (US08).
  - **Sem data de admissão** na RAIS Estabelecimentos: a US10 não tem fonte na base atual.
  - A Região Norte não tem lista oficial de bairros no Plano Diretor (DEC-015 aberta).
  - Sem identificação nominal das empresas (DEC-004): os rankings são por setor.

- Escopo reduzido: sem novas fontes além da RAIS 2024 e do PIB dos Municípios, sem atualização automática e sem alterar o painel publicado na Sprint 2. As melhorias sugeridas estão em [Próximos passos](#-próximos-passos-e-melhorias-sugeridas).

---

## 👥 Personas / Usuários-Alvo

- **Persona 1:** Gestor público (usuário do observatório): quer ver no mapa onde estão os polos e vazios produtivos da cidade e quais setores pesam mais no emprego e no PIB, para direcionar fomento, investimento e qualificação.
- **Persona 2:** Cliente (CADI e Secretaria de Desenvolvimento Econômico): quer receber uma ferramenta final, documentada e pronta para uso, com o vídeo e a apresentação.
- **Persona 3:** Analista de mercado: quer comparar regiões, setores e porte dos estabelecimentos de São José dos Campos.

---

## 🔑 User Stories (Backlog do MVP)

| ID   | User Story | Prioridade | Estimativa | Status |
| ---- | ---------- | ---------- | ---------- | ------ |
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. *(restante da Sprint 2)* | Alta | 13 pontos | Parcial (mapa por coordenadas e filtro por região no painel; 78,3% com ponto, meta 90%) |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. *(restante da Sprint 2)* | Média | 8 pontos | Parcial (participação e ranking por setor; evolução depende da RAIS 2022–2023) |
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | Baixa | 5 pontos | Não iniciada (a base não tem data de admissão; critério a revisar com o cliente) |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | Alta | 13 pontos | Parcial (painel único publicado e documentado; apresentação e aprovação na Feira de Soluções) |

> Detalhamento no [Backlog da Sprint 3](../docs/09-Backlog-Sprint-3.md) e no [Relatório da Sprint 3](../docs/RELATORIO_SPRINT_3.md).

---

## 📅 Sprint(s) Relacionadas

| Sprint | Entregas Principais | Entrega | Status |
| ------ | ------------------- | ------- | ------ |
| 01 | US01 a US05: ETL em Colab, CSVs tratados, Log de Decisões (DEC-001 a DEC-005), documentação Scrum e repositório no GitHub | 28/09/2026 | Concluído ([MVP](sp1.md)) |
| 02 | US06 a US09: painel com KPIs, setores (CNAE), PIB e emprego; base geocodificada com região oficial; Log de Decisões até DEC-022 | 26/10/2026 | Concluído, 2 parciais ([MVP](sp2.md)) |
| 03 | Restante de US06 e US08, US10 e US11: painel consolidado publicado, documentação final e vídeo no canal LogMulti | 23/11/2026 | Entregue |
| Feira de Soluções | Apresentação final do observatório ao cliente | 03/12/2026 | A fazer |

---

## 📊 Critérios de Aceitação

| US | Critério | Resultado |
| -- | -------- | --------- |
| US06 | O mapa no Power BI plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%, e filtra pelas regiões oficiais do município. | Mapa por latitude/longitude e filtro por região no painel. 37.084 estabelecimentos (78,3%) com ponto: **meta não atingida**. |
| US08 | Visual mostra a evolução de contratações por setor (CNAE agrupado), ou o critério revisado com o cliente está registrado no Log de Decisões. | Participação e Top 10 por setor no painel; sem série histórica e sem critério revisado registrado. |
| US10 | O painel exibe as contratações do período mais recente disponível, ordenadas por data, ou o critério revisado com o cliente está registrado no Log de Decisões. | Não atendido: a RAIS Estabelecimentos não tem data de admissão. |
| US11 | O dashboard publicado reúne todos os visuais das sprints anteriores; relatório técnico final e apresentação entregues e aprovados pelos orientadores. | Painel único com as 4 páginas publicado; relatório da Sprint 3 entregue e canal LogMulti criado para o vídeo; apresentação e aprovação na Feira (03/12). |

---

## 📈 Métricas de Validação

| Métrica | Meta | Resultado |
| ------- | ---- | --------- |
| Estabelecimentos com ponto no mapa | acima de 90% | 37.084 de 47.339 (78,3%) |
| Vínculos ativos em estabelecimentos com ponto no mapa | — | 146.702 de 206.717 (71,0%) |
| Estabelecimentos com região oficial | 100% | 47.334 (99,99%) |
| Decisões de dados em aberto | DEC-015, DEC-017 e DEC-022 resolvidas ou com encaminhamento | 3 abertas, com encaminhamento registrado (ver relatório) |
| Usuários que testaram o MVP | equipe, orientadores e cliente | equipe; orientadores e cliente na Feira de Soluções |
| Feedback qualitativo do cliente | aprovação do painel final | a coletar na Feira de Soluções (03/12/2026) |

---

## 🚀 Próximos passos e melhorias sugeridas

**Até a Feira de Soluções (03/12/2026)**

- Publicar o vídeo de apresentação no [canal LogMulti](https://www.youtube.com/@LogMulti) e colocar o link direto do vídeo aqui e no README.
- Corrigir os ajustes visuais da página 1 (cartões com "Mil", título "Distruibuição", subtítulos de dois cartões), listados em [`powerbi/README.md`](../powerbi/README.md).
- Levar à Feira um QR Code para o painel publicado e outro para o repositório.
- Perguntar ao cliente, na apresentação, se aceita revisar os critérios de US08 e US10 (ver abaixo) e registrar a resposta no Log de Decisões.

**Melhorias sugeridas para o painel e os dados**

| # | Melhoria | Por quê | Esforço |
| - | -------- | ------- | ------- |
| 1 | Dar ponto no mapa aos estabelecimentos sem coordenada cujo bairro já foi geocodificado em outro CEP | 5.024 estabelecimentos ganham ponto e a cobertura vai de 78,3% para cerca de 88,9% | Baixo (uma etapa no notebook 02) |
| 2 | Regeocodificar os 9 bairros homônimos (DEC-017) e trocar a fonte do mapa pela base única (DEC-022) | 331 pontos hoje caem fora da região certa; fecha duas decisões abertas | Baixo |
| 3 | Criar uma página "Regiões" com vínculos e estabelecimentos por região, tipo de atividade, intensidade tecnológica (OCDE) e porte SEBRAE | As colunas já estão na base única (DEC-021) e respondem aos requisitos do cliente | Médio |
| 4 | Processar a RAIS 2022 e 2023 pelo notebook 01 | Permite mostrar a evolução dos setores (US08) | Médio (arquivos de cerca de 3 GB cada) |
| 5 | Revisar com o cliente o critério da US10: usar a RAIS Vínculos (mês de admissão) ou trocar por "estabelecimentos com atividade no ano" | A base atual não tem data de admissão | Baixo para decidir; médio para implementar |
| 6 | ✅ Feito em 23/11: parâmetro `PastaFontes` no lugar dos caminhos `C:\Users\...`, projeto renomeado para `Observatorio_SJC` e `.pbix` antigos em `powerbi/versoes_anteriores/` | Qualquer integrante ou o cliente consegue atualizar o painel | Concluído (falta a aba "PIB anual" em `powerbi/fontes/`) |
| 7 | Transcrever DEC-007, DEC-010 e DEC-012 para o Log de Decisões | O log fica completo para a entrega final | Baixo |

---

## 📂 Anexos / Evidências

- Relatório da Sprint 3: [`docs/RELATORIO_SPRINT_3.md`](../docs/RELATORIO_SPRINT_3.md)
- Backlog da Sprint 3: [`docs/09-Backlog-Sprint-3.md`](../docs/09-Backlog-Sprint-3.md)
- Log de Decisões de Dados: [`docs/06-Decisoes-de-Dados.md`](../docs/06-Decisoes-de-Dados.md)
- **Painel publicado:** [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) · projeto [`powerbi/pbip/Observatorio_SJC.pbip`](../powerbi/pbip/) e planilhas em [`powerbi/fontes/`](../powerbi/fontes/) · [PDF das 4 páginas](../powerbi/Powerbi_API_Sprint2.pdf)
- Base única e dicionário de dados: [`dados/RAIS_SJC_2024_PowerBI.csv`](../dados/RAIS_SJC_2024_PowerBI.csv) · [`dados/README.md`](../dados/README.md)
- Notebooks: [`01_ETL_RAIS_SJC.ipynb`](../notebooks/01_ETL_RAIS_SJC.ipynb) · [`02_Base_PowerBI_SJC.ipynb`](../notebooks/02_Base_PowerBI_SJC.ipynb)
- **Vídeo do MVP:** [canal LogMulti no YouTube](https://www.youtube.com/@LogMulti)

### Prints de tela do MVP

O painel publicado é o mesmo da Sprint 2; os prints estão em `evidencias/sprint2/`.

| KPIs e Mapa | Setor de Atividades (CNAE) |
| :---: | :---: |
| ![KPIs e Mapa](../evidencias/sprint2/painel_kpis_mapa.png) | ![Setor de Atividades](../evidencias/sprint2/painel_setor_atividades.png) |
| **PIB e Emprego** | **Notas Metodológicas** |
| ![PIB e Emprego](../evidencias/sprint2/painel_pib_emprego.png) | ![Notas Metodológicas](../evidencias/sprint2/painel_notas_metodologicas.png) |
