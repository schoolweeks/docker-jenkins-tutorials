## 基于 Linux 操作系统安装 Docker

```
wget https://download.docker.com/linux/static/stable/x86_64/docker-17.12.1-ce.tgz
tar xvf docker-17.12.1-ce.tgz -C /tmp/
cp -i /tmp/docker/docker* /usr/bin/
chmod +x /usr/bin/docker*
```

https://download.docker.com/linux/static/stable/x86_64/

## 创建 docker 用户及用户组

dockerd 依赖 docker 用户组，将 unix 套接字（unix:/var/run/docker.sock）设置为 docker 组可读;

```
groupadd docker
useradd -g docker -s /sbin/nologin docker

# 此处为了方便 Jenkins 官方镜像访问 docker 程序，特设置 docker 用户及组 ID 为 1000
groupadd -g 1000 -o docker
useradd -u 1000 -o -g docker -s /sbin/nologin docker
```

## 拷贝 systemd 服务文件，启动 docker 程序

```
cp -i docker.service /usr/lib/systemd/system/
cp -i docker.socket /usr/lib/systemd/system/
systemctl daemon-reload
systemctl start docker
```

## Docker 中国官方镜像加速

由于 docker 默认访问位于美国的 Docker Hub 公有仓库下载镜像速度很慢，通过使用 Docker 中国官方镜像加速，中国区用户能够快速访问最流行的 Docker 镜像，私有镜像仍需要从美国镜像库中拉取；

**使用 docker 中国镜像仓库手动拉取镜像**

Docker 中国官方镜像加速可通过 registry.docker-cn.com 访问

手动拉取镜像示例

```
docker pull registry.docker-cn.com/nginx:1.14
```

**配置 docker 加速镜像**

修改 /etc/docker/daemon.json 文件并添加上 registry-mirrors 键值

```
vim /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

配置好 docker 加速镜像后，需要重新启动 docker 服务：

```
systemd restart docker
```

重启 docker 后，在拉取镜像将不需要输入镜像加速的地址，直接输入 docker 镜像的名称及标签(TAG)即可拉取镜像（dockerd 程序将自动后后台选择镜像加速地址下载镜像）；

```
docker pull nginx:1.14
```

https://www.docker-cn.com/registry-mirror

## 推荐阅读

**systemd**

http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html

