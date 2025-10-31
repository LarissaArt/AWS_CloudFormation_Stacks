# AWS_CloudFormation_Stacks

<h1 align="center">☁️ AWS CloudFormation — Desafio DIO Santander Code Girls ☁️</h1>

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/5/5c/AWS_CloudFormation_Logo.svg" alt="AWS CloudFormation" width="200"/>
</p>

<p align="center">
  Repositório criado para o desafio prático do Bootcamp <strong>Santander Code Girls</strong> na plataforma <strong>DIO</strong>, com foco no uso do AWS CloudFormation para criar e gerenciar recursos de forma automatizada na nuvem ☁️.
</p>

---

## 📘 Sobre o Projeto

Este projeto demonstra como criar uma **Stack na AWS** usando o **CloudFormation**, incluindo a configuração de uma **instância EC2** e de um **grupo de segurança (Firewall)**.  
O objetivo é entender o processo de provisionamento automatizado de infraestrutura como código (**IaC – Infrastructure as Code**).

---

## 🧩 O que é o AWS CloudFormation?

O **AWS CloudFormation** é um serviço que permite **criar, configurar e gerenciar recursos da AWS automaticamente** através de **modelos (templates)** escritos em **YAML ou JSON**.

💡 Em vez de criar recursos manualmente, você descreve tudo em um arquivo — e o CloudFormation faz o resto por você.  

---

## ⚙️ Estrutura do Template

Um template CloudFormation geralmente é dividido em seções como:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Configuração de instância EC2 com grupo de segurança (Firewall)

Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0ed9277fb7eb570c9
      InstanceType: t2.micro
      Tags:
        - Key: Name
          Value: Webserver-Firewall
      UserData:
        Fn::Base64: |
          #!/bin/bash -xe
          yum install -y httpd.x86_64
          systemctl start httpd.service
          systemctl enable httpd.service
          echo "<h1>OLÁ AWS FOUNDATIONS do $(hostname -f)</h1>" > /var/www/html/index.html
      SecurityGroups:
        - Ref: GrupoSeguranca

  GrupoSeguranca:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Permitir acesso HTTP
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
```
---
🧱 O que é uma Stack?

Uma Stack é o conjunto de recursos AWS (como EC2, S3, VPC etc.) que o CloudFormation cria e gerencia a partir de um template.

➡️ Em resumo:  
O template é o plano da casa 🏗️  
A stack é a casa construída 🏠

---

🚀 Como Criar uma Stack no AWS CloudFormation

Acesse o Console da AWS

Vá em CloudFormation → Create stack → With new resources (standard)  

Escolha Upload a template file e envie o seu arquivo .yaml  

Clique em Next e dê um nome à sua stack  

Continue com as opções padrão e finalize clicando em Create stack  

Aguarde a criação ser concluída (status: CREATE_COMPLETE)  

---

🔥 Configurando o Firewall (Grupo de Segurança)

No template acima, criamos um Security Group chamado GrupoSeguranca.    
Ele funciona como um firewall, permitindo que apenas o tráfego HTTP (porta 80) seja aceito.    

#### 🟢 YAML (para CloudFormation, pipelines, etc.)  
```yaml
SecurityGroupIngress:
  - IpProtocol: tcp
    FromPort: 80
    ToPort: 80
    CidrIp: 0.0.0.0/0
```

💡 Isso significa que qualquer pessoa pode acessar o site que você hospedar na sua instância EC2.  

---

🖥️ Testando a Instância    

Após a stack ser criada:  

1- Vá até o serviço EC2    

2- Copie o Endereço IPv4 público da instância   

3- Cole o IP no navegador  

4- Você verá a mensagem:  

`OLÁ AWS FOUNDATIONS do (nome-da-instância)`  



🎉 Pronto! Sua instância EC2 e seu firewall foram configurados com sucesso via CloudFormation!  
---

🏁 Conclusão  

Com o AWS CloudFormation, é possível criar e gerenciar infraestrutura de forma automatizada, padronizada e repetível.  
Isso economiza tempo, reduz erros e facilita o controle de versões — essencial para quem trabalha com DevOps e Infraestrutura como Código (IaC).

🧠 Tecnologias utilizadas  

🟠 AWS CloudFormation  

🟡 Amazon EC2  

🟢 YAML  

🔵 Firewall (Security Group)   

---

✨ Créditos  

Desafio prático desenvolvido por Larissa Silva para o Bootcamp Santander Code Girls (DIO) 💻  
Instrutor: Especialista Alexsandro Lechner em AWS Foundations  


---
