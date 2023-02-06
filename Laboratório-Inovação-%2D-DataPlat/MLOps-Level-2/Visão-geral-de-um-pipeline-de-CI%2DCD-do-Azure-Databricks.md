#**Visão geral de um pipeline típico de CI/CD do Azure Databricks**

Embora possa variar de acordo com suas necessidades, uma configuração típica de um pipeline do Azure Databricks inclui as seguintes etapas:

##Integração Contínua (**C**ontinous **I**ntegration)

###1. Código
- Desenvolve códigos e testes de unidade em um notebook do Azure Databricks ou usando um IDE externo.
- Executa testes manualmente.
- Faz commit de código e testa em um branch do git.


###2. Build
- Coleta código e testes novos e atualizados.
- Executa testes automatizados.
- Cria bibliotecas e códigos não notebook do Apache Spark.

##3. Versão: 

- Gere um artefato de versão.



##Entrega Contínua (**C**ontinous **D**eployment)

###1. Implantar
- Implantar notebooks
- Implantar bibliotecas

###2. Testar
- executar testes automatizados
- reportar resultados dos testes

###3. Operar
- Agendar programaticamente os fluxos de trabalho
- engenharia de dados
- DataOps
- MLOps

