## docker-compose

docker-compose 使用 Yaml 文件定义、描述多个服务（容器），使用一条命令即可启动、停止多个服务；

## 安装

```
curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose
chmod +x /usr/bin/docker-compose
```

## 启动 docker-compose 中定义的服务

默认 docker-compose 命令会使用当前目录中命名为 `docker-compose.yml` 的描述文件。

```
docker-compose up -d
```

* up: 启动 docker-compose.yml 文件中定义的服务；
* -d: 后台方式运行

## 停止 docker-compose 中定义的服务

```
docker-compose stop
```

## 推荐阅读

https://docs.docker.com/compose/overview/
https://github.com/docker/compose/releases`
https://docs.docker.com/compose/compose-file/compose-file-v2/
