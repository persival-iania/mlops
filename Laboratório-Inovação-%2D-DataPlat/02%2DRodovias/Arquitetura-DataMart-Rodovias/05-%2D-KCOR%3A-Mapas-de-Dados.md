# Mapa de dados - KCOR
Mapeamento de dados do sistema KCOR referente as rodovias sob concessão da CCR.

Obs: A rodovia AUTOBAN foi parâmetro para o rastreamento de colunas diferentes em  tabelas que são utilizadas em todas as rodovias.

Os arquivos de excel disponibilizados com os mapeamentos possuem as seguintes colunas:

**ID_COLUNA:** Id da coluna na respectiva tabela;
**NOME_COLUNA:** Nome da coluna na respecita tabela;
**TIPO:** Tipo de dado da coluna;
**TAMANHO:** Tamanho do campo;
**CHAVE:** Indica se é um campo chave da tabela;
**OBSERVAÇÃO:** Facultativo para inserção de observaçoes sobre uma determinada coluna;
**Tem na AUTOBAN e não tem na "XPTO":** Contém as colunas que estão presentes na mesma tabela na AUTOBAN mas não estão na rodovia "XPTO";
**Tem na "XPTO" mas não tem na AUTOBAN:** Contém as colunas que estão na mesma tabela na rodovia "XPTO" mas não estão na AUTOBAN.

**Obs:** As duas últimas colunas só estarão presentes em tabelas que apresentarem estruturas diferentes em relação a AUTOBAN.

**RODOVIAS:**
 
- **AUTOBAN** 
  * Utilizada como parâmetro de comparação para as demais rodovias.

O mapeamento das tabelas e suas respectivas colunas da AUTOBAN pode ser verificado no arquivo abaixo.

AUTOBAN/KCOR - [MAPA_TBL_KCOR_AUTOBAN.xlsx](/.attachments/MAPA_TBL_KCOR_AUTOBAN-83543093-8dd5-40e7-99d1-f8d138f4a549.xlsx)

- **SPVIAS**   
  * A composição da Primary Key da tabela TABRECURSOSACIONADOS na SPVIAS é diferente da mesma na AUTOBAN.

O mapeamento das tabelas e suas respectivas colunas da SPVIAS pode ser verificado no arquivo abaixo.

SPVIAS/KCOR - [MAPA_TBL_KCOR_SPVIAS.xlsx](/.attachments/MAPA_TBL_KCOR_SPVIAS-c9fb904a-a15a-4c34-b189-1f7da16479b9.xlsx)

- **VIAOESTE E RODOANEL**  
  * No sistema KCOR os dados das rodovias VIAOESTE e RODOANEL são disponilizados na mesma base. Somente a tabela abaixo apresenta diferença em números de colunas  comparadas a estrutura da AUTOBAN:

    - TABVEICULOSENVOLVIDOS

O mapeamento das tabelas e suas respectivas colunas da VIAOESTE e RODOANEL pode ser verificado no arquivo abaixo.

VIAOESTE E RODOANEL - [MAPA_TBL_KCOR_VIAOESTEeRODOANEL.xlsx](/.attachments/MAPA_TBL_KCOR_VIAOESTEeRODOANEL-3cab7fdc-0c9c-4ae9-8fe4-267305ba41c1.xlsx)


- **RODONORTE**
  * As seguintes tabelas apresentam diferenças em números de colunas ou em composição de suas primary keys comparadas a estrutura da AUTOBAN:

    - TABACIDENTES
    - TABANIMAIS
    - TABOCORRENCIAS
    - TABPROVIDENCIASTOMADAS
    - TABRECURSOSACIONADOS
    - TABRECURSOSCOBERTURAS
    - TABRECURSOSCONTROLE
    - TABRECURSOSPERC
    - TABVEICULOSENVOLVIDOS
    - TABVITIMAS
    - TAUXANIMAIS
    - TAUXBASES
    - TAUXCAUSASPROVAVEIS
    - TAUXCONCESSIONARIAS
    - TAUXCONDICOESTRAFEGO
    - TAUXFUNCIONARIOS
    - TAUXGPS
    - TAUXLOCAIS
    - TAUXMUNICIPIOS
    - TAUXRECURSOS
    - TAUXRODOVIAS
    - TAUXSENTIDOS
    - TAUXTIPOSACIDENTES
    - TAUXTIPOSATENDIMENTOS
    - TAUXTIPOSOCORRENCIAS
    - TAUXTIPOSPROVANIMAIS
    - TAUXTIPOSRECURSOS
    - TAUXVITPOSICOES
    - TAUXVITSITUACOES
    - TSYSUSUARIOS

O mapeamento das tabelas e suas respectivas colunas da RODONORTE pode ser verificado no arquivo abaixo.

RODONORTE - [MAPA_TBL_KCOR_RODONORTE.xlsx](/.attachments/MAPA_TBL_KCOR_RODONORTE-e4bc1311-d549-40ab-93d0-ef1c6721971b.xlsx)

- MSVIAS
  * As seguintes tabelas apresentam diferenças em números de colunas ou em composição de suas primary keys comparadas a estrutura da AUTOBAN:

    - TABACIDENTES
    - TABANIMAIS
    - TABOCORRENCIAS
    - TABPROVIDENCIASTOMADAS
    - TABRECURSOSACIONADOS
    - TABRECURSOSACIONADOS
    - TABRECURSOSCONTROLE
    - TABRECURSOSPERC
    - TABVEICULOSENVOLVIDOS
    - TABVITIMAS
    - TAUXANIMAIS
    - TAUXBASES
    - TAUXCAUSASPROVAVEIS
    - TAUXCONCESSIONARIAS
    - TAUXCONDICOESTRAFEGO
    - TAUXFUNCIONARIOS
    - TAUXGPS
    - TAUXLOCAIS
    - TAUXMUNICIPIOS
    - TAUXSENTIDOS
    - TAUXRODOVIAS
    - TAUXSENTIDOS
    - TAUXTIPOSACIDENTES
    - TAUXTIPOSATENDIMENTOS
    - TAUXTIPOSOCORRENCIAS
    - TAUXTIPOSPROVANIMAIS
    - TAUXTIPOSRECURSOS
    - TAUXVITPOSICOES
    - TAUXVITSITUACOES
    - TSYSUSUARIOS

O mapeamento das tabelas e suas respectivas colunas da MSVIAS pode ser verificado no arquivo abaixo.

MSVIAS - [MAPA_TBL_KCOR_MSVIAS.xlsx](/.attachments/MAPA_TBL_KCOR_MSVIAS-78f7c2f7-ea1e-487c-beaa-f499b288428b.xlsx)
   
- VIALAGOS 
   * As seguintes tabelas apresentam diferenças em números de colunas ou em composição de suas primary keys comparadas a estrutura da AUTOBAN:

     - TABACIDENTES
     - TABANIMAIS
     - TABOCORRENCIAS
     - TABPROVIDENCIASTOMADAS
     - TABRECURSOSACIONADOS
     - TABRECURSOSCOBERTURAS
     - TABRECURSOSCONTROLE
     - TABRECURSOSPERC
     - TABVEICULOSENVOLVIDOS
     - TABVITIMAS
     - TAUXANIMAIS
     - TAUXBASES
     - TAUXCAUSASPROVAVEIS
     - TAUXCONCESSIONARIAS
     - TAUXCONDICOESTRAFEGO
     - TAUXFUNCIONARIOS
     - TAUXLOCAIS
     - TAUXMUNICIPIOS
     - TAUXRECURSOS
     - TAUXRODOVIAS
     - TAUXSENTIDOS
     - TAUXTIPOSACIDENTES
     - TAUXTIPOSATENDIMENTOS
     - TAUXTIPOSOCORRENCIAS
     - TAUXTIPOSPROVANIMAIS
     - TAUXTIPOSRECURSOS
     - TAUXVITPOSICOES
     - TAUXVITSITUACOES
     - TSYSUSUARIOS

O mapeamento das tabelas e suas respectivas colunas da VIALAGOS pode ser verificado no arquivo abaixo.

VIALAGOS - [MAPA_TBL_KCOR_VIALAGOS.xlsx](/.attachments/MAPA_TBL_KCOR_VIALAGOS-340ecaa1-ad92-47cd-b198-01c7ede20463.xlsx)

- NOVADUTRA
   * As seguintes tabelas apresentam diferenças em números de colunas ou em composição de suas primary keys comparadas a estrutura da AUTOBAN:

     - TABACIDENTES
     - TABANIMAIS
     - TABOCORRENCIAS
     - TABPROVIDENCIASTOMADAS
     - TABRECURSOSACIONADOS
     - TABRECURSOSCOBERTURAS
     - TABRECURSOSCONTROLE
     - TABRECURSOSPERC
     - TABVEICULOSENVOLVIDOS
     - TABVITIMAS
     - TAUXANIMAIS
     - TAUXBASES
     - TAUXCAUSASPROVAVEIS
     - TAUXCONCESSIONARIAS
     - TAUXCONDICOESTRAFEGO
     - TAUXFUNCIONARIOS
     - TAUXGPS
     - TAUXLOCAIS
     - TAUXRODOVIAS
     - TAUXSENTIDOS
     - TAUXTIPOSACIDENTES
     - TAUXTIPOSACIDENTESSUB
     - TAUXTIPOSATENDIMENTOS
     - TAUXTIPOSCOBERTURAS
     - TAUXTIPOSOCORRENCIAS
     - TAUXTIPOSPROVANIMAIS
     - TAUXTIPOSPROVIDENCIAS
     - TAUXTIPOSRECURSOS
     - TAUXVITPOSICOES
     - TAUXVITPOSICOES
     - TSYSUSUARIOS

O mapeamento das tabelas e suas respectivas colunas da NOVADUTRA pode ser verificado no arquivo abaixo.

NOVADUTRA- [MAPA_TBL_KCOR_NOVADUTRA.xlsx](/.attachments/MAPA_TBL_KCOR_NOVADUTRA-5138fff1-1e94-4fc6-81c0-57820c98d491.xlsx)

**MAPA DE TABELAS:**

Todos os mapeamentos também estão disponíveis no Sharepoint abaixo.

Sharepoint:

https://grupoccr.sharepoint.com/sites/LaboratriodeInovao/Documentos%20Compartilhados/Forms/AllItems.aspx?ga=1&id=%2Fsites%2FLaboratriodeInovao%2FDocumentos%20Compartilhados%2FProjetos%2FDocumenta%C3%A7%C3%A3o%20Projetos%2FRodovias%2FDataMart%2DRodovias%2FMapaTabelas%5FTOR%5FKCOR%2FEngenharia%2FMapeamentos%20Rodovias&viewid=92e83c7e%2D1932%2D4368%2Dbf46%2Dfac1f2309c17

**ARQUIVOS JSON**

Todos os arquivos json para criação das tabelas na camada bronze estão disponíveis no Sharepoint abaixo.

https://grupoccr.sharepoint.com/sites/LaboratriodeInovao/Documentos%20Compartilhados/Forms/AllItems.aspx?ga=1&id=%2Fsites%2FLaboratriodeInovao%2FDocumentos%20Compartilhados%2FProjetos%2FDocumenta%C3%A7%C3%A3o%20Projetos%2FRodovias%2FDataMart%2DRodovias%2FMapaTabelas%5FTOR%5FKCOR%2FEngenharia%2FArquivos%20Json%2FKCOR&viewid=92e83c7e%2D1932%2D4368%2Dbf46%2Dfac1f2309c17

