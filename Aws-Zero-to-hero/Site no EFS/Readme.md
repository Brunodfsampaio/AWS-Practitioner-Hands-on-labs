### Neste lab, ao invés de usarmos o EBS da instância para armazenar os dados do site estático, vamos usar o EFS. Dessa forma, as instâncias EC2 serão servidores stateless, pois o site será rodado no EFS e não dentro da instância.
---

## ✅ 1º Passo – Criar o EFS

- Ao criar o EFS, cliquei em **Personalizar**:
  
  ![image](https://github.com/user-attachments/assets/4e259a71-5441-48c1-9d32-fcb12773c789)
  ![image](https://github.com/user-attachments/assets/cc472cbb-2b8b-43a2-87ee-891f55dc1682)

- Não configurei nenhuma política de gerenciamento de ciclo de vida dos dados:

  ![image](https://github.com/user-attachments/assets/084a67b8-834a-487a-8286-63175d56cf61)
- (US)
  ![image](https://github.com/user-attachments/assets/d98e3aba-3ac5-4158-a85b-fa302be3354e)
  ![image](https://github.com/user-attachments/assets/eefcb228-285e-491d-b4b7-31b5d9a3866e)  

- next
  ![image](https://github.com/user-attachments/assets/b67980b9-daf8-4e51-9f4c-3b8aaf7f0e5c)
- políticas de segurança do efs (+IAM):
  ![image](https://github.com/user-attachments/assets/b9310dd9-3c4c-4011-adea-fb05ab3827d0)
- depois só ir em 'create'
  ![image](https://github.com/user-attachments/assets/3db28d5c-e297-4e13-ad01-3702b57c0ea4)
  ![image](https://github.com/user-attachments/assets/9514fd9f-2a03-47bb-bd8f-827e4ee85990)
  ![image](https://github.com/user-attachments/assets/2fbf597f-6de4-4ee8-8350-800b96cf7f2a)

## 1.1º passo
- selecionar a opção do lado direito superior "ATTACH"
  ![image](https://github.com/user-attachments/assets/78d68089-7fc4-4c68-9ec5-adfa2a626f29)
- são fornecidos os comandos que serão usados mais na frente para montar na instância linunx...

## 2º Passo
- criar uma instância ec2 linux, com acesso para porta 80 e porta 22. (vpc,subnet, ip automático, sg....)

## 3º Passo
- conectar na instância na própria console. (ec2-user);
- logar via root sudo su - ;
- realizar atualização via 'yum update -y";
- depois instalar o apache "yum install httpd -y ;
- em seguida dar o 'service httpd start' > chkconfig httpd on

## 4º Passo
- instalar pacote efs utils > yum install amazon-efs-utils -y
- após, verificado os discos da instância via 'df -h', temos:
  ![image](https://github.com/user-attachments/assets/584fa7e8-1396-484b-8c2a-0c3b9410ffa8)
  ![image](https://github.com/user-attachments/assets/3246d03d-952d-434c-b610-0de584a97089)
- comando: sudo mount -t efs -o tls fs-(número do efs):/ /var/www/html (montar dentro do apache)
- porém, surgiur um erro!!!!!!!
  ![image](https://github.com/user-attachments/assets/f571c666-c14e-4b87-aec4-061374253d95)

- o SG do efs está como padrão!
- para corrigir é só clicar em 'manage' e editar o SG e depois......... ir no SG e adicionar a regra para NFS, porta 2049 com a:
  ![image](https://github.com/user-attachments/assets/2f551d94-4e0d-4a3b-bc9b-6e1cf1430293)
- após liberar a porta 2049...ele vai aceitar o comando sudo mount...
  ![image](https://github.com/user-attachments/assets/5d9029e9-1251-4986-819d-c4b70f6842b0)
- realizando df -h novamente...
  ![image](https://github.com/user-attachments/assets/12996eb9-6a91-47c0-971d-9b7030ce204f)
- existe um armazednamento 8.0E !

## 5º Passo
- acessar o efs e criar o arquivo index.html 
  ![image](https://github.com/user-attachments/assets/d102a8ef-69ce-4f4e-9ef2-dc33d77a3ce2)

- após isso, vamos desmontar o efs da instância, retornar no diretório /var/www/html e notar que o arquivo já não está lá! (é o esperado, pois ele foi feito no efs...)
![image](https://github.com/user-attachments/assets/9efb1e58-a80f-4f99-ba4e-e8ddf08e10f3)
- após umount:
![image](https://github.com/user-attachments/assets/57e86a90-9934-4365-a390-3a4b80694cbc)
- com mount:
![image](https://github.com/user-attachments/assets/6fc55035-4d69-4e64-931b-83b0a95c5c2e)
- comandos:
![image](https://github.com/user-attachments/assets/7b8bf79e-8758-41ea-a0cf-24daa6bc4309)

## 6º apagar a instância atual e depois criar uma nova instância com 'bootstrap' automatizado.
![image](https://github.com/user-attachments/assets/74815c31-3726-4463-90a8-6d94044ce31f)
- comandos do bootstrap:
![image](https://github.com/user-attachments/assets/39f4c1f5-194d-447a-8ecb-33d8747ec3f8)

- Após a instância nova criada, é só copiar o ip e colar...ela já vai entrar diretamente ao site.
![image](https://github.com/user-attachments/assets/fa01e14c-a1a2-4fdf-a6de-97758ec2e029)
- enviando um df -h :
![image](https://github.com/user-attachments/assets/5dfbcee7-6856-4748-8f53-301b6f35112c)
- dando umount /var/www/html/
![image](https://github.com/user-attachments/assets/16725298-170f-4778-abc8-585634920c36)


## Limpando tudo:
- apagar instância
- apagar vpc
- apagar efs -> botão delete
- ![image](https://github.com/user-attachments/assets/1459ad0b-141b-48fd-bbe3-97fa393e8ed8)
- ![image](https://github.com/user-attachments/assets/a1bd7e9a-e180-4b4a-843c-ab1804e40ba6)


- **tenha certeza de que apagou tudo ;)**

----
> stay focused!
