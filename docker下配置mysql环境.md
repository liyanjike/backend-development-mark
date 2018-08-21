#docker下配置mysql环境
```
docker run -d -p 3306:3306 -v /Users/liyan/mysql/conf/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v /Users/liyan/database:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=123456wl --name mysql mysql:5.7.20
```