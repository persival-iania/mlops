# Integração Data Factory com Databricks

## O que é o Azure Data Factory?

É um serviço de integração de dados baseado em nuvem que permite criar fluxos de trabalho orientados a dados na nuvem para orquestrar e automatizar a movimentação e transformação de dados. 

No Data Factory, há três atividades suportadas: 

- movimentação de dados, 
- transformação de dados e 
- atividades de controle. 

O Azure Data Factory anunciou no início de 2018 que uma integração completa do Azure Databricks com o Azure Data Factory v2 está disponível como parte das atividades de transformação de dados, ou seja é possível criarmos uma esteira de DataOps integrada à todos os recursos do Databricks através de uma interface *"low code"*


<IMG  src="https://www.element61.be/sites/default/files/img_knowledge_base/architecture.png"  alt="How can we use Azure Databricks and Azure Data Factory to train our ML algorithms?"/>


## Orquestração

Podemos utilizar o Azure Data Factory como um orquestrador de todo o ciclo de MLOps, como por exemplo:

- acionamento de modelos para predição
- treino e teste de modelos
- monitoramento de modelos em produção


# Fazendo uma predição de um modelo no Databricks através do DataFactory

## 1. Iniciando o Data Factory


Primeiramente iniciamos o serviço ##Data Factory Studio#

![Captura de Tela 2022-12-14 às 16.31.45.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.31.45-3b99e335-eb5a-454d-9686-a8ec08480594.png)

#

## 2. Iniciando uma orquestração

Uma vez iniciada, esta é a interface do Data Factory Studio

![Captura de Tela 2022-12-14 às 16.32.57.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.32.57-59da0678-855c-4b82-aae6-460ef2b0037d.png)

Nesta página vamos escolher a opção do 2o botão **ORQUESTRAR**

![Captura de Tela 2022-12-14 às 16.34.33.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.34.33-8aa877ec-7f24-4bbc-8a98-eccae61ce911.png)

## 3. Criando um pipeline

Na interface de *pipelines* selecione no menu à esquerda a opção de criar um novo pipeline

![Captura de Tela 2022-12-14 às 16.41.47.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.41.47-fbad29d4-c051-46ce-b623-ae55c51fc2cb.png)





