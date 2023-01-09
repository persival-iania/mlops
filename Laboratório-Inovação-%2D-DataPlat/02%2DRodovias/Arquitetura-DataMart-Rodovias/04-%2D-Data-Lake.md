![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-0259b883-c48a-46a1-8aea-9da7c5b138aa.png)

A Estrutura do Datalake é composta de 4 camadas **Landing**, **Bronze**, **Silver** e **Gold** subdivididos em **SUAT**, **TOR** e **KCOR** e com um arquivo de configuração para cada objeto\tabela dentro dele. 

**Landing**

A camada landing armazena os dados extraídos das fontes de dados, já preparado para a execução do processo de batch. Esses dados, nessa camada, estão dividido por origem e domínio. Aqui, ainda não temos nenhum tipo de tratamento sobre o dado. - Raw Data

**Bronze**

A camada bronze armazena os dados extraídos das fontes de dados, já preparado para a execução do processo de batch. Esses dados, nessa camada, estão dividido por origem e domínio. Aqui, ainda não temos nenhum tipo de tratamento sobre o dado. - Raw Data

**Silver**

A camada silver é responsável por armazenar e concatenar os dados de mesmo domínio. Os dados ingestados por essa camada já estão tratados e padronizados. Para a composição da entidade é necessário aplicar a regra de mescla. Outro ponto relevante é que nessa camada temos o versionamento do dados. - Unified Data

**Gold**

A camada gold é a área de visualização dos dados. Inicialmente, essa camada também apresenta versionamento dos registros. Aqui, os dados estão disponibilizados para consultas, aonde já foi efetuado uma curatela sobre as informações aqui presente. Tambem contem pré-processamento de valores e aplicação de regras de negócio. Na gold tambem temos, alem dos próprios domínios(dados mestres), também temos as modelagens dos Data Warehouses. Vale ressaltar que os dados gerados pelo os cientistas de dados também serão disponibilizados nessa camada.

![Captura de Tela 2023-01-09 às 12.39.06.png](/.attachments/Captura%20de%20Tela%202023-01-09%20às%2012.39.06-0b560f91-bab2-4a1b-8fe2-501d40764630.png)


Para a camada landing os dados vão ficar de forma de raw, ou seja, vamos manter uma cópia fiel dos dados de de acordo com origem, na camada bronze faremos o armazenamento dos dados deltas, na silver teremos os dados delta e transformados ja na camada gold o dado estará pronto para o consumo pela companhia.



![image.png](/.attachments/image-90831555-4f82-4b70-a1e4-89657bd5c14b.png)





