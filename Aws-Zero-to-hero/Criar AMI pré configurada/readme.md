# Guia para Criação de Golden Image (AMI) na AWS

## MODO 1 – Golden Image

- Imagem customizada com todas as funcionalidades já pré-configuradas para uso. As AMIs criadas ficarão disponíveis em **"Minhas AMIs"**.

---

### Passo 1
- Iniciar uma nova instância **Linux Free Tier** com VPC, SG e demais configurações seguindo o padrão dos labs anteriores.

---

### Passo 2
- Conectar na instância usando **Instance Connect** e instalar o Apache:
- Comandos:
    yum update -y
    yum install httpd -y
    service httpd start
    chkconfig httpd on
- Isso garante que o Apache inicie automaticamente a cada reinicialização.

### Passo 3
- Criar um arquivo de teste na raiz web:
    cd /var/www/html
    echo "<html><h1> site blablabla </h1></html>" > index.html

### Passo 4
- Testar o site acessando o IP público da instância via navegador.

### Passo 5
- Criar a imagem (AMI):
- Selecione a instância em execução
- Vá em Actions > Image and templates > Create image
- Preencha:
  - Nome da imagem
  - Descrição
  - Escolha se deseja reiniciar a instância ou não
  - Os volumes serão automaticamente copiados
  - Adicione tags (opcional)
  - Clique em Create image
- A imagem estará disponível em "AMIs" > "Owned by me".

### Passo 6
- Ao criar uma nova instância, selecione sua imagem em Minhas AMIs. Como o Apache já está configurado, basta acessar o IP público e o site estará disponível.

### Passo 7 – Importante
- Para a imagem ser criada, será gerado um Snapshot (pode haver cobrança).
- Se o snapshot for apagado, a AMI correspondente será invalidada.

---

## MODO 2 – Criação por Snapshot (Método Antigo)

### Passo 1
- Vá até Snapshots
- Selecione o Volume ID desejado
- Adicione descrição e tags
- Clique em Create snapshot

### Passo 2
- Vá em Instâncias
- Em Actions, escolha Create image from snapshot
- Preencha:
-   Nome da imagem
-   Descrição, arquitetura, root device name (opcional)
-   Ajuste os volumes se necessário
- Clique em Create image

### Acesso às Imagens Criadas
- Suas AMIs estarão disponíveis em Minhas AMIs
- As imagens ficarão disponíveis somente na região em que foram criadas

### Copiar AMI/Snapshot para Outra Região
- Vá em AMIs ou Snapshots
- Selecione a imagem ou snapshot
- Vá em Actions > Copy AMI (ou Copy Snapshot)
- Na tela de cópia:
-   Defina o nome, descrição e a região de destino
-   Habilite ou não a criptografia do EBS

### Apagando Recursos
- Apague as instâncias criadas
- Para apagar a AMI:
-   Selecione a AMI
-   Vá em Actions > Deregister AMI
- Vá em Snapshots, selecione os snapshots associados e exclua

> Nota: Lembre-se de revisar as cobranças associadas a snapshots e armazenamento antes de deixar recursos ativos por muito tempo.
---


> stay focused!


  



