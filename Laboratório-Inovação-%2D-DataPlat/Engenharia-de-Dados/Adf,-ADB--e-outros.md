![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-de75df70-57dd-45af-b692-bb50b8c27d89.png)

# Padronização do Armazenamento dos arquivos

Foi construído um padrão para armazenagem das automações construídas, por pastas e subpastas, conforme o conjunto de assuntos e sub-assuntos para cada ferramenta disponibilizada no portal


1. **ADF: Padronização dos caminhos, pastas e subpastas**
<IMG  src="https://geekshangout.com/wp-content/uploads/2021/11/azure-data-factory-feature-e1637705398102.png"  alt="Azure Data Factory – How to backup and restore a pipeline – Geeks Hangout"/>
![adf_pastas.JPG](/.attachments/adf_pastas-3c6a415c-2cac-40f1-8c51-e1ea3bcedf9a.JPG)
Padronização dos nomes:

As pastas deverão ser criadas com os nomes maiúsculos, seguindo a padronização de até 3 steps sendo eles divididos entre as fontes de dados e os projetos

**Fonte de dados**: Esta deverá conter a origem dos dados, por exemplo:

1. Step 1 : Sistemas diversos
  
a. *Fonte*: ORACLE, SQLSERVER, FTP, SFTP, SAP, FIREBIRD ..
 Toda origem será, obrigatoriamente, associada um desenho template seguindo a estrutura inicial apresentada. sobre ingestões de dados, este template deve ser executado para cada tarefa seguindo a padronização;

b. *Sistema*: Nome dos que serão inseridos, do qual deriva o dado: por exemplo: SUAT

c. *Assunto*:  Referencia do micro grupo do Domínio no caso de Rodovias temos as concessionárias tais como: Autoban, ViaOeste ou o Sistema

d. *Nome do arquivo*: Padronização do arquivo de configuração os 3 e 2 primeiros 
dígitos informarão o tipo do arquivo que será utilizado

 2. **Projetos** será a primeira pasta da estrutura o que diferenciará a fonte do dado.

Seguirão dentro desta pasta os dados referente ao desenvolvimento especifico para atender a particularidade de cada projeto, respeitando a divisão:

a: Domínio: Refere-se ao grupo principal da CCR sendo eles das Rodovias,  Mobilidade e Aeroportos , GBS com a area a qual se refere, exemplo Rodovias-Callcenter, descrição principal do projeto

b. Assunto do Projeto

c. Nome do arquivo


## Nomes dos componentes 
Os nomes de cada sub-recurso do ADF deverão iniciar com as primeira letras conforme tabela abaixo, para determinar qual o tipo do sub-recurso

Nomes dos componentes deverão iniciar com

1. **pip – para pipeline**

2. **trg – para trigger**

3. **df - para dataflow**

4. **ls – para linked servisse**

5. **ds –para dataset**


#Parametrização:

A parametrização, dados que serão dados a alguma condição da programação deve vir do lake. Ou seja, Todos os parâmetros serão passados via arquivo json, disponibilizado individualmente para cada ingestão no contêiner de configurações (config)

**Modelo dos parâmetros**

{
  "datasetorigem": {
    "nomeCarga": "pip_oracle_autoban_avniew_transacao",
    "descricao": "Ingerir os dados da tabela Transação no lake",
    "schema": "AVINEW",	
    "tabela": "TRANSACAO",
		"sistema": "AUTOBAN",
		"chaveparticao": "DTTRANSACAO",
    "query": "SELECT * FROM AVINEW.TRANSACAO WHERE DTTRANSACAO >= SYSDATE-40",
    "sefull": "N"
	 },
  "datasetcarga": {
    "filesystem": "bronze",
    "directory": "ORACLE/AUTOBAN/AVINEW/TRANSACAO/TRANSIENT",
    "file": "transient_transacao"
	 },
  "datasetcargadia": {
    "filesystem": "bronze",
	"directory": "ORACLE/AUTOBAN/AVINEW/TRANSACAO/TRANSACTIONAL/",
	"file": "transacao"
	 },
  "datasetsilver": {
    "filesystem": "silver",
    "directory": "ORACLE/AVINEW/TRANSACAO/",
    "file": "transacao"
	 }
}



#Triggers:

Há dois tipos de triggers principais que serão utilizadas no projeto:

1. Por eventos:

  Programada a partir de alguma alteração ou movimentação de um blob

2. Por schedulle:

Programada por periodicidade, seja ela diaria, mensal, semanal, intra-hora, entre outras


###Para estas deverão seguir a padronização de nomenclatura abaixo:

![triggers.JPG](/.attachments/triggers-07544a67-f470-48a0-b820-d00ec1f0d4d7.JPG)



Aonde, em por Schedule temos:

a. TIPO: Refere-se ao tipo de recorrência: diária, semanal, IntraHora, Mensal, 30min

b. Recorrência: Refere-se quantas vezes se repete:
1. Para todos os dias da semana incluir apenas a notação diária e ir para o horário
2. Para um ou mais dias incluir semanal e a quantidade e os dias exemplo: 2_seg_ter
3.  Para mensal incluir mensal e o dia da semana que vai rodar exemplo: _10_
4. Para intra-hora incluir os dias ou intervalo que rodam seg-sab, seg-dom, de_8-10h

c. Time: HH e MM que irá rodar o evento, exemplo: _10h00min ou _13h30min. E no caso de intra-hora ou de 30 min incluir o intervalo exemplo: _30min, _1h, _2h


##Padronização da nomenclatura do dataflow:

_**df_assunto_subassunto**_

- [ ]   Aonde df faz referência ao nome **d**ata **f**low



#Padronização da nomenclatura do Dataset:

Para dados que serão tratados: 

**ds_input_ou_output_3letrasdaorigem+assunto_Ou_tipo_3letrasambiente_useroulocal**

Aonde,
##ds
1. ds: DataSet

##Input ou Output
1. input será usado para arquivos que serão tratados e 
2. output para os arquivos que sairão

##Origem ou tipo de arquivo:

A origem pode ser:

_1. Para bancos de dados (Sql/noSql)_
 
Nestes casos, iremos colocar as 3 primeiras letras do serviço exemplo:

- [ ] _ora_ para dados provindos do oracle

- [ ] _fon_: para dados provindos dos diversos banco de dados, ser par SqlServer, Fir para firebird, ou seja, deverão ter os 3 primeiros dígitos

_Para outros tipos de fontes:_

- [ ] _xls_ para dados provindos do excel

- [ ] _csv_: para dados provindos de csv

- [ ] _txt_: para dados provindos de txt
* deverá conter após o txt, o tipo de separador, exemplo 
 ds_txt_virgula ou ds_txt_ptovirgula ....


##Assunto ou sistema:

Logo após o detalhamento da fonte de dados, no caso de um banco de dados, deverá ter a referência da informação

Por exemplo, oracle do sistema suat, teremos: _ds_input_oracle__**suat**_...


##ADF e Lógic APPS: Padronização dos caminhos, pastas e subpastas



Padronização dos nomes:
:
As pastas deverão ser criadas com os nomes maiúsculos, seguindo a padronização de até 3 steps sendo eles divididos entre as fontes de dados e os projetos

![Imagem1.png](/.attachments/Imagem1-342f9447-1111-4afa-8e28-b7028432f309.png)

Databricks e Logic APPs


1. Area: que desenvolveu exemplo: Engenharia, Cientistas de dados

2. Fonte de dados: Esta deverá conter a origem dos dados, por exemplo:

  2.1.  Fonte: ORACLE, SQLSERVER, FTP, SFTP, SAP, FIREBIRD ..

*Toda origem será, obrigatoriamente, associada um desenho template seguindo a estrutura inicial apresentada. sobre ingestões de dados, este template deve ser executado para cada tarefa seguindo a padronização;

Ou Sistema: Nome dos que serão inseridos, do qual deriva o dado: por exemplo: SUAT 

3. Domínio: Refere-se ao grupo principal da CCR sendo eles Rodovias,  Mobilidade e Aeroportos , GBS; 

2) Fonte de dados ou contêiner do qual origina o dado
3) Assunto: Assunto principal
4) Subassunto ou projetos

###Nome do notebook

adb_brevedescriacaoassunto_subassunto.py

###nome da programação

lap_brevedescricaodatarefa                                                                                                                       



