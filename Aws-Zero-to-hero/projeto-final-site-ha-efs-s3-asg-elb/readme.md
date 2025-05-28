## Projeto final - AWS Zero to Hero !
#### Aqui iremos criar um sistema de um site altamente disponível, com autoscaling (asg) configurado, elastic load balancer, entre várias outras features envolvidas!


# Parte 1:
---
## 1 passo - criar uma vpc com 2 az's
- não irei abordar essa etapa neste lab.

## 2 passo - criar o EFS
![image](https://github.com/user-attachments/assets/f91545db-a952-48d7-a6a2-728c473db6d6)
- aqui vamos copiar o ID do EFS e também ir em "attach" e copiar o comando mount.

## 3 passo - criar o bucket S3
![image](https://github.com/user-attachments/assets/63af6997-e9d0-4633-a874-163290ea20a6)
![image](https://github.com/user-attachments/assets/cc574760-c8bd-400c-8ed5-72367b2e7d8c)
![image](https://github.com/user-attachments/assets/9cf0942f-c70f-4727-8710-4709fcc7e6e1)

## 4 passo - criar as instâncias em 2 AZ's distintas!
- antes é interessante ter SG's configurados para liberar as portas 22 e 80.
- importante também dar uma **IAM Role de full access ao S3** às instâncias.
- atenção para colocar cada EC2 em AZ's diferentes...
- EC2 - 01:
![image](https://github.com/user-attachments/assets/f1368592-f55b-46a8-b75f-dad22fdf0cf5)
![image](https://github.com/user-attachments/assets/4c6821fb-2fc7-413d-8e47-2485301646ac)
![image](https://github.com/user-attachments/assets/05566f61-581b-4bf0-b946-2cda597d5eba)
- Bootstrap:
![image](https://github.com/user-attachments/assets/7e282a7a-79c5-4337-a4be-21ed07fcb14f)
> manda ver na ec2-01!
- EC2 - 02:
- mesma coisa, só vai alterar a AZ e o bootstrap:
![image](https://github.com/user-attachments/assets/e7c3dfd2-54d0-43c4-a337-e98ccb01ad1a)
- após as instâncias criadas, se deve esperar um pouco para elas subirem e então copiar o endereço do ip delas e colar no browser.... o conteúdo do site deve ser aberto!
![image](https://github.com/user-attachments/assets/8bb87025-eb1f-4a24-9fa3-505642181d9d)

 -após, voltarei no s3 para verificar se o backup ficou lá.
 ![image](https://github.com/user-attachments/assets/48836a80-a3b0-4d6e-87d2-0460ddd79b70)
 
> funfou!
----

# Parte 2 (agora vai ter alguns de investimentos (R$$$) nesse aprendizado rs!)
---

## 1 Passo - criar o ELB para distribuir o acesso.
![image](https://github.com/user-attachments/assets/0148a94f-4803-4eb2-bf76-6a4d39a3283a)
- será usado o ALB:
![image](https://github.com/user-attachments/assets/50270a46-ef4f-467a-b4a0-2b0602ae00e1)
- seguir padrão de instalação - auto interpretar....
![image](https://github.com/user-attachments/assets/939d3c70-4cf5-4bf7-9fab-1cceb6b7d716)
![image](https://github.com/user-attachments/assets/aaf3e88c-e925-45d9-93c9-1bc7640305cd)
- o SG total engloba a porta 22 e 80
![image](https://github.com/user-attachments/assets/d94f4d6b-0f2f-4714-9ba3-60fb45fcf556)
- aqui é preciso criar um "Target Group"
![image](https://github.com/user-attachments/assets/69cdb4bb-4393-4921-8b7e-8e25cea0b003)
![image](https://github.com/user-attachments/assets/1a828511-e2ca-4d1c-b3d6-e049523eff63)
![image](https://github.com/user-attachments/assets/c713e278-522e-480a-93d3-d68963848e83)
![image](https://github.com/user-attachments/assets/e8bbd152-2d86-48d3-8d7f-56531ee3adfc)
![image](https://github.com/user-attachments/assets/14d44156-b1fa-484c-933d-8755d993bfaf)
- next...
![image](https://github.com/user-attachments/assets/f0bdb9da-6bc1-45d7-b8aa-7501e5dff080)
![image](https://github.com/user-attachments/assets/c2aac6ac-5957-4a76-b38b-80de14df65a6)
- voltar na criação do elb...
![image](https://github.com/user-attachments/assets/4a58ac4e-0267-4003-8ca8-9ec6ed246abf)
![image](https://github.com/user-attachments/assets/d6081325-6975-4e11-a1dc-f1db2a7c1a59)
![image](https://github.com/user-attachments/assets/2e600aca-edc5-445e-a7d9-346f4554029b)
- após o elb ficar pronto para o uso, copiar o DNS Name e colar no browser, o site será aberto!
![image](https://github.com/user-attachments/assets/48c3a202-6c88-4423-9185-01cf41bddc48)
![image](https://github.com/user-attachments/assets/978ff93f-2d4d-46a6-b4d9-0fecde8d70e2)
![image](https://github.com/user-attachments/assets/a0c59e85-38c2-4295-ab4a-b2f3707772d3)
---

# Parte 3 - CRIAR AMI E ASG !
- antes será criada uma imagem AMI "golden image"
- mesmas configurações, o que vai mudar será o bootstrap. Aqui o background do autoscale será diferente das outras instâncias do elb, para podermos notar qual acesso está acontecendo, se nas instâncias padrões (elb) ou nas instâncias criadas via autoscaling!
- atenção para aplicar a iam role do s3 full access
- bootstrap:
![image](https://github.com/user-attachments/assets/fb4d8afe-814d-4e9f-a7bf-eb616e6b4714)
- aguardar a instância carregar, copiar o ip público e colar no browser, o site deverá abrir com background amarelo.
![image](https://github.com/user-attachments/assets/3d574351-e0ef-4e26-9e2e-4b602e7dd436)
![image](https://github.com/user-attachments/assets/c6067af3-c3a9-4cd5-aece-1c5b436e4f5c)
> (ew maravilha...)
- após isso, essa golden image vai virar uma image.
![image](https://github.com/user-attachments/assets/9b93468f-8725-4adc-b391-2e63deb4671f)
![image](https://github.com/user-attachments/assets/29476a17-b6a1-4f4f-abeb-8b6777aad388)
![image](https://github.com/user-attachments/assets/c1995944-52cb-4a1a-977c-4d11dc081bd5)
- depois que a imagem for criada, iremos excluir a goden image. o intuito aqui foi criar uma instância, configurar ela e então criar a imagem que vai ser lançada no autoscaling.
![image](https://github.com/user-attachments/assets/4fe2910c-0bd1-4394-b05b-af17522b3d96)
- quando status sair de 'pending' para 'available', podemos apagar a instância golden.
![image](https://github.com/user-attachments/assets/60ac9801-1697-4d3b-a288-0f844373a921)

## CONTINUANDO....
- AUTOSCALING:
![image](https://github.com/user-attachments/assets/741a2dd4-9875-44c8-a6da-620d36650d85)
- antes de criar o ASG, vamos criar o launch template.
![image](https://github.com/user-attachments/assets/328ddfc1-a467-4f0a-908d-2fe90c4a54a8)
![image](https://github.com/user-attachments/assets/e97bca9f-29fc-4ec2-b650-a38e56cd5b57)
![image](https://github.com/user-attachments/assets/5c8f433a-d273-45d3-9f16-8e04eced073d)
- create launch template!]
----
### atenção!!!!!
-eu havia esquecido de atribuir ip público no launch template... voltei e recriei...
![image](https://github.com/user-attachments/assets/c5d23522-9778-45d6-853d-2113b263db42)
---
![image](https://github.com/user-attachments/assets/eef97222-dca4-4f34-95c8-f70e2e3211b0)
![image](https://github.com/user-attachments/assets/c74a75ae-f9ef-426f-96a9-fecd76612658)
- aqui ja irei selecionar o launch template que criei.
![image](https://github.com/user-attachments/assets/90d97d8a-a036-4718-9985-2c34773afa52)
![image](https://github.com/user-attachments/assets/2e903a73-61ef-4ef6-b9a2-faa579bbe903)
![image](https://github.com/user-attachments/assets/07ddf2e7-2d9a-43f1-b178-35be879ae218)
![image](https://github.com/user-attachments/assets/d1d9545a-71a5-4515-8fc5-b2c7d3bf9111)
- nessas políticas, configurei para quando a CPU atingir os 25%, ela suba novas instâncias. desabilitei o scale in, para que o número possa voltar para 1 em caso de baixo número de requisições.
![image](https://github.com/user-attachments/assets/dbb70857-91dc-40aa-ab6f-9717591ae7eb)
![image](https://github.com/user-attachments/assets/0ac8d27f-3ddc-4cb7-b55d-0ddb08a2017a)

---

-se formos no painel de instâncias, poderemos ver que já existe 1 instância padrão de autoscaling sendo criada:
![image](https://github.com/user-attachments/assets/43ce887f-2339-487e-8739-bcdcc8bbe58a)
![image](https://github.com/user-attachments/assets/064110e5-73d3-48f2-9de2-c67fe9289145)

---
## agora vêm a mágica! vamos pegar o endereço do load balancer! vamos acessar e ficar dando o F5, ele vai abrir background branco e amarelo, qnd abrir o background branco, vai ser das instâncias, quando for amarelo, será da instância do ASG!!!
![image](https://github.com/user-attachments/assets/7b93f660-ab50-43ab-aec9-eceeeff5c815)
![image](https://github.com/user-attachments/assets/fe1860f3-283a-4696-bfa2-f72c189b4cea)
-- na 3x:
![image](https://github.com/user-attachments/assets/8b10d7ae-672f-424c-93ba-f9a0ff8690d1)
- porém temos hoje 3 instância, 2 criadas e 1 básica do ASG:
![image](https://github.com/user-attachments/assets/356372b8-2907-4e46-917b-ab7f540503ad)

---
## Vamos começar o stress para o ASG subir automático!!

### 1 passo 
- entrar na instância do ASG e ir em instance connect!
![image](https://github.com/user-attachments/assets/01a0f6c9-d081-4d62-a629-4d51d5f84c90)
---

## atenção! as subnets que as instâncias estavam sendo criadas, não estava com a opção de auto assign ip... ocorrendo que as novas instâncias do ASG, não vinha com ip publico. Tive que voltar na VPC, ir em subnets, selecionar elas, ir em Ações, editar.... e marcar a opção de auto assign:
![Imagem do WhatsApp de 2025-05-27 à(s) 20 41 38_d712b2d4](https://github.com/user-attachments/assets/11cbdf7e-46a0-4850-b9fc-8c60efeacee4)
----

- depois disso, a ec2 vai pegar ip, se nao pegar, exclua que outra vai ser iniciada e a nova já vai vir com ip publico!!!

- ----

## conectar na instância do ASG para instalar o teste de stress!!!
- instance connect
![image](https://github.com/user-attachments/assets/08779fb9-6dc3-46a3-86f1-3fb5c2d06cfb)
![image](https://github.com/user-attachments/assets/1b1f689f-e891-460a-9412-49e6dad24a6e)
emitir comando top
![image](https://github.com/user-attachments/assets/2751cc76-d5c8-4c84-8bae-aec44ab2577f)

o teste de stress vai chamar as novas instancias, após isso, para parar o teste, digitar comando "kill - 9 "ID do stress"

.....


## Limpando tudo
- laucnh template
- asg
- ec2
- load balancer
- target groups
- ami (desregister ami)
- snapshots (ami)
- s3
- efs
- vpc

----

### considerações:
- infelizmente o link da aplicação de stress que eu consegui, deu erro. procurei alguns links da internet e acabei utilizando um.... aparentemente, como mostrado nas imagens, ele rodou o teste, porém não tenho a certeza do correto funcionamento. O ASG nao subiu novas instâncias, apesar das configurações corretas.
- mas enfim, é isso!
- se alguém fazer essa lab, e tiver um novo link do teste de stress, favor entra em contato comigo!

-ah! quando o valor cobrado aparecer, vou postar aqui! :~)


> stay focused !!!









 





 






























