# Comandos dispoíneis

Para acessar/manipular a sua aplicação no servidor/container, seguem alguns comandos úteis permitidos para serem executados via SSH. Comando a ser executado precisa necessariamente seguir esse padrão:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br <COMANDO> <NOME_DA_APLICAÇÃO>
```
Lembramos que conforme explicitado no tópico [Configurando ambiente local(ambiente-local.md)], podemos suprimir os modificadores `-t` e `-p 2299`. Fica a critério do usuário.

# Comandos permitidos:

## Comandos para banco de dados: 

- `postgres:expose <service> <ports>`

Este exemplo acima foi feito com comando de banco de dados postgreSQL, mas poderia ser outro. O comando expõe o banco de dados presente no container Docker a uma porta para acesso externo ao processo. Isso é útil para realizar consultas no banco, backups e afins. Exemplo de execução:


```
$ ssh -t -p 2299 dokku@app.ic.ufba.br postgres:expose teste
```

Nesse momento, o servidor retornará em quais portas o serviço está exposto/disponível para acesso. 

# Obs.: Precisamos definir internamente no NATI como será esse acesso ao banco de dados dos containers e se erá mesmo possível, uma vez que vai demandar liberação de portas pela STI. Se for possível, precisaremos permitir mais comandos no ACL para manipulação do banco.

## Comandos dokku

- `run`

O comando `run` pode ser usado para executar um processo único para um comando específico. Isso iniciará um novo contêiner e executará o comando desejado dentro desse contêiner. A imagem do contêiner será a mesma imagem do contêiner usada para iniciar o aplicativo atualmente implantado. Exemplo de execução de listagem detalhada de arquivos de uma aplicação: 

```
# roda `ls -lah` no diretório `/app` da aplicação `teste`
$ ssh -t -p 2299 dokku@app.ic.ufba.br run teste ls -lah
```
Obs.: Observe que nos caso do comando `run`, o nome da aplicação precisa vir ANTES do comando que se quer rodar.

- `logs`

Exibe os logs da aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br logs teste
```

- `urls`

Exibe as urls vinculadas à aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br urls teste
```
Obs.: Decartar a usabilidade da url com schema http. Somente as requisições https irão funcionar por motivos de segurança. 

- `apps:destroy`

Comando que literalmente desvincula a applicação do seu banco de dados associado e a apaga do servidor. Após a execução do comando, o sistema exigirá que escrevamos exatamente o nome da aplicação para confirmação da destruição. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br apps:destroy teste
```
Obs.: O banco de dados não morre junto com a aplicação. Para destruí-lo, vejamos um exemplo com um banco de dados postgresSQL:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br postgres:destroy teste_db
```
Da mesma forma como para os apps, o sistema exigirá confirmação de segurança antes de proceder.

- `builder:set` 

Configura o modo de construção(build) conforme visto no tópico [configurando modo de construção(modo-build.md)]

- `config:show`

Exibe as configurações da aplicação no container Docker, bem como as variáveis de ambiente. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:show teste
```
Saída do comando:

```
=====> teste env vars
DATABASE_URL:          postgres://postgres:4d289d66a5617ca55a696ab70eea145f@dokku-postgres-teste-production:5432/teste_production
DOKKU_APP_PROXY_TYPE:  nginx
DOKKU_APP_RESTORE:     1
DOKKU_APP_TYPE:        herokuish
DOKKU_PROXY_PORT:      80
DOKKU_PROXY_PORT_MAP:  http:80:5000 https:443:5000
DOKKU_PROXY_SSL_PORT:  443
GIT_REV:               50b80751d267c9202ca34775b81ff3edd7b45f2c

```
- `config:set`

Comando para configuração das [variáveis de ambiente(variaveis-de-ambiente.md)] conforme já visto anteriormente. Exemplo de execução para configuração de duas variáveis:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set <NOME_DA_APLICAÇÃO> VAR1="valor\ 1" VAR2="valor\ 2"
```
Exemplo de execução em base64:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br config:set --encoded <NOME_DO_APP> KEY="$(base64 ~/.ssh/id_rsa)"
```
## Comandos Docker (containers)

- `ps:inspect`

Este comando reunirá todos os IDs de contêiner em execução para seu aplicativo e chamará a inspeção do docker, limpando os dados de saída para que possam ser copiados e colados em outro lugar com segurança. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:inspect <NOME_DA_APLICAÇÃO> "
```
- `ps:report`

Exibe um relatório de processo para um ou mais aplicativos. Exemplo de execução com a aplicação:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:report <NOME_DA_APLICAÇÃO> "
```
Exemplo de saída com a aplicação "teste":

```
=====> teste ps information
       Deployed:                      true
       Processes:                     1
       Ps can scale:                  true
       Ps computed procfile path:     Procfile
       Ps global procfile path:       Procfile
       Ps procfile path:              
       Ps restart policy:             on-failure:10
       Restore:                       true
       Running:                       true
       Status web 1:                  running (CID: 05850b537eb)
```
- `ps:start`

Inicializa a aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:start <NOME_DA_APLICAÇÃO> "
```
- `ps:stop`

Para a execução de uma aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:stop <NOME_DA_APLICAÇÃO> "
```
- `ps:restart`

Reinicializa uma aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:restart <NOME_DA_APLICAÇÃO> "
```
- `ps:rebuild`

Reconstrói o contêiner Docker da aplicação. Exemplo de execução:

```
$ ssh -t -p 2299 dokku@app.ic.ufba.br ps:rebuild <NOME_DA_APLICAÇÃO> "
```

