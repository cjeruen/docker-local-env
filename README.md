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
