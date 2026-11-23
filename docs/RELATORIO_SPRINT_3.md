# Relatório da Sprint 3

**Projeto:** Observatório do Ecossistema Industrial e de Serviços de São José dos Campos
**Disciplina:** API (Aprendizagem por Projetos Integrados), curso de Logística, Fatec São José dos Campos
**Cliente:** CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos
**Orientadores:** Prof. José Jaétis (M2) e Prof. Marcus Nascimento (P2)
**Período:** 27/10/2026 a 23/11/2026 · **Entrega da Sprint 3:** 23/11/2026 · **Feira de Soluções:** 03/12/2026
**Painel publicado:** [abrir no Power BI](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9)
**Canal do projeto no YouTube:** [LogMulti](https://www.youtube.com/@LogMulti)

---

## 1. Objetivo da Sprint

Consolidar o observatório como entrega final: um painel único publicado, documentado e pronto para o cliente consultar, com o vídeo do projeto e a preparação da apresentação na Feira de Soluções.

## 2. Resultado da Sprint

| Indicador | Resultado |
|---|---|
| User Stories planejadas | 4: US06 e US08 (herdadas da Sprint 2), US10 e US11 |
| Situação | US06, US08 e US11 parciais; US10 não iniciada (sem fonte de dados) |
| Painel Power BI | Mesma versão publicada na Sprint 2, com 4 páginas: KPIs e Mapa, Setor de Atividades (CNAE), PIB e Emprego, Notas Metodológicas — [publicado online](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9) |
| Estabelecimentos na base | 47.339 (15.058 com vínculos ativos em 31/12/2024) |
| Vínculos ativos | 206.717 |
| Estabelecimentos com ponto no mapa | 37.084 (78,3%); meta de 90% não atingida |
| Vínculos ativos com ponto no mapa | 146.702 (71,0%) |
| Estabelecimentos com região oficial | 47.334 (99,99%) |
| Decisões de dados | 22 registradas (DEC-001 a DEC-022); 4 abertas (DEC-004, DEC-015, DEC-017, DEC-022) |
| Divulgação | Canal [LogMulti](https://www.youtube.com/@LogMulti) criado para o vídeo de apresentação do projeto |

## 3. Backlog da Sprint 3

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US06 | Como gestor público (usuário do observatório), quero visualizar a distribuição geográfica das empresas de SJC no mapa, para que eu possa identificar polos e vazios industriais na cidade. | O mapa plota os estabelecimentos geocodificados a partir do CEP, com taxa de acerto acima de 90%, e filtra pelas regiões oficiais do município. | 2 | Parcial |
| US08 | Como gestor público, quero identificar quais setores/áreas estão em alta em termos de contratação, para que eu possa priorizar investimentos e qualificação de mão de obra. | Visual mostra a evolução de contratações por setor (CNAE agrupado), ou o critério revisado com o cliente está registrado no Log de Decisões. | 8 | Parcial |
| US10 | Como gestor público, quero acompanhar as contratações mais recentes registradas na RAIS, para que eu possa monitorar a dinâmica do mercado de trabalho local. | O painel exibe as contratações do período mais recente, ordenadas por data, ou o critério revisado com o cliente está registrado no Log de Decisões. | 10 | Não iniciada |
| US11 | Como cliente (CADI / Secretaria de Desenvolvimento Econômico), quero um dashboard consolidado no Power BI, nos moldes do Observatório da Inovação RS, acompanhado do relatório técnico final e da apresentação, para que eu possa usar a ferramenta na tomada de decisão. | O dashboard publicado reúne todos os visuais das sprints anteriores; relatório técnico final e apresentação entregues e aprovados pelos orientadores. | 11 | Parcial |

**Por que cada uma ficou assim**

- **US06:** o painel já usa latitude e longitude e filtra por região oficial, mas 10.255 estabelecimentos (21,7%) seguem sem ponto: CEPs genéricos de avenida e bairros que o geocodificador não encontrou (DEC-018). Esses estabelecimentos concentram 60.015 vínculos (29,0%), mais que a fatia de estabelecimentos, o que indica que ficam de fora do mapa unidades maiores, em avenidas.
- **US08:** o painel mostra quais setores concentram estabelecimentos e empregos em 2024, mas "em alta" pede comparação entre anos, e só a RAIS 2024 foi processada.
- **US10:** a RAIS Estabelecimentos não tem data de admissão. A fonte com essa informação é a RAIS Vínculos (microdados por vínculo), que não faz parte do escopo atual.
- **US11:** as 4 páginas estão num só painel publicado, com fontes e limites explicados na página de Notas Metodológicas. Falta a apresentação ao cliente e a aprovação, que acontecem na Feira de Soluções.

## 4. Entregas e evidências

### 4.1 Documentação

- `MVP/sp3.md`: MVP da Sprint 3 no modelo da Fatec, com resultados e métricas.
- `docs/RELATORIO_SPRINT_3.md`: este relatório.
- `README.md`: status final das sprints, link do painel e do canal do YouTube.
- `powerbi/README.md`: versão do painel usada na entrega e lista de melhorias.

### 4.2 Painel e dados

- Painel publicado (mesmo link da Sprint 2) e projeto `powerbi/pbip/Observatorio_SJC.pbip`, com as fontes lidas pelo parâmetro `PastaFontes`, com PDF das 4 páginas em `powerbi/Powerbi_API_Sprint2.pdf`.
- Base única `dados/RAIS_SJC_2024_PowerBI.csv` (47.339 linhas, 46 colunas) e notebooks 01 e 02 para refazer todo o tratamento com uma nova RAIS.

### 4.3 Vídeo e divulgação

- Canal do projeto no YouTube: [LogMulti](https://www.youtube.com/@LogMulti).
- Vídeo de apresentação: gravação de tela de até 5 minutos, mostrando o GitHub e o painel, com os gráficos que respondem aos requisitos do cliente. Responsáveis: Beatriz, Milena e João Pedro.

### 4.4 Evidências a anexar

- [x] Painel publicado no Power BI ([link](https://app.powerbi.com/view?r=eyJrIjoiMDdlOThiMzQtNWQ5Ny00Mzk1LWI0YWEtNGM2NzAzZmNhNDRmIiwidCI6ImVhYmU2NGM1LTY4ZjUtNGE3Ni04MzAxLTk1NzdhNjc5ZTQ0OSIsImMiOjR9))
- [x] Prints das 4 páginas do painel (`evidencias/sprint2/`, mesma versão)
- [x] Canal do projeto no YouTube ([LogMulti](https://www.youtube.com/@LogMulti))
- [ ] Link direto do vídeo de apresentação publicado no canal
- [ ] Apresentação da Feira de Soluções (`docs/`)
- [ ] Relatório de Desenvolvimento da Sprint 3 (modelo Anexo 8 da Fatec, `docs/Relatorio_Sprint3_Anexo8.docx`)

## 5. Pendências e riscos

| Pendência | Impacto | Encaminhamento |
|---|---|---|
| Cobertura do mapa (DEC-018) | 21,7% dos estabelecimentos e 29,0% dos vínculos sem ponto | Usar o ponto do bairro já geocodificado em outro CEP (melhoria 1) |
| Bairros homônimos (DEC-017) | 331 estabelecimentos com ponto fora da região certa | Regeocodificar os 9 bairros |
| Fonte do mapa (DEC-022) | O painel ainda usa a tabela CEP x Região, que deixa 603 sem região (a base única deixa 5) | Trocar a fonte pela base única |
| Região Norte (DEC-015) | 1.024 estabelecimentos com região de confiabilidade média | Pedir à Prefeitura, via cliente, a tabela bairro → região ou o shapefile |
| Identificação nominal (DEC-004) | Rankings só por setor | Mantido; depende de base identificada do cliente |
| Série histórica e data de admissão | US08 e US10 não atendidas | Decidir com o cliente na Feira: nova fonte ou critério revisado |
| Aba "PIB anual" ausente em `powerbi/fontes/` | A tabela `PIB anual` não atualiza a partir do repositório (as outras 5 atualizam) | Enviar para `fontes/` a planilha de cruzamento completa usada no painel |
| DEC-007, DEC-010 e DEC-012 | Decisões citadas sem registro no log | Transcrever para `docs/06-Decisoes-de-Dados.docx` |

## 6. Melhorias sugeridas

| # | Melhoria | Resultado esperado | Esforço |
|---|---|---|---|
| 1 | Dar ponto no mapa aos estabelecimentos sem coordenada cujo bairro já foi geocodificado em outro CEP | 5.024 estabelecimentos a mais no mapa; cobertura de 78,3% para cerca de 88,9% | Baixo (uma etapa no notebook 02) |
| 2 | Regeocodificar os 9 bairros homônimos e trocar a fonte do mapa pela base única | Fecha DEC-017 e DEC-022; região do painel igual à da base | Baixo |
| 3 | ✅ **Feito em 23/11 no `.pbip`.** Corrigir os ajustes visuais da página 1 (cartões com "Mil", título "Distruibuição", subtítulos); falta republicar | Números lidos corretamente (47.339, não "47,339 Mil") | Concluído |
| 4 | Criar uma página "Regiões" com vínculos e estabelecimentos por região, tipo de atividade, intensidade tecnológica (OCDE) e porte SEBRAE | Responde aos requisitos do cliente com colunas que já existem (DEC-021) | Médio |
| 5 | Processar a RAIS 2022 e 2023 pelo notebook 01 | Evolução dos setores (US08) | Médio |
| 6 | Revisar o critério da US10 com o cliente: RAIS Vínculos (mês de admissão) ou "estabelecimentos com atividade no ano" | US10 com fonte ou critério registrado | Baixo para decidir |
| 7 | ✅ **Feito em 23/11.** Trocar os caminhos `C:\Users\...` das fontes pelo parâmetro de pasta `PastaFontes` | Qualquer integrante ou o cliente atualiza o painel | Concluído |
| 8 | ✅ **Feito em 23/11.** Renomear o projeto do painel de "Powerbi Sprint2" para "Observatorio_SJC" e mover as versões `.pbix` antigas para `powerbi/versoes_anteriores/` | Repositório mais claro para quem recebe a entrega final | Concluído |
| 9 | Escrever um guia curto "Como atualizar o observatório com uma nova RAIS" | O cliente consegue manter a ferramenta depois do projeto | Baixo |

## 7. Próximos passos

**Feira de Soluções (03/12/2026): apresentação final**

1. Publicar o vídeo no canal LogMulti e atualizar o link no README e no MVP.
2. Abrir o `.pbip` no Power BI Desktop e republicar no mesmo workspace, para o link mostrar os ajustes da página 1. Aplicar as melhorias 1 e 2, se houver tempo antes da Feira; as demais ficam como recomendação ao cliente.
3. Preparar a apresentação e um QR Code para o painel e para o repositório.
4. Registrar o feedback do cliente e a decisão sobre US08 e US10 no Log de Decisões.

## 8. Equipe

| Integrante | Papel | Função na Sprint 3 |
|---|---|---|
| Pedro Henrique Oliveira de Carvalho | Product Owner | Apoio geral e demais demandas |
| Juliano Souza Santana | Scrum Master | Dados e documentação |
| Beatriz Oliveira Sepulvida | Scrum Team | CSV e Excel; vídeo do projeto |
| Caio Moreira | Scrum Team | Power BI e dados |
| Hemilly Christiny da Silva Freitas | Scrum Team | Documentação |
| João Pedro Faria Vital de Souza | Scrum Team | Apoio geral; vídeo do projeto |
| Milena Silva Nogueira | Scrum Team | Dados e documentação; vídeo do projeto |
| Thalya Awany Berti | Scrum Team | Power BI |

---

*Última atualização: 23/11/2026*
