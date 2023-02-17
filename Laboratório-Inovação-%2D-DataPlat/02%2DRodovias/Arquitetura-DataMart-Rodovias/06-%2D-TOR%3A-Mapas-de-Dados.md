# Mapa de dados - TOR
Mapeamento de dados do sistema TOR referente as rodovias sob concessão da CCR.

O sistema TOR conta com somente duas rodovias no momento, VIACOSTEIRA e VIASUL. A rodovia VIACOSTEIRA foi tomada como parâmetro para o rastreamento de colunas diferentes em  tabelas que são utilizadas nas duas rodovias.

Diferente das rodovias do sistema KCOR, as rodovias do sistema TOR disponibilizam suas bases no SQL Server e não no Oracle.

Os arquivos de excel disponibilizados com os mapeamentos possuem as seguintes colunas:

**ID_COLUNA:** Id da coluna na respectiva tabela;
**NOME_COLUNA:** Nome da coluna na respecita tabela;
**TIPO:** Tipo de dado da coluna;
**TAMANHO:** Tamanho do campo;
**CHAVE:** Indica se é um campo chave da tabela;
**OBSERVAÇÃO:** Facultativo para inserção de observaçoes sobre uma determinada coluna;
**Tem na VIACOSTEIRA e não tem na VIASUL:** Contém as colunas que estão presentes na mesma tabela na VIACOSTEIRA mas não estão na rodovia VIASUL;
**Tem na VIASUL mas não tem na VIACOSTEIRA:** Contém as colunas que estão na mesma tabela na rodovia VIASUL mas não estão na VIACOSTEIRA.

**Obs:** As duas últimas colunas só estarão presentes em tabelas que apresentarem estruturas diferentes em relação a VIACOSTEIRA.

**RODOVIAS:**
 
- **VIACOSTEIRA** 
  * Utilizada como parâmetro de comparação para as demais rodovias.

O mapeamento das tabelas e suas respectivas colunas da VIACOSTEIRA pode ser verificado no arquivo abaixo.

VIACOSTEIRA/TOR - [MAPA_TBL_TOR_VIACOSTEIRA.xlsx](/.attachments/MAPA_TBL_TOR_VIACOSTEIRA-a6e7d24a-1b94-44c7-95c1-e1c4d6a7874f.xlsx)

- **VIASUL**   
  * As seguintes tabelas apresentam diferenças em números de colunas ou em composição de suas primary keys comparadas a estrutura da VIACOSTEIRA:

    - OCORRENCIA
    - OCORRENCIA_RECURSO
    - RODOVIA
    - SENTIDO
    - VITIMA_SITUACAO

O mapeamento das tabelas e suas respectivas colunas da VIASUL pode ser verificado no arquivo abaixo.

VIASUL/TOR - [MAPA_TBL_TOR_VIASUL.xlsx](/.attachments/MAPA_TBL_TOR_VIASUL-a1398593-847c-4db4-8af4-89548e05c3bc.xlsx)


**MAPA DE TABELAS:**

Todos os mapeamentos também estão disponíveis no Sharepoint abaixo.

Sharepoint:

https://grupoccr.sharepoint.com/sites/LaboratriodeInovao/Documentos%20Compartilhados/Forms/AllItems.aspx?ga=1&id=%2Fsites%2FLaboratriodeInovao%2FDocumentos%20Compartilhados%2FProjetos%2FDocumenta%C3%A7%C3%A3o%20Projetos%2FRodovias%2FDataMart%2DRodovias%2FMapaTabelas%5FTOR%5FKCOR%2FEngenharia&viewid=92e83c7e%2D1932%2D4368%2Dbf46%2Dfac1f2309c17
