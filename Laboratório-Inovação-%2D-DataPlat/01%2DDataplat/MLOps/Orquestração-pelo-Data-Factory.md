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

## 4. Integrando ao Databricks

Assim que iniciar a criação do novo pipeline abrirá uma janela de **Atividades** e em seguida clique na 5a opção **Databricks**

![Captura de Tela 2022-12-14 às 16.45.11.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.45.11-ee8b27f2-2c7d-4c79-8227-357bf29625ae.png)

Aqui veremos que temos 3 opções
- **Caderno** (aqui a versão está traduzida, mas é **Notebook**)
- **Jar** para acionamento direto de um Jar no Databricks (pergunte para um arquiteto o conceito de Jar)
- **Python** para execução de código Python diretamente

Para nosso tipo de pipeline iremos conectar diretamente à um **Notebook** (neste exemplo traduzido, opção **Caderno**)



## 5. Integrando com um Notebook no Databricks

Clique e arraste a opção **Caderno** (ou **Notebook** na versão original em inglês)

![Captura de Tela 2022-12-14 às 16.49.50.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.49.50-e026904f-3ea2-40f0-99b6-04fd98279856.png)

### Vamos preencher os dados gerais

![Captura de Tela 2022-12-14 às 16.52.26.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.52.26-24e591bc-6ebd-438e-a6ac-64131d7d77b2.png)

Nesta aba informamos dados descritivos da tarefa que estamos criando.

## 6. Conectando ao Databricks

Na aba **Azure Databricks** iremos informar o serviço vinculado, este serviço já vir totalmente configurado pelos nossos Arquitetos da Plataforma, basta selecionarmos.

![Captura de Tela 2022-12-14 às 16.53.35.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.53.35-89f6b579-5b9f-4102-816b-509da539838c.png)

### recomendável testar a conexão, 

- basta clicar no botão **Testar Conexão** 
- caso ocorra algum tipo de erro, contatar algum administrador da Plataforma

![Captura de Tela 2022-12-14 às 16.55.27.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.55.27-fc3e5e53-830d-4a96-b307-e8aa230a7df0.png)

## 7. Conectando ao notebook no Workspace

Na aba **Configurações** em **Caminho do Notebook** clique no botão **PROCURAR**

![Captura de Tela 2022-12-14 às 16.57.24.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.57.24-7138ed44-eb2a-4902-8155-b739c7177056.png)


### O Data Factory irá abrir as pastas do Workspace onde seu usuário do AD permite acesso

![Captura de Tela 2022-12-14 às 16.59.06.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2016.59.06-3036be10-1f9f-45a7-931a-8d8983e98053.png)


### Navegue até o notebook

Navegue nas pastas do workspace e selecione o modelo que quer usar no pipeline e clique **OK** no final da página

![Captura de Tela 2022-12-14 às 17.00.15.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2017.00.15-9d83038f-1618-4099-894e-126d258d7ee4.png)


### Notebook pronto para execução

![Captura de Tela 2022-12-14 às 17.02.06.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2017.02.06-89a56d09-e123-4398-9d94-8ebbf7444bdb.png)

## 8. Testando o pipeline

### Clique no botão **DEPURAR** acima da imagem do notebook

![Captura de Tela 2022-12-14 às 17.02.58.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2017.02.58-841ff910-4faf-4d79-804c-f6956252ca8e.png)







