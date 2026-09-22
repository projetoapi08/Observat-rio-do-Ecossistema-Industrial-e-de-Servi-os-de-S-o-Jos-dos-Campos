# Documento de Visão e Escopo do Projeto

## 1. Nome e descrição resumida do projeto

**Nome:** Observatório do Ecossistema Industrial e de Serviços de São José dos Campos

**Descrição:** Ferramenta de Business Intelligence, desenvolvida em Power BI e inspirada no modelo do Observatório da Inovação RS (Secretaria de Inovação, Ciência e Tecnologia do Rio Grande do Sul), que mapeia o ecossistema industrial e de serviços de São José dos Campos a partir de dados de contratações formais (RAIS) e do PIB municipal (IBGE). O painel permite identificar os maiores empregadores, os setores em crescimento, a distribuição geográfica das empresas na cidade e a participação estimada de cada setor no PIB municipal.

## 2. Problema real identificado

Gestores, analistas de mercado e órgãos de fomento local não dispõem de uma visão consolidada e visual sobre o comportamento do mercado de trabalho formal e o ecossistema produtivo de São José dos Campos — quais empresas mais contratam, quais setores estão em expansão, onde essas empresas estão concentradas geograficamente e qual o peso econômico de cada segmento na cidade. Os dados existem (RAIS, IBGE), mas estão dispersos e não são analisados de forma integrada e acessível. Outras esferas de governo, como o Estado do Rio Grande do Sul, já desenvolveram ferramentas públicas semelhantes (o Observatório da Inovação RS), mas São José dos Campos ainda não conta com um instrumento equivalente em escala municipal.

## 3. Cliente, organização ou público interessado

**Cliente:** CADI e Secretaria de Desenvolvimento Econômico de São José dos Campos

- Professor M2: José Jaétis
- Professor P2: Marcus
- Contato do cliente: Marcus, via grupo do WhatsApp
- Público interessado: órgãos municipais de desenvolvimento econômico, associações empresariais locais, estudantes e pesquisadores de economia regional

## 4. Justificativa do projeto

São José dos Campos é um polo industrial e tecnológico relevante no Vale do Paraíba, com forte presença dos setores aeroespacial, automotivo, químico e de serviços especializados, além de um ecossistema de inovação reconhecido (certificação internacional Platina em Smart City). Apesar dessa relevância, não existe um mapeamento estruturado e público da estrutura produtiva regional. O próprio cliente apresentou como referência o modelo de governança de hélice tríplice/quádrupla (Empresa, Academia, Sociedade, Governo) e o Observatório da Inovação RS como "modelo interessante" a ser seguido.

## 5. Objetivo geral

Desenvolver um painel analítico (observatório) em Power BI que consolide dados da RAIS e do PIB dos Municípios (IBGE) para apresentar indicadores sobre contratações, setores em alta, distribuição geográfica das empresas e impacto econômico das empresas de São José dos Campos, inspirado no formato do Observatório da Inovação RS.

## 6. Objetivos específicos

- Identificar as empresas com maior volume de contratações formais no município
- Apontar os setores/áreas (CNAE) com maior crescimento de contratações
- Estimar a participação de cada setor no PIB municipal, cruzando RAIS e dados do IBGE
- Mapear geograficamente a distribuição das empresas/setores no município, identificando concentrações (polos, distritos, hubs) quando os dados permitirem
- Exibir as contratações mais recentes registradas
- Permitir filtros por período e por setor de atividade

## 7. Público-alvo e personas

- **Gestor público/econômico:** quer indicadores para embasar decisões sobre desenvolvimento econômico local
- **Analista de mercado:** quer identificar tendências de contratação por setor e por região da cidade
- **Administrador do sistema:** quer manter os dados atualizados e o painel funcionando

## 8. Escopo incluído

- Coleta e tratamento de microdados da RAIS para o município de São José dos Campos
- Cruzamento com dados de PIB dos Municípios (IBGE) por setor de atividade (CNAE)
- Construção de dashboard interativo em Power BI com os indicadores definidos
- Classificação e mapeamento geográfico das empresas por setor de atividade e, quando aplicável, por tipo de ambiente de inovação (polo, hub, distrito, núcleo)
- Filtros por período (ano/mês) e por setor
- Documentação técnica do processo de ETL e do modelo de dados

## 9. Escopo explicitamente excluído

- Dados de emprego informal (não capturados pela RAIS)
- Previsões ou modelos preditivos de contratação (sugestão de trabalho futuro)
- Dados de empresas fora do município de São José dos Campos
- Aplicativo mobile ou sistema web próprio (entrega via Power BI/relatório publicado)
- Réplica completa dos quatro eixos do Observatório da Inovação RS (indicadores de pesquisa, editais da Fapergs, programas estaduais) — usado apenas como inspiração de formato/UX

## 10. Restrições de prazo, tecnologia, dados ou infraestrutura

- Prazo: 1 semestre letivo, dividido em 4 sprints
- Tecnologias definidas pelo cliente: Google Colab + Python 3+, Power BI, GitHub
- Dados limitados à granularidade e periodicidade de divulgação da RAIS (geralmente anual)
- PIB municipal por setor também segue periodicidade do IBGE (defasagem de divulgação)
- A RAIS não fornece coordenadas geográficas prontas das empresas

## 11. Critérios gerais de sucesso

- Painel publicado e funcional, com todos os indicadores planejados
- Dados da RAIS corretamente filtrados para o município de SJC
- Cruzamento RAIS x PIB validado com metodologia clara e documentada
- Painel apresenta ao menos uma visualização geográfica das empresas/setores
- Aprovação da equipe docente na entrega final

## 12. Tecnologias previstas

- Google Colab + Python 3+ (tratamento inicial dos microdados)
- Power BI (modelagem e visualização)
- GitHub (versionamento e documentação)
- Fontes de dados: RAIS e PIB dos Municípios (IBGE)
- Referência de formato/UX: Observatório da Inovação RS

## 13. Riscos iniciais e estratégias de mitigação

| Risco | Mitigação |
|---|---|
| Volume grande de microdados da RAIS pode ser difícil de processar | Filtrar por município (SJC) o quanto antes no ETL, usando Colab/Python |
| Defasagem entre a divulgação da RAIS e do PIB municipal | Usar o último ano disponível em ambas as bases e documentar isso |
| Dificuldade em estimar participação de empresa individual no PIB | Deixar claro que a estimativa é por setor de atividade (CNAE) |
| Tentar replicar o escopo completo do Observatório RS | Usar como inspiração de formato apenas; manter escopo restrito a RAIS + PIB |
| Falta de dado estruturado sobre localização exata das empresas | Usar bairro/distrito disponível na RAIS e documentar a limitação |
