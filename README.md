# Docker

> O sistema utilizado foi o linux ubuntu

### Caso não tenha o Docker instalado, rode os seguintes comandos:

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install docker.io
```

## Comandos uteis

- `docker images` exibe todas as imagens disponiveis no sistema
- `docker ps` exibe os containers em execução
- `docker ps -a` exibe todos os containers
- `docker stop <ID or name>` para um container que esta executando
- `docker start <ID or name>` inicia um container
- `docker rm -f <ID or name>` remove um container e força a remoção se estiver em execução

## MySQL

- Para fazer o uso do MYSQL siga os comandos abaixo

### Baixar o mysql e o mysql na versao 5.7 que será utilizada para testes

```
docker pull mysql
docker pull mysql:5.7
docker run mysql:5.7
```

- Ao executar o docker será gerado um erro de variavél de ambiente não especificada, para corrigir utilize o comando abaixo

```
docker run -e MYSQL_ROOT_PASSWORD=root --name meu-mysql -d mysql:5.7
```

> `root` representa a senha para acessar o banco, `--name` define o nome do container que será criado, `-d` executa o container em segundo plano

### Buscar ip do container gerado do MySql

```
docker inspect <ID or name> | grep IPAddress
```

### Acessar banco de dados

```
mysql -h <IP> -P 3306 --protocol=tcp -u root -p
```

## Volume com MySQL

- Nos comandos abaixo será mostrado um exemplo de execução do docker volume utilizando o mysql

### Criar container para utilizar volume

```
docker run -e MYSQL_ROOT_PASSWORD=root --name mysql-vol -d mysql:5.7
docker volume ls
docker inspect mysql-vol
docker volume prune
```

> Inicia um container para utilizar o mysql, em seguida é listado todos os volumes existentes, depois faz a inspeção do container `mysql-vol` para ver informações sobre a sua localização, tipo de leitura, etc. O comando `prune` remove os volumes que não estão sendo utilizados. Por padrão será criado um volume automaticamente utilizando uma hash aleatoria.

### Criar volume

- A criação dos volumes gerá uma hash que pode ser confusa de ler, logo é possivel utilizar um nome para o volume

```
docker volume create mysql-db
docker run -d --name mysql-vol -e MYSQL_ROOT_PASSWORD=root -v mysql-db:/tmp/meus-volumes mysql
```

> O comando acima iniciliza um volume com o nome `mysql-db`, em seguida é criado um container que irá utilizar o volume criado alé de especificar o caminho para acessar o volume no container.

### Acessar o container criado acima

```
docker exec -it mysql-vol /bin/bash
```
