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

Em Resources to create selecionei VPC and more.

Em Name tag auto-generation coloquei o nome "docker-vpc".

Em Number of Availability Zones (AZs) selecionei 2.

Em NAT gateways selecionei In 1 AZ.

Em VPC endpoints selecionei None.

Cliquei em Create VPC.


![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/73d6768a-0633-4f11-9425-b3d07ac18edd)

## **Criando os Security Group:**

• No menu EC2 procure por ``Security groups`` na barra de navegação à esquerda.

• Acesse e clique em ``Criar novo grupo de segurança``, o meu ficou assim:

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/f4bab2b7-fb90-46a3-b7b3-675e34f6fbc5)


## **Criando o EFS:**

• Busque por ``EFS``
• Na Página de EFS clique em ``Criar sistema de arquivos``.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/18fd24f8-8925-43c8-8568-91fa8071b1d6)

No campo Virtual Private Cloud (VPC) selecionei a VPC que foi criada anteriormente.

No campo Subnet ID selecionei as subnets privadas de cada AZ.

No campo Security groups selecionei o grupo "EFS" que foi criado anteriormente.

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

Dentro de Load Balancers cliquei no botão Create load balancer.

Em Load balancer types cliquei em Classic Load Balancer e depois em Create.

No campo Load balancer name digitei "ws-clb".

Na seção Network mapping, no campo VPC selecionei a VPC criada anteriormente.

No campo Mappings selecionei as duas AZ's e suas respectivas subnets públicas.

No campo de Security groups selecionei o grupo "Load Balancer" que foi criado anteriormente.

Na seção Health checks, no campo Ping path adicionei o caminho "/wp-admin/install.php".

Cliquei em Create load balancer para finalizar.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/b82e10bb-162d-48af-b280-9ab880a0dec3)


## **Criando o Auto Scaling:**

• No menu a esquerda, vá até ``Grupos de Auto Scaling``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/88043420-1b32-4946-af11-8cdd4a6770fb)

Acessei o console AWS e entrei no serviço EC2.

No menu lateral esquerdo, na seção de Auto Scaling selecionei Auto Scaling Groups.

Dentro de Auto Scaling groups cliquei no botão Create Auto Scaling group.

Executei a seguinte configuração:

•  - Choose launch template:
Na seção Launch template selecionei o template criado anteriormente.

•  - Choose instance launch options:
Na seção Network, no campo VPC selecionei a VPC criada anteriormente.
No campo Availability Zones and subnets selecionei as duas subnets privadas criadas previamente.

•  - Configure advanced options:
Na seção Load balancing selecionei Attach to an existing load balancer.
Na seção Attach to an existing load balancer cliquei em Choose from Classic Load Balancers e selecionei o load balancer criado anteriormente.
Na seção Health checks marquei a opção Turn on Elastic Load Balancing health checks.

•  - Configure group size and scaling:
No campo Desired capacity digitei "2".
Em Scaling, no campo Min desired capacity digitei "2".
No campo Max desired capacity digitei "4".
Em Automatic scaling selecionei a opção Target tracking scaling policy
No campo Metric type deixei selecionado Average CPU utilization.
No campo Target value digitei "75".


## **Endpoint**

• Vá até Endpoint e clique em ``Criar Endpoint``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/0d8745c7-1a96-443f-b24e-19a5caebd7e1)

• Dentro de Endpoints cliquei no botão Create endpoint.

• Faça as alterações:

Em Service category selecionei EC2 Instance Connect Endpoint.

Em VPC selecionei a VPC criada anteriormente.

Em Security groups selecionei o grupo "EC2 ICE" que foi criado anteriormente.

Em Subnet selecionei uma subnet privada que foi criada anteriormente.


## **WorldPress**

• Vá em ``Load Balancer``

• Clique no que foi criado

• Copie o ``Nome do DNS``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/87c4e4e8-e083-4723-98ae-bd2c7e385e1f)

• Abra no navegador

• Faça a configuração inicial, idioma, e login

• Terá essa página:

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/f150c24c-6677-4b8c-9fa1-60306b3c4eee)


## **Teste os Serviços:**

• Acessando a instância via endpoint.

• Testando a montagem do EFS:

Comando ``df -h`` para verificar se o EFS está montado.

Comando ``cat /etc/fstab`` para verificar se a montagem persistente está configurada.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/b47cac4b-841f-445d-93fe-8c765f946ee5)



• Testando o docker e docker-compose:

Comando ``docker ps`` para verificar se o container wordpress está executando.

Comando abaixo para verificar se o docker-compose está funcionando: ``docker-compose -f /efs/docker-compose.yaml ps``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/6fe6d101-6df9-4185-af59-eb99278dce4c)


• Acessando o banco de dados da aplicação WordPress:

Copie o ID do container WordPress
Acesse o container com ``docker exec -it <container-id> /bin/bash``

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/85cf0faa-bb4c-4ddd-897a-12258bfd6126)

Dentro do container, use ``apt-get update`` para atualizar a lista de pacotes dos repositórios do container.

![image](https://github.com/RafaDavila/Atividade-Docker-AWS-Compass/assets/113639519/b686e79a-73ca-469e-a207-d35bd636af9a)


Para instalar o MySql use ``apt-get install default-mysql-client -y``

Para acessar o MySQL executei o comando abaixo passando o endpoint, porta e usuário do RDS: ``mysql -h <RDS-endpoint> -P 3306 -u <Master username> -p``

Digite a senha

Comando show databases; para listar os bancos de dados disponíveis.
Comando use dockerdb para selecionar o banco de dados dockerdb.
Comando show tables; para listar todas as tabelas criadas dentro do banco de dados dockerdb.































