
# Ubuntu中的tomcat


# Centos下安装tomcat

1. 下载apache-tomcat-8.5.34.tar.gz

https://tomcat.apache.org/download-80.cgi

2. 解压

```bash
$ tar -zxvf apache-tomcat-8.5.13.tar.gz
```

3. 开放8080端口

```bash
$ firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

说一下这一句的意思吧，因为centos7 已经更改了防火墙策略，所以使用这种方式来打开端口

--zone #作用域

--add-port=8080/tcp #添加端口，格式为：端口/通讯协议

--permanent #永久生效，没有此参数重启后失效

重启防火墙：

```bash
$ firewall-cmd --reload
```

4. 运行

```bash
cd /root/apache-tomcat-8.5.34
./startup.bat
```

5. 浏览器访问

# 关闭和打开服务器

1. 先切换到：cd usr/local/tomcat5/bin
2. ./startup.sh 打开服务器
3. ./shutdown.sh 关闭服务器

# 日志文件

tomcat启动时的报错日志太过简单，不方便排查问题，这时，可以在项目的classes下新增一个文件logging.properties

内容如下：

```prop
handlers = org.apache.juli.FileHandler, java.util.logging.ConsoleHandler 
org.apache.juli.FileHandler.level = FINE    
org.apache.juli.FileHandler.directory = ${catalina.base}/logs    
org.apache.juli.FileHandler.prefix = error-debug.      
java.util.logging.ConsoleHandler.level = FINE    
java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter   
```

# 实时监控日志

查看tomcat日志

1. 先切换到：

```bash
cd usr/local/tomcat5/logs
```

2. 运行

```bash
tail -f catalina.out
```

3. 这样运行时就可以实时查看运行日志了
