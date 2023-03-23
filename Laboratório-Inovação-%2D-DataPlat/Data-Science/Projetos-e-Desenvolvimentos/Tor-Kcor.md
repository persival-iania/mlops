Página com as informações levantadas sobre a base do Tor e Kcor.

## Levantamento Inicial das tabelas do Tor/Kcor
- [Planilha](https://grupoccr-my.sharepoint.com/:x:/g/personal/marcelomine_triad_grupoccr_com_br/EcMc_Ynr2fVDtzd4_7sx3vYBS5EkACSucw9Ak4ZAbbK0oQ
), com as respectivas colunas, tipo do dado e alguns relacionamentos entre as tabelas.

## Tor
Esta base possui informação da **Rodovia ViaSul** e possui estas 36 tabelas:
  - acidente_condicoes_metereologicas 
  - animal 
  - base_operacional 
  - causa_acidente 
  - concessao 
  - condicao_pista 
  - condicao_superficie 
  - especie_animal 
  - funcionario 
  - genero_animal 
  - local_destino_animal 
  - ocorrencia 
  - ocorrencia_acidente 
  - ocorrencia_animal 
  - ocorrencia_providencia 
  - ocorrencia_recurso 
  - ocorrencia_veiculo 
  - ocorrencia_vitima 
  - parada 
  - perfil 
  - porte_animal 
  - providencia 
  - recurso 
  - recurso_atividade 
  - recurso_parada 
  - rodovia 
  - sentido 
  - situacao_animal 
  - tipo_acidente 
  - tipo_atendimento_recurso 
  - tipo_ocorrencia 
  - tipo_pista 
  - tipo_recurso 
  - tipo_veiculo 
  - usuario 
  - vitima_situacao
- As tabelas que possuem no nome "tipo_" são tabelas de-para.

## Kcor
Esta base possui informação destas rodovias: **AutoBAn, Msvias, Rodonorte, Spvias, Vialagos e Viaoeste-Rodoanel**. Rio-SP, Dutra e ViaRio estão apenas no Suat. Os dados do Rodoanel (Suat) e ViaOeste (Suat) estão na ViaOeste-Rodoanel (Kcor).

A base Kcor possui estas 45 tabelas:
 - tabacidentes  
 - tabanimais  
 - tabocorrencias  
 - tabprovidenciastomadas  
 - tabrecursosacionados  
 - tabrecursoscoberturas  
 - tabrecursoscontrole  
 - tabrecursosperc  
 - tabveiculosenvolvidos  
 - tabvitimas  
 - tauxacidentes  
 - tauxanimais  
 - tauxbases  
 - tauxcausasprovaveis  
 - tauxconcessionarias  
 - tauxcondicoesmeteorologicas  
 - tauxcondicoestrafego  
 - tauxcondicoesvisibilidade  
 - tauxfuncionarios  
 - tauxgps  
 - tauxlocais  
 - tauxmanuttipos  
 - tauxmunicipios  
 - tauxrecursos  
 - tauxrodovias  
 - tauxsentidos  
 - tauxtiposacidentes  
 - tauxtiposacidentessub  
 - tauxtiposatendimentos  
 - tauxtiposcoberturas  
 - tauxtiposocorrencias  
 - tauxtiposocorrenciassub  
 - tauxtiposprovanimais  
 - tauxtiposprovidencias  
 - tauxtiposrecursos  
 - tauxtiposveiculos  
 - tauxvitlesoestipos  
 - tauxvitmateriais  
 - tauxvitnaturezas  
 - tauxvitposicoes  
 - tauxvitprocedimentos  
 - tauxvitsituacoes  
 - tauxvittiposatendclinico  
 - tauxvittiposremocoes  
 - tsysusuarios

As tabelas "taux" são tabelas auxiliares de-para.

## Projeto dos Tempos Médios

- **Objetivo**: Obter o tempo médio que os certos recursos levam, do momento que são acionados até chegar na ocorrência

- **Critério**: Intervalo de tempo entre o acionamento e a chegada dos recursos

- **Recursos**: Guincho Leve e Guincho Pesado

- **Período**:
  - Todo o Histórico
  - Ano
  - Semestre
  - Trimestre


- **Notebook** com os **cálculos** dos **tempos médios**: 
  - [Tor](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/3955256019522656/command/3955256019522657)
  - [Kcor](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/1436695849975907/command/1436695849975932)  


- **Regras de Negócio** para análise dos dados:

  - O Intervalo de Tempo entre a Chegada no Local da Ocorrência e o Momento do Acionamento do recurso foi chamado de **Delta**.
    - Foram observados alguns valores de **Delta extremamente altos**, que iriam afetar no valores das médias. Foi desconsiderado os 15% dos deltas mais altos (outliers) e calculado a média com os 85% restantes. Os demais 15% são considerados expurgos e permitido por contrato;
    - Há casos obtidos do **Delta Negativo** (chegada anterior ao acionamento). Nestes casos, por meio de alinhamentos com a cliente, o tempo de chegada foi igualado ao tempo de acionamento (Transformado em **Delta = Zero**) e foi considerado para o cálculo da média;
    - Há outros casos no qual obteve-se **Delta Zero** (momento da chegada igual ao de acionamento). Este caso é comum e correto, pois entra no sistema de fato com os mesmos tempos (quando o recurso em andamento identifica a ocorrência na rodovia antes dela ser acionada).
      - Estas ocorrências foram consideradas para um cenário do cálculo de média (Delta maior ou igual a Zero) e desconsiderada em outro (somente Delta maior que Zero), explicitadas em planilha do Excel
      - Esta segunda situação, que foi considerado apenas o Delta Positivo, foi considerado para as situações que somente há deslocamento, um dos focos de interesse.
  - Há casos que **não haviam informações do momento da chegada do recurso**, só havia o **momento da saída**. Estes casos estão relacionados com o **cancelamento** da ocorrência pelo usuário e foi **desconsiderado** para o cálculo da média.
