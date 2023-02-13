![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-de75df70-57dd-45af-b692-bb50b8c27d89.png)
# Padronização do Armazenamento dos Dados
### Lake: Padronização dos caminhos, pastas e subpastas


Foi construído um padrão para o conjunto de assuntos e subasuntos no lake a fim de padronizar e harmonizar a visualização e consulta dos dados do LAKE.

Como já sabido, a estrutura se caracteriza pela metodologia de medalhas na qual temos as cargas realizadas no lake conforme, confiabilidade, tipo e tratamento dos dados.

Além da padronização e distribuição destes dados, se viu a necessidade de descer os níveis e estruturar as pastas e subpastas referente ao micro negócio.

Segue abaixo a padronização realizada e esperada para os novos desenvolvimentos:

**Conteiner config**

O conteiner config foi criado para ter disponibilizado os arquivos de parametrizações das tarefas desenvolvidas entre os recursos do azure.
Neste conteiner os arquivos devem ser carregados em formato json. Ou seja, os arquivos disponibilizados nesta camada, são arquivos de configuração, e são 
utilizados para parametrizar os códigos

As subpastas do conjunto de dados devem ser escritas em letras de caixa alta e o nome do arquivo e conteiner devem ser escritos em minúsculo.
 
![config.JPG](/.attachments/config-775b2e07-56ee-4e15-907e-8b6c1ecbcbf0.JPG)

Aonde,

1. Domínio: Refere-se ao grupo principal da CCR sendo eles Rodovias, 
Mobilidade e Aeroportos , GBS;
2. Assunto: Sistema do qual deriva o dado: o sistema que origina o dado por 
exemplo: SUAT
3. Subassunto: Referencia do micro grupo do Domínio no caso de Rodovias 
temos as concessionárias tais como: Autoban, ViaOeste;
4. Nome do arquivo: Padronização do arquivo de configuração os 3 primeiros 
dígitos informarão o local que será utilizado:
- [ ] pip: pipeline do ADF
- [ ] ntb: notebook do ADF
- [ ] lga: Logic APPS


**Conteiner bronze**

A Camada Bronze contempla os arquivos originais, exatamente como chegam a plataforma, cópia fiel da 
origem, ou agrupado em deltatable para reduzir espaço quando os dados são transacionais, ou seja, não há a carga full.
Nesta camada, os dados podem ter diversos formatos, tais como: csv, xls, parquet, avro ... 

As subpastas do conjunto de dados devem ser escritas em letras de caixa alta e o nome do arquivo e conteiner devem ser escritos em minúsculo.

![padro_bronze.JPG](/.attachments/padro_bronze-a2714fef-75c2-4e71-a149-2f7e2f14c70e.JPG)

Aonde,

1. Domínio: Refere-se ao grupo principal da CCR sendo eles Rodovias, 
Mobilidade e Aeroportos, GBS;
2. Fonte de dados: Refere-se a origem dos dados, se for um banco de dados 
informar qual ORACLE, SQLSERVER, SAS, se for de uma fonte manual 
provinda de um usuário seguir os passos:

    A. Input User: Informa que a origem dos dados é manual

       i. Area fonte: Area que disponibilizou o dado, Sharepoint ou FTP
       ii. Assunto: Sistema 
       iii. Subssunto: Concessionária
       iv. Nome do arquivo apenas abaixo desta pasta podem ser entregues os dados como cvs, xls diversas fontes
3. Assunto: Sistema do qual deriva o dado: o sistema que origina o dado por 
exemplo: SUAT
4. Subassunto: Referência do microgrupo do Domínio no caso de Rodovias 
temos as concessionárias tais como: Autoban, ViaOeste;
5. Referência: Nome da tabela, do arquivo, da informação referente ao dado
6. Particionamento: Os deltatables devem ser particionados por:
    **ano=yyyyy, mês=MM e dia=DD**
7. Nome do arquivo: Se particionado poderá ser mantido o nome da partição, 
caso contrário incluir o nome em minúsculo e sua extensão, lembrando que 
dados devem ser carregados como parquet e se particionado como deltatable



**Conteiner silver**

A Camada Silver contempla os dados confiáveis para consumo, já com alguns tratamentos, como eliminação de campos duplicados, filtros e union de dados. 
Nesta camada só é permitida a carga dos dados após a primeira carga realizada na camada bronze, e passados por ETL para tratamento e carga em formato delta table.


As subpastas do conjunto de dados devem ser escritas em letras de caixa alta e o nome do arquivo e conteiner devem ser escritos em minúsculo.

![padro_silver.JPG](/.attachments/padro_silver-9e97b17b-1ff5-4ad3-941d-f46a6c8374e0.JPG)

Aonde,

1. Domínio: Refere-se ao grupo principal da CCR sendo eles Rodovias, 
Mobilidade e Aeroportos, GBS;
2. Fonte de dados: Refere-se a origem dos dados, se for um banco de dados 
informar qual ORACLE, SQLSERVER, SAS, se for de uma fonte manual 
provinda de um usuário a estrutura assunto referência
3. Assunto: Sistema do qual deriva o dado: o sistema que origina o dado por 
exemplo: SUAT
4. Referência: Nome da tabela, do arquivo, da informação referente ao dado
5. Particionamento: Os deltatables devem ser particionados por
1. ano=yyyyy, mês=MM e dia=DD
6. Nome do arquivo: Se particionado poderá ser mantido o nome da partição, caso 
contrário incluir o nome em minúsculo e sua extensão, lembrando que dados 
devem ser carregados, como delta table

**Conteinêr gold**

Na camada gold, os dados são carregados de acordo com o projeto e conforme desenho do DATAMart em questão, os formatos permitidos são delta tables, e os dados são carregados por projetos e subdivididos em fatos e dimensões.

![padro_gold.JPG](/.attachments/padro_gold-b76d8b40-5f01-42be-931e-6cb3ecc31e21.JPG)

Aonde,

1. Domínio: Refere-se ao grupo principal da CCR sendo eles Rodovias, 
Mobilidade e Aeroportos;
2. Projeto área: Refere-se ao nome do projeto que foi implantado mais o nome da 
área a que ele atende
3. Assunto: Refere ao assunto principal que servira de base para encontrar o nome 
do datamart criado
4. Dimensão ou Fato: Nome da tabela, que foi tratada via databricks que fará parte 
do cubo, datamart montado para o projeto, sendo padronizada, com letras 
maiúsculas conforme será disposto:
1. Para dimensões o nome devera seguir DM_NOME_TABELA
2. Para fatos o nome devera seguir FT_NOME_TABELA
5. Particionamento: Os maiúsculas devem ser particionados por
1. ano=yyyyy, mês=MM e dia=DD
6. Nome do arquivo: Se particionado poderá ser mantido o nome da partição, caso 
contrario incluir o nome em minúsculo e sua extensão, lembrando que dados 
devem ser carregados, como delta tables

versão: v1-2022-10-11


#Stream

A seguir um padrão de armazenamento para Iot e mensagens tartadas no EventHub. Poderá ser aplicado também a CDC.

![Arquitetura_All-V3-Stream Iot.jpg](/.attachments/Arquitetura_All-V3-Stream%20Iot-f5c2bca9-17db-4641-92b1-cf9afc8984e2.jpg)