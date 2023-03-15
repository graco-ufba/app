# Configurando as variáveis de ambiente

Normalmente, um aplicativo exigirá alguma configuração para ser executado corretamente. O Dokku oferece suporte à configuração de aplicativos por meio das variáveis de ambiente. Essas variáveis podem conter dados privados, como senhas ou chaves de API, por isso não é recomendável armazená-las no repositório do seu aplicativo.

As variáveis de ambiente estão disponíveis no tempo de execução e durante a etapa de construção/compilação do aplicativo para implementações baseadas em buildpack.

Para implantações de buildpack, o Dokku criará um arquivo `/app/.env` que pode ser usado para buildpacks herdados. Observe que isso não é atualizado quando `config:set` ou `config:unset` é chamado e é gravado apenas durante uma implantação (deploy) ou `ps:rebuild`. Os desenvolvedores são incentivados a ler diretamente do ambiente do aplicativo, pois os valores adequados estarão disponíveis.

Você pode definir várias variáveis de ambiente de uma só vez:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set <NOME_DO_APP> KEY="VALORES\ COM\ ESPAÇOS"
```
Dokku também pode ler valores codificados em base64. Essa é a maneira mais fácil de definir um valor com novas linhas ou espaços. Para definir um valor com novas linhas, você precisa primeiro codificá-lo em base64 e passar o sinalizador `--encoded`:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set --encoded <NOME_DO_APP> KEY="$(base64 ~/.ssh/id_rsa)"
```
Obs.: `id_rsa` é o id ssh da sua máquina local.

Obs.1: Caso a sua aplicação não utilize variáveis de ambiente, o Dokku utilizará a suas configurações globais para essa configuração.

Obs.2: Lembramos que é possível suprimir os modificadores `-t` e `-p 2299` conforme indicado no tópico de ([ambientes locais](ambiente-local.md))
