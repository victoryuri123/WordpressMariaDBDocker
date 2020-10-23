# WordpressMariaDBDocker
Wordpress na AWS com MariaDB

--- 1 passo ---

É necessário criar uma instância EC2 (t2.micro)
na AWS, EBS volume SSD de 30 GB e liberando
as portas SSH (22), HTTP (80) e HTTPS (443) e dar
launch para rodar a instância.

--- 2 passo ---

Após baixado a key, é necessário dar permissão
utilizando o comando CHMOD no terminal linux ,
conectar via SSH com a instância e estará dentro
do seu ec2.

Comandos utilizados:
- chmod 400 wptutorial
- ssh -i “wptutorial.pem”
ec2.user@00.000.000.000

--- 3 passo ---

Será necessário fazer a instalação do docker e o
docker-compose para orquestrar nossos
wordpress e o mariadb.

Comandos utilizados:
- sudo apt install docker
- sudo apt install docker-compose

--- 4 passo ---

Pós instação dos programas, criaremos um
arquivo de configuração .yaml utilizando o vim
para cetar os serviços a serem instalados
(wordpress e mariadb) e a integração entre eles.

Comandos utilizados:
- vim docker-compose.yaml

Wordpress + MariaDB

version: '2'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 80:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: db
    volumes:
      - wordpress:/var/www/html

  db:
    image: mariadb
    restart: always
    environment:
      MYSQL_DATABASE: db
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mariadb

volumes:
  wordpress:
  db:
  
  --- 5 passo ---
  
  Configurado o arquivo .yml, subiremos os
serviços e utilizando do dockerstats podemos
acompanhar os contêineres rodando. Só abrir o
navegador e inserir o IP que o wordpress estará
up.
Comandos utilizados:
- docker-compose up -d
- docker stats
  
