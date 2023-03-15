# Configurando as variáveis de ambiente

Normalmente, um aplicativo exigirá alguma configuração para ser executado corretamente. O Dokku oferece suporte à configuração de aplicativos por meio das variáveis de ambiente. Essas variáveis podem conter dados privados, como senhas ou chaves de API, por isso não é recomendável armazená-las no repositório do seu aplicativo.

Você pode definir várias variáveis de ambiente de uma só vez:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set <NOME_DO_APP> KEY="VALORES\ COM\ ESPAÇOS"
```
ou ainda:

```
ssh -t dokku@app.ic.ufba.br config:set sisfila VAR1="valor\ 1" VAR2="valor\ 2"
```
Dokku também pode ler valores codificados em base64. Essa é a maneira mais fácil de definir um valor com novas linhas ou espaços. Para definir um valor com novas linhas, você precisa primeiro codificá-lo em base64 e passar o sinalizador `--encoded`:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set --encoded <NOME_DO_APP> KEY="$(base64 ~/.ssh/id_rsa)"
```
Obs.: `id_rsa` é apenas um exemplo com o id SSH da sua máquina local.

Obs.1: Caso a sua aplicação não utilize variáveis de ambiente, o Dokku utilizará a suas configurações globais para essa configuração.

Obs.2: Lembramos que é possível suprimir os modificadores `-t` e `-p 2299` conforme indicado no tópico [configurando ambiente local](ambiente-local.md)
