#Início

> docker-compose up -d

#Server

Repetir os passos para cada um dos 3 servers

## Para entrar no agent
> docker exec -it consulserver01 sh

## Para descobrir o IP do agent
> ifconfig

Editar o server.json respectivo com o IP próprio e dos outros servers

## Iniciar agent
>consul agent -config-dir=/etc/consul.d

#Client

## Para entrar no agent
>docker exec -it consulclient01 sh

## Para descobrir o IP do agent
>ifconfig

## Iniciar agent
>consul agent -bind=172.30.0.2 -data-dir=/tmp -config-dir=/etc/consul.d -retry-join=172.30.0.4

Utilizar no retry-join o ip de um dos servers

## Consultar client

### Instalar bind tools
> apk -U add bind-tools

### Consultar clients
> dig @localhost -p 8600 nginx.service.consul

# Subindo NGINX para testar o Health Check

## Instalando NGINX
> apk add nginx

## Executar NGINX

> nginx

## Fazendo o NGINX responder um status válido

> mkdir /usr/share/nginx/html -p

> apk -U add vim

> vim /etc/nginx/http.d/default.conf

Trocar o bloco do meio que retorna 404 pra tudo por:
> root /usr/share/nginx/html;

Escrever um "Hello"
> vim /usr/share/nginx/html/index.html

Recarregar nginx:
> nginx -s reload

# Outros

## Para verificar todos os agents rodando

Dentro de qualquer agent
> consul members

## Gerar chave de criptografia

> consul keygen

## User interface

> http://localhost:8500/ui