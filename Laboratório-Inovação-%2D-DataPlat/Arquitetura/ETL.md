![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-2f296e8d-d67e-4756-a1e1-19ca81506340.png)
# ETL

Trata-se do processo da carga, transformação e disponibilização dos dados a serem consumidos pela área solicitante.
Este é o processo fundamental para a disponibilização dos dados, realizado pelas áreas de engenharia de dados e engenharia de machine learning.

Para este tratamento, segundo a arquitetura proposta, são utilizados alguns recursos da plataforma Microsoft Azure. São eles:

- Data Factory ou ADF

- DataBricks ou ADB

- Logic Apps ou LApps

Para a disponibilização de dados no lake, e ferramentas de consumo de dados na camada semântica, utilizamos o ADF como orquestrador do processo de ETL e ferramenta para a primeira carga.

![Recursos.JPG](/.attachments/Recursos-f7da4d6e-a964-4862-93e0-caf1f5bfc1ce.JPG)

Os recursos são disponibilizados segundo domínio **(Rodovias, 
Mobilidade e Aeroportos , GBS)**, ou seja, há criação de um recurso por ambiente, sendo eles: Produção, Homologação e Desenvolvimento, e no caso do databricks há a disponibilização de dois recursos por área e ambiente:

## Datafactory


O Datafactory ou ADF, é um serviço de integração de dados, disponibilizado na plataforma Microsoft Azure, baseado na nuvem.

### ![adf_fontes.png](/.attachments/adf_fontes-7cf3b522-3f4a-4a2d-8ea6-be46f7e301be.png)***Fonte Figura:Microsoft***


Que automatiza o movimento e realiza a primeira carga oficial ao lake, além da orquestração da transformação de dados.

Para este projeto ele é utilizado como link de acesso a diversas fontes de dados, e realiza toda a orquestração do processo de ingestão dos dados no LAKE.

Realizamos a comunicação com o lake via usuário principal, acessando o nosso SPA com chaveamento e autenticação pré configurado, com acesso de leitura e escrita nas camadas desenvolvidas e apartadas por conteiners, há ambiente de desenvolvimento, homologação e produção. Ou seja, há autenticação da entidade de serviço, especificada a cada ambiente de nuvem do Azure em que o aplicativo do Azure Active Directory está registrado.

O ADF o usuário habilitado na VM de integração se conecta em todos os recursos disponibilizados para plataforma, sendo eles: lake, databricks, synapse.

#TODO
 
  - Keys e Tokens (Autenticação no lake)
  - Código do Pipeline de desenvolvimento (CI/CD)
  - Padronização dos arquivos de automação:


## Databricks
  - O que é
  - Como se desenvolve?
  - Pipeline de desenvolvimento (CI/CD)
  - Keys e Tokens (Autenticação no lake)
  - Secrets and Scopes
  - Cluster do Databricks

## ...Desculpe os transtornos, estamos em construção.
![construcao-002.png](/.attachments/construcao-002-49935089-a52d-4bee-9e1b-ecd4a117b108.png)