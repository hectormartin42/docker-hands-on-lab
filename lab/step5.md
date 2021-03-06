While running a single container is useful, it is far more useful to be able to run multiple containers in tandem such that an entire application can be run. Docker makes this feature available through docker-compose.

Analyze the following `docker-compose.yml` file.

<pre class="file" data-filename="docker-compose.yml" data-target="replace">version: '3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "80:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:
</pre>

You can also get the contents from here: [https://github.com/Flux7Labs/docker-hands-on-lab/blob/master/lab/docker-compose.yml](https://github.com/Flux7Labs/docker-hands-on-lab/blob/master/lab/docker-compose.yml)

Now run this file as:
`docker-compose up -d`{{execute}}

You can view the containers using `docker ps` and see Wordpress running on the URL: https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/
