### Como boas práticas de segurança, no ato da criação de uma instância EC2, o recomendado é criptografar o EBS logo na criação. 

### Esse passo a passo vai mostrar como criptografar o disco EBS de uma instância existente (Downtime)

## Passos:
- A partir do volume criado (ir em Volumes)
- em volumes, selecionar o volume desejado que será criado o snapshot;
- vale ressaltar que a criptografia não vai ser gerada no ato de fazer o snapshot do disco, mas sim, a partir do snapshot já existente.
- após o snap criado, vai existir 2 formas:
	- copiando o snapshot (gerando um novo snapshot a partir do snapshot atual, recém criado da instância)
	- copiando (levando para outra região)
		- nessas 2 opções, vai aparecer a opção de cripto.

### Passos seguintes:
- depois do snap criado e já criptografado (ebs), poderá ser iniciado uma nova imagem ou volume a partir do snapshot (em actions)
> stay focused.
