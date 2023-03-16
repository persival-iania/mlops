![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-1a1b3763-69fa-4f6f-9907-bbdd76fabbbb.png)

# Notebooks desenvolvidos pelo time de Ciência de Dados do Laboratório da CCR para diversos projetos. 

## Esta página visa organizar os notebooks desenvolvidos no Databricks em diversos projetos, estudos e trabalhos.

## 1. Estudos Tor/Kcor
- 1.1.	Levantamento de informações das tabelas que compõem o KCOR e que possam servir para futuros estudos.
  - Análise 1:
Verificação das ocorrências \ KM
  - Análise 2:
Quebra das ocorrências pelos tipos: Animais, Acidentes e Outros
  - Análise 3:
Verificação das ocorrências por tempo e quebras
Quebra das séries temporais em tendência, sazonalidade e resíduos
  - Análise 4:
Análise da base de recursos e recursos acionados
Tipos e tempos de deslocamento
Cruzamento das ocorrências com as series em que ocorreram ambulâncias
  - Análise 5:
Análise para estudo das áreas de atuação das ambulâncias
Quebra das regiões em átomos
levantamento dos tempos de ocorrências por átomos, tipo ambulância
Levantamento dos tempos de ocorrências\hora para cada ambulância
  - Ambiente databricks: brkprdbidata 
  - [Analises_AutoBan_KCOR_Fix - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/2235771888014278/command/2235771888014280)

---------------

- 1.2.	Analise das estatísticas das ocorrências com acionamento de ambulâncias
  - Ambiente databricks: brkprdbidata 
  - [Análise_Area_Atuacao_Ambulancias - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/4472428869583977/command/4472428869584014) 

-------

- 1.3.	Notebook com os testes dos menores caminhos para rotas dos recursos utilizando algoritmo
  - Ambiente databricks: brkprdbidata 
  - Utilizar algoritmo de menor caminho para determinar as melhores rotas de uma base até um acidente.
  - [Algoritmo_Menores_Caminhos - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/4070032663066058/command/2571644304477403)

------------

- 1.4.	Cálculos dos tempos médios e suas respectivas estatísticas dos diferentes tipos de recursos do tipo guincho
  - Ambiente databricks: brkprdbidata 
  - [Cálculo - Tempos Médios (Analises_AutoBan_KCOR_Fix (1)) - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/4181973559848910/command/4127203371650324)

-------------
- 1.5.	Informações gerais dos dados na base Kcor – autoBAn. 
  - Ambiente databricks: brkprdbidata 
  - Levantamento da quantidade de registros por cada tipo recursos 
  - [Bases_ocorrencias_e_recursos_acionados - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/1989494933375938/command/2761971847735531)

--------------
- 1.6. Notebook com os códigos dos estudos para as ocorrências que utilizam o recurso Ambulância na base Kcor - AutoBAn  
  - Sugestão de instalação de bases com o conceito de Centro de Massa. Foi aplicado o conceito de centro de massa nas Ocorrências da Rodovia AutoBAn (Kcor, camada raw_processados), onde a massa é a quantidade de Ocorrências por km, baseado no histórico de dados da rodovia, para identificar a melhor localização das bases com ambulâncias para diminuição do tempo de atendimento. 
  - Ambiente databricks: brkprdbidata
  - [Localização Ambulâncias - Centro de Massa - Databricks (azuredatabricks.net)](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/3790029860022697/command/3790029860022698)

----------------

## 2. Performance do Arrecadador
- 2.1.	Estudos diversos relacionados à performance do arrecadador 
  - Quebras por datas - dia\semana\mês
  - Quebras por praça
  - Análises do fator de produtividade
  - Modelos teste para prever fator de produtividade
  - Ambiente: adb-eng-brazilsouth-pdev 
  - [Análise Fator de Produtividade - Databricks (azuredatabricks.net)](https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/4496946086356841/command/4496946086356842)

------

## 3. Previsão de Demandas
- 3.1.	Pipeline completo para modelo exemplo de previsão de demandas
  - Data preparation
  - Criação de features
  - Modelo
  - Verificação de métricas
  - Inferência  
  - Ambiente: adb-eng-brazilsouth-pdev 
  - [Pipeline de teste para modelos de previsão de demandas](https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#folder/4496946086356622) 

---------
## 4. Estudos Visão Computacional 
- 4.1.	Teste de modelo de visão computacional na plataforma databricks (Experimental)
  - Teste simplificado para verificar o funcionamento do Databricks e ambiente com o uso da ferramenta Yolo V8 na tarefa de identificação de artefatos em vídeos\imagem
  - Ambiente: adb-eng-brazilsouth-pdev 
  - [Teste_CV - Databricks (azuredatabricks.net)](https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/2062248893296984/command/3405116729545172)

-------------
## 5. Anomalias
- Estudo de correlação entre as anomalias nas transações nas praças de pedágio da AutoBan, base Suat.  
  - Ambiente: adb-eng-brazilsouth-pdev 
  - [Anomalias_testes_2022 - Databricks (azuredatabricks.net)](https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/4024650243638445/command/4024650243638451) 




