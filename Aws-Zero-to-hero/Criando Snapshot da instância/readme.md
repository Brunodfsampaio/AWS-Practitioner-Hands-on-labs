## Neste lab eu não vou gerar o snapshot da instância, porém irei abrir a feature e mostrar as opções!!!

1. localizar na console:
![image](https://github.com/user-attachments/assets/42d550ae-ccca-4784-a6d7-6cb44ea40594)

2. "Criando" o Snapshot
![image](https://github.com/user-attachments/assets/c69ac6b9-4d5f-4435-aeef-c2e6eefb6fed)
![image](https://github.com/user-attachments/assets/104d5d1f-be57-42db-94bb-dda8b3dfe7a2)

#### Na opção Volumes, existem caixas para marcar. Nelas podemos excluir o volume raiz ou volume de dados específicos... por exemplo, se a instância possuir mais de um disco (ebs) e os dados principais estiverem nos discos (não root - raiz), o usuário poderá fazer o snap apenas daquels discos, excluindo o raiz... ou excluir os outros e deixar apenas o snap com o disco root.)

  1. dessa forma, se cria o snaptshot e a partir disso, podemos iniciar novas instâncias a partir de um snapshot criado;
  2. vale lembrar que nao criação do snapshot, ele pergunta se deseja excluir volumes... isto é, ou vai limpo ou com os dados de volume criados.

stay focused!!!


