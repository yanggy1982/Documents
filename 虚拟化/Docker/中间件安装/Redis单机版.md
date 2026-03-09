
# Redis安装

## 1、单机版安装

### 一、下载镜像

```shell
docker pull docker.io/redis:6.2.14
```

### 二、创建目录

```shell
mkdir -p ~/platform/data/redis/conf
mkdir -p ~/platform/data/redis/data
```

### 三、下载配置文件并修改配置

修改配置文件，redis.conf内容如下：

```text
# 原本：
bind 127.0.0.1
protected-mode yes

# 修改为
# bind 127.0.0.1
protected-mode no # 禁用保护模式，实现远程连接
logfile "/data/redis.log" # 设置日志，和两个文件(data,redis.conf)一起挂载到宿主机
dir /data # 控制备份文件(包括rdb和aof存放在什么路径)，一同放在data文件夹下挂载到宿主机，将redis的备份文件持久化，保证重启容器之后，数据也不会丢失
appendonly yes # 开启aof备份(看自身情况进行修改)
requirepass yourpassword # 配置redis密码，这个是必要的，越复杂越好
```

### 四、启动容器

```shell
docker run -d --name redis -p 6379:6379 --restart=always -v ~/platform/data/redis/conf:/etc/redis/redis.conf -v ~/platform/data/redis/data:/data redis:6.2.14 redis-server /etc/redis/redis.conf  --appendonly yes
```

### 五、安装客户端工具

AnotherRedisDesktopManager

下载地址为：

https://github.com/qishibo/AnotherRedisDesktopManager/releases










