# Teste de Força Bruta com Burp Suite

# 🏁 Indice

- [Sobre](#-sobre)
- [Features](#-features)
- [Tecnologias Utilizadas](#%EF%B8%8F-tecnologias-utilizadas)
- [Como executar o projeto django](#-como-baixar-o-projeto)
- [Desenvolvedores](#desenvolvido-por)

## 🔖&nbsp; Sobre
O projeto consiste em uma aplicação de teste e um relatório com definições e utilização de um ataque de força bruta. 

### Conceitos utilizados
Descrição breve dos conceitos envolvidos;
1. Conceito 1
2. Conceito 2

### Ferramenta de teste: Burp Suite
Descrição da ferramenta de teste

### Aplicação de teste
Foi criada uma aplicação django contendo apenas as configurações padrões e autenticação. O middleware CsrfViewMiddleware, responsável pela proteção contra Cross Site Request Forgeries, foi desativado para facilitar o ataque. 

### Como funciona?
Com a aplicação django em execução, nós criamos uma tentativa de login que foi interceptada pelo Burp Suite e então enviamos ela para a area de Intruder. Veja abaixo.
1. Na aba proxy, vá em Intercept. Com o intercept desligado, clique em Open Browser e realize uma tentativa de login no site que será atacado.
![alt text](/images/1.png)

2. Vá para a aba HTTP history e envie a requisição POST para o Intruder(ctrl+I)
![alt text](/images/2.png)

Na aba Intruder, fizemos as configurações para realizar um ataque de força bruta. Aqui consideramos duas formas: A primeira, que vamos partir de que temos uma lista de possiveis login e senhas, e a segunda, que consideramos não saber nenhuma informação sobre login e senha. Veja abaixo o passo-a-passo.

1. Vá para a aba Intruder e selecione a requisição que acabou de enviar.
![alt text](/images/3.png)
2. Vá em Positions, altere o tipo de ataque para Cluster Bomb e coloque entre "§" os campos que serão enviadas informações.
![alt text](/images/4.png)
3. Vá em Options, ache Grep - Extract e clique em add. Selecione algo do HTML que indique que a tentativa de login não foi bem sucedida. No nosso caso selecionamos isso:

        <p class="errornote">
            Please enter the correct username and password for a staff account. Note that both fields may be case-sensitive.
        </p>
    ![alt text](/images/5.png)

4. Vá em Payloads e selecione o tipo do payload de cada conjunto. Pode alternar entre os conjuntos em Payload Set. 
    - Caso selecione Simple list, adicione a wordlist em Payload Options;
    ![alt text](/images/6.png)
    - Caso selecione Brute Forcer, indique um conjunto de caracteres e a quantidade minima e maxima em Payload Options. Esses dados serão utilizados para formar logins e senhas.
    ![alt text](/images/7.png)

5. Agora clique em Start Attack, será aberta uma guia separa. Aguarde o ataque finalizar.
![alt text](/images/8.png)

6. Agora é possivel ordenar a lista pelas tentativas realizadas com sucesso e obter o login e senha utilizados.
![alt text](/images/9.png)
---

## 🚀 Features
- [] Descrição breve dos conceitos envolvidos
- [] Descrição da ferramenta de teste
- [x] Desenvolvimento da aplicação de teste
- [x] Descrição da utilização da ferramenta

---
## ⚒️ Tecnologias utilizadas

O projeto foi desenvolvido utilizando as seguintes tecnologias

- [Python](https://python.org)
- [Django](https://www.djangoproject.com)
- [Burp Suite](https://portswigger.net)

---

## 🗂 Como executar o projeto django
```bash
# Entre no diretorio do projeto
$ cd django_forca_bruta

# Execute as migrações do banco de dados
$ python manage.py migrate

# Crie um usuario, será necessario preencher informações
$ python manage.py createsuperuser

# Execute o servidor
$ python manage.py runserver
```

## Desenvolvido por
[Jacyiricê Silva Oliveira](https://github.com/jacyirice/)

[Rayanna Quirino](https://github.com/rayannaQuirino/)

## Disponivel em 
[GitHub](https://github.com/jacyirice/Forca-bruta)
