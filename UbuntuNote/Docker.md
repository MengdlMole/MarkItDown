# Docker命令

## 镜像加速器

```配置镜像加速器
# 配置镜像加速器
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://***.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 用户组

```将用户添加到docker组
# 将用户添加到docker组
sudo groupadd docker # 创建名叫docker的组
sudo gpasswd -a 用户名 docker # 添加用户
sudo gpasswd -d 用户名 docker # 删除用户
newgrp docker # 更新组
```

## 服务相关命令

```启动docker
# 启动docker
systemctl start docker
```

```查看docker状态
# 查看docker状态
systemctl status docker
```

```停止docker
# 停止docker
systemctl stop docker 
```

```重启docekr
# 重启docekr
systemctl restart docker
```

```开机启动docker
# 开机启动docker
systemctl enable docker
```

## 镜像相关命令

```查看镜像
# 查看镜像
docker images
docker images -q # 查看镜像ID
```

```搜索镜像
# 搜索镜像
docker search 镜像名
```

```下载镜像
# 下载镜像
docker pull 镜像名 # 下载默认版本
docker pull 镜像名:版本号
```

```删除镜像
# 删除镜像
docker rmi 镜像ID
docker rmi 镜像名:版本号
docker rmi 'docker images -q' # 删除全部镜像
```

## 容器相关命令

```创建容器
# 创建容器
docker run -it --name=容器名 镜像名:版本号 /bin/bash
docker run -id --name=容器名 镜像名:版本号
exit # 退出容器
```

```参数
# 参数
docker run --help
-i # Keep STDIN open even if not attached
-t # Allocate a pseudo-TTY
-d # Run container in background and print container ID (退出后不会关闭)
```

```-it和-id
-it创建的容器创建后直接进入容器，退出后容器自动关闭（交互式容器）；
-id创建的容器在后台运行，退出后不会自动关闭（守护式容器）；
```

```查看容器
# 查看容器
docker ps # 查看正在运行的容器
docker ps -a # 查看全部容器
docker ps -aq # 查看全部容器ID
```

```进入容器
# 进入容器
docker exec -it 容器名 /bin/bash
# 使用exec进入的容器退出时不会关闭
```

```启动容器
# 启动容器
docker start 容器名
```

```停止容器
# 停止容器
docker stop 容器名
```

```删除容器
# 删除容器
docker rm 容器名
docker rm 容器ID
docker rm 'docker ps -aq' 删除全部容器
# 不能删除正在运行的容器
```

```查看容器信息
# 查看容器信息
docker inspect 容器名
```

## 数据卷

```创建容器时使用-v参数设置数据卷
# 创建容器时使用-v参数设置数据卷
docker run ... -v 宿主机目录（文件）:容器内目录（文件） ...
# 绝对路径
# 目录不存在会自动创建
# 可以挂在多个数据卷
```

```数据卷容器
# 数据卷容器
# 1. 创建启动数据卷容器
docker run -it --name=数据卷容器名 -v /volume ubuntu:latest /bin/bash
# 2. 创建其他启动容器，使用--volumes-from参数设置
docker run -it --name=容器名1 --volumes-from 数据卷容器名 ubuntu:latest /bin/bash
docker run -it --name=容器名2 --volumes-from 数据卷容器名 ubuntu:latest /bin/bash
```
