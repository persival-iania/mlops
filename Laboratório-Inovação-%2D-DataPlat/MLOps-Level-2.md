## Integração e entrega contínuas no Azure Databricks usando o Azure DevOps

-   Artigo
-   26/01/2023
-   34 minutos para o fim da leitura

## Neste artigo

1.  [Visão geral de um pipeline típico de CI/CD do Azure Databricks](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#overview-of-a-typical-azure-databricks-cicd-pipeline)
2.  [Desenvolver e confirmar seu código](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#develop-and-commit-your-code)
3.  [Sobre o exemplo](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#about-the-example)
4.  [Antes de começar](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#before-you-begin)
5.  [Etapa 1: definir o pipeline de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-1-define-the-build-pipeline)
6.  [Etapa 2: adicionar os arquivos de origem de teste de unidade ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-2-add-the-unit-test-source-files-to-the-repository)
7.  [Etapa 3: adicionar o script de empacotamento da roda do Python ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-3-add-the-python-wheel-packaging-script-to-the-repository)
8.  [Etapa 4: adicionar o notebook Python ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-4-add-the-python-notebook-to-the-repository)
9.  [Etapa 5: definir o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-5-define-the-release-pipeline)
10.  [Etapa 6: definir variáveis de ambiente para o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-6-define-environment-variables-for-the-release-pipeline)
11.  [Etapa 7: configurar o agente de versão para o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-7-configure-the-release-agent-for-the-release-pipeline)
12.  [Etapa 8: definir a versão do Python para o agente de versão](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-8-set-the-python-version-for-the-release-agent)
13.  [Etapa 9: desempacotar o artefato de build do pipeline de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-9-unpackage-the-build-artifact-from-the-build-pipeline)
14.  [Etapa 10. Instalar a CLI do Databricks e o relatórios XML unittest](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-10-install-the-databricks-cli-and-unittest-xml-reporting)
15.  [Etapa 11: implantar o notebook no workspace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-11-deploy-the-notebook-to-the-workspace)
16.  [Etapa 12: implantar a biblioteca no DBFS](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-12-deploy-the-library-to-dbfs)
17.  [Etapa 13: instalar a biblioteca no cluster](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-13-install-the-library-on-the-cluster)
18.  [Etapa 14: executar testes de integração no notebook Python](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-14-run-integration-tests-on-the-python-notebook)
19.  [Etapa 15: executar o notebook](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-15-run-the-notebook)
20.  [Etapa 16: gerar e avaliar os resultados de teste](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-16-generate-and-evaluate-test-results)
21.  [Etapa 17: publicar resultados de teste](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-17-publish-test-results)
22.  [Etapa 18: executar os pipelines de lançamento e de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-18-run-the-build-and-release-pipelines)

Observação

Este artigo aborda o Azure DevOps, que não é fornecido nem tem suporte do Databricks. Para entrar em contato com o provedor, confira o [Suporte do Azure DevOps Services](https://azure.microsoft.com/support/devops).

CI/CD (integração contínua e entrega contínua) refere-se ao processo de desenvolvimento e entrega de software em ciclos curtos e frequentes por meio do uso de pipelines de automação.

A integração contínua começa com a prática de fazer commit do seu código com alguma frequência para um branch em um repositório de código-fonte. Cada confirmação é mesclada com as confirmações de outros desenvolvedores para garantir que nenhum conflito foi introduzido. As alterações são então validadas criando um build e executando testes automatizados nesse build. Esse processo, em última análise, resulta em um artefato ou pacote de implantação, que terminará sendo implantado em um ambiente de destino, neste caso do artigo um workspace do Azure Databricks.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#overview-of-a-typical-azure-databricks-cicd-pipeline)

## Visão geral de um pipeline típico de CI/CD do Azure Databricks

Embora possa variar de acordo com suas necessidades, uma configuração típica de um pipeline do Azure Databricks inclui as seguintes etapas:

**Integração contínua:**

1.  Código
    1.  Desenvolve códigos e testes de unidade em um notebook do Azure Databricks ou usando um IDE externo.
    2.  Executa testes manualmente.
    3.  Faz commit de código e testa em um branch do git.
2.  Build
    1.  Coleta código e testes novos e atualizados.
    2.  Executa testes automatizados.
    3.  Cria bibliotecas e códigos não notebook do Apache Spark.
3.  Versão: gere um artefato de versão.

**Entrega contínua:**

1.  Implantar
    1.  Implanta notebooks.
    2.  Implanta bibliotecas.
2.  Testar: executa testes automatizados e relata os resultados.
3.  Operar: agenda programaticamente os fluxos de trabalho de engenharia de dados, análise e aprendizado de máquina.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#develop-and-commit-your-code)

## Desenvolver e confirmar seu código

Uma das primeiras etapas na criação de um pipeline de CI/CD é decidir uma estratégia de confirmação e ramificação de código para gerenciar o desenvolvimento e a integração de código novo e atualizado sem afetar negativamente o código atualmente em produção. Parte dessa decisão envolve escolher um sistema de controle de versão para conter seu código e facilitar a promoção desse código. O Azure Databricks dá suporte a [integrações com vários provedores Git](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/repos/#supported-git-providers), que permitem confirmar códigos e notebooks em um repositório Git.

Se o sistema de controle de versão não estiver entre os que têm suporte por meio da integração direta do notebook, ou se você quiser mais flexibilidade e controle do que a integração de provedor Git de autoatendimento, você poderá usar a [documentação de &configuração da CLI do Databricks](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/cli/) para exportar notebooks e fazer commit deles do computador local. Esse script deve ser executado de dentro de um repositório git local que está definido para sincronizar com o repositório remoto apropriado. Quando executado, esse script deve fazer o seguinte:

1.  Fazer check-out do branch desejado.
2.  Efetuar pull de novas alterações do branch remoto.
3.  Exportar código e notebooks do workspace do Azure Databricks usando a CLI do workspace do Azure Databricks.
4.  Solicitar ao usuário uma mensagem de confirmação ou usar o padrão se uma mensagem não for fornecida.
5.  Fazer commit de código e notebooks atualizados para o branch local.
6.  Efetuar push das alterações para o branch no repositório remoto.

O script a seguir executa estas etapas:

```
git checkout <branch>
git pull
databricks workspace export_dir --profile <profile> -o <path> ./Workspace

dt=`date '+%Y-%m-%d %H:%M:%S'`
msg_default="DB export on $dt"
read -p "Enter the commit comment [$msg_default]: " msg
msg=${msg:-$msg_default}
echo $msg

git add .
git commit -m "<commit-message>"
git push
```

Se você preferir desenvolver em um IDE em vez de em notebooks do Azure Databricks, poderá usar os recursos de integração do provedor de Git a IDEs modernos ou à CLI do Git para fazer commit do código.

O Azure Databricks fornece o [Databricks Connect](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/databricks-connect), que conecta IDEs a clusters do Azure Databricks. Isso é especialmente útil ao desenvolver bibliotecas, pois permite que você execute e faça o teste de unidade do seu código em clusters do Azure Databricks sem precisar implantar esse código. Confira [Limitações do Databricks Connect](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/databricks-connect#limitations) para determinar se há suporte para seu caso de uso.

Observação

Embora esse exemplo do artigo demonstre o Databricks Connect, o Databricks recomenda usar o [dbx](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/dbx) do Databricks Labs para desenvolvimento local em vez do Databricks Connect.

Dependendo da sua estratégia de ramificação e do processo de promoção, o ponto de início de um pipeline de CI/CD vai variar. No entanto, o código confirmado de vários colaboradores acabará sendo mesclado em um branch designado a ser criado e implantado. As etapas de gerenciamento de branch são executadas fora do Azure Databricks, usando as interfaces fornecidas pelo sistema de controle de versão.

Há várias ferramentas de CI/CD que você pode usar para gerenciar e executar seu pipeline. Este artigo ilustra como usar o [Azure DevOps](https://azure.microsoft.com/products/devops/). A CI/CD é um padrão de design, portanto, as etapas e os estágios descritos neste exemplo do artigo devem ser transferidos com algumas alterações para a linguagem de definição de pipeline de cada ferramenta. Além disso, grande parte do código neste pipeline de exemplo executa o código Python padrão, que você pode invocar em outras ferramentas.

O restante deste artigo descreve um par de pipelines de exemplo no Azure DevOps que você pode adaptar às suas próprias necessidades para o Azure Databricks.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#about-the-example)

## Sobre o exemplo

O exemplo deste artigo usa dois pipelines para criar e liberar código Python de exemplo, um notebook Python de exemplo e arquivos de configurações de build e versão relacionados, todos armazenados em um repositório Git remoto.

O primeiro pipeline, conhecido como pipeline de _build_, prepara artefatos de build para o segundo pipeline, conhecido como pipeline de _lançamento_. Separar o pipeline de build do pipeline de lançamento permite que você crie um build sem implantá-lo, ou implantar artefatos de vários builds de uma só vez.

Neste exemplo, você cria os pipelines de build e de lançamento, que fazem o seguinte:

1.  Criam uma máquina virtual do Azure para o pipeline de build. Essa máquina virtual usa a versão correta do Python para corresponder àquela no cluster do Azure Databricks remoto.
2.  Instala ferramentas do Python na máquina virtual para testar e empacotar o código Python de exemplo.
3.  Instala e configura na máquina virtual uma versão do Databricks Connect para corresponder àquela no cluster remoto.
4.  Copiam os arquivos do repositório Git para a máquina virtual.
5.  Executam testes de unidade no código Python e publicam os resultados do teste.
6.  Se os testes de unidade forem aprovados, empacotam o código Python em uma roda do Python e, em seguida, cria um arquivo tar gzip'ed que contém a roda e os arquivos de configurações de versão relacionados.
7.  Copia o arquivo tar gzip'ed como um arquivo zip em um local para o pipeline de lançamento acessar.
8.  Criam outra máquina virtual do Azure para o pipeline de lançamento. Essa máquina virtual também usa a versão correta do Python para corresponder àquela no cluster do Azure Databricks remoto.
9.  Obtêm o arquivo zip do local do pipeline de build e, em seguida, descompactam o arquivo zip para obter a roda do Python e os arquivos de configurações de versão relacionados.
10.  Implantam o notebook Python de exemplo em seu workspace remoto do Azure Databricks.
11.  Implantam a roda do Python e os arquivos de configurações de versão relacionados ao workspace do Azure Databricks remoto.
12.  Instalam a roda do Python implantado no cluster do Azure Databricks remoto.
13.  Executam testes de integrações no notebook Python implantado e ele chama uma função na roda do Python implantado e publica os resultados do teste.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#before-you-begin)

## Antes de começar

Para usar o exemplo deste artigo, você deve ter:

-   Um projeto existente do [Azure DevOps.](https://azure.microsoft.com/products/devops) Se ainda não tiver um projeto, [criar um projeto no Azure DevOps](https://learn.microsoft.com/azure/devops/organizations/projects/create-project?view=azure-devops).
-   Um repositório existente com um provedor Git com suporte do Azure DevOps. Você adicionará o código de exemplo do Python, o notebook Python de exemplo e os arquivos de configurações de versão relacionados a esse repositório. Se você ainda não tiver um repositório, crie um seguindo as instruções do provedor Git. Em seguida, conecte o projeto do Azure DevOps ao repositório existente, caso ainda não tenha feito isso. Para obter instruções, siga os links em [Repositórios de origem com suporte](https://learn.microsoft.com/azure/devops/pipelines/repos/?view=azure-devops).

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-1-define-the-build-pipeline)

## Etapa 1: definir o pipeline de build

O Azure DevOps oferece uma interface hospedada em nuvem para definir os estágios do seu pipeline de CI/CD usando o YAML. Para obter mais informações sobre o Azure DevOps e pipelines, consulte a [documentação do Azure DevOps](https://learn.microsoft.com/azure/devops/).

Nesta etapa você define o pipeline de build, que executa testes de unidade e cria um artefato de implantação. Para implantar o código em um workspace do Azure Databricks, especifique esse pipeline de build como um artefato de implantação em um pipeline de lançamento. Defina esse pipeline de lançamento mais tarde na Etapa 5.

Para executar pipelines de build, o Azure DevOps fornece agentes de execução sob demanda hospedados na nuvem que dão suporte a implantações no Kubernetes, VMs, Azure Functions, Aplicativos Web do Azure e muitos outros destinos. Neste exemplo, você usará um agente sob demanda para automatizar a implantação de código no workspace do Azure Databricks de destino. As ferramentas ou pacotes exigidos pelo pipeline de build devem ser definidos no script de pipeline de build e instalados no agente no tempo de execução. Este exemplo define e instala ferramentas e pacotes no agente que correspondem àqueles no cluster do Azure Databricks de destino e este exemplo usa o Databricks Runtime 10.4 LTS, que inclui o Python 3.8.

Agora, defina o pipeline de build da seguinte maneira:

1.  Entre no [Azure DevOps](https://azure.microsoft.com/products/devops) e abra o projeto do Azure DevOps.
    
2.  Clique em **Pipelines** na barra lateral e clique em **Pipelines** no menu **Pipelines**.
    
    ![Menu do Pipeline do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/ci-cd-demo-pipelines.png)
    
3.  Clique no botão **Criar Pipeline** para abrir o editor de pipeline, no qual você definirá seu script de pipeline de build no arquivo `azure-pipelines.yml` exibido. Se o editor de pipeline não estiver visível depois que você clicar no botão **Criar Pipeline**, selecione o nome do pipeline de build e clique em **Editar**.
    
    Você pode usar o seletor do GIT branch ![Seletor do GIT branch](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/git-selector.png) para personalizar o processo de build de cada branch no seu repositório Git. É uma melhor prática de CI/CD não fazer o trabalho de produção diretamente no branch `main` do repositório; este exemplo considera que já existe um branch chamado `release` no repositório a ser usado.
    
    ![Editor do Pipeline do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/script-in-ui.png)
    
    O script de pipeline de build `azure-pipelines.yml` é armazenado por padrão no diretório raiz do repositório Git remoto associado ao pipeline.
    
4.  Configure as variáveis de ambiente que os pipelines de build referenciam clicando no botão **Variáveis**.
    
    Para este exemplo, defina as cinco variáveis de ambiente a seguir e lembre-se de clicar em **Salvar** depois de defini-las:
    
    -   `DATABRICKS_ADDRESS`, que representa a [URL por workspace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/workspace/per-workspace-urls) do workspace do Azure Databricks, começando com `https://`, por exemplo `https://adb-<workspace-id>.<random-number>.azuredatabricks.net`. Não inclua o `/` à direita após `.net`.
        
    -   `DATABRICKS_API_TOKEN`, que representa o [token de acesso pessoal](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/auth#pat) do Azure Databricks ou o [token do Azure AD (Azure Active Directory)](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/auth#aadt).
        
    -   `DATABRICKS_CLUSTER_ID`, que representa a [ID do cluster](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/workspace/workspace-details#cluster-url-and-id) do Azure Databricks em seu workspace.
        
    -   `DATABRICKS_ORG_ID`, que é a [ID do workspace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/workspace/per-workspace-urls) do seu workspace.
        
    -   `DATABRICKS_PORT`, que representa a porta usada pelo Databricks Connect. Esse valor normalmente é `15001`.
        
5.  Substitua o conteúdo inicial do arquivo `azure-pipelines.yml` do pipeline pela definição a seguir e clique em **Salvar**.
    
    ```
    # Specify the trigger event to start the build pipeline.
    # In this case, new code merged into the release branch initiates a new build.
    trigger:
    - release
    
    # Specify the operating system for the agent that runs on the Azure virtual
    # machine for the build pipeline (known as the build agent). The virtual
    # machine image should match the one on the Azure Databricks cluster as
    # closely as possible. For example, Databricks Runtime 10.4 LTS runs
    # Ubuntu 20.04.4 LTS, which maps to the Ubuntu 20.04 virtual machine
    # image in the Azure Pipeline agent pool. See
    # https://learn.microsoft.com/azure/devops/pipelines/agents/hosted#software
    pool:
      vmImage: ubuntu-20.04
    
    # Install Python. The version of Python must match the version on the
    # Azure Databricks cluster. This pipeline assumes that you are using
    # Databricks Runtime 10.4 LTS on the cluster.
    steps:
    - task: UsePythonVersion@0
      displayName: 'Use Python 3.8'
      inputs:
        versionSpec: 3.8
    
    # Install required Python modules and their dependencies. These
    # include pytest, which is needed to run unit tests on a cluster,
    # and setuptools, which is needed to create a Python wheel. Also
    # install the version of Databricks Connect that is compatible
    # with Databricks Runtime 10.4 LTS on the cluster.
    - script: |
        pip install pytest requests setuptools wheel
        pip install -U databricks-connect==10.4.*
      displayName: 'Load Python dependencies'
    
    # Use environment variables to pass Azure Databricks workspace and cluster
    # information to the Databricks Connect configuration function.
    - script: |
        echo "y
        $(DATABRICKS_ADDRESS)
        $(DATABRICKS_API_TOKEN)
        $(DATABRICKS_CLUSTER_ID)
        $(DATABRICKS_ORG_ID)
        $(DATABRICKS_PORT)" | databricks-connect configure
      displayName: 'Configure Databricks Connect'
    
    # Download the files from the designated branch in the Git remote repository
    # onto the build agent.
    - checkout: self
      persistCredentials: true
      clean: true
    
    # For library code developed outside of an Azure Databricks notebook, the
    # process is like traditional software development practices. You write a
    # unit test using a testing framework, such as the Python pytest module, and
    # you use JUnit-formatted XML files to store the test results.
    - script: |
        python -m pytest --junit-xml=$(Build.Repository.LocalPath)/logs/TEST-LOCAL.xml $(Build.Repository.LocalPath)/libraries/python/dbxdemo/test*.py || true
      displayName: 'Run Python unit tests for library code'
    
    # Publishes the test results to Azure DevOps. This lets you visualize
    # reports and dashboards related to the status of the build process.
    - task: PublishTestResults@2
      inputs:
        testResultsFiles: '**/TEST-*.xml'
        failTaskOnFailedTests: true
        publishRunAttachments: true
    
    # Package the example Python code into a Python wheel.
    - script: |
        cd $(Build.Repository.LocalPath)/libraries/python/dbxdemo
        python3 setup.py sdist bdist_wheel
        ls dist/
      displayName: 'Build Python Wheel for Libs'
    
    # Generate the deployment artifacts. To do this, the build agent gathers
    # all the new or updated code to be deployed to the Azure Databricks
    # environment, including the sample Python notebook, the Python wheel
    # library that was generated by the build process, related release settings
    # files, and the result summary of the tests for archiving purposes.
    # Use git diff to flag files that were added in the most recent Git merge.
    # Then add the Python wheel file that you just created along with utility
    # scripts used by the release pipeline.
    # The implementation in your pipeline will likely be different.
    # The objective here is to add all files intended for the current release.
    - script: |
        git diff --name-only --diff-filter=AMR HEAD^1 HEAD | xargs -I '{}' cp --parents -r '{}' $(Build.BinariesDirectory)
        mkdir -p $(Build.BinariesDirectory)/libraries/python/libs
        cp $(Build.Repository.LocalPath)/libraries/python/dbxdemo/dist/*.* $(Build.BinariesDirectory)/libraries/python/libs
        mkdir -p $(Build.BinariesDirectory)/cicd-scripts
        cp $(Build.Repository.LocalPath)/cicd-scripts/*.* $(Build.BinariesDirectory)/cicd-scripts
        mkdir -p $(Build.BinariesDirectory)/notebooks
        cp $(Build.Repository.LocalPath)/notebooks/*.* $(Build.BinariesDirectory)/notebooks
      displayName: 'Get Changes'
    
    # Create the deployment artifact and then publish it to the
    # artifact repository.
    - task: ArchiveFiles@2
      inputs:
        rootFolderOrFile: '$(Build.BinariesDirectory)'
        includeRootFolder: false
        archiveType: 'zip'
        archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip'
        replaceExistingArchive: true
    
    - task: PublishBuildArtifacts@1
      inputs:
        ArtifactName: 'DatabricksBuild'
    ```
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-2-add-the-unit-test-source-files-to-the-repository)

## Etapa 2: adicionar os arquivos de origem de teste de unidade ao repositório

Para permitir que o agente de build execute os testes de unidade, adicione os três arquivos `addcol.py`, `test-addcol.py` e `__init__.py` a seguir, conforme mostrado, em um caminho de pasta `libraries/python/dbxdemo` criado na raiz do repositório Git remoto associado.

O primeiro arquivo, `addcol.py`, representa uma função de biblioteca que pode ser instalada em um cluster do Azure Databricks. Essa função simples adiciona uma nova coluna, populada por um literal, a um DataFrame do Apache Spark.

```
# addcol.py
import pyspark.sql.functions as F

def with_status(df):
  return df.withColumn("status", F.lit("checked"))
```

O segundo arquivo, `test-addcol.py`, testa o código do arquivo `addcol.py` passando um objeto DataFrame fictício para a função `with_status` anterior. O resultado é então comparado a um objeto do DataFrame que contém os valores esperados. Se os valores corresponderem, o teste será aprovado.

```
# test-addcol.py
import pytest

from pyspark.sql import SparkSession
from .addcol import with_status

@pytest.fixture
def spark() -> SparkSession:
  return SparkSession.builder.getOrCreate()

def test_with_status(spark):
  source_data = [
    ("pete", "pan", "peter.pan@databricks.com"),
    ("jason", "argonaut", "jason.argonaut@databricks.com")
  ]
  source_df = spark.createDataFrame(
    source_data,
    ["first_name", "last_name", "email"]
  )

  actual_df = with_status(source_df)

  expected_data = [
    ("pete", "pan", "peter.pan@databricks.com", "checked"),
    ("jason", "argonaut", "jason.argonaut@databricks.com", "checked")
  ]

  expected_df = spark.createDataFrame(
    expected_data,
    ["first_name", "last_name", "email", "status"]
  )

  assert(expected_df.collect() == actual_df.collect())
```

O terceiro arquivo, `__init__.py`, deve estar em branco e também deve existir no caminho da pasta `libraries/python/dbxdemo`. Esse arquivo permite que o arquivo `test-addcol.py` carregue o arquivo `addcol.py` como uma biblioteca.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-3-add-the-python-wheel-packaging-script-to-the-repository)

## Etapa 3: adicionar o script de empacotamento da roda do Python ao repositório

Para permitir que o agente de build use as [Setuptools](https://setuptools.pypa.io/en/latest/) do Python para empacotar a roda do Python para dar ao pipeline de lançamento, adicione uma versão mínima do seguinte arquivo `setup.py` ao caminho da pasta `libraries/python/dbxdemo` no repositório Git remoto associado:

```
# setup.py
from setuptools import setup, find_packages

setup(
  name = 'dbxdemo',
  version = '0.1.0',
  packages = ['.']
)
```

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-4-add-the-python-notebook-to-the-repository)

## Etapa 4: adicionar o notebook Python ao repositório

Para permitir que o agente de build forneça o notebook Python de exemplo ao pipeline de lançamento, adicione o seguinte arquivo `dbxdemo-notebook.py` a uma pasta `notebooks` criada na raiz do repositório Git remoto associado:

```
# Databricks notebook source
import sys
sys.path.append("/databricks/python3/lib/python3.8/site-packages")

# COMMAND ----------

import unittest
from addcol import *

class TestNotebook(unittest.TestCase):

  def test_with_status(self):
    source_data = [
      ("pete", "pan", "peter.pan@databricks.com"),
      ("jason", "argonaut", "jason.argonaut@databricks.com")
    ]

    source_df = spark.createDataFrame(
      source_data,
      ["first_name", "last_name", "email"]
    )

    actual_df = with_status(source_df)

    expected_data = [
      ("pete", "pan", "peter.pan@databricks.com", "checked"),
      ("jason", "argonaut", "jason.argonaut@databricks.com", "checked")
    ]

    expected_df = spark.createDataFrame(
      expected_data,
      ["first_name", "last_name", "email", "status"]
    )

    self.assertEqual(expected_df.collect(), actual_df.collect())

unittest.main(argv = [''], verbosity = 2, exit = False)
```

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-5-define-the-release-pipeline)

## Etapa 5: definir o pipeline de lançamento

O pipeline de lançamento implanta os artefatos de build em um ambiente do Azure Databricks. Separar o pipeline de liberação do pipeline de build nesta etapa permite que nas etapas anteriores você crie um build sem implantá-lo, ou que implante artefatos de vários builds de uma só vez.

1.  No projeto do Azure DevOps, no menu **Pipelines** na barra lateral, clique em **Lançamentos**.
    
    ![Lançamentos do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/ci-cd-releases.png)
    
2.  Clique em **Novo pipeline**.
    
3.  Na lateral da tela, há uma lista de modelos em destaque de padrões comuns de implantação. Nesse pipeline de lançamento, clique em ![Trabalho vazio](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/empty-job.png).
    
    ![Pipeline de lançamento 1 do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-1.png)
    
4.  Na caixa **Artefatos** na lateral da tela, clique em ![Adicionar](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/plus-add.png). No painel **Adicionar um artefato**, em **Origem (pipeline de build),** selecione o pipeline de build criado anteriormente. Clique em **Adicionar**.
    
    ![Pipeline de lançamento 2 do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-add-artifact.png)
    
5.  Você pode configurar como o pipeline é disparado clicando no ![Ícone de Raio](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/lightning-bolt.png), que exibirá as opções de disparo na lateral da tela. Se você quiser que um lançamento seja iniciado automaticamente com base na disponibilidade do artefato de compilação ou após um fluxo de trabalho de solicitação de pull, habilite o gatilho apropriado. Para este exemplo, na última etapa deste artigo, você dispara manualmente o pipeline de build e, em seguida, o pipeline de lançamento.
    
    ![Fase 1 do pipeline de lançamento do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-stage-1.png)
    
6.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-6-define-environment-variables-for-the-release-pipeline)

## Etapa 6: definir variáveis de ambiente para o pipeline de lançamento

O pipeline de lançamento depende das três variáveis de ambiente a seguir, que você pode adicionar clicando em **Adicionar** na seção **Variáveis de pipeline** na guia **Variáveis**, com um **Escopo** do **Estágio 1**:

-   `DATABRICKS_HOST`, que representa a [URL por workspace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/workspace/per-workspace-urls) do workspace do Azure Databricks, começando com `https://`, por exemplo `https://adb-<workspace-id>.<random-number>.azuredatabricks.net`. Não inclua o `/` à direita após `.net`. Esse deve ser o mesmo valor que `DATABRICKS_ADDRESS` definido anteriormente no pipeline de build. (O Databricks Connect no pipeline de build espera encontrar uma variável de ambiente `DATABRICKS_ADDRESS`, enquanto a CLI do Databricks no pipeline de lançamento espera que essa variável de ambiente seja nomeada como `DATABRICKS_HOST`.)
    
-   `DATABRICKS_TOKEN`, que representa o [token de acesso pessoal](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/auth#pat) do Azure Databricks ou o [token do Azure AD (Azure Active Directory)](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/auth#aadt). Esse deve ser o mesmo valor que `DATABRICKS_API_TOKEN` definido anteriormente no pipeline de build. (No pipeline de build, o Databricks Connect espera encontrar uma variável de ambiente `DATABRICKS_API_TOKEN`. No pipeline de lançamento, a CLI do Databricks espera que essa variável de ambiente seja nomeada como `DATABRICKS_TOKEN`.)
    
-   `DATABRICKS_CLUSTER_ID`, que representa a [ID do cluster](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/workspace/workspace-details#cluster-url-and-id) do Azure Databricks em seu workspace. Esse deve ser o mesmo valor que a variável de ambiente `DATABRICKS_CLUSTER_ID` definida anteriormente no pipeline de build.
    

![Variáveis de ambiente do pipeline de lançamento do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-env-vars.png)

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-7-configure-the-release-agent-for-the-release-pipeline)

## Etapa 7: configurar o agente de versão para o pipeline de lançamento

1.  Clique no link **1 trabalho, 0 tarefa** no objeto **Estágio 1**.
    
    ![Adicionar fase do pipeline de lançamento do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/stage-button.png)
    
2.  Na guia **Tarefas**, clique em **Trabalho do agente**.
    
3.  Na seção **Seleção do agente**, para **Pool de agentes**, selecione **Azure Pipelines**.
    
4.  Para **Especificação do Agente**, selecione o mesmo agente que você especificou para o agente de build anteriormente, neste exemplo **ubuntu-20.04**.
    
    ![Definição de trabalho do agente de pipeline de lançamento do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-agent-job.png)
    
5.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-8-set-the-python-version-for-the-release-agent)

## Etapa 8: definir a versão do Python para o agente de versão

1.  Clique no sinal de adição na seção **Trabalho do agente**, indicada pela seta vermelha na figura a seguir. Uma lista pesquisável de tarefas disponíveis será exibida. Há também uma guia **Marketplace** para plug-ins de terceiros que podem ser usados para complementar as tarefas padrão do Azure DevOps. Você adicionará várias tarefas ao agente de versão durante as próximas etapas.
    
    ![Adicionar tarefa do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-add-task.png)
    
2.  A primeira tarefa adicionada é **Usar a versão do Python**, localizada na guia **Ferramenta**. Se você não encontrar essa tarefa, use a caixa **Pesquisar** para procurá-la. Ao encontrar a caixa, selecione-a e clique no botão **Adicionar** próximo à tarefa **Usar versão do Python**.
    
    ![Definir versão 1 do Python do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-set-python-version.png)
    
3.  Assim como no pipeline de build, você deseja garantir que a versão do Python seja compatível com os scripts chamados nas tarefas subsequentes. Nesse caso, clique na tarefa **Usar Python 3.x** próxima ao **Trabalho do agente** e, em seguida, defina a **Especificação de versão** como `3.8`. Defina também o **Nome de exibição** como `Use Python 3.8`.
    
    ![Definir versão 2 do Python do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/use-python-version.png)
    
4.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-9-unpackage-the-build-artifact-from-the-build-pipeline)

## Etapa 9: desempacotar o artefato de build do pipeline de build

1.  Em seguida, faça com que o agente de versão extraia a roda do Python, os arquivos de configurações de versão relacionados e o notebook Python de exemplo do arquivo zip usando a tarefa **Extrair arquivos**: clique no sinal de adição na seção **Trabalho do agente**, selecione a tarefa **Extrair arquivos** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Extrair arquivos** próxima ao **Trabalho do agente**, defina **Padrões de arquivo morto** como `**/*.zip` e defina a **pasta de destino** como a variável do sistema `$(Release.PrimaryArtifactSourceAlias)/Databricks`. Defina também o **Nome de exibição** como `Extract build pipeline artifact`.
    
    Observação
    
    `$(Release.PrimaryArtifactSourceAlias)` representa um alias gerado pelo Azure DevOps para identificar o local de origem do artefato primário no agente de versão, por exemplo `_<your-github-alias>.<your-github-repo-name>`. O pipeline de lançamento define esse valor como a variável de ambiente `RELEASE_PRIMARYARTIFACTSOURCEALIAS` na fase **Inicializar trabalho** para o agente de versão. Confira [Variáveis de lançamento e artefatos clássicos](https://learn.microsoft.com/azure/devops/pipelines/release/variables?view=azure-devops&tabs=batch).
    
3.  Defina o **Nome de exibição** como `Extract build pipeline artifact`.
    
    ![Desempacotar Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/unpackage-build-artifact.png)
    
4.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-10-install-the-databricks-cli-and-unittest-xml-reporting)

## Etapa 10. Instalar a CLI do Databricks e o relatórios XML unittest

1.  Em seguida, instale a CLI do Databricks e o pacote de relatórios XML `unittest` no agente de versão, pois o agente de versão chamará a CLI do Databricks e `unittest` nas próximas tarefas. Para fazer isso, use a tarefa **Bash**: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Bash** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Script bash** próxima ao **Trabalho do agente**.
    
3.  Em **Tipo**, selecione **Embutido**.
    
4.  Substitua o conteúdo do **Script** pelo seguinte comando, que instala a CLI do Databricks:
    
    ```
    pip install databricks-cli
    pip install unittest-xml-reporting
    ```
    
5.  Defina o **Nome de exibição** como `Install Databricks CLI and unittest XML reporting`.
    
    ![Pacotes de instalação do pipeline de lançamento do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-install-packages.png)
    
6.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-11-deploy-the-notebook-to-the-workspace)

## Etapa 11: implantar o notebook no workspace

1.  Em seguida, faça com que o agente de versão use a CLI do Databricks para implantar o notebook Python de exemplo no workspace do Azure Databricks usando outra tarefa **bash**: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Bash** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Script bash** próxima ao **Trabalho do agente**.
    
3.  Em **Tipo**, selecione **Embutido**.
    
4.  Substitua o conteúdo do **Script** pelo seguinte comando, que executa o subcomando `databricks workspace import` para copiar o notebook Python do agente de versão para o workspace do Azure Databricks:
    
    ```
    databricks workspace import --language=PYTHON --format=SOURCE --overwrite $(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/notebooks/dbxdemo-notebook.py /Shared/dbxdemo-notebook.py
    ```
    
    Observação
    
    `$(System.ArtifactsDirectory)` representa o diretório do qual os artefatos são baixados durante a implantação de uma versão, por exemplo `/home/vsts/work/r1/a`. O pipeline de lançamento define esse valor como a variável de ambiente `SYSTEM_ARTIFACTSDIRECTORY` na fase **Inicializar trabalho** para o agente de versão. Confira [Variáveis de lançamento e artefatos clássicos](https://learn.microsoft.com/azure/devops/pipelines/release/variables?view=azure-devops&tabs=batch).
    
5.  Defina o **Nome de exibição** como `Copy notebook to workspace`.
    
    ![Notebook de cópia do pipeline de lançamento para o workspace do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-copy-notebook-to-workspace.png)
    
6.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-12-deploy-the-library-to-dbfs)

## Etapa 12: implantar a biblioteca no DBFS

1.  Em seguida, faça com que o agente de versão use a CLI do Databricks para implantar a biblioteca Python em um local DBFS no workspace do Azure Databricks usando outra tarefa **bash**: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Bash** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Script bash** próxima ao **Trabalho do agente**.
    
3.  Em **Tipo**, selecione **Embutido**.
    
4.  Substitua o conteúdo do **Script** pelo seguinte comando, que executa o subcomando `databricks fs cp` para copiar a biblioteca Python do agente de versão para o workspace do Azure Databricks:
    
    ```
    databricks fs cp  --overwrite $(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/libraries/python/libs/dbxdemo-0.1.0-py3-none-any.whl dbfs:/libraries/python/libs/dbxdemo-0.1.0-py3-none-any.whl
    ```
    
5.  Defina o **Nome de exibição** como `Copy Python wheel to workspace`.
    
    ![Roda de cópia do pipeline de lançamento para o workspace do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/release-pipeline-copy-wheel-to-workspace.png)
    
6.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-13-install-the-library-on-the-cluster)

## Etapa 13: instalar a biblioteca no cluster

1.  Em seguida, faça com que o agente de versão instale a biblioteca que acabou de ser copiada para o workspace em um cluster específico dentro desse workspace. Para fazer isso, crie uma tarefa de **Script Python**: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Script Python** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Executar um script Python** próxima ao **Trabalho do agente**.
    
3.  Defina o **Caminho do script** como `$(Release.PrimaryArtifactSourceAlias)/Databricks/cicd-scripts/installWhlLibrary.py`. O script Python, `installWhlLibrary.py`, está no artefato criado pelo nosso pipeline de build. O script `installWhlLibrary.py` usa cinco argumentos, que você definirá nesta tarefa da seguinte maneira:
    
    -   `shard` - A URL do workspace de destino (por exemplo, `https://<region>.azuredatabricks.net`). Isso mapeia para a variável de ambiente `DATABRICKS_HOST` definida anteriormente para o pipeline de lançamento. Essa URL não deve incluir o `/` à direita após `.net`.
        
    -   `token` - Um token de acesso pessoal do Azure Databricks ou token do Azure AD para workspace. Isso mapeia para a variável de ambiente `DATABRICKS_TOKEN` definida anteriormente para o pipeline de lançamento.
        
    -   `clusterid` - A ID do cluster no qual será instalada a biblioteca. Isso mapeia para a variável de ambiente `DATABRICKS_CLUSTER_ID` definida anteriormente para o pipeline de lançamento.
        
    -   `libs` - O diretório extraído que contém as bibliotecas. Isso mapeia para o caminho no agente de versão que contém a roda do Python. O local _deve_ incluir `/` à direita.
        
    -   `dbfspath` - O caminho dentro do sistema de arquivos DBFS para recuperar as bibliotecas. O caminho _não deve_ incluir o `dbfs:` inicial, mas _deve_ incluir o `/` inicial. Além disso, o caminho _não deve_ incluir o `/` à direita.
        
4.  Defina **Argumentos** para o seguinte:
    
    ```
    --shard=$(DATABRICKS_HOST) --token=$(DATABRICKS_TOKEN) --clusterid=$(DATABRICKS_CLUSTER_ID) --libs=$(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/libraries/python/libs/ --dbfspath=/libraries/python/libs
    ```
    
    ![Instalar biblioteca do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/python-script-install-library.png)
    
5.  Defina **Nome de exibição** como **Instalar a roda do Python no cluster**.
    
6.  Clique em **Salvar> OK**.
    

O arquivo `installWhlLibrary.py` anterior verifica se, antes de instalar uma nova versão de uma biblioteca em um cluster do Azure Databricks, a biblioteca existente foi desinstalada primeiro. Para fazer isso, o arquivo `installWhlLibrary.py` chama a API REST do Databricks para executar as seguintes etapas:

1.  Verificar se a biblioteca está instalada.
2.  Se estiver, desinstale a biblioteca.
3.  Reiniciar o cluster se alguma desinstalação for executada.
4.  Aguardar até que o cluster esteja em execução antes de continuar.
5.  Instalar a biblioteca.

O conteúdo do arquivo `installWhlLibrary.py` é o seguinte. Para que o pipeline de lançamento execute esse script, crie uma pasta chamada `cicd-scripts` na raiz do repositório Git e adicione esse arquivo `installWhlLibrary.py` à pasta `cicd-scripts`:

```
# installWhlLibrary.py
#!/usr/bin/python3
import json
import requests
import sys
import getopt
import time
import os

def main():
  shard = ''
  token = ''
  clusterid = ''
  libspath = ''
  dbfspath = ''

  try:
    opts, args = getopt.getopt(sys.argv[1:], 'hstcld',
      ['shard=', 'token=', 'clusterid=', 'libs=', 'dbfspath='])
  except getopt.GetoptError:
    print(
      'installWhlLibrary.py -s <shard> -t <token> -c <clusterid> -l <libs> -d <dbfspath>')
    sys.exit(2)

  for opt, arg in opts:
    if opt == '-h':
      print(
        'installWhlLibrary.py -s <shard> -t <token> -c <clusterid> -l <libs> -d <dbfspath>')
      sys.exit()
    elif opt in ('-s', '--shard'):
      shard = arg
    elif opt in ('-t', '--token'):
      token = arg
    elif opt in ('-c', '--clusterid'):
      clusterid = arg
    elif opt in ('-l', '--libs'):
      libspath=arg
    elif opt in ('-d', '--dbfspath'):
      dbfspath=arg

  print('-s is ' + shard)
  print('-t is ' + token)
  print('-c is ' + clusterid)
  print('-l is ' + libspath)
  print('-d is ' + dbfspath)

  # Generate the list of files from walking the local path.
  libslist = []
  for path, subdirs, files in os.walk(libspath):
    for name in files:

      name, file_extension = os.path.splitext(name)
      if file_extension.lower() in ['.whl']:
        print('Adding ' + name + file_extension.lower() + ' to the list of .whl files to evaluate.')
        libslist.append(name + file_extension.lower())

  for lib in libslist:
    dbfslib = 'dbfs:' + dbfspath + '/' + lib
    print('Evaluating whether ' + dbfslib + ' must be installed, or uninstalled and reinstalled.')

    if (getLibStatus(shard, token, clusterid, dbfslib)) is not None:
      print(dbfslib + ' status: ' + getLibStatus(shard, token, clusterid, dbfslib))
      if (getLibStatus(shard, token, clusterid, dbfslib)) == "not found":
        print(dbfslib + ' not found. Installing.')
        installLib(shard, token, clusterid, dbfslib)
      else:
        print(dbfslib + ' found. Uninstalling.')
        uninstallLib(shard, token, clusterid, dbfslib)
        print("Restarting cluster: " + clusterid)
        restartCluster(shard, token, clusterid)
        print('Installing ' + dbfslib + '.')
        installLib(shard, token, clusterid, dbfslib)

def uninstallLib(shard, token, clusterid, dbfslib):
  values = {'cluster_id': clusterid, 'libraries': [{'whl': dbfslib}]}
  requests.post(shard + '/api/2.0/libraries/uninstall', data=json.dumps(values), auth=("token", token))

def restartCluster(shard, token, clusterid):
  values = {'cluster_id': clusterid}
  requests.post(shard + '/api/2.0/clusters/restart', data=json.dumps(values), auth=("token", token))

  waiting = True
  p = 0
  while waiting:
    time.sleep(30)
    clusterresp = requests.get(shard + '/api/2.0/clusters/get?cluster_id=' + clusterid,
      auth=("token", token))
    clusterjson = clusterresp.text
    jsonout = json.loads(clusterjson)
    current_state = jsonout['state']
    print(clusterid + " state: " + current_state)
    if current_state in ['TERMINATED', 'RUNNING','INTERNAL_ERROR', 'SKIPPED'] or p >= 10:
      break
      p = p + 1

def installLib(shard, token, clusterid, dbfslib):
  values = {'cluster_id': clusterid, 'libraries': [{'whl': dbfslib}]}
  requests.post(shard + '/api/2.0/libraries/install', data=json.dumps(values), auth=("token", token))

def getLibStatus(shard, token, clusterid, dbfslib):

  resp = requests.get(shard + '/api/2.0/libraries/cluster-status?cluster_id='+ clusterid, auth=("token", token))
  libjson = resp.text
  d = json.loads(libjson)
  if (d.get('library_statuses')):
    statuses = d['library_statuses']

    for status in statuses:
      if (status['library'].get('whl')):
        if (status['library']['whl'] == dbfslib):
          return status['status']
  else:
    # No libraries found.
    return "not found"

if __name__ == '__main__':
  main()
```

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-14-run-integration-tests-on-the-python-notebook)

## Etapa 14: executar testes de integração no notebook Python

Você também pode executar testes diretamente de notebooks que contenham declarações usando `unittest`. Nesse caso, você usará os mesmos testes usado nos testes de unidade anteriores, mas agora eles importarão a biblioteca `addcol` instalada do `whl` que você acabou de instalar no cluster.

Para automatizar esses testes e incluí-los no pipeline de CI/CD, use a API REST do Databricks para executar o notebook a partir do servidor de CI/CD. Isso permite verificar se a execução do notebook foi aprovada ou falhou usando `unittest`. Falhas de declaração aparecerão na saída JSON retornada pela API REST e nos resultados do teste JUnit.

1.  Adicione uma tarefa de **linha de comando** ao pipeline de lançamento: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Linha de comando** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Script de linha de comando** próxima ao **Trabalho do agente**.
    
3.  Substitua o conteúdo da caixa **script** pelo seguinte script. Esses comandos criam diretórios para os logs de execução do notebook e os resumos do teste. Esses comandos também incluem um comando `pip` para instalar os módulos `requests` e `pytest` necessários.
    
    ```
    mkdir -p $(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/logs/json
    mkdir -p $(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/logs/xml
    pip install pytest requests
    ```
    
4.  Defina **Nome de exibição** como **Criar diretórios de testes de integração**.
    
    ![Configurar o ambiente de teste do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/commandline-configure-test-envt.png)
    
5.  Clique em **Salvar> OK**.
    

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-15-run-the-notebook)

## Etapa 15: executar o notebook

1.  Crie uma tarefa de **Script Python**: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Script Python** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Executar um script Python** próxima ao **Trabalho do agente**.
    
3.  Com o **caminho do arquivo** selecionado, defina o **caminho do script** como `$(Release.PrimaryArtifactSourceAlias)/Databricks/cicd-scripts/executenotebook.py`. O script Python, `executeNotebook.py`, está no artefato criado pelo nosso pipeline de build. O script `executeNotebook.py` usa cinco argumentos, que você definirá nesta tarefa da seguinte maneira:
    
    -   `shard` - A URL do workspace de destino (por exemplo, `https://<region>.azuredatabricks.net`). Isso mapeia para a variável de ambiente `DATABRICKS_HOST` definida anteriormente para o pipeline de lançamento. Essa URL não deve incluir o `/` à direita após `.net`.
        
    -   `token` - Um token de acesso pessoal do Azure Databricks ou token do Azure AD para workspace. Isso mapeia para a variável de ambiente `DATABRICKS_TOKEN` definida anteriormente para o pipeline de lançamento.
        
    -   `clusterid` - A ID do cluster no qual será instalada a biblioteca. Isso mapeia para a variável de ambiente `DATABRICKS_CLUSTER_ID` definida anteriormente para o pipeline de lançamento.
        
    -   `localpath` - O diretório extraído que contém os notebooks de teste. O caminho _não deve_ incluir o `/` à direita.
        
    -   `workspacepath` - O caminho no workspace no qual os notebooks de teste foram implantados. O local _deve_ incluir o `/` inicial. Além disso, o caminho _não deve_ incluir o `/` à direita.
        
    -   `outfilepath` - O caminho que você criou para armazenar a saída JSON retornada pela API REST.
        
4.  Defina **Argumentos** para o seguinte:
    
    ```
    --shard=$(DATABRICKS_HOST) --token=$(DATABRICKS_TOKEN) --clusterid=$(DATABRICKS_CLUSTER_ID) --localpath=$(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/notebooks --workspacepath=/Shared --outfilepath=$(System.ArtifactsDirectory)/$(Release.PrimaryArtifactSourceAlias)/Databricks/logs/json
    ```
    
5.  Defina **Nome de exibição** como **Executar notebook**.
    
    ![Executar notebooks do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/pythonscript-executenotebooks.png)
    
6.  Clique em **Salvar> OK**.
    

O script `executenotebook.py` a seguir executa o notebook usando o ponto de extremidade de envio de execuções dos trabalhos, que envia um trabalho anônimo. Por ser este um ponto de extremidade assíncrono, ele usa a ID do trabalho retornada inicialmente pela chamada REST para a sondagem do status do trabalho. Após a conclusão do trabalho, a saída JSON é salva no caminho especificado pelos argumentos da função passados na invocação.

Para que o pipeline de lançamento execute esse script, adicione esse arquivo `executenotebook.py` à pasta `cicd-scripts` na raiz do repositório Git, na qual você adicionou o arquivo `installWhlLibrary.py` anteriormente:

```
# executenotebook.py
#!/usr/bin/python3
import json
import requests
import os
import sys
import getopt
import time

def main():
  shard = ''
  token = ''
  clusterid = ''
  localpath = ''
  workspacepath = ''
  outfilepath = ''

  try:
    opts, args = getopt.getopt(sys.argv[1:], 'hs:t:c:lwo',
      ['shard=', 'token=', 'clusterid=', 'localpath=', 'workspacepath=', 'outfilepath='])
  except getopt.GetoptError:
    print(
      'executenotebook.py -s <shard> -t <token>  -c <clusterid> -l <localpath> -w <workspacepath> -o <outfilepath>)')
    sys.exit(2)

  for opt, arg in opts:
    if opt == '-h':
      print(
        'executenotebook.py -s <shard> -t <token> -c <clusterid> -l <localpath> -w <workspacepath> -o <outfilepath>')
      sys.exit()
    elif opt in ('-s', '--shard'):
        shard = arg
    elif opt in ('-t', '--token'):
        token = arg
    elif opt in ('-c', '--clusterid'):
        clusterid = arg
    elif opt in ('-l', '--localpath'):
        localpath = arg
    elif opt in ('-w', '--workspacepath'):
        workspacepath = arg
    elif opt in ('-o', '--outfilepath'):
        outfilepath = arg

  print('-s is ' + shard)
  print('-t is ' + token)
  print('-c is ' + clusterid)
  print('-l is ' + localpath)
  print('-w is ' + workspacepath)
  print('-o is ' + outfilepath)

  # Generate the list of notebooks from walking the local path.
  notebooks = []
  for path, subdirs, files in os.walk(localpath):
    for name in files:
      fullpath = path + '/' + name
      # Remove the localpath to the repo but keep the workspace path.
      fullworkspacepath = workspacepath + path.replace(localpath, '')

      name, file_extension = os.path.splitext(fullpath)
      if file_extension.lower() in ['.scala', '.sql', '.r', '.py']:
        row = [fullpath, fullworkspacepath, 1]
        notebooks.append(row)

  # Run each notebook in the list.
  for notebook in notebooks:
    nameonly = os.path.basename(notebook[0])
    workspacepath = notebook[1]

    name, file_extension = os.path.splitext(nameonly)

    # workspacepath removes the extension, so now add it back.
    fullworkspacepath = workspacepath + '/' + name + file_extension

    print('Running job for: ' + fullworkspacepath)
    values = {'run_name': name, 'existing_cluster_id': clusterid, 'timeout_seconds': 3600, 'notebook_task': {'notebook_path': fullworkspacepath}}

    resp = requests.post(shard + '/api/2.0/jobs/runs/submit',
      data=json.dumps(values), auth=("token", token))
    runjson = resp.text
    print("runjson: " + runjson)
    d = json.loads(runjson)
    runid = d['run_id']

    i=0
    waiting = True
    while waiting:
      time.sleep(10)
      jobresp = requests.get(shard + '/api/2.0/jobs/runs/get?run_id='+str(runid),
        data=json.dumps(values), auth=("token", token))
      jobjson = jobresp.text
      print("jobjson: " + jobjson)
      j = json.loads(jobjson)
      current_state = j['state']['life_cycle_state']
      runid = j['run_id']
      if current_state in ['TERMINATED', 'INTERNAL_ERROR', 'SKIPPED'] or i >= 12:
        break
      i=i+1

    if outfilepath != '':
      file = open(outfilepath + '/' +  str(runid) + '.json', 'w')
      file.write(json.dumps(j))
      file.close()

if __name__ == '__main__':
  main()
```

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-16-generate-and-evaluate-test-results)

## Etapa 16: gerar e avaliar os resultados de teste

Esta tarefa executa um script Python usando `pytest` para determinar se as declarações nos notebooks de teste passaram ou falharam.

1.  Adicione uma tarefa de **Script Python** ao pipeline de lançamento: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Script Python** na guia **Utilitário** e clique em **Adicionar**.
    
2.  Clique na tarefa **Executar um script Python** próxima ao **Trabalho do agente**.
    
3.  Com o **caminho do arquivo** selecionado, defina o **caminho do script** como `$(Release.PrimaryArtifactSourceAlias)/Databricks/cicd-scripts/evaluatenotebookruns.py`.
    
4.  Defina **Nome de exibição** como **Criar e avaliar resultados de teste do notebook**.
    
    ![Gerar resultados do teste do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/commandline-generate-test-results.png)
    
5.  Clique em **Salvar> OK**.
    

O script `evaluatenotebookruns.py` define a função `test_job_run`, que analisa e avalia o JSON gerado pela tarefa anterior. Outro teste, `test_performance`, procura testes que estão mais tempo em execução do que o esperado.

Para que o pipeline de lançamento execute esse script, adicione esse arquivo `cicd-scripts` à pasta `evaluatenotebookruns.py` na raiz do repositório Git, na qual você adicionou o arquivo `installWhlLibrary.py` e `executenotebook.py` anteriormente:

```
# evaluatenotebookruns.py
#!/usr/bin/python3
import io
import xmlrunner
from xmlrunner.extra.xunit_plugin import transform
import unittest
import json
import glob
import os

class TestJobOutput(unittest.TestCase):

  test_output_path = '<path-to-json-logs-on-release-agent>'

  def test_performance(self):
    path = self.test_output_path
    statuses = []

    for filename in glob.glob(os.path.join(path, '*.json')):
      print('Evaluating: ' + filename)
      data = json.load(open(filename))
      duration = data['execution_duration']
      if duration > 100000:
        status = 'FAILED'
      else:
        status = 'SUCCESS'

      statuses.append(status)

    self.assertFalse('FAILED' in statuses)

  def test_job_run(self):
    path = self.test_output_path
    statuses = []

    for filename in glob.glob(os.path.join(path, '*.json')):
      print('Evaluating: ' + filename)
      data = json.load(open(filename))
      status = data['state']['result_state']
      statuses.append(status)

    self.assertFalse('FAILED' in statuses)

if __name__ == '__main__':
  out = io.BytesIO()

  unittest.main(testRunner=xmlrunner.XMLTestRunner(output=out),
    failfast=False, buffer=False, catchbreak=False, exit=False)

  with open('TEST-report.xml', 'wb') as report:
    report.write(transform(out.getvalue()))
```

No script anterior, substitua `<path-to-json-logs-on-release-agent>` pelo caminho absoluto completo para a pasta `Databricks/logs/json/` no agente de build. Por exemplo, isso pode ser algo como `/home/vsts/work/r1/a/_<your-github-alias>.<your-github-repo-name>/Databricks/logs/json/`. Consulte a discussão anterior sobre `$(System.ArtifactsDirectory)` e `$(Release.PrimaryArtifactSourceAlias)` nas Etapas 9 e 11.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-17-publish-test-results)

## Etapa 17: publicar resultados de teste

Use a tarefa **Publicar resultados de teste** para arquivar os resultados JSON e publicar os resultados do teste em um hub de testes do Azure DevOps. Isso permite que você visualize relatórios e dashboards relacionados ao status das execuções de teste.

1.  Adicione uma tarefa **Publicar Resultados de Teste** ao pipeline de lançamento: clique no sinal de adição novamente na seção **Trabalho do agente**, selecione a tarefa **Publicar Resultados de Teste** na guia **Teste** e clique em **Adicionar**.
    
2.  Clique na tarefa \*\*Publicar Resultados de Teste **/TEST-\*.xml** próxima ao **Trabalho do agente**.
    
3.  Mantenha todas as configurações padrão inalteradas.
    
    ![Publicar resultados do teste do Azure DevOps](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_static/images/ci-cd/publish-test-results.png)
    
    Observação
    
    `$(System.DefaultWorkingDirectory)` representa o caminho local dele no agente em que os arquivos de código-fonte são baixados, por exemplo `/home/vsts/work/r1/a`. O pipeline de lançamento define esse valor como a variável de ambiente `SYSTEM_DEFAULTWORKINGDIRECTORY` na fase **Inicializar trabalho** para o agente de versão. Confira [Usar variáveis predefinidas](https://learn.microsoft.com/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml).
    
4.  Clique em **Salvar> OK**.
    

Você concluiu neste ponto um ciclo de integração e implantação usando o pipeline de CI/CD. Ao automatizar esse processo, você garante que seu código seja testado e implantado por meio de um processo eficiente, consistente e repetível.

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-18-run-the-build-and-release-pipelines)

## Etapa 18: executar os pipelines de lançamento e de build

Nesta etapa, você executará os pipelines de build e de lançamento manualmente. Para saber como configurar isso mais tarde para executar os pipelines automaticamente, consulte o comentário na Etapa 5 anterior.

Execute o pipeline de build:

1.  No menu **Pipelines** na barra lateral, clique em **Pipelines**.
2.  Clique no nome do pipeline e clique em **Executar pipeline**.
3.  Para **Branch/tag**, selecione o nome do branch no repositório Git que contém todo o código-fonte que você adicionou. Este exemplo considera que ele esteja no branch de **lançamento**.
4.  Clique em **Executar**. A página de execução do pipeline de build é exibida.
5.  Para exibir o progresso do pipeline de build e os logs relacionados, clique no ícone de rotação próximo ao **Trabalho**.

Execute o pipeline de lançamento:

1.  Depois que o pipeline de build for executado com êxito (há todos os ícones de marca de seleção na lista de detalhes do **trabalho**), no menu **Pipelines** na barra lateral, clique em **Lançamentos**.
2.  Clique no nome do pipeline de lançamento e clique em **Criar lançamento**.
3.  Clique em **Criar**.
4.  Para ver o progresso do pipeline de lançamento, clique no lançamento mais recente na guia **Lançamentos**.
5.  Clique na caixa **Estágio 1**.
6.  Clique em **Exibir logs**.

Exiba os resultados da execução de teste para os pipelines de build e de lançamento:

1.  No menu **Test Plans** na barra lateral, clique em **Execuções**.
2.  Na seção **Execuções de teste recentes**, na guia **Execuções de teste**, clique duas vezes nas entradas mais recentes do painel de log na lista.

___

## Conteúdo recomendado

-   [
    
    ### CI/CD com o Jenkins no Azure Databricks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/dev-tools/ci-cd/ci-cd-jenkins?source=recommendations)
    
    Saiba como usar Jenkins para habilitar a CI/CD para projetos do Azure Databricks.
    
-   [
    
    ### Configuração do Repos do Databricks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/repos/repos-setup?source=recommendations)
    
    Configure o Repos do Databricks para usar o Git para controle de versão. O Repos dá suporte a operações comuns do Git, como clonar, fazer check-out, confirmar, efetuar pull e push.
    
-   [
    
    ### Teste de unidade para notebooks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/notebooks/testing?source=recommendations)
    
    Saiba como aplicar técnicas e estruturas para funções de código de teste de unidade para os notebooks do Azure Databricks.
    
-   [
    
    ### Obter um token de acesso do Git e conectar um repositório remoto ao Azure Databricks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/repos/get-access-tokens-from-git-provider?source=recommendations)
    
    Saiba como obter um token de acesso do Git e conectar um repositório remoto ao Databricks Repos. Conecte-se a provedores Git como o GitHub, o Gitlab, o Bitbucket e o Azure DevOps.
    
-   [
    
    ### Usar CI/CD – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/dev-tools/index-ci-cd?source=recommendations)
    
    Saiba como usar sistemas de CI/CD (integração contínua e entrega contínua) com o Databricks.
    
-   [
    
    ### Integração do Git com Repos do Databricks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/repos/?source=recommendations)
    
    Saiba como usar o Git para controle de versão de seus notebooks e outros arquivos para desenvolvimento no Azure Databricks.
    
-   [
    
    ### Fluxos de trabalho de CI/CD com integração entre o Git e o Repos do Databricks – Azure Databricks
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/repos/ci-cd-best-practices-with-repos?source=recommendations)
    
    Conheça as melhores práticas para usar o Repos do Databricks em um fluxo de trabalho de CI/CD. A integração de repositórios Git com Repos do Databricks fornece controle do código-fonte para arquivos de projeto.
    
-   [
    
    ### Usar Databricks CLI do Azure Cloud Shell
    
    ](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/pt-br/azure/databricks/scenarios/databricks-cli-from-azure-cloud-shell?source=recommendations)
    
    Saiba como usar a CLI do Databricks do Azure Cloud Shell para executar operações no Azure Databricks.
    

___

## Recursos adicionais

## Recursos adicionais

-   [Visão geral de um pipeline típico de CI/CD do Azure Databricks](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#overview-of-a-typical-azure-databricks-cicd-pipeline)
-   [Desenvolver e confirmar seu código](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#develop-and-commit-your-code)
-   [Sobre o exemplo](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#about-the-example)
-   [Antes de começar](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#before-you-begin)
-   [Etapa 1: definir o pipeline de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-1-define-the-build-pipeline)
-   [Etapa 2: adicionar os arquivos de origem de teste de unidade ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-2-add-the-unit-test-source-files-to-the-repository)
-   [Etapa 3: adicionar o script de empacotamento da roda do Python ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-3-add-the-python-wheel-packaging-script-to-the-repository)
-   [Etapa 4: adicionar o notebook Python ao repositório](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-4-add-the-python-notebook-to-the-repository)
-   [Etapa 5: definir o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-5-define-the-release-pipeline)
-   [Etapa 6: definir variáveis de ambiente para o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-6-define-environment-variables-for-the-release-pipeline)
-   [Etapa 7: configurar o agente de versão para o pipeline de lançamento](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-7-configure-the-release-agent-for-the-release-pipeline)
-   [Etapa 8: definir a versão do Python para o agente de versão](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-8-set-the-python-version-for-the-release-agent)
-   [Etapa 9: desempacotar o artefato de build do pipeline de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-9-unpackage-the-build-artifact-from-the-build-pipeline)
-   [Etapa 10. Instalar a CLI do Databricks e o relatórios XML unittest](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-10-install-the-databricks-cli-and-unittest-xml-reporting)
-   [Etapa 11: implantar o notebook no workspace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-11-deploy-the-notebook-to-the-workspace)
-   [Etapa 12: implantar a biblioteca no DBFS](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-12-deploy-the-library-to-dbfs)
-   [Etapa 13: instalar a biblioteca no cluster](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-13-install-the-library-on-the-cluster)
-   [Etapa 14: executar testes de integração no notebook Python](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-14-run-integration-tests-on-the-python-notebook)
-   [Etapa 15: executar o notebook](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-15-run-the-notebook)
-   [Etapa 16: gerar e avaliar os resultados de teste](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-16-generate-and-evaluate-test-results)
-   [Etapa 17: publicar resultados de teste](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-17-publish-test-results)
-   [Etapa 18: executar os pipelines de lançamento e de build](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#step-18-run-the-build-and-release-pipelines)
