# Configurando ambiente local 

Para enviar comandos via SSH para a sua aplicação no servidor (veremos os comandos disponíveis mais adiante), fazer:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br <COMANDO> <NOME_DA_APLICAÇÃO>
```
- `-p 2299` indica que o comando deve ser reallizado no domínio app.ic.ufba.br na porta 2299;
- `-t` indica que o SSH requer um psudoterminal para execução de comandos shell (PTY). É altamente recomendada a sua utilização.

Para que não seja necessário executar todo esse comando a cada vez, podemos suprimir esses modificadores de porta e PTY, configurando um script em `~/.ssh/config` inserindo as seguintes linhas de comando:

```
Host app.ic.ufba.br 200.128.51.122
  HostName 200.128.51.122
  Port 2299
  User dokku
  IdentityFile ~/.ssh/dokku
  RequestTTY yes
```
Desta forma, podemos agora executar os comandos suprimindo esses modificadores:

```
$ ssh dokku@app.ic.ufba.br <COMANDO> <NOME_DA_APLICAÇÃO>
```
