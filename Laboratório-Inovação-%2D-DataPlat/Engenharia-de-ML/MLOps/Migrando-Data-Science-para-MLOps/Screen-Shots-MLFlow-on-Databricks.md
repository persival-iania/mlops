# Interface MLFlow 


### Interface default do Databricks

Quanto trabalhamos com engenharia de dados ou ciência de dados, utilizamos esta interface no Databricks

![Captura de Tela 2022-12-14 às 12.37.26.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2012.37.26-711bc45d-3c7c-498d-9cd8-721aa58bcbf2.png)

### Interface MLOps

Para MLOps utilizamos a aba **Machine Learning** bem no alto à esquerda e passamos a ter esta interface:

![Captura de Tela 2022-12-14 às 12.38.03.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2012.38.03-398c912d-6df8-4fb8-a2b9-932c2a61baf1.png)


# 1. MLFlow Experiments


![Captura de Tela 2022-12-14 às 13.08.34.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.08.34-7e939172-3c8a-4f07-97c9-29b1a4748753.png)

Nesta interface são registrados todos os dados dos experimentos, em cada linha temos o nome do experimento criado, o local onde estão registrados os dados, data e hora e quem criou

## 1.1 Detalhes do experimento

![Captura de Tela 2022-12-14 às 13.15.23.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.15.23-c295d7ef-7483-4539-abc9-9b324f0ff18f.png)

Esta interface apresenta os modelos matemáticos ou de machine learning utilizados e em cada linha apresenta:

- o modelo matemático utilizado no experimento (no nosso exemplo xgboost, lightgbm, random forests, decision tree, etc)
- data da execução do experimento
- duração da execução
- um link para o notebook com o código fonte do experimento
- o framework de machine learning (por exemplo sklearn, Pytorch, Tensorflow)
- e as métricas obtidas na validação do modelo


### 1.2 Detalhes de um modelo específico

![Captura de Tela 2022-12-14 às 13.30.58.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.30.58-693bff7e-10a6-4b4d-9d3c-19695022da27.png)

Esta interface apresenta todos os **Artifacts** do modelo, como ele pode ser acionado e permite ao engenheiro de ML que faça o registro do modelo para inferência


# 2. Feature Store

Conforme mencionado em outro tópico, os modelos consomem Features e no Databricks temos como consultar as feature tables criadas.

![Captura de Tela 2022-12-14 às 13.34.10.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.34.10-cec7a144-de53-4de6-9b68-816982754e6a.png)

### 2.1 Consultando uma feature table

![Captura de Tela 2022-12-14 às 13.35.58.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.35.58-e11943d0-7625-4555-8df3-3e906391e972.png)

Interface que apresenta detalhes da **feature table**:

- nome da feature table (ou conjunto de features)
- data de criação
- data da última atualização
- chave primária ou indíce das features
- userid de quem criou as features
- fontes de dados que geraram as features
- descrição da feature
- link para o código fonte ou notebook que criou as features

### 2.2 Detalhes das features da tabela

![Captura de Tela 2022-12-14 às 13.39.03.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.39.03-8374343e-660c-43b2-a3c3-a49eb9c3f5ff.png)

Fazendo um "scroll down" da página anterior verificamos todas as features da tabela.

# 3. Model Registry


![Captura de Tela 2022-12-14 às 13.49.46.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.49.46-1322507b-dee2-4190-9fd9-e7735087919a.png)

 
Aqui nesta interface temos as informações dos modelos armazenados dentro do **Model Registry**

Contém as seguintes informações

- Name: nome do modelo
- Latest Version: a última versão do modelo, o MLFlow versiona automaticamente os modelos	
- Ambiente da versão corrente do modelo: "Staging" ou "Production"
- Last Modified: data da último update no Registry
- Tags: caso sejam informadas tags no registro
- Serving: indica se o modelo está sendo atualmente **"servido"** ou seja está disponível para inferência externa

### 3.1 Detalhes do registro do modelo

![Captura de Tela 2022-12-14 às 13.56.19.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2013.56.19-33d934a4-7ef8-4c0c-b830-326cb429a900.png)

Inferface que exibe informações como o **Schema** de acionamento do modelo, como por exemplo os parâmetros de input e o output da predição do modelo

Através desta interface o Engenheiro de Machine Learning efetua a liberação do modelo para ser acionado de forma batch ou on-line via API ou mesmo em Python ou gerar um container.