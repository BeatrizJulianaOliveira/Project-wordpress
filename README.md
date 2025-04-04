# 🚀 Configuração de Servidor Wordpress com Docker na AWS

## 🛠 Tecnologias utilizadas
- **GitHub**
- **Amazon Web Services (AWS)**
- **Visual Studio Code**
- **Docker**

> **Observação:** É essencial utilizar o **GitHub** para a elaboração e versionamento deste projeto.

---

## 🎯 Objetivo

Este projeto tem como objetivo configurar um servidor **WordPress** utilizando **Docker** dentro de uma instância EC2 na **AWS**. O ambiente será integrado com diversos serviços da AWS, como:

- **Amazon EFS** (armazenamento de arquivos)
- **Amazon RDS** (banco de dados)
- **ALB** (Application Load Balancer - balanceamento de carga)
- **ASG** (Auto Scaling Group - escalabilidade automática)

---

## 📌 Passo a passo

### 1️⃣ Criar uma **VPC** na AWS

![vpc passo 1](images/vpc%20passo%201.png)


---

### 2️⃣ Configurar **sub-redes públicas**  
- Habilitar a opção para que as sub-redes recebam **endereços IP públicos automaticamente**

![subrede pub](images/subrede%20pub.png)
![subrede pub 1](images/subrede%20pub%201.png)
![subrede pub 2](images/subrede%20pub%202.png)

> **Agora repita o mesmo processo com a sub-rede publica da zona B.**
![subrede pub](images/sub%20b.png)

---

### 3️⃣ Em security group, crie o **Security Group** para o servidor web  
*(Não adicione regras de entrada/saída neste momento)*

### 4️⃣ Criar o **Security Group** para o banco de dados (RDS - MySQL)

![sg rds](images/sg%20rds.png)
![sg rds 1](images/sg%20rds%201.png)

---

### 5️⃣ Criar o **Security Group** para o EFS

![sg efs](images/sg%20efs.png)
![sg efs 1](images/sg%20efs%201.png)

---

### 6️⃣ Criar o **Security Group** para o ALB (Application Load Balancer)

![alb](images/alb.png)
![alb 1](images/alb%201.png)

---

### 7️⃣ Editar o **Security Group** do WebServer  
- Adicione as **regras de entrada** e **saída** conforme necessidade da aplicação WordPress

![web sg](images/web%20sg.png)
![web sg 1](images/web%20sg%201.png)

---

### 8️⃣ Criar o **EFS**

- Navegue pelas abas e selecione o **Security Group** criado anteriormente

📸 *[inserir imagem]*
#### Aperte para ir para próxima aba

#### Selecionar o grupo de segurança do EFS criado anteriormente
### Criar o RDS.
Escolher a ultima versão disponível
Escolher o nivel gratuito
Guardar essas informações:
Mudar para t3 micro:
Alterar o limite maximo de armazenamento escalonavel:
Verificar se está na VPC correta:
Selecionar o grupo de segurança do RDS
Antes de finalizar a criação RDS, definir um nome pro banco de dados inicial e guardar essa informação
Pegar e armazenar o endereço do banco de dados && o ponto de montagem EFS.
RDS
EFS
Alterar esse userdata && o docker-compose.yml para que contenha suas informações
Criar um Modelo de Execução (Lauch Template)
Escolher o linux aws (o userdata que criei só funciona nele)
Não escolha uma sub-rede especifica e escolha o grupo de segurança criado para os servidores web
Colocar as Tags que a patricia passou nas tags de recurso, nos detalhes avançados colocar o arquivo no user-data (observação: terá que trocar o ponto de montagem pelo que está no seu EFS)
Clique em criar um loadbalancer
Selecione o ALB
Coloque um nome nele e escolha as subnets que serão responsaveis pelo servidor web

### 9.Criar o ASG com o ALB 
Colocar um nome && ecolher o launch template que criamos anteriormente
Escolher as subnetes publicas de zonas diferentes para o LT
