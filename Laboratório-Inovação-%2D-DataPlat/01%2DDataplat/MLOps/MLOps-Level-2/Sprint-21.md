# 5) Título Estória:  Esteira Nível 2 MLOps

**Objetivo:** `Criação da esteira Nivel 2 de MLOPS, utilizando o Databricks como Framework / Cluster, orquestração sendo realizada pelo Factory e versioning/ CI CD sendo realizando pelo Az DevOps` 

- Parâmetros de Entrada: Modelo do Data Scientist
- Saída Esperada: Dados Treinados, Métricas calculadas, Retreino Automático e Deploy Automático.
- Formato do Entregável: notebook do Databricks , config. Az. DevOps, Parte do Projeto do Data Factory Orquestração 
- Condições de Validação da Entrega:   Valido ou Valido Parcial ou Inválido       
- Notebook do DataBricks: Codigo que irá conter cada parte da orquestração da esteira de treino                      
- Codigo que irá conter cada parte da orquestração da esteira d Execução
- Config. Az DevOps:   Codigo JSON, no qual irá conter as sessões de CI levando em consideração o TRIGGER                              
- Código JSON, no qual irá conter as sessões de CD levando em consideração o modelo GIT Adotado (padrão XXXX)                           
- Orquestração no Data Factory:             
- Esteira 1 Treino (Coleta, Limpeza, Feature Store, Treino, Versionamento do Modelo, Versionamento do Código, Gravação Dados, Métricas                                                 
- Esteira 2 Execução ( Subir O modelo em Execução, Acionamento, Fazer Predição, Gravar os Dados, Calcular as Métricas, Avaliar as Métricas , Se métrica for satisfatória, então encerrar, senão chamar a esteira de treino novamente.


#Escopo Técnico

1. Eleger um modelo de um data Scientist
1. Efetuar o split do notebook nas 6 etapas MLOps
1. Permitir CI/CD integrado ao Azure DevOps
1. Identificar métricas a serem monitoradas
1. Registrar métricas dos modelos em uma tabela para monitoramento pelo Data Factory
1. Definir triggers para as métricas
1. Entregar notebooks de cada etapa/fase
1. Criar tabela ou ponto de referência no Data Factory para monitorar as métricas
1. Desenvolver orquestração Data Factory para monitoramento e acionamento da esteira MLOps nível 2
1. Esteira 1 Treino (Coleta, Limpeza, Feature Store, Treino, Versionamento do Modelo, Versionamento do Codigo, Gravação Dados, Metricas
1. Esteira 2 Execucao ( Subir O modelo em Execução, Acionamento, Fazer Predição, Gravar os Dados, Calcular as Metricas, AvaliarMetricas                                                      
1. Se metrica for satisfatória, então encerrar, senão chamar a esteira de treino novamente.
1. Gerar documentação do processo


`(avaliar se iremos ter a situação de atuarmos em 3 instâncias do Databricks DEV/UAT/PROD) - dúvida...`

#Desmembramento da estória na visão técnica
### Grupo de tarefas, sub-tarefas e entregáveis

## 1. Componentes do Databricks

- split do modelo do Data Scientist
- **alternativa** Persival e Fabricio criam o modelo com dados reais em cima de uma esteira DataOps já existente e em uso por Analytics ou BI
- retreino
- avaliação
- CI
- CD: promoção staging e/ou production
- Serve 
- monitoramento de métricas
###Entregáveis:
1. Notebooks criados no Databricks
1. JSON e configurações necessárias ao Azure DevOps
1. Desenho arquitetura e fluxo da esteira

##2. CI do Databricks com o Azure DevOps

- Definir fluxo de CI dos notebooks
- Etapas manuais
- Etapas automatizadas integradas ao Azure DevOps
- Testes CI com os notebooks criados na "sub-estória"
###Entregáveis:
1. JSON e configurações necessárias ao Azure DevOps 
1. Evidências dos testes

## 3. Esteiras Data Factory
- Criar tabela com registro das métricas para acesso pelo Data Factory
- Pipeline programado(pode ser diário ou configurável) para monitoramento de métricas
- Manter métricas dos modelos atualizadas na tabela (Databricks)
- Manter indicadores de histórico e resultados das execuções de cada esteira
- Eleger `caso de teste`: dados de entrada esperados, condições do trigger, saida esperada
- `Esteira 1`: **Treino** feature engineering, feature Store, treino, versionamento do modelo, versionamento do código, gravação Dados, métricas
- `Esteira 2` **Execução** Subir modelo em execução, acionamento, fazer predição, gravar os dados, calcular as métricas, avaliar métricas
###Entregáveis:
1. Definição das tabelas utilizadas
1. Pipeline criado no Data Factory
1. Parametrização dos Pipelines
1. Integração Databricks
1. Integração Azure DevOps
1. Evidências dos testes         
                           
              
## 4. Backlog ou itens adicionais
-  Documentação Final na Wiki
- Avaliar o uso de mais de uma instância na esteira (decidir após reunião com Databricks)
- Treinamento