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

## **Criando os Security Group:**

• No menu EC2 procure por ``Security groups`` na barra de navegação à esquerda.

• Acesse e clique em ``Criar novo grupo de segurança``, o meu ficou assim:

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/387ebf56-6d56-43d1-84e2-d72e26a961a9)

## **Criando o EFS:**

• Busque por ``EFS``
• Na Página de EFS clique em ``Criar sistema de arquivos``.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/18fd24f8-8925-43c8-8568-91fa8071b1d6)

• Clique em ``Personalizar`` e coloque o SG do EFS criado posteriormente.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/f1311382-1e4f-4584-a438-fd23c086268b)

## **Criando o RDS:**

• Vá até ``RDS`` na AWS e em ``Criar Banco de Dados``.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/d76c6ed1-3f0c-4cbd-bf46-2abaf9983602)

• Escolha ``MySQL``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/87158273-c072-45f4-81c3-e24119c8a13e)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/97713137-6ae4-4899-8546-0f97ac33fb40)

• Escolha o nome do usuário e senha.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/02a47261-897b-4393-beea-d415e0ddd460)

• Escolha a VPC criada anteriormente.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/32c3b55f-2487-4609-8a0c-097cc903a653)

• Permita o acesso público e coloque o SG criado anteriormente.


![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/4d1c4830-0212-401d-a5a5-a0992dc5fa39)

## **Criando o modelo de execução:**

• Vá ate o painel ``EC2`` e no menu esquerdo escolha ``Modelos de Execução`` 

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/3ae9a5e5-1c24-490d-9c43-d5c00ccfc13d)

• Em detalhes avançado, desca até ``Dados do Usuário`` e coloque o conteudo do arquivo StartScript.sh contido neste repositório.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/272f2d52-1974-4254-874f-75518ae746d2)

## **Criando o Grupo de Destino:**

• No menu esquerdo, escolha ``Grupos de Destino`` e crie um novo.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/da280d98-13fa-4c2a-889e-f7a4bf7be8f8)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/4da84efc-c25f-495a-bf4b-4fd668d5d47d)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/57e94a39-671a-4b56-a831-62096ad3d9d6)

• Escolha a VPC criada anteriormente

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/9d18fc69-8610-453d-8e7b-3985fbb0303f)

## **Criando o Load Balancer:**

• Ainda no menu esquerdo EC2, busque por ``Load Balancer`` e crie um novo

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/c2b983f2-81d6-4162-b5bd-f61e4e3f5e9d)

• Escolha Apllication Load Balancer

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/067cfcd8-fc8d-4f19-a1f3-3b6dd536150f)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/b82e10bb-162d-48af-b280-9ab880a0dec3)

• Selecione a VPC criada anteriormente e o grupo de segurança ALB

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/0912f370-3d1f-482d-8af7-21716af0a19b)

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/27130c3a-b421-408c-bf02-9ae68ab8da06)

• Selecione o grupo de destino criado anteriormente

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/46f58cc7-7222-4d3c-8105-8549d97880c0)

























