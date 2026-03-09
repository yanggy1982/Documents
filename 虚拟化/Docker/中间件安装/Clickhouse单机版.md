
# Clickhouse单机安装

## 一、下载镜像

```shell
docker pull clickhouse/clickhouse-server
```

## 二、创建目录

```shell
mkdir -p ~/platform/data/clickhouse/config
mkdir -p ~/platform/data/clickhouse/data
mkdir -p ~/platform/data/clickhouse/logs
```

## 三、创建目录

### 1、启动临时容器

```shell
docker run -d \
  --name clickhouse-server \
  --ulimit nofile=262144:262144 \
  -p 8123:8123 \
  -p 9000:9000 \
  -p 9009:9009 \
  -e CLICKHOUSE_USER=admin \
  -e CLICKHOUSE_PASSWORD=admin123 \
  -e CLICKHOUSE_DEFAULT_ACCESS_MANAGEMENT=1 \
  -e TZ=Asia/Shanghai \
  clickhouse/clickhouse-server:25.4
```

### 2、复制配置文件到宿主机

```shell
docker cp clickhouse-server:/etc/clickhouse-server/config.xml ~/platform/data/clickhouse/config/config.xml
```

### 3、删除临时容器

```shell
docker rm -f clickhouse-server
```

## 四、修改配置

编辑 ~/platform/data/clickhouse/config/config.xml，主要改两个地方：

### 1、时区配置（重要）

找到 <timezone> 或添加以下配置：

<!-- 设置默认时区为上海，不设置的话时间会差 8 小时 -->
<default_time_zone>Asia/Shanghai</default_time_zone>

踩坑提醒：不配置时区，now() 函数返回的时间会是 UTC，查询结果和你预期的差 8 小时。问就是血泪教训。

### 2、Prometheus 监控端点

找到 <prometheus> 配置段，取消注释或添加：

```xml
<prometheus>
    <endpoint>/metrics</endpoint>
    <port>9363</port>
    <metrics>true</metrics>
    <events>true</events>
    <asynchronous_metrics>true</asynchronous_metrics>
    <status_info>true</status_info>
</prometheus>
```

## 五、正式启动

```shell
docker run -d \
  --name clickhouse-server \
  --ulimit nofile=262144:262144 \
  -p 8123:8123 \
  -p 9000:9000 \
  -p 9009:9009 \
  -p 9363:9363 \
  -v ~/platform/data/clickhouse/data:/var/lib/clickhouse \
  -v ~/platform/data/clickhouse/logs:/var/log/clickhouse-server \
  -v ~/platform/data/clickhouseconfig/config.xml:/etc/clickhouse-server/config.xml \
  -e CLICKHOUSE_USER=admin \
  -e CLICKHOUSE_PASSWORD=admin123 \
  -e CLICKHOUSE_DEFAULT_ACCESS_MANAGEMENT=1 \
  -e TZ=Asia/Shanghai \
  clickhouse/clickhouse-server

```


   


















