[Conceitos de Acesso](#conceitos)
[Definição e Implantaçaõ do Gibraltar](#definições-no-gibraltar)

# Conceitos
- O que é o RBAC do Azure (controle de acesso baseado em função do Azure)?
O gerenciamento de acesso para recursos de nuvem é uma função crítica para qualquer organização que esteja usando a nuvem. O RBAC do Azure (controle de acesso baseado em funções do Azure) ajuda a gerenciar quem tem acesso aos recursos do Azure, o que pode fazer com esses recursos e a quais áreas tem acesso.

O RBAC do Azure é um sistema de autorização baseado no Azure Resource Manager que fornece gerenciamento de acesso refinado dos recursos do Azure.

- O que posso fazer com o RBAC do Azure?
Aqui estão alguns exemplos do que você pode fazer com o RBAC do Azure:

Permitir que um usuário gerencie máquinas virtuais em uma assinatura e outro usuário gerencie redes virtuais
Permitir que um grupo de DBA gerencie bancos de dados SQL em uma assinatura
Permitir que um usuário gerencie todos os recursos em um grupo de recursos, como máquinas virtuais, sites e sub-redes
Permitir que um aplicativo acesse todos os recursos em um grupo de recursos

- Como o RBAC do Azure funciona
A maneira de controlar o acesso aos recursos usando o RBAC do Azure é atribuir funções do Azure. Esse é um conceito fundamental que deve ser entendido: como as permissões são aplicadas. Uma atribuição de função consiste em três elementos: entidade de segurança, definição de função e escopo.

- Entidade de segurança
Uma entidade de segurança é um objeto que representa um usuário, grupo, entidade de serviço ou uma identidade gerenciada que está solicitando acesso aos recursos do Azure. Você pode atribuir uma função a qualquer uma dessas entidades de segurança.

- Definição de função
Uma definição de função é um conjunto de permissões. Normalmente ela é chamada apenas de função. Uma definição de função lista as ações que podem ser executadas, como leitura, gravação e exclusão. Funções podem ser de alto nível, como proprietário, ou específicas, como leitor de máquina virtual.

- Escopo
Escopo é o conjunto de recursos ao qual o acesso se aplica. Quando você atribui uma função, você pode limitar ainda mais as ações permitidas definindo um escopo. Isso será útil se você quiser tornar alguém um colaborador do site, mas apenas para um grupo de recursos.

No Azure, você pode especificar um escopo em quatro níveis: grupo de gerenciamento, assinatura, grupo de recursos ou recurso. Os escopos são estruturados em uma relação pai-filho. Você pode atribuir funções em qualquer um desses níveis de escopo.

![Items.png](/.attachments/Items-af623b6f-35d2-4cd3-b8d0-f907ed03b08c.png)

- Atribuições de função
Uma atribuição de função é o processo de associar uma definição de função a um usuário, grupo, entidade de serviço ou identidade gerenciada em um escopo específico com a finalidade de conceder acesso. O acesso é concedido criando uma atribuição de função, e é revogado removendo uma atribuição de função.

O diagrama a seguir mostra um exemplo de uma atribuição de função. Neste exemplo, o grupo de Marketing foi atribuído à função Colaborador para o grupo de recursos vendas farmacêuticas. Isso significa que os usuários do grupo de Marketing podem criar ou gerenciar qualquer recurso do Azure no grupo de recursos de vendas do setor farmacêutico. Os usuários de Marketing não possuem acesso a recursos fora do grupo de recursos de vendas do setor farmacêutico, a menos que sejam parte de outra atribuição de função.
![Items (1).png](/.attachments/Items%20(1)-c105c1a2-666d-4479-a687-d87244e64c16.png)

- Grupos
As atribuições de função são transitivas para grupos, o que significa que, se um usuário for membro de um grupo e esse grupo for membro de outro grupo que tenha uma atribuição de função, o usuário terá as permissões na atribuição de função.

- ACL

# CCR - DATAPLAT
Os acessos foram definidos com base no uso de RBAC, ACL e Grants. Nos recursos como: Databricks, Data Factory e Purview foi utilizado o RBAC. No Datalake(Storage Account Gen2), por ACL devido a necessidade de um acesso mais granular, por lista e objeto. No caso do Synapse, os acessos foram concedidos por grants, similar ao SQL Server. A seguir imagem e anexos dos arquivos:

A seguir imagem e documento em anexo com o controle de acesso:
![image.png](/.attachments/image-d94627e4-6314-45c9-8de6-462436802a02.png)
[CCR_Acessos_Preenchidov2.xlsx](/.attachments/CCR_Acessos_Preenchidov2-9e1cb4f8-6fe6-4098-8efa-529d7483c467.xlsx)

A seguir um desenho para facilitar entendimento em relação dos acesso RBAC x ACL x Grant.

Figura de acesso RBAC x ACL x Grant
![Arquitetura_All-V1-Acessos-RBAC&ACL.jpg](/.attachments/Arquitetura_All-V1-Acessos-RBAC&ACL-d4297b46-d732-4444-9436-fedfa785d6b2.jpg)

Com intuito de facilitar o entendimento, um diagrama foi criado com a relação dos acessos e grupos:
![Arquitetura_All-V3-IAM.png](/.attachments/Arquitetura_All-V3-IAM-5e961900-8cbe-430d-afda-a5a477c912d7.png)
