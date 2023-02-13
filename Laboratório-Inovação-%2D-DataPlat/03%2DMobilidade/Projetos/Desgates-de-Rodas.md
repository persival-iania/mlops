![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-c966143a-ebc6-4b44-9548-395e41aac6ab.png)
# Introdução

###Objetivo Inicial
De forma preventiva e automatizada, obter a correção da curva de desgaste das rodas, demais consumíveis e trilhos para projetar trocas e compras de ativos.
- Implementar as práticas de manutenção sob condição para reduzir, de maneira proativa, os custos com manutenções corretivas das rodas dos trens e metrôs.​
- Conhecer o consumo de rodas para projeção de manutenções e trocas.​
- Definir padrões e critérios de manutenção e monitoramento destes ativos.​
- Aperfeiçoar os conhecimentos e formar os colaboradores da manutenção para atendimento a manutenções em rodas ferroviárias.​
- Implementar estratégias de gestão do atrito e boas práticas que aumentem a vida útil desses ativos.​



###Motivadores & Problemas
- Deficiência no monitoramento do desgaste de rodas e demais consumíveis como pastilhas de freio, etc. devido ao trabalho manual e falta de infraestrutura de dados.​
- Problemas de medição como erro de digitação e manuseio dos dados que podem tanto levar a parada desnecessária de um trem, o desgaste forçado em excesso do material das rodas quanto manter em uso as rodas que não atendem aos critérios de segurança. ​
- Dificuldade de análise dos dados de medição e manutenção preventiva/corretiva para práticas que aumentem a vida útil das rodas.​
- Falta de padronização de critérios de manutenção e monitoramento destes ativos, assim como treinamento dos colaboradores da manutenção.​
- Custo elevado com manutenção das rodas dos trens.​


# Estrutura de Dados

###Arquitetura  
![ArquiteturaConsumoRodas.PNG](/.attachments/ArquiteturaConsumoRodas-0425ee7b-a37a-451a-91f3-9af57a20c2a3.PNG)

##Especificações
###Equipamento Calipri:
 Equipamento físico utilizado para medição das rodas do trem.
###Arquivo Calipri: 
Arquivo padronizado no formato Excel gerado pelo equipamento de medição Calipri.
###Diretório: 
Local de rede interna onde são disponibilizados e centralizados os arquivos Excel.

###Formulário Usinagem: 
Formulário de preenchimento de dados referentes ao processo de usinagem realizados periodicamente em algumas rodas.
###Arquivo Usinagem:
Arquivo padronizado no formato Excel gerado pelo formulário de usinagem.

###Storage Layer (Azure Blob Storage): 
Camada que possibilita o armazenamento e centralização de todos os dados recebidos, proporcionando maior velocidade, escalabilidade e segurança  da informação recebida. 

###Process Layer (Databricks): 
Camada de processamento dos dados recebidos, possibilitando construção de relatórios com base nas especificações desejadas utilizando linguagens de programação (SQL, Python e Scala)

###Orchestration (Azure Data Factory): 
Camada que permite a automatização, controle e monitoramento de todas as etapas do fluxo de dados

###Serve Layer (Power BI): 
Camada analítica que permite aos usuários a construção de consultas SQL,
desenvolvimento de Dashboards para visualização em formato de gráficos dos dados e documentação das bases de dados e variáveis de dados

# Estrutura de Visualização
Ferramenta que apresenta o histórico das medições (valores medidos em campo) na frota das linhas 4 e 5 e os cálculos de projeção de troca de roda em 3 telas:
1. Trem - fornece a visão geral de todos os trens incluindo a quilometragem de trocas das rodas, ultima medição de todas as rodas, desgaste acumulado e taxa média de desgaste (/100.00km).
2. Carro - fornece uma visão por carro de todos os trens e dos carros do trem selecionado.
3. Truque - visão por truque de todos os trens e de todos os truque do trem selecionado.

Tabelas = 
a. Tabela geral importada e atualiza semanalmente com os dados de medição e os principais cálculos de projeção.
b. Tabela de códigos dos trens por linha.
c. Tabela com os detalhes de posicionamento das rodas non trem (numeração, lado, carro, truque e eixo).

# Link para os dashboards - linhas 8 e 9
Estação Pinheiros:
https://app.powerbi.com/groups/063f6905-9119-43c1-82c6-a0a3bece1cd1/dashboards/20ae3191-ff00-4469-981c-c6ac3c6601fc

Estação Osasco
https://app.powerbi.com/groups/063f6905-9119-43c1-82c6-a0a3bece1cd1/dashboards/78b20734-f692-460e-b5d9-5d6ec2b98616

![Items (3).png](/.attachments/Items%20(3)-80899a9b-69e9-4a18-876b-1686dc57c294.png)