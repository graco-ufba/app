# Visão geral

A Rede IC fornece o serviço de hospedagem de aplicações web para a comunidade do Instituto de Computação, ainda de forma experimental. Neste momento, não realizamos backup dos dados e não hospedamos aplicações que utilizem intensivamente recursos de processamento ou armazenamento.

O serviço de hospedagem é baseado no [Dokku](https://dokku.com/), uma solução open source para plataforma como serviço (PaaS). O Dokku possibilita que o usuário faça o upload do código-fonte da aplicação via Git; o servidor realiza o build da aplicação e a executa em containers Docker isolados.

Para hospedar sua aplicação web, abra um chamado no [Sistema de Suporte do IC](https://suporteic.ufba.br), utilizando o tópico de ajuda "Suporte TI: hospedagem de aplicação". Será necessário fornecer uma chave SSH pública (veja o [tópico a seguir](chave-ssh.md))



<!-- 
# Encriptação da url da aplicação

Uma vez realizado o deploy da aplicação, se der tudo certo como o esperado, o servidor irá gerar a url para acesso à aplicação do usuário, porém sem a certificação SSL de criptografia. O usuário, portanto, **DEVE**, responder ao chamado aberto no [Sistema de Suporte](https://suporteic.ufba.br) informando ao suporte de TI a efetivação do deploy e a url gerada, para que as providências de certificação da sua aplicação sejam tomadas.

Isso **não pode nem deve** ser negligenciado, haja vista que o acesso a todas as aplicações do servidor **DEVEM** ser acessadas a partir de requisições **HTTPS**. -->