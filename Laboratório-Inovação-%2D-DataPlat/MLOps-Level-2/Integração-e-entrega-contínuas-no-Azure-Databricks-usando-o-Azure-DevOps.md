#**O Que é CI/CD?**



CI/CD (integração contínua e entrega contínua) refere-se ao processo de desenvolvimento e entrega de software em ciclos curtos e frequentes por meio do uso de pipelines de automação.

A integração contínua começa com a prática de fazer commit do seu código com alguma frequência para um branch em um repositório de código-fonte. 

Cada confirmação é mesclada com as confirmações de outros desenvolvedores para garantir que nenhum conflito foi introduzido. As alterações são então validadas criando um build e executando testes automatizados nesse build. 

Esse processo, em última análise, resulta em um artefato ou pacote de implantação, que terminará sendo implantado em um ambiente de destino, neste caso do artigo um workspace do Azure Databricks.

