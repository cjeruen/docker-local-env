# docker-local-env
docker for local php env


### php扩展容器
```
// 1. 构建镜像
$ docker-compose build
// 2. 启动容器
$ docker-compose up -d
// 3. 进入容器
$ docker exec -it php_ext_v5 /bin/bash

// 编译扩展 重启 php-fpm  laosiji 参考 .bashrc 别名
root@local_php_ext_v5:/var/www/html# laosiji
```


### Mysql 主从

```
1. local_mysql_master

> GRANT REPLICATION SLAVE ON *.* to 'hui'@'local_mysql_slave' identified by 'hui';

> show master status;   // Position: 444

2. local_mysql_slave

change master to 
master_host='local_mysql_master',
master_port=3306,
master_user='hui',
master_password='hui',
master_log_file='mysql-bin.000003',
master_log_pos=444;

start slave;

```

### Zan* Docker

项目移至

- https://github.com/cjeruen/zan-docker
