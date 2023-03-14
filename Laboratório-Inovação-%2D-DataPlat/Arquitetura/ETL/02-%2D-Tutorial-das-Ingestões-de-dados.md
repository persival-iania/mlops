![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-2f296e8d-d67e-4756-a1e1-19ca81506340.png)

# **DataPlat Ingestões Padronizadas**   ![logoccrlabs.jpg](/.attachments/logoccrlabs-ab60d0c8-2c16-492e-915d-02ad63688ae7.jpg)



**Tutorial de ingestão padronizada**


***Passo a Passo***

• Passo1: Conhecer a base de dados a ser ingerida 
Este passo é fundamental para definição dos parâmetros iniciais para iniciar o processo de ingestão do dado. O que coletar:
1. Tamanho da base, 
2. Comportamento da base, se é realizado update, insert, delete
3. Campo de data para particionamento, se necessário
4. Campos chaves

• Passo2: Preenchimento do arquivo json
Este passo deve ser muito bem preenchido, pois dará informações para a coleta do dado
1. Tipo de carga a realizar se será uma carga full, ou seja se terá uma ingestão cópia de todos os dados ou terá uma ingestão incremental, para isso a variável sefull deve 
ser preenchida com N ou S
2. Preencher o campo data para particionamento
3. Preencher o campo do sistema para union dos dados na silver
4. Incluir nomenclatura padrão do pipeline e salva-lo como arquivo json
5. Realizar upload do arquivo no contêiner config, seguindo a estrutura padronizada
Banco ou Projeto de origem/ Sistema de origem/pip_nomedoarquivo.json

• Passo3:Criar pipeline com a função de execução do pipeline padrão
- Se atentar ao preencher corretamente o nome do json criado e caminho

• Passo4:Incluir trigger do processo

• Passo5:Publicar na Master

- Após carga: Criar external table no pool do synapse.

**NOTA: Ao realizar a primeira carga de uma base muito grande, se importar com o tempo que levará a ingestão, para não prejudicar/derrubar o banco de origem, quando 
isso acontecer, parametrizar as cargas por tempo, ou por tamanho. Ou seja realizar as cargas de forma fragmentada até atingir a carga atual**


# **Templates**

A fim de padronizar, configuramos alguns templates para a ingestão e tratamento dos dados, cuja fonte contenha similaridade, foram eles:


1. Arquivo de parâmetro json
2. Notebook para ingestão de arquivos se a ingestão for full
3. Notebook para ingestão de arquivos na camada bronze e silver com particionamento dos dados
4. Pipeline padrão de ingestão na camada bronze e silver
5. Synapse: Schemas conforme lake e data source padronizado

![labingestaotemplate1.JPG](/.attachments/labingestaotemplate1-bbb56bcd-851f-4690-a0bd-e7d2c570b465.JPG)

![labingestaotemplate2.JPG](/.attachments/labingestaotemplate2-8e7c6d41-3c23-4ece-90fc-4132677c3c44.JPG)

![labingestaotemplate3.JPG](/.attachments/labingestaotemplate3-6a300571-cab8-4450-a8b8-1eaf3ac91a33.JPG)

![labingestaotemplate4.JPG](/.attachments/labingestaotemplate4-0732ba72-907b-4924-9ac1-d2710580a784.JPG)

![labingestaotemplate4.1.JPG](/.attachments/labingestaotemplate4.1-aa60444b-2510-4fea-9ae4-fba70ede8a8b.JPG)

![labingestaotemplate5.JPG](/.attachments/labingestaotemplate5-6186b801-a9e5-4e7d-8869-acfa62cf9b44.JPG)


**OBS: Poderão haver alterações no processo e padrões tendo em vista estarmos em fase de desenvolvimento.**