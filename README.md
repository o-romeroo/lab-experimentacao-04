# lab-experimentacao-04

## Dataset analisado (poc-ti6)

- Visão geral:
  - Prova de conceito que identifica repositórios OSS que "morrem" (período sem commits) e "ressuscitam" (retornam a commitar) entre 2018 e 2025.
  - Detecta lacunas de atividade de pelo menos 180 dias no branch padrão e registra a primeira morte e o primeiro retorno.

- Fonte e amostragem:
  - API: GitHub GraphQL API.
  - Consulta utilizada: `created:2018-01-01..2025-12-31 sort:stars`.
  - Amostragem atual: primeiros 10 repositórios retornados pela busca (prova de conceito).
  - Commits considerados: histórico mais recente (até 100 commits) do branch padrão do repositório.

- Estrutura e campos (saída principal em Excel):
  - Nome (string): owner/repo.
  - Stargazers (int): número de estrelas.
  - URL (string): link do repositório.
  - Data de morte (date, ISO 8601): última data de commit antes do gap ≥ 180 dias.
  - Data de ressurreição (date, ISO 8601): primeira data de commit após o gap.
  - Morreu após reviver (int {0,1}): 1 quando há mais de um período de inatividade após a primeira ressurreição, 0 caso contrário.

- Critérios e regras:
  - Inatividade ("morte") = diferença entre commits consecutivos ≥ 180 dias.
  - Apenas o branch padrão é analisado.
  - Primeiro período detectado é usado para rotular morte/ressurreição; períodos adicionais acionam o indicador "Morreu após reviver".

- Pré-processamento e limitações conhecidas (versão atual):
  - Limite de commits: apenas os 100 commits mais recentes; gaps mais antigos podem não ser detectados.
  - Viés de popularidade ao ordenar por estrelas.
  - Busca restringe-se a repositórios criados entre 2018–2025.
  - Possível impacto de fuso horário (datas estão em ISO 8601/UTC) e de rate limits da API.

- Artefatos gerados:
  - Arquivo Excel: `repositorios_morte_ressurreicao.xlsx` contendo as colunas acima.

- Reprodutibilidade (script de coleta):
  - Script: `pipeline-unificado-v1.py` (Python; depende de requests e pandas).
  - Como executar: `python pipeline-unificado-v1.py` (necessita variável/token GitHub válido para GraphQL API).
