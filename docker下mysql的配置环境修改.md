#Mac系统docker下mysql的配置环境修改<br>

##针对docker的mysql镜像在使用中会遇到的sql_mode问题

很多docker用户在使用mysql的5.7以上版本的容器会经常遇到关于sql_mode的问题，然而经过一番尝试，我发现在docker内的mysql镜像中通过安装vim等编辑器来直接修改配置文件的方法经常受阻，反而通过本地配置文件映射的方法一次成功，下面将陈述我的经验。
##配置步骤
###1.进入已建立的docker mysql5.7+版本容器
```
docker exec -it mysql(docker mysql name) /bin/bash
```
###2.打开docker容器内mysql配置文件
cat /etc/mysql/my.cnf
![avator](/Users/liyan/Desktop/WechatIMG2.jpeg)
可以看到两行：<br>
!includedir /etc/mysql/conf.d <br>
!includedir /etc/mysql/mysql.conf.d <br>
其中mysql.conf.d文件夹下的文件是我们要修改的mysql配置文件，但我们这里不修改它，是取其内容并改之，再在本地映射<br>
cat /etc/mysql/mysql.conf.d/mysqld.cnf
![avator](/Users/liyan/Desktop/WechatIMG3.jpeg)
###3.查看sql_mode
此时的配置文件内是没有sql_mode的，可以在mysql中输入“select @@sql_mode”并执行，取去除掉“ONLY_FULL_GROUP_BY”的部分，并在刚才的mysqld.cnf中加一行"sql_mode = 一串去除““ONLY_FULL_GROUP_BY”"的部分，复制全文
###4.本地配置文件
本地新建一个配置文件,我在本地/Users/liyan/mysql/conf目录下新建了一个名为mysqld.cnf的文件，vim打开后，粘贴刚才复制的内容<br>
![avator](/Users/liyan/Desktop/WechatIMG4.jpeg)
esc + :wq 退出保存
###5.重新在docker中拉去mysql5.7+版本的镜像
```
docker run -d -p 3306:3306 -v /Users/liyan/mysql/conf/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v /Users/liyan/database:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=123456 -e TZ="Asia/Shanghai" --name mysql mysql:5.7.20
```
-v /Users/liyan/mysql/conf/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf是本地配置文件对docker下配置文件的一个重新映射，重新连接本地数据库，成功