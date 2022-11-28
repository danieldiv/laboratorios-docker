# Docker Compose

- Vamos criar vários containers. Com o tempo esses containers ficam difíceis de manipular por causa da quantidade, com isso, vamos utilizar o Docker Compose para fazer todo o processo de forma mais automatizada.

- Git utilizado como referência. [^1]

- YouTube utilizado como referência. [^2]

### Caso não tenha o Docker Compose instalado, execute os seguintes comandos:

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

## Criação de vários Containers utilizando Compose

- Crie o arquivo docker-compose.yml [^3]
- Remova os Containers criados

### Subir Compose

```
docker-compose up -d
docker-compose logs
```

> Executa todos os containers do arquivo [^3] e exibe os logs.

- Crie o arquivo .env [^4]

### Executar o Compose através do .env

```
docker-compose --env-file .env up -d
```

## Referências

[^1]: [GitHub](<https://github.com/fabricioveronez/live-docker>)

[^2]: [YouTube](<https://www.youtube.com/watch?v=hue967OT4gw>)

[^3]: [docker-compose.yml](<https://github.com/fabricioveronez/live-docker/blob/main/wodpress/docker-compose.yml>)

[^4]: [.env](<https://github.com/fabricioveronez/live-docker/blob/main/wodpress/.env>)
