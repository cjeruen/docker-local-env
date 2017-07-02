## docker for youzan/zan

> 1. docker-compose 方式参考本项目下的 docker-compose.yml

> 2. 单独 dockerfile build 的方式

> `docker build -t zan_container .`

> `docker run -d -p 8030:8030 -v /host/zansrc:/zan --name docker_zan zan_container`

> 3. 本地 访问 localhost:8030 试试看

### php版本选择

> FROM php:7.1

或

> FROM php:5.6

### 配置文件  zan 扩展文件

```

// 1. 自行克隆 zan-extension 代码到对应目录
// 2. php_swoole.h 改了下 sockets 通不过
// 3. php.ini 我加入了 zan 的配置

https://github.com/youzan/zan
http://zanphpdoc.zanphp.io/config/phpini.html

COPY php.ini         /usr/local/etc/php/php.ini
COPY sources.list    /etc/apt/sources.list
COPY src/zan/zan-extension /usr/src/php/ext/zan
COPY php_swoole.h /usr/src/php/ext/zan/php_swoole.h

```


### 相关安装

```

// 注意格式  

RUN .......

```


### 运行相关

```

EXPOSE 8030

WORKDIR /zan

ENTRYPOINT ["php", "bin/httpd"]

```
