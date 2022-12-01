![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-cd159af2-27e0-42a2-8c75-c85a20987ae8.png)

#Introdução

- Acesso
- Network Group
- AVD !?
- VPN Dedicada
- Gerenciamento de senhas
- Processo de disponibilização de senhas para o ADF e ADB

## Acesso

Os acessos estão sendo feitos considerando a conexão privada, entre VPN CCR e Ambiente Azure.

## Gerenciamento de senhas
As senhas serão armazenadas nos Key Vaults, bem como as chaves das SPAs e suas chaves. 
Exemplo:
![image.png](/.attachments/image-df1ef360-28f3-4b3e-9ac6-e9db0133f3b0.png)

O Key Vault está planejato para ser usado de 1 para 1, ou seja, um cofre uma chave. 

## AVD

Com objetivo de reduzir os riscos relacionados a "vazamento de dado", criaremos uma estação de trabalho com acesso exclusivo ao dado denominada AVD. A ideia é que a conexão seja limitada em rede privada e ao uso dessa estação para os recursos de dados abertos, aderente a LGPD.

# VPN Dedica

As conexões entre os sites, localizados os Oracles Database, serão realizadas via VPN própria e Vnet da Azure. 


## Processo de disponibilização de senhas para o ADF e ADB
As senhas do ADF e ADB serão feitos por Key Vault, não exposta no código. No caso do ADB, uso de Scope.

## ...Desculpe os transtornos, estamos em construção.

![construcao-002.png](/.attachments/construcao-002-49935089-a52d-4bee-9e1b-ecd4a117b108.png)
