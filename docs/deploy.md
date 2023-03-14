# Realizando deploy

A partir do momento em que o usuário receber a notificação de aptidão por parte do suporte de TI do IC, este já poderá realizar o deploy da sua aplicação através de comandos git seguindo os seguintes passos **em sua máquina local**:

* Navegar até o repositório Git da aplicação
* Adicionar um repositório remoto com o comando: 

```bash
$ git remote add dokku dokku@app.ic.ufba.br:<NOME_DA_APLICAÇÃO>
```

Troque `<NOME_DA_APLICAÇÃO>` pelo nome da sua aplicação (ou seja, o nome que vem antes de `app.ic.ufba.br` na URL de sua aplicação)

**Obs.: O repositório remoto criado para push PRECISA se chamar "dokku". Caso contrário, o deploy sempre retornará uma falha. Isso é uma exigência do sistema.**

* Realizar o deploy com o comando (**O primeiro deploy precisa necessariamente utilizar o modificador -f no comanfo git**): 

```
$ git push -f dokku master
```

* Após o primeiro deploy, se houver necessidade de realizar outros, não é mais necessário utilizar o modificador indicado acima. Pode-se fazer apenas: 

```
$ git push dokku master
```
