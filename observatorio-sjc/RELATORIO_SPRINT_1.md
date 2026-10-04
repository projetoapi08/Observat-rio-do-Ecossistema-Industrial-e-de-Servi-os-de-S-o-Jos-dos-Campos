# Relatório da Sprint 1

**Projeto:** Observatório do Ecossistema Industrial e de Serviços de São José dos Campos
**Disciplina:** API (Aprendizagem por Projetos Integrados), curso de Logística, Fatec São José dos Campos
**Cliente:** CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos
**Orientadores:** Prof. José Jaétis (M2) e Prof. Marcus Nascimento (P2)
**Entrega da Sprint 1:** 28/09/2026
**Repositório:** `projetoapi08/observatorio-sjc`

---

## 1. Objetivo da Sprint

Construir a fundação técnica do Observatório: pipeline de dados, tratamento das inconsistências da RAIS e documentação da metodologia. Isso inclui alinhar o escopo com o cliente, extrair e tratar os dados da RAIS filtrados para São José dos Campos e registrar formalmente as decisões sobre os problemas encontrados.

Nesta sprint, o escopo mudou de um relatório voltado à contratação de mão de obra para um observatório abrangente do ecossistema municipal, inspirado no Observatório da Inovação RS.

## 2. Resultado da Sprint

| Indicador | Resultado |
|---|---|
| User Stories planejadas / concluídas | 5 / 5 (US01 a US05) |
| ETL em Google Colab (Python) | Executado com sucesso, 3 arquivos CSV gerados |
| Arquivo de origem | `RAIS_ESTAB_PUB`: 12.643.067 estabelecimentos no país |
| Recorte geográfico | 47.339 estabelecimentos de São José dos Campos (município 354990) |
| Power BI | Pré-visualização inicial produzida; modelagem e versão final dos visuais ficam para a Sprint 2 |
| Tipos de estabelecimento | 46.244 CNPJ, 708 CAEPF e 387 CNO |
| Ano-base da RAIS | 2024 (confirmado pelo cliente) |
| Decisões de dados | 5 registradas: 4 fechadas e 1 aberta |

## 3. Backlog da Sprint 1

| ID | User Story | Critério de aceite | Prior. | Status |
|---|---|---|---|---|
| US01 | Como equipe do projeto, quero um pipeline de ETL no Google Colab (Python) que extraia e prepare os dados brutos da RAIS, para que os dados estejam prontos para análise no Power BI. | O notebook executa de ponta a ponta e gera os CSVs de saída sem erros. | 1 | Concluído |
| US02 | Como equipe do projeto, quero filtrar e padronizar os dados para o município de São José dos Campos (código 354990), para que a análise reflita exclusivamente o ecossistema local. | 100% dos registros do CSV final pertencem ao município 354990. | 3 | Concluído |
| US03 | Como equipe do projeto, quero identificar e tratar as inconsistências dos dados da RAIS (vínculos zerados, mistura de tipos de estabelecimento, ausência de ano e de identificação), para que o dashboard não apresente conclusões distorcidas. | Cada inconsistência está registrada no Log de Decisões (DEC-XXX) com o tratamento adotado. | 4 | Concluído |
| US04 | Como equipe do projeto, quero produzir a documentação formal do projeto (Visão e Escopo, DoR, DoD, Log de Decisões), para que o trabalho siga a metodologia Scrum/API exigida pela disciplina. | Todos os documentos da Sprint 1 aprovados pelo orientador. | 5 | Concluído |
| US05 | Como equipe do projeto, quero estruturar o repositório no GitHub (docs/, notebooks/, powerbi/), para que o código, os dados e a documentação fiquem organizados e versionados. | Repositório publicado com as três pastas e README inicial. | 6 | Concluído |

## 4. Entregas e evidências

### 4.1 Documentação (Scrum)

Os documentos estão na pasta `docs/`:

- Visão e Escopo
- Backlog do Produto (11 User Stories distribuídas em 3 sprints)
- Backlog da Sprint 1
- Checklist DoR (Definition of Ready)
- DoD (Definition of Done)
- Log de Decisões de Dados
- Relatório Técnico (modelo Anexo 8 da Fatec)

### 4.2 Tratamento dos dados

- **Ferramenta:** Google Colab com Python 3+ (`notebooks/`)
- **Fonte:** RAIS (Ministério do Trabalho e Emprego), arquivo público `RAIS_ESTAB_PUB`, ano-base 2024
- **Método:** leitura sequencial (streaming) com a biblioteca `csv`, porque o arquivo bruto tem cerca de 3,27 GB e não abre em ferramentas como o Excel
- **Saída:** 3 arquivos CSV, entre eles `RAIS_SJC_in_.csv`, 100% filtrado para o município 354990

### 4.3 Log de Decisões de Dados

| ID | Problema | Decisão | Status |
|---|---|---|---|
| DEC-001 | RAIS negativa: 30.470 de 47.339 estabelecimentos (64,37%) sem vínculos ativos | Manter na base, com indicador próprio, pois o cliente esclareceu que não é um erro a descartar. As análises de contratação usam por padrão os 16.869 estabelecimentos com vínculo ativo | Fechada |
| DEC-002 | A base mistura três tipos de estabelecimento (CNPJ, CAEPF e CNO) | Segmentar os dados, com recorte padrão em CNPJ | Fechada |
| DEC-003 | O arquivo não tem campo de ano ou competência | Ano-base 2024, confirmado pelo cliente | Fechada |
| DEC-004 | A base pública não traz razão social, CNPJ ou CPF dos estabelecimentos | Em aberto, aguardando o cliente sobre uma base identificada. Contingência: indicadores agregados por setor e região | **Aberta** |
| DEC-005 | O PIB dos Municípios mais recente publicado é a série 2022–2023 | Cruzar a RAIS 2024 com o PIB 2023, documentando a defasagem de 1 ano | Fechada |

### 4.4 Evidências a anexar

Marque cada item depois de adicionar o print ou arquivo na pasta `evidencias/`.

- [ ] Notebook executado no Google Colab (saídas visíveis)
- [ ] Conferência do filtro por município 354990 (US02)
- [ ] Os 3 arquivos CSV gerados (US01)
- [ ] Contagem de estabelecimentos com e sem vínculos ativos (base do DEC-001)
- [ ] Pré-visualização inicial no Power BI (print ou link do arquivo)
- [ ] Log de Decisões de Dados (DEC-001 a DEC-005) (US03)
- [ ] Documentos da Sprint 1 aprovados pelo orientador (US04)
- [ ] Repositório publicado com `docs/`, `notebooks/`, `powerbi/` e README (US05)
- [ ] Confirmação do cliente sobre o ano-base 2024 (mensagem do grupo)

## 5. Estrutura do repositório

```
observatorio-sjc/
├── README.md
├── RELATORIO_SPRINT_1.md
├── MVP/           MVP de cada sprint
├── docs/          documentação Scrum e relatório técnico
├── notebooks/     ETL em Google Colab
├── powerbi/       dashboard
└── evidencias/    prints e comprovações da Sprint 1
```

## 6. Pendências e riscos

| Pendência | Impacto | Encaminhamento |
|---|---|---|
| Dados nominais de estabelecimentos (DEC-004) | Define o formato do ranking de empresas (US07) | Aguardar a Secretaria. Se negativo, aplicar o ranking agregado por setor e região |
| Detalhamento das Entregas 2 e 3 | Planejamento das Sprints 2 e 3 | Confirmar com os professores. Datas previstas: 26/10/2026 e 23/11/2026 |
| PIB dos Municípios (IBGE) ainda a filtrar para SJC | US09 depende da abertura por setor, que precisa ser confirmada na edição 2022–2023 | Filtrar na Sprint 2 e confirmar se há abertura por setor de atividade |
| Mapa dos estabelecimentos (US06) | Exige taxa de acerto acima de 90% na geocodificação | Geocodificar a partir do CEP presente na base da RAIS, conforme Morelli, Fiedler e Cunha (2023) |

## 7. Próximos passos

**Sprint 2 (entrega em 26/10/2026): análises centrais e mapeamento geográfico**

1. US06: mapa da distribuição geográfica das empresas, com geocodificação via CEP.
2. US07: ranking das empresas que mais contratam, com filtro por setor.
3. US08: setores e áreas em alta em contratação.
4. US09: impacto do ecossistema de empresas no PIB municipal.

**Sprint 3 (entrega em 23/11/2026): consolidação e entrega final**

1. US10: contratações mais recentes registradas na RAIS.
2. US11: dashboard consolidado, relatório técnico final e apresentação.

A Feira de Soluções (03/12/2026) é o marco de apresentação final.

## 8. Equipe

| Integrante | Papel |
|---|---|
| Pedro Henrique Oliveira de Carvalho | Product Owner |
| Juliano Souza Santana | Scrum Master |
| Beatriz Oliveira Sepulvida | Scrum Team |
| Caio Moreira | Scrum Team |
| Hemilly Christiny da Silva Freitas | Scrum Team |
| João Pedro Faria Vital de Souza | Scrum Team |
| Milena Silva Nogueira | Scrum Team |
| Thalya Awany Berti | Scrum Team |

---

*Última atualização: 04/10/2026*
