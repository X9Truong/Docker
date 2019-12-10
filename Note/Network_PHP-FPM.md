### Install docker php:7.3-fpm

`docker run -d --name C10 -h c-php -v /root/mycode:/home/mycode --network www-net php:7.3-fpm`

`docker exec -it name_container bash`

`cd /var/www/html`

```
vi index.html
<?php
        echo "Apache httpd"
		phpinfo();
```

* Run file

`php index.html`

`docker pull httpd`

`docker run --rm -v /root/mycode:/home/mycode httpd cp /usr/local/apache2/conf/httpd.conf /home/mycode` ## --rm delete container 

`docker run --network www-net --name c1-httpd -h httpd -p 9999:80 -v /root/mycode/:/home/mycode/ -v /root/mycode/httpd.conf:/usr/local/apache2/conf/httpd.conf httpd`

`docker pull mysql`


```
Mysql 8

- port 3306

- file config /etc/mysql.conf

[mysqld]
default-authentication-plugin=mysql_native_password

MYSQL_ROOT_PASSWORD=abc123
databases: /var/lib/mysql
```

`docker run --rm -v /mycode/:/home/mycode/ mysql cp /etc/mysql/my.cnf /home/mycode/`

`docker run -r MYSQL_ROOT_PASSWORD=abc123 -v /root/mycode/my.cnf:/etc/mysql/my.cnf -v /root/mycode/db/:/var/lib/mysql --name c-mysql mysql`

```
docker exec -it c-mysql bash                       #nhảy vào container
mysql -uroot -pabc123                              #kết nối vào MySQL Server

#Từ dấu nhắc MySQL, Tạo một user tên testuser với password là testpass

CREATE USER 'testuser'@'%' IDENTIFIED BY 'testpass';

#Tạo db có tên db_testdb
create database db_testdb;

#Cấp quyền cho user testuser trên db - db_testdb
GRANT ALL PRIVILEGES ON db_testdb.* TO 'testuser'@'%';
flush privileges;

show database;            #Xem các database đang có, kết quả có db bạn vừa tạo
exit;                     #Ra khỏi MySQL Server
```








