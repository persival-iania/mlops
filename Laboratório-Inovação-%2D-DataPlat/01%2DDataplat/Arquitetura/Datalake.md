![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-0259b883-c48a-46a1-8aea-9da7c5b138aa.png)

####  Data Lake

>*O Azure Data Lake inclui todos os recursos necessários para que seja mais fácil para desenvolvedores, cientistas de dados e analistas armazenar dados de qualquer tamanho, forma e velocidade, bem como realizar todo tipo de processamento e análise em diferentes plataformas e linguagens. Ele remove as complexidades relacionadas a ingerir e armazenar todos os seus dados, enquanto acelera a execução de análises em lote, streaming e interativas. O Azure Data Lake trabalha com investimentos existentes em TI para oferecer identidade, gerenciamento e segurança para que haja um controle e um gerenciamento de dados simplificados. Ele também tem integração direta com repositórios operacionais e data warehouses, de modo que você pode ampliar aplicativos de dados atuais. Aproveitamos nossa experiência de trabalho com clientes empresariais e da execução de algumas das análises e processamentos de maior escala no mundo para produtos da Microsoft como Office 365, Xbox Live, Azure, Windows, Bing e Skype. O Azure Data Lake soluciona muitos dos desafios de produtividade e escalabilidade que o impedem de maximizar o valor de seus ativos de dados com um serviço que está pronto para atender as suas necessidades comerciais atuais e futuras.* - Extraído do site da Microsoft

O armazenamento do data lake foi divido em 3 (três camadas): **Bronze** (Bronze), **Silver** (Prata) e **Gold** (Ouro).

> A nomenclatura as camadas se dá em função das medalhas da olimpíadas

**Bronze**

A camada `bronze` armazena os dados extraídos das fontes de dados, já preparado para a execução do processo de batch. Esses dados, nessa camada,estão dividido por origem e domínio. Aqui, ainda não temos nenhum tipo de tratamento sobre o dado. - *Raw Data*

**Silver**

A camada `silver` é responsável por armazenar e concatenar os dados de mesmo domínio. Os dados ingestados por essa camada já estão tratados e padronizados. Para a composição da entidade é necessário aplicar a regra de mescla. Outro ponto relevante é que nessa camada temos o versionamento do dados. - *Unified Data*

**Gold**

A camada `gold` é a área de visualização dos dados. Inicialmente, essa camada também apresenta versionamento dos registros. Aqui, os dados estão disponibilizados para consultas, aonde já foi efetuado uma curatela sobre as informações aqui presente. Tambem contem pré-processamento de valores e aplicação de regras de negócio. Na gold tambem temos, alem dos próprios domínios(dados mestres), também temos as modelagens dos Data Warehouses. Vale ressaltar que os dados gerados pelo os cientistas de dados também serão disponibilizados nessa camada.

> Uma diferença super relavante entre a camada da Silver e da Gold, quando se trata do domínio, é que na Gold, temos um dado que já foi passado por um processo de curatela e possíveis regras de negócio aplicadas, e na Silver, temos uma grande tabela com os dados importados das origens. (Full Join)

![Items.jpg](/.attachments/Items-7ad81a89-0e6d-4161-ad78-f9230483e713.jpg)

### Visualização

Uma vez que os dados estão armazenados no Data Lake (Bronze, Silver e Gold), o projeto do Lab-DataPlat oferece ao usuário as capacidades de poder acessar essas informações de três maneiras distintas: Por Painel (Microsoft Power BI), Queries no banco de dados dedicado e por consulta direta no data lake. Fora tambem a possibilidade de modelagens de data warehouse e exibir esses valores nos formatos acima citados.

### Machine Learning & Data Science

Aqui entra a grande cereja do bolo! O projeto do Lab-DataPlat oferece uma plataforma integrada para favorecer aos cientistas de dados criar seus algorítmos. Os DS podem acessar os dados disponíveis na Silver e na Gold do Data lake.


#POC de Dados

Com objetivo da prova de conceito para a plataforma, foram carregadas 14 tabelas sendo estruturadas como evidênciado abaixo:

##Evidências de estruturação:

##Bronze
A estruturação dos dados da Suat para POC de dados.
![image.png](/.attachments/image-34f66244-3401-44a3-ba7e-3efb34f52536.png)
##Silver
![image.png](/.attachments/image-c0a14982-d46e-42be-b483-67372e04cb40.png)
Atualmente, os dados estão sendo particionados por data a partir da silver.

##Gold
![image.png](/.attachments/image-506a9c12-4ade-4faa-9498-cee3016175bd.png)

**OBS: Poderão haver alterações no processo e padrões tendo em vista estarmos em fase de desenvolvimento.**