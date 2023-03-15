# Configurando o modo de construção (build)

No Dokku, é possível configurar o modo de build da sua aplicação. Esse é o método que será utilizado pelo Dokku para implementação da aplicação no container Docker no durante o deploy. Por padrão, no momento do deploy, o Dokku utilizar o construtor herokuish, uma ferramenta open source do Heroku. Para selecionar o modo build, fazer:

- Build herokuish: 

```
ssh -t -p 2299 dokku@app.ic.ufba.br builder:set <APP> selected herokuish
```
- Build Dockerfile:

```
ssh -t -p 2299 dokku@app.ic.ufba.br builder:set <APP> selected dockerfile
```
Caso o usuário não possua um Dockerfile na sua aplicação, um Procfile precisa necessariamente ser criado na raiz da aplicação. Um exemplo de configuração simples e funcional pode ser configurado da seguinte forma:

```
web: bundle exec puma -C config/puma.rb       # Utiliza o puma como serviço web
# worker: bundle exec sidekiq -c 3            # Necessário caso o usuário queira definir um worker
release: bin/rails db:migrate                 # configuração de migração automática do banco de dados no momento do deploy
```
Note que a linha `worker: bundle exec sidekiq -c 3` está comentada, pois é para ser utilizada somente em caso de especificação de worker, podendo ser omitida essa linha caso contrário. Nesse caso, utilizamos o `sidekiq` como exemplo. Na linha `release: bin/rails db:migrate` usamos o `rails` como exemplo por se tratar de um Procfile configurado para uma aplicação Ruby. Deve ser substituído pelo da sua aplicação.
