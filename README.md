# Projeto kube-news

### Objetivo
O projeto Kube-news é uma aplicação escrita em NodeJS e tem como objetivo ser uma aplicação de exemplo pra trabalhar com o uso de containers.

### Configuração
Pra configurar a aplicação, é preciso ter um banco de dados Postgre e pra definir o acesso ao banco, configure as variáveis de ambiente abaixo:

DB_DATABASE => Nome do banco de dados que vai ser usado.

DB_USERNAME => Usuário do banco de dados.

DB_PASSWORD => Senha do usuário do banco de dados.

DB_HOST => Endereço do banco de dados.



#Comandos docker Uteis
###Comando de build
docker build -t dgsbarbosa/kube-news:v1 -f src/Dockerfile src/

###Execução do app
docker container run -d -p 8080:8080 -e DB_DATABASE=kubenews -e DB_USERNAME=kubenews -e DB_PASSWORD=Pg123 -e DB_HOST=kube_news_db --network kube_news_net  dgsbarbosa/kube-news:v1

###Execução do db
docker container run -d -p 5432:5432 --name kube_news_db -e POSTGRES_PASSWORD=Pg123 -e POSTGRES_USER=kubenews -e POSTGRES_DB=kubenews --network kube_news_net -v kube_news_vol:/var/lib/postgresql/data postgres:12.17

