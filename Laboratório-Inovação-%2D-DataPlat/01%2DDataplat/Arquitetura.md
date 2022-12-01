![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-1a1b3763-69fa-4f6f-9907-bbdd76fabbbb.png)

Esse seção apresentará os pontos relevantes para a definição e concepsão do desenho arquitetural do produto Lab-DataPlat.

- [Visão Geral](#visão-geral)
- [Visão de Alto Nível](#visão-de-alto-nível)
  - [Fluxo dos dados](#fluxo-dos-dados)
    - [Integração](#integração)
    - [Ingestão](#ingestão)
      - [Data Lake](#data-lake)
    - [Visualização](#visualização)
    - [Machine Learning & Data Science](#machine-learning--data-science)
- [Leitura recomendada](#leitura-recomendada)
- [Continue Lendo](#continue-lendo)
- [Arquivos Anexos](#arquivos-anexos)

# Visão Geral

A nuvem está mudando a maneira como os aplicativos são criados, incluindo como os dados são processados e armazenados. Em vez de um único banco de dados de uso geral que manipula todos os dados da solução, as soluções de persistência poliglota usam vários armazenamentos de dados especializados, cada um otimizado para fornecer funcionalidades específicas. A perspectiva sobre os dados na solução muda como resultado disso. Não existem mais várias camadas de lógica de negócios que leem e gravam em uma única camada de dados. Em vez disso, as soluções são projetadas em torno de um pipeline de dados que descreve como os dados fluem por uma solução, o local em que são processados, o local em que são armazenados e como eles são consumidos pelo próximo componente do pipeline.

Para maior aprofundamento sobre o tema de Arquitetura de Dados no Azure, recomendamos a leitura do [Guideline](https://docs.microsoft.com/pt-br/azure/architecture/data-guide/) propostos pelo Azure.

# Visão de Alto Nível

O desenho arquitetural do projeto Lab-DataPlat visa atender a todo que qualquer projeto que deseje consumir os dados corporativos. Para uma visão geral do projeto, veja [aqui](./Introdu%C3%A7%C3%A3o).

O produto, por ser estruturante, será definirá padrões de desenvolvimento e processo para os demais projetos que queiram ser inseridos internamente ao produto.

## Fluxo dos dados

O fluxo de dados proposto para a ingestão e consumo segue o apresentado abaixo.
![Items (4).jpg](/.attachments/Items%20(4)-90749d95-dbe8-404c-8c17-2a1c265a8a7f.jpg)


### Integração

Para iniciar o fluxo de dados é necessário realizar a conexão com as fonte de dados necessária para fazer seu ideial consumo. Essa base de dados pode ser do tipo Relacional, Não relacional, Evento (Stream) e ou qualquer outro lugar ao qual tenham dados e deseja-se consumi-los, pode ser até um upload de arquivo.

Os desafios presentes nesse ponto são:

- **Protocolo de conexão**: Realizar a conexão com a origem do dado depende, diretamente, de quem é essa origem. Cada SGBD apresenta um protocolo de comunição, caso seja evento, acontecerá em outro formato, por exemplo utilizando o [Apache Kafka](https://kafka.apache.org/).
- **Autenticação**: É necessário definir as formas de autenticação do agente que irá fazer a ingestão dos dados.
- **Conectividade**: Uma vez tenha as formas de conexão com a base de dados, é necessário levantar se a infraestrutura do Lab-Dataplat tem visibilidade com a origem dos dados.  Caso não tenha, será necessario a verificar os pontos com o time de redes.

### Ingestão

Quando a conexão com a fonte de dados estiver bem estabelecida, é necessário entender qual o formato do dado que será importado para o *data lake*. Veja abaixo:

- **Janela de ingestão**: É necessário levantar qual a recorrência para a ingestão dos dados: Em lote (`batch`), em pequenos lotes (`microbatch`), Tempo real (`real-time`), ou Próximo ao Tempo Real (`near real-time`). Para essa decisão é necessário avaliar e modelar junto com a área cliente, donos dos dados (`data owners`), arquiteto de dados e o próprio engenheiro de dado.
- **Domínio**: É necessário concatenar dentro do data lake as informações de mesmo domínio, e para tal, é necessário envolver os data owners para definir as possíveis regras de mescla dos domínios.
> **Regra de mesclar** é uma regra de negócio que permiter concatenar os atributos de múltiplas fontes de dados em um mesmo domínio. Por exemplo: Digamos que tenhamos informações de alunos em duas fontes de dados: A e B. Dentro do Data Lake teremos, somente, um única entidade (domínio) de Aluno. Para tal, como será feita a junção dos dados de ambas fontes de dados.
- **Limpeza e padronização das informações (Data Cleasing)**: Ao realizar a ingestão dos dados, é necessário tratar os dados para que tenhamos informações padronizadas e confiáveis.

####  Data Lake

> *O Azure Data Lake inclui todos os recursos necessários para que seja mais fácil para desenvolvedores, cientistas de dados e analistas armazenar dados de qualquer tamanho, forma e velocidade, bem como realizar todo tipo de processamento e análise em diferentes plataformas e linguagens. Ele remove as complexidades relacionadas a ingerir e armazenar todos os seus dados, enquanto acelera a execução de análises em lote, streaming e interativas. O Azure Data Lake trabalha com investimentos existentes em TI para oferecer identidade, gerenciamento e segurança para que haja um controle e um gerenciamento de dados simplificados. Ele também tem integração direta com repositórios operacionais e data warehouses, de modo que você pode ampliar aplicativos de dados atuais. Aproveitamos nossa experiência de trabalho com clientes empresariais e da execução de algumas das análises e processamentos de maior escala no mundo para produtos da Microsoft como Office 365, Xbox Live, Azure, Windows, Bing e Skype. O Azure Data Lake soluciona muitos dos desafios de produtividade e escalabilidade que o impedem de maximizar o valor de seus ativos de dados com um serviço que está pronto para atender as suas necessidades comerciais atuais e futuras.* - Extraído do site da Microsoft

O armazenamento do data lake foi divido em 3 (três camadas): **Bronze** (Bronze), **Silver** (Prata) e **Gold** (Ouro).

> A nomenclatura as camadas se dá em função das medalhas da olimpíadas

**Bronze**

A camada `bronze` armazena os dados extraídos das fontes de dados, já preparado para a execução do processo de batch. Esses dados, nessa camada,estão dividido por origem e domínio. Aqui, ainda não temos nenhum tipo de tratamento sobre o dado. - *Raw Data*

**Silver**

A camada `silver` é responsável por armazenar e concatenar os dados de mesmo domínio. Os dados ingestados por essa camada já estão tratados e padronizados. Para a composição da entidade é necessário aplicar a regra de mescla. Outro ponto relevante é que nessa camada temos o versionamento do dados. - *Unified Data*

**Gold**

A camada `gold` é a área de visualização dos dados. Inicialmente, essa camada também apresenta versionamento dos registros. Aqui, os dados estão disponibilizados para consultas, aonde já foi efetuado uma curatela sobre as informações aqui presente. Tambem contem pré-processamento de valores e aplicação de regras de negócio. Na gold tambem temos, alem dos próprios domínios(dados mestres), também temos as modelagens dos Data Warehouses. Vale ressaltar que os dados gerados pelo os cientistas de dados também serão disponibilizados nessa camada.

> Uma diferença super relavante entre a camada da Silver e da Gold, quando se trata do domínio, é que na Gold, temos um dado que já foi passado por um processo de curatela e possíveis regras de negócio aplicadas, e na Silver, temos uma grande tabela com os dados importados das origens. (Full Join)

![Items.jpg](/.attachments/Items-af198bbe-2d8a-4ae3-bc5b-c619ade36177.jpg)

Veja aqui, mais informações sobre o [Data Lake](/Arquitetura/Data-Lake).

### Visualização

Uma vez que os dados estão armazenados no Data Lake (Bronze, Silver e Gold), o projeto do Lab-DataPlat oferece ao usuário as capacidades de poder acessar essas informações de três maneiras distintas: Por Painel (Microsoft Power BI), Queries no banco de dados dedicado e por consulta direta no data lake. Fora tambem a possibilidade de modelagens de data warehouse e exibir esses valores nos formatos acima citados.

### Machine Learning & Data Science

- Aqui entra a grande cereja do bolo! O projeto do Lab-DataPlat oferece uma plataforma integrada para favorecer aos cientistas de dados criar seus algorítmos. Os DS podem acessar os dados disponíveis na Silver e na Gold do Data lake.

# Arquitetura do Projeto Data Plat
- A arquitetura foi idealizada para suportar uma grande quantidade de dados de diversas áreas da CCR, seja em esteira batch como Stream. A estratégia de elasticidade foi adotada com a criação de no mínimo um recurso por área, melhor elucidado na figura abaixo:

![Arquitetura_All-V2-Arquitetura Simplificada.png](/.attachments/Arquitetura_All-V2-Arquitetura%20Simplificada-a4791bdf-e228-4999-971a-a75c65d3ef17.png)
_Segunda versão Arquitetura da plataforma._ 

A seguir documento em formato original, em drawio.
[Arquitetura_All-V2.zip](/.attachments/Arquitetura_All-V2-e7889d65-5048-4d54-9f13-81aa78696695.zip)

#Datamarts
- Iniciado pela parte de rodovias, trará dados do SUAT, sistema que armazena dados no Oracle em diversas instancias apartadas nas estações e sites. Outras Squads podem ser iniciadas em conjunto, tais como Datamarts de Aeroportos e Mobilidade. 

#Recursos:

- ##Databricks: 
  - São 6 unidades, dois para Aeroportos, Mobilidade e Rodovias, sendo que um deles para o propósito de pipeline de engenharia de dados e executar modelos preditivos.

- ##Data Factoty
  - São 3 recursos, um para cada área: Mobilidade, Aeroportos e Rodovias.

- ##Storge Account
  - Por se tratar de armazenamento, apenas um foi considerado. Dentro do recurso, foram criados containers com estrutura medalha: Bronze, Silver e Gold. Uma nova será usada denominada Landing Zone quando utilizado CDC. 

- ##Synapse
  - Foi considerado o uso de Serverless pelo ótimo custo e benefício. Tabelas externas serão criadas com base nos Datamarts da Gold Zone no Storage Account. A versão dedicada foi descartada devido a um grande custo e pouco retorno de seus benefícios. 




# Leitura recomendada


Recomendamos muito a leitura desse artigo:

[Lakehouse: A New Generation of Open Platforms that Unify
Data Warehousing and Advanced Analytics](http://www.cidrdb.org/cidr2021/papers/cidr2021_paper17.pdf)


Demais leituras:
- [ETL (extração, transformação e carregamento)](https://docs.microsoft.com/pt-br/azure/architecture/data-guide/relational-data/etl)
- [Artigo data lake na Microsoft](https://azure.microsoft.com/pt-br/solutions/data-lake/)
- [O que é o Delta Lake](https://docs.microsoft.com/pt-br/azure/synapse-analytics/spark/apache-spark-what-is-delta-lake)
- [Guia do Delta Lake e do Delta Engine](https://docs.microsoft.com/pt-br/azure/databricks/delta/)
- [Introdução ao Delta Lake](https://docs.microsoft.com/pt-br/azure/databricks/delta/delta-intro)
- [Azure Databricks](https://docs.microsoft.com/pt-br/azure/databricks/)
- [Azure Data Factories](https://docs.microsoft.com/pt-br/azure/data-factory/)
- [Data warehouse, data mart, data lake, and operational data storage](https://medium.com/dataprophet/data-warehouse-data-mart-data-lake-and-operational-data-storage-3a69f8701466)

