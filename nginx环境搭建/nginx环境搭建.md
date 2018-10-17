# nginx的使用

# nginx和tomcat的区别

* Apache/Nginx应该被称为’http server’

* Tomcat则是一个’Application Server‘，或者更加准确的说，是一个‘servlet /JSP’应用的容器

一个 HTTP Server 关心的是 HTTP 协议层面的传输和访问控制，所以在 Apache/Nginx 上你可以看到代理、负载均衡等功能。客户端通过 HTTP Server 访问服务器上存储的资源（HTML 文件、图片文件等等）。通过 CGI 技术，也可以将处理过的内容通过 HTTP Server 分发，但是一个 HTTP Server 始终只是把服务器上的文件如实的通过 HTTP 协议传输给客户端。

而Application Server，则是一个应用执行的容器。它首先需要支持开发语言的 Runtime（对于 Tomcat 来说，就是 Java），保证应用能够在应用服务器上正常运行。其次，需要支持应用相关的规范，例如类库、安全方面的特性。对于 Tomcat 来说，就是需要提供 JSP/Sevlet 运行需要的标准类库、Interface 等。为了方便，应用服务器往往也会集成 HTTP Server 的功能，但是不如专业的 HTTP Server 那么强大，所以应用服务器往往是运行在 HTTP Server 的背后，执行应用，将动态的内容转化为静态的内容之后，通过 HTTP Server 分发到客户端。

# 应用场景

1. http服务器：nginx是一个http服务，可以独立提供http服务，可以做网页静态服务器
2. 虚拟主机：可以实现在一台服务器中虚拟出多个网站
3. 反向代理：nginx可以将请求转发给不同的应用服务器


# ubuntu下部署nginx环境

## 通过apt安装

```bash
sudo apt-get update
sudo apt-get install nginx
```

## 调整防火墙设置

1. 查看防火墙的应用列表
```bash
$ sudo ufw app list

Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

As you can see, there are three profiles available for Nginx:

* Nginx Full: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
* Nginx HTTP: This profile opens only port 80 (normal, unencrypted web traffic)
* Nginx HTTPS: This profile opens only port 443 (TLS/SSL encrypted traffic)

2. 允许应用通过防火墙
```bash
sudo ufw allow 'Nginx HTTP'
```

3. 查看防火墙的状态
```bash
sudo ufw status

Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

4. 禁止使用防火墙
```bash
sudo ufw disable
```

## 开启服务

```bash
#ubuntu 14
service nginx start
# ubuntu 15 or higher
systemctl status nginx
```

## 在服务器上查看

```bash
localhost:80
```

# centos下部署nginx环境

1. 安装依赖包

```bash
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel pcre
```

2. 安装nginx

```bash
rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
yum install nginx
```

3. 启动nginx

```bash
systemctl start nginx
```

> 使用这种方式安装好之后：
> 配置文件在/etc/nginx中
> nginx存放在/usr/sbin中，这样就不必再配置路径了
> 访问日志在/var/log/nginx/access.log
> 错误日志在/var/log/nginx/error.log
> 静态文件存放在/usr/share/nginx
> pid存放在/var/run/nginx.pid


# 命令


启动nginx的服务器

```bash
nginx
```

显示nginx服务器的版本号

```bash
nginx -v
```

## 配置文件

> 有关配置文件的语法，请参考本仓库下的nginx.conf

测试配置是否有语法错误

```bash
nginx -t
```

设置配置文件

默认为  {nginx的安装目录}/conf/nginx.conf

```bash
nginx -c nginx.conf的路径
```

## 发送信号


快速关闭nginx的服务器

```bash
nginx -s stop
```

优雅地关闭nginx的服务器

```bash
nginx -s quit
```

重新加载配置

```bash
nginx -s reload
```

重新打开日志文件

```bash
nginx -s reopen
```
