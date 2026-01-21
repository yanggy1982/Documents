
# Oceanbase数据库安装

## 1、Docker安装

### 1.1、创建网路

```shell
docker network create --subnet=192.168.0.0/16 tongtong-net
```

### 1.2、查看创建的网络

```shell
docker network ls
```

### 1.3、创建容器

```shell
docker run -p 2881:2881 --name obstandalone -e MODE=NORMAL -e OB_TENANT_PASSWORD=Happy123# -d quay.io/oceanbase/oceanbase-ce --memory 5g --network tongtong-net --ip 192.168.0.2 -e TZ=Asia/Shanghai --restart=always
```