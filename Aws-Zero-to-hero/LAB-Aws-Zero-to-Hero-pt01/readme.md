# Laboratório Zero To Hero

## Criando as EC2's - Linux e Windows

### EC2 - Linux 
1. Primeiros passos
   ![image](https://github.com/user-attachments/assets/419de779-7011-44fa-8369-59af38b48eb1)
   ![image](https://github.com/user-attachments/assets/c212cd01-78e4-4536-b6d8-c58159970d6f)
   ![image](https://github.com/user-attachments/assets/a5d55775-fc56-4f97-8243-f3f6de18341c)
   ![image](https://github.com/user-attachments/assets/8d6a586a-1627-425b-8ce0-ba6a3e44536e)
   ![image](https://github.com/user-attachments/assets/fb49fd97-0db7-4917-8070-4001729b23b7)

1.2 Conexão via PuTTy
  ![image](https://github.com/user-attachments/assets/32abd2eb-f89d-45f9-936e-69cda19de0eb)
  ![image](https://github.com/user-attachments/assets/fd289fac-b1c3-4c4c-9333-26204e32b8da)
  ![image](https://github.com/user-attachments/assets/f4221c79-c8ec-4146-9b90-57d4b80acbd0)
  ![image](https://github.com/user-attachments/assets/e584ede0-74e0-4c87-a6ec-d3b8cc44f7b2)
  site on:
  ![image](https://github.com/user-attachments/assets/e45742b6-39ee-41f8-8caf-edd838ca04d7)


1.3 Outra forma de conectar à instância Linux - Usando o SSH Terminal Web-based
  ![image](https://github.com/user-attachments/assets/d823d366-39f4-4b78-ab9c-173f88432730)
  ![image](https://github.com/user-attachments/assets/bb0cbebe-b1ec-462a-885b-f858140ac65e)
  ![image](https://github.com/user-attachments/assets/606d9812-9703-4b12-8bc8-61c6e3192031)

1.4 Outra maneira seria usando o Session Manager via System Manager, porém ela vai exigir configuração IAM e isso será objeto de estudo para outro momento.
  ![image](https://github.com/user-attachments/assets/caa4d354-fb1b-49ad-b406-c57a9da6b669)


## Atenção:
![Imagem do WhatsApp de 2025-05-24 à(s) 10 46 38_b46ebe8a](https://github.com/user-attachments/assets/e5db91c6-91db-4eb3-81af-523c7a2c660f)
---
isto é, uma instância windows server vai precisar de no mínomo 30gb de espaço na sua criação, com isso, encerrando a opção free tier...
o ideal é excluir a instância linux, que já possui 8gb de armazenamento em uso....

### EC2 - Windows Server

1. Primeiros passos
     criei uma nova VPC, EC2 Windows e SG.
   ![image](https://github.com/user-attachments/assets/ded86655-711f-4165-b670-88aad5cd9be0)
   ![image](https://github.com/user-attachments/assets/5ed7e726-1353-4436-8ea1-f682344f2049)

2. Passo
   conectar na instância via console - RDP Client.
   primeiro, no ato da criação da instância, criei uma chave nova windows e salvei.
   nessa parte vou clicar para 'obter a senha', inserindo o arquivo baixado na própria console e clicando para ela gerar a senha...
   ![image](https://github.com/user-attachments/assets/23e6a259-2b7a-4fed-9d2f-5a3eeac8bb4a)
   ![image](https://github.com/user-attachments/assets/cfa98e2f-4dea-4f00-ac05-40f811fa2235)
   ![image](https://github.com/user-attachments/assets/38aae28b-30a8-4dee-a24c-61b8bbf4832f)
   descriptografa e salva.
   depois, vamos fazer download do arquivo de área de trabalho remota.
   ![image](https://github.com/user-attachments/assets/e646596e-6f4d-4693-9b69-7f2fc456a127)
   ![image](https://github.com/user-attachments/assets/1763768c-2c37-4fc1-9686-320c45385c38)

3. Passo
   instalar o ISS > iniciar > server manager
   ...vamos esperar ele finalizar e então clicar em add roles...
   ![image](https://github.com/user-attachments/assets/7a38fb5a-3ac8-4f6b-83f5-962ac7f55c48)
   em seguida vamos de 'next-next' até habilitar a opção do webserver:
   ![image](https://github.com/user-attachments/assets/b05f21f7-2fe1-418e-a0dd-c6eb75437f44)
   ![image](https://github.com/user-attachments/assets/65865511-5873-4490-a73d-7aa35f8836cc)

web server na instância windows rodando!


stay focused!



   




      

