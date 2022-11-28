# Docker Compose

- Vamos criar vários containers. Com o tempo esses containers ficam difíceis de manipular por causa da quantidade, com isso, vamos utilizar o Docker Compose para fazer todo o processo de forma mais automatizada.

### Caso não tenha o Docker Compose instalado, rode os seguintes comandos:

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install docker-compose
```
## Criação de vários Containers manualmente

### Criar network

```
docker network create wordpress_net
docker network ls
```

> O comando acima irá criar um network e em seguida será impresso na tela

### Criar um container para utilizar o MySQL

```
docker container run --name wp-db -e MYSQL_ROOT_PASSWORD=rootpwd -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=wordpresspwd --network=wordpress_net -d mysql:8.0.30
```

### Criar um container para utilizar o Wordpress

```
docker container run --name wp -web -e WORDPRESS_DB_HOST=wp-db -e WORDPRESS_DB_USESR=wordpress -e WORDPRESs_DB_PASSWORD=wordpresspwd -e WORDPRESS_DB_NAME=wordpress --networkd=wordpress_net -p:8080:80 -d wordpress
```

> Acesse `localhost:8080` para verificar o funcionamento

### Criar um container para utilizar o PHPMyAdmin

```
docker container run --name wp -phpmyadmin -e PMA_HOST=wp-db -e PMA_PORT=3306 -e PMA_USER=wordpress -e PMA_PASSWORD=wordpresspwd --network wordpress_net -p 8181:80 -d phpmyadmin
```

> Acesse `localhost:8181` para verificar o funcionamento

- Compartilhar todos os containers com uma equipe nova pode ser complicado. Visando isso, surge o Docker Compose, que é uma solução para criar uma receita que executa seus containers de uma forma organizada.

oi [^1] oi


## Criação de vários Containers utilizando Compose

## Referência

[^1]: <https://github.com/fabricioveronez/live-docker>
