# Gerando chave SSH

A autenticação no servidor de aplicações se dá através de uma chave SSH.

## Procedimento a ser realizado na **máquina local do usuário**

No dispositivo do usuário, verificar a existência da chave "id_rsa.pub":
```
$ ls -al ~/.ssh
```
Caso o usuário não tenha a chave, precisa-se gerar uma nova:
```
$ ssh-keygen -t rsa
```
Basta apertar "Enter" nas requisições que aparecem, **sem inserir password**, que a chave será gerada conforme a imagem a seguir:

![Captura de tela de 2022-11-18 22-54-38](https://user-images.githubusercontent.com/83249854/202828866-abed049b-0aef-453c-8cae-04d3fcea8763.png)

Listando novamente, agora devemos ter o seguinte resultado:

![Captura de tela de 2022-11-18 23-01-08](https://user-images.githubusercontent.com/83249854/202829105-716c1447-4632-41f6-970b-e1d7ebad2578.png)

Agora o usuário deve gerar a string da chave:
```
$ cat ~/.ssh/id_rsa.pub 
```
![Captura de tela de 2022-11-19 00-15-03](https://user-images.githubusercontent.com/83249854/202831595-728493eb-0f56-4a12-ad9b-bed66fdfd13f.png)

O usuário deve copiar a string gerada e disponibilizar para o administrador do servidor Dokku realizar a inclusão deste no sistema.

**Obs.: Obviamente, a string gerada será diferente em outra máquina.**