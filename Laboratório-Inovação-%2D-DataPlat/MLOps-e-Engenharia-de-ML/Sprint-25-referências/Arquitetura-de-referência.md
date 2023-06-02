# Fluxo esteira MLOps 

O fluxo abaixo ilustra cada uma das etapas do ciclo de vida de modelos de machine learning, com foco nas automações de MLOps, respeitando as etapas do ciclo de desenvolvimento de ML:




<IMG  src="https://www.saviantconsulting.com/images/blog/machine-learning-development-lifecycle.jpg"  alt="How are CIOs successful at Machine Learning Implementation?"/>


###Detalhamento por fase

- Compreensão do negócio e do problema: Nesta etapa, o objetivo é entender o objetivo do projeto e o contexto dos dados. Isso inclui entender os objetivos do negócio, os problemas a serem resolvidos e os dados disponíveis. Também é importante definir claramente os objetivos e metas do projeto de mineração de dados.

- Preparação dos dados: Nesta etapa, os dados são coletados, limpos e preparados para análise. Isso inclui tarefas como coletar dados de fontes diversas, lidar com dados ausentes ou inconsistentes, formatar dados e transformá-los para adequá-los às necessidades do projeto.

- Modelagem dos dados: Nesta etapa, os dados são explorados e modelados para gerar insights. Isso inclui tarefas como visualizar dados, descobrir padrões e relações, selecionar e aplicar modelos de mineração de dados.

- Avaliação: Nesta etapa, a qualidade e a validade dos modelos gerados são avaliadas. Isso inclui tarefas como verificar a precisão e validade dos modelos, avaliar a robustez dos modelos e identificar problemas.

- Implantação: Nesta etapa, os modelos gerados são implementados em um ambiente de produção. Isso inclui tarefas como preparar os modelos para uso em produção, testar os modelos em ambientes de produção e monitorar o desempenho dos modelos em produção.

- Monitoramento: Nesta etapa, os modelos implementados são monitorados e mantidos. Isso inclui tarefas como monitorar o desempenho dos modelos, identificar e corrigir problemas e atualizar os modelos com novos dados.

É importante notar que essas fases não são linear e sim iterativa, e é possível retornar a uma fase anterior caso seja necessário, e que as fases não tem necessariam


# Como fica todo um fluxo de MLOps dentro de uma squad de dados?

![Captura de Tela 2022-12-14 às 19.28.30.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2019.28.30-dae6ba6d-86b7-4634-8440-114bbcca9974.png)



# Arquitetura de referência CCR


![MicrosoftTeams-image (3).png](/.attachments/MicrosoftTeams-image%20(3)-9a195695-bfb6-4ead-ad40-61b58297108d.png)


`Desenho revisado em 30 de maio de 2023`

## Etapas desenvolvidas pela engenharia de dados

- Data Extraction
- Data Validation
- "commit" dos notebooks anteriores no REPO

## Etapas desenvolvidas pelo cientista de dados
- Data Preparation
- Feature Selection
- Model Selection
- Model Training
- Model Validation
- "commit" dos notebooks no REPO

## Etapas do ML Engineer
- Feature Engineering to Feature Store
- commit notebook Feature Engineering
- Model deployment
  - Model registry update
  - Model promotion (staging ou production)
  - Model serving (batch inference)
- Model Prediction
- Save Predictions em uma Delta Table

## Etapas automatizadas da Esteira MLOps (ML engineer)
- Model execution (batch inference)
- Metrics checking (monitoramento de métricas do modelo)
- Se métricas estão dentro do range esperado
  - segue normalmente
- Se métrica fora do esperado (Loop por no máximo 3 vezes)
  - efetua retreino do modelo
  - checa novamente as métricas
  - Se métrica melhorou
    - Registra novo modelo
    - promove 
    - efetua o commit do notebook retreino no REPO
    - Batch serving
    - efetua predictions
    - salva predictions    
- Caso contrário, se passou no loop 3 vezes e não melhorou
    - envia aviso de que o modelo precisa ser retreinado  


# Etapas desenvolvidas

1. Split notebooks
   - data prep
   - feature engineering
   - model registry
   - model promotion
   - model serving - batch inference
   - commit notebooks no REPO
2. Pipeline Data Factory
   - link com Databricks
   - Pipeline monitoramento
     - registro de métricas em uma tabela
     - checagem de métricas
     - etapas automatizadas de monitoramento
     - gravação de métricas
3. Teste Pipeline
   

# Itens pendentes

- Auto commit de notebooks
- Deploy integrado com Azure DevOps 
