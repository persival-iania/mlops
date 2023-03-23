Página com as informações levantadas sobre a base do Tor e Kcor.

# Levantamento Inicial das tabelas do Tor/Kcor
- [Planilha](https://grupoccr-my.sharepoint.com/:x:/g/personal/marcelomine_triad_grupoccr_com_br/EcMc_Ynr2fVDtzd4_7sx3vYBS5EkACSucw9Ak4ZAbbK0oQ
), com as respectivas colunas, tipo do dado e alguns relacionamentos entre as tabelas.

# Tor
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

# Kcor
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

# Projeto dos Tempos Médios

- **Objetivo**: Obter o tempo médio que os certos recursos levam, do momento que são acionados até chegar na ocorrência

- **Critério**: Intervalo de tempo entre o acionamento e a chegada dos recursos

- **Recursos**: Guincho Leve e Guincho Pesado

- **Período**:
  - Todo o Histórico
  - Ano
  - Semestre
  - Trimestre

## Notebooks com os cálculos dos tempos médios: 
  - [Tor](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/3955256019522656/command/3955256019522657)
  - [Kcor](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/1436695849975907/command/1436695849975932)  

## Análise das Bases
- Tor: 
  - A tabela de de-para com a descrição dos tipos dos recursos é a **tipo_recurso**, identificando que os códigos para os recursos **Guincho Leve** e **Guincho Pesado** são, respectivamente, 2 e 3:
<IMG  src="https://grupoccr.atlassian.net/secure/attachment/15295/15295_image-20230314-184243.png"/>
    - Porém, nenhuma outra tabela com os códigos dos recursos possuem estes códigos 2 ou 3. 
    - Em conversa com o Rogerio Aparecido Moreira, ele orientou que estes recursos possuem um identificador pra cada viatura. Por exemplo, Guincho Leve é GL-22, GL-23, etc. E Guincho Pesado é GP-01, GP-02, etc. Esta informação foi detectada na tabela **ocorrencia_recurso**, na coluna **ATIVIDADE**: 
<IMG  src="https://grupoccr.atlassian.net/secure/attachment/15296/15296_image-20230314-184601.png"/>
    - Por esta tabela, a lista destas viaturas destes recursos são: 'GL-13', 'GL-03', 'GL-12', 'GL-09', 'GL-02', 'GL-04', 'GL-24', 'GL-08', 'GL-25', 'GL-22', 'GL-06', 'GL-05', 'GP-02', 'GP-04', 'GL-07', 'GL-11', 'GL-23', 'GL-01','GL-21', 'GL-10', 'GL-20', 'GP-03', 'GP-01', 'GP-05'.
  - Foi feito a filtragem por estas viaturas e um dos campos de data precisa de tratamento no tempo. Está neste formato o campo dos segundos: SS.SSSSSS, e foi alterado para SS para os cálculos. Caso não seja alterado, o cálculo para o delta não é feito:
<IMG  src="https://grupoccr.atlassian.net/secure/attachment/15304/15304_image-20230315-120404.png"/>
  - Arrumado este formato de data e foi calculada a média estes períodos, os mesmos períodos definidos no Kcor:
    - Todo o Histórico (até março/2023);
    - Anual (de 2019 a 2023);
    - Semestral (1º Sem 2019 a 1º Sem 2023);
    - Trimestral (1Q 2019 a 1Q 2023).

- Kcor: 
  - Os recursos das unidades estão descritos na coluna "**DESCRICAORECURSO**", na tabela final "**oco_rec_a**" (Ver [Notebook](https://adb-7255094420308168.8.azuredatabricks.net/?o=7255094420308168#notebook/1436695849975907/command/1436695849975940)). Esta tabela é resultado do _join_ da **tabrecursosacionados** com a **tabocorrencias**, e posteriormente _join_ com a **tauxrecursos**.
  - Sobre as Unidades e a forma que estão descritos os recursos
    - As unidades **Msvias**, **Vialagos** e **ViaOeste-Rodoanel** estão com os recursos descritos desta forma: 'Guincho Leve', 'Guincho Pesado'. 
    - A **AutoBAn**: "GUINCHO LEVE', 'GUINCHO PESADO'. 
    - A **Spvias**: 'Inspeção/Guincho Leve', 'Guincho Pesado' (Pois o recurso Guincho Leve também é utilizado para Inspeção). 

## Regras de Negócio para análise dos dados:

  - O Intervalo de Tempo entre a Chegada no Local da Ocorrência e o Momento do Acionamento do recurso foi chamado de **Delta**.
    - Foram observados alguns valores de **Delta extremamente altos**, que iriam afetar no valores das médias. Foi **desconsiderado os 15%** dos deltas mais altos (_**outliers**_) e calculado a **média com os 85% restantes**. Os demais 15% são considerados **expurgos** e **permitido** por contrato;
    - Há casos obtidos do **Delta Negativo** (chegada anterior ao acionamento). Nestes casos, por meio de alinhamentos com a cliente, o tempo de chegada foi igualado ao tempo de acionamento (Transformado em **Delta = Zero**) e foi considerado para o cálculo da média;
    - Há outros casos no qual obteve-se **Delta Zero** (momento da chegada igual ao de acionamento). Este caso é **comum e correto**, pois entra no sistema de fato com os mesmos tempos (quando o recurso em andamento identifica a ocorrência na rodovia antes dela ser acionada).
      - Estas ocorrências foram consideradas para um cenário do cálculo de média (Delta maior ou igual a Zero) e desconsiderada em outro (somente Delta maior que Zero), explicitadas em planilha do Excel, anexado abaixo.
      - Esta segunda situação, que foi considerado apenas o **Delta Positivo**, foi considerado para as situações que somente há deslocamento, um dos focos de interesse.
  - Há casos que **não haviam informações do momento da chegada do recurso**, só havia o **momento da saída**. Estes casos estão relacionados com o **cancelamento** da ocorrência pelo usuário e foi **desconsiderado** para o cálculo da média.

## Resultados
- Foram compilados numa planilha os resultados dos valores dos tempos médios, considerando Delta = 0 (ou seja, até o percentil 85) e desconsiderando Delta = 0 (considerando apenas quando há de fato deslocamento do recurso)
    - [tor_kcor_medias_tempo_atendimento_guincho_leve_pesado_v1_1.xlsx](/.attachments/tor_kcor_medias_tempo_atendimento_guincho_leve_pesado_v1_1-c0dbefa2-b939-4ff1-b5da-447b81ab3383.xlsx)

- O Notebook apresenta outras métricas estatísticas em detalhes. Por exemplo, para a **AutoBAn**, todo o **histórico**, para o **Guincho Leve** (sem outliers, Delta >= 0). Tempo em minutos: 
![image.png](/.attachments/image-d257b476-1fa6-48da-b329-843ad6dc7c64.png)
![image.png](/.attachments/image-80d16873-9a64-48e5-9b3d-87a0240e1170.png) 