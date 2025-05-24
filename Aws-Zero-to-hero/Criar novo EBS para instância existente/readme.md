### Aqui eu vou usar a instância linux para criar novos discos ebs, pois no caso da instância windows server, só 1 já vai consumir o máximo de EBS free tier (30gb). Para nao ocorrer custos, não vou conseguir demonstrar a criação e formatação de novos discos ebs na instância windows...
---

### A instância Linux já está criada de laboratórios passados.
1. Verificar o ebs existente com a instância linux
   ![image](https://github.com/user-attachments/assets/5ce2de0a-471b-4d73-ab9e-fcdee7f81300)

2. Criar um novo disco EBS para a instância:
   ![image](https://github.com/user-attachments/assets/872d4256-c6e8-49c6-9e38-09ee6b873c0e)
   ![image](https://github.com/user-attachments/assets/bd5834a5-164c-4ec6-bd02-d02d243cbf9f)
   ![image](https://github.com/user-attachments/assets/c107520e-efdc-49fb-aea1-727d0f2e238c)
   ![image](https://github.com/user-attachments/assets/5c32c81b-661d-4a79-aea6-24f4dbbcb6fb)

3. Associar o EBS criado à instância:
  ![image](https://github.com/user-attachments/assets/7b34153a-0eda-4308-b62a-20d2eddce1fd)
  ![image](https://github.com/user-attachments/assets/418b3139-faa9-4976-a20d-64306a891b0b)
  ![image](https://github.com/user-attachments/assets/55e5c8e9-b208-4f88-b480-019edfc61751)

3.1 Anexar via CLI
  a) Listando os discos: "df -h"
  ![image](https://github.com/user-attachments/assets/71b1125f-562e-48cb-9508-05c66262d461)
  b) listando discos nao formatados "lsblk"
  ![image](https://github.com/user-attachments/assets/5d108a7b-ac7b-4f26-9716-fe00678d3c43)
  
3.2 Formatando o disco
  a) comando "mkfs -t ext4 /dev/xvdc/  (USAR SUDO)
  ![image](https://github.com/user-attachments/assets/3147ff2b-9e74-4b04-8041-48ea9d1a2bb1)

3.3) Criar a partição
  a) comando: mkdir /mnt/ebsdisk (usar sudo)
  ![image](https://github.com/user-attachments/assets/6c65a500-39b0-4b52-ae60-dedd8512ab1e)
  b) comando: mount /dev/xvdc /mnt/ebsdisk/
  ![image](https://github.com/user-attachments/assets/1372f374-99d0-4171-9514-f9f308a92218)
  ![image](https://github.com/user-attachments/assets/e955db8b-d4c1-49cf-b5ce-2ebecc84d555)


stay focused!


