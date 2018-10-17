# 安装redis

1. 下载安装包

```cmd
wget http://download.redis.io/releases/redis-4.0.8.tar.gz
```

2. 解压到文件夹/usr/redis中

```cmd
mkdir -p /usr/redis
tar -xzf redis-4.0.8.tar.gz -C /usr/redis
```

3. 进入目录，安装

```cmd
cd redis-4.0.8.tar.gz
make
make install
```

4. 将可执行文件和配置文件拷贝到/usr/redis

```cmd
cd src
sudo cp redis-server  /usr/redis
sudo cp redis-benchmark /usr/redis
sudo cp redis-cli  /usr/redis
cd ..
sudo cp redis.conf  /usr/redis
cd /usr/redis
```

5. 运行和关闭redis服务器

```cmd
./redis-server redis.conf
./redis-cli shutdown
```

6. 远程连接

首先将redis服务器中的配置文件修改为

```conf
# 表明需要在后台运行
daemonize yes
# 设置信任的主机
bind 0.0.0.0
```

然后执行：

```cmd
redis-cli -h 10.170.63.180 -p 6379
```

7. 数据迁移

* 在要备份的redis上执行sync命令后停掉服务
* 停掉备份服务器的redis
* 将dump.rdb替换备份服务器的dump.rdb
* 重启服务。