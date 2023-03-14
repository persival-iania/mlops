#Definição
Trata-se de uma replicação de banco de dados relacional. Estão envolvidos 2 tipos de banco: Oracle e SQL Server, sendo o Oracle o principal deles. Existem algumas formas de realizar a replicação, a mais comumente utilizada é por CDC (Change Data Capture). No caso do Oracle existem alguns vendors, um deles é o Goldengate. A CCR possui muitas licenças de Goldengate For Oracle que atende bem a demanda. Embora também dê suporte a SQL Server, recomenda-se uso de ferramentas nativas, tais como: Mirror, Replication transacional, ou CDC MS SQL. Recomenda-se seu uso  para leitura, seja por usuários ou sistemas com CRQS, desonerando base original e agilizando novos acessos para processo Batch. Nessa documentação, iniciaremos com o Oracle, sendo incluído posteriormente SQL Server.  

#Arquitetura Oracle Recomendada:
* Conguração do Servidor mínima(Para Single):
  * Memória: Recomenda-se 64Gb de RAM (MMA ou SGA+PGA)
  * CPU: 32vCPU
  * Disco: 10Tb e formatado para RAID10 ou RAID 6 como segunda opção;
* Configuração para Oracle:	
  * RAC ou Single: Single pode ser uma boa opção por ser mais simples de implementar mas RAC é bem vindo.
  * CDB ou noCDB: Recomenda-se o uso de arquitetura CDB para divisão lógica de bases para cada concessão
  * Necessário DG? Como já é uma réplica por replicação consolidada, não recomenda-se montar um Data Guard para isso.

<IMG  src="https://www.oracle.com/technetwork/articles/servers-storage-admin/f1-2016882.gif"  alt="Oracle Multitenant Database Architecture - ScriptDBA.com"/>

#Estratégia GG
Loading
Data from File to Replicat
Conforme já supracitado, esse é o método recomendado para a carga. Será uma carga inicial utilizando o Extract que converte SQL em Trail file em um diretório local do Linux(Ex.: /u03/ogg/data/trailfile/). Após extração arquivo será replicado para tabela destino de pdb correspondente (Origem:Concessão transacao -> Destino:PDB:transacao). 

![image.png](/.attachments/image-9447c2f9-11f8-4f30-ab35-ee4fc92aee35.png)

A seguir desenho completo:

![Arquitetura_All-V1-Intermediate Layer 2.1.jpg](/.attachments/Arquitetura_All-V1-Intermediate%20Layer%202.1-29321f53-efac-400b-9930-c102a4e030c7.jpg)