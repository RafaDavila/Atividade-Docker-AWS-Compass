# Atividade-Docker-AWS-Compass
Segundo projeto do Estágio de AWS e DevOps da Compass

# **Sobre a atividade**
1.Instalação e configuração do DOCKER ou CONTAINERD no host EC2.

• Ponto adicional para o trabalho que utilizar a instalação via script de Start Instance (user_data.sh)

2.Efetuar Deploy de uma aplicação Wordpress com:

• Container de aplicação

• RDS database MySQL

3.Configuração da utilização do serviço EFS AWS para estáticos do container de aplicação WordPress

4.Configuração do serviço de Load Balancer AWS para a aplicação Wordpress

# **Passo a passo**:

## **Criando a VPC:**
• Vá ate o painel VPC na ``AWS``

• Clique em "Criar VPC" depois em "VPC e muito mais"
![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/eb04214e-8515-4d37-8054-10bab45471c7)

• Após criar a VPC ainda no menu vá até ``Gateways NAT``.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/add8a64b-c4ac-442f-80f8-73e129aa93d2)

• Clique em Criar ``gateway NAT ``.

• Escolha uma das sub-redes públicas.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/6bee2087-638a-443b-8ddd-7a20a6fbcba7)

• Após criar o NAT gateway, acesse ``Tabelas de rotas`` no menu da esquerda.

• Na Tabela de rotas selecione as rotas privadas, clique em Ações e selecione Editar rotas.

• Em Editar rotas em destino selecione 0.0.0/0

• Em Alvo selecione Gateway NAT e selecione o NAT gateway criado anteriormente.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/2dab5805-b5d6-4d97-be4a-0fb7001b2aab)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/73d6768a-0633-4f11-9425-b3d07ac18edd)




