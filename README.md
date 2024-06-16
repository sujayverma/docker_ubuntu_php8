# Php Development Enivironment on Ubuntu OS #

PHP 8.2 new development environment based on docker

### What are the components used in this environment? ###

Only Important dependencies are listed here

* OS [Ubuntu 22.04] : A Base operating system for this current development environment
* Apache2
* PHP 8.2
* MySQL 8.0.26
* Phpmyadmin 4.4.15
* Composer 2.1.9
* Phpunit 9.5.10
* Xdebug 3.1.0

### Prerequisites  ###
* Docker Daemon
* Docker Client
* Docker Compose
* Docker user with root privilege
* Git

### Some Optional Settings ###

All these settings are optional but if you want then you can override the default settings

* Set your timezone for PHP in `Dockerfile.ubuntu` by default timezone is `'Asia/Kolkata'`
* Set your timezone for MYSQL in `docker-compose.yml` by default timezone is `'Asia/Kolkata'`
* Set your database name in `docker-compose.yml` file `[MYSQL_DATABASE: docker_php]` default database name is `'cpcms'`
* Set your database username in `docker-compose.yml` file `[MYSQL_USER: admin]` defalt database user is `'admin'`
* Set your database user's password in `docker-compose.yml` file `[MYSQL_PASSWORD: admin]` default password is `'admin'`
* Set your database root user password `[MYSQL_ROOT_PASSWORD: admin]` default root user's password is `'admin'`

### Installation guidelines ###

* Go inside the docker-dev-env-php directory: $ 
* Run command: `$ docker-compose up --build`

### Verify the Environment ###

* Once the above command run successfully you can open browser and type: http://localhost
* To access phpmyadmin open browser and type: http://localhost/phpmyadmin

### Backup/Resotre mysql data from dump file ###



### Connection of MySQl from workbench or sqlyog ###

If with `host=localhost` unable to connect with mysql then in that case first open browser and hit `http://localhost` and note the ip address in `REMOTE_ADDR` in my case the ip address is `172.18.0.1` which is the mysql host ip.

* host = `REMOTE_ADDR IP` / `localhost`
* user = `YOUR_MYSQL_USER`
* password = `YOUR_MYSQL_PASSWORD`
* port = `3306`

### Apache virtual host setup (Optional) ###

By default the container is open for the port 80, 443 and from port 8080 to 8085. You can set your virtual host like one already setup in docker/posts.conf file for port 8080.

You have to add `Listen YOUR_PORT_NO` and the following virtualhost setup in apache config `ports.conf` file.

```
<VirtualHost *:YOUR_PORT_NO>

  <Directory /var/www/html/YOUR_PROJECT_FOLDER>

    Options Indexes FollowSymLinks MultiViews

    AllowOverride All

    Require all granted

  </Directory>

  ServerAdmin webmaster@localhost

  DocumentRoot /var/www/html/YOUR_PROJECT_FOLDER

  ErrorLog ${APACHE_LOG_DIR}/error.log

  CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

NOTE: `YOUR_PORT_NO` and `YOUR_PROJECT_FOLDER` should be replace by correct one

### Additional Commands ###

Once you have used the command `$ docker-compose up --build` and every thing works fine then no need to use this command again until you did not modified any thing in `Dockerfile.ubuntu` or `docker-compose.yml` file

* To remove containers: `$ docker-compose down` (this command must run from root folder path .i.e. centos7)
* To Build the image: $ `docker-compose build` (this command must run from root folder path .i.e. centos7)
* To create the containers: `$ docker-compose up` (this command must run from root folder path .i.e. centos7)
* To go inside my_php8 container: `$ docker exec -it my_php8 bash`
* To go inside db container: $ `docker exec -it my_db_php8 bash`


### PHP ini settings (Optional) ###
You can customize your php settings as per your need the file path is `docker/php.ini`

### Apache logs ###
You can find any type of error in logs file its path is `docker/logs`

### Author ###

* Sujay Barma
* sujay.barma@indusnet.co.in
