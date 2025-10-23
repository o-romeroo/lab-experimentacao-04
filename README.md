
# Caracterização do Dataset

## Origem
O dataset utilizado nesta pesquisa é derivado dos resultados da Fase 1 (`dataset_fase1_validacao.xlsx`), contendo repositórios de software livre que passaram por períodos de inatividade ("morte") e posterior revivência entre 2018 e 2025. Os principais campos do dataset são:

- `owner/repo`
- `url`
- `stargazers`
- `data_morte`
- `data_ressurreicao`
- `morreu_novamente`

## Estrutura do Dataset
- **Aba 1:** Repositórios mortos (sem revival)
- **Aba 2:** Repositórios ressuscitados (com revival detectado)
- **Aba 3:** Estatísticas gerais da coleta

## Foco da Pesquisa
O foco central deste estudo é a **qualidade do código** dos repositórios em dois momentos:

1. **No momento da morte** (commit imediatamente anterior à `data_morte`)
2. **Após a revivência** (10 commits após a `data_ressurreicao`)

Essa abordagem permite comparar a evolução da qualidade do código antes e depois do processo de ressuscitação dos projetos.

## 1. Snapshots
Para cada repositório ressuscitado, são gerados **dois snapshots** do código:

- **Pré-morte:** commit anterior à `data_morte`
- **Pós-revive:** 10º commit após a `data_ressurreicao`

## 2. Ferramentas de Análise
A análise de qualidade é realizada utilizando o **SonarQube Cloud** (https://sonarcloud.io/organizations/ti6/projects) e o `sonar-scanner-CLI`, que fornecem métricas detalhadas de qualidade, segurança e manutenibilidade do código.

## 3. Métricas Coletadas por Snapshot
As principais métricas extraídas de cada snapshot são:

- **Maintainability / Reliability / Security scores** (SonarQube)
- **Complexidade ciclomática** (média e máxima)
- **Percentual de duplicação de código**
- **Quantidade de code smells**
- **Número de vulnerabilidades**
- **Cobertura de testes (%)** (quando disponível)

No contexto deste trabalho, as métricas efetivamente coletadas são:

- **M3.1:** Métricas de análise estática de código (complexidade, duplicação, code smells)
- **M3.2:** Índice de maintainability/qualidade Sonar (pontuação agregada de qualidade e segurança)

## 4. Questões de Pesquisa (RQs)

**RQ1:** Como a qualidade do código evolui após a revivência dos repositórios OSS?

*Métricas analisadas:*
- Maintainability score (SonarQube)
- Quantidade de code smells
- Complexidade ciclomática média

**RQ2:** Quais aspectos de qualidade de código mais se alteram entre o momento de morte e o pós-revive?

*Métricas analisadas:*
- Percentual de duplicação de código
- Número de vulnerabilidades
- Índice de reliability (SonarQube)

Essas métricas são extraídas e comparadas entre os snapshots pré-morte e pós-revive, permitindo avaliar o impacto da revivência na qualidade do código dos projetos analisados.
