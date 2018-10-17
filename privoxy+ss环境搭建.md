# 安装ShadowSocks


1. 安装pip（在python2环境下即可）

```bash
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
```

2. 安装shadowsocks

```bash
pip install shadowsocks
```

安装成功之后，在/bin下面有sslocal和ssserver

3. 编写配置文件

```bash
vi /etc/shadowsocks.json
```

```
{
    "server":"your_server_ip",      #ss服务器IP
    "server_port":your_server_port, #端口
    "local_address": "127.0.0.1",   #本地ip
    "local_port":1080,              #本地端口
    "password":"your_server_passwd",#连接ss密码
    "timeout":300,                  #等待超时
    "method":"rc4-md5",             #加密方式
    "fast_open": false,             # true 或 false。如果你的服务器 Linux 内核在3.7+，可以开启 fast_open 以降低延迟。开启方法： echo 3 > /proc/sys/net/ipv4/tcp_fastopen 开启之后，将 fast_open 的配置设置为 true 即可
    "workers": 1                    # 工作线程数
}
```

4. 后台运行

```bash
nohup sslocal -c /etc/shadowsocks.json
```


# 使用yum安装privoxy

```bash
yum install privoxy
```

# 使用源码安装privoxy
1. 下载压缩包

```bash
curl -o privoxy.tar.gz https://nchc.dl.sourceforge.net/project/ijbswa/Sources/3.0.26%20%28stable%29/privoxy-3.0.26-stable-src.tar.gz
```

2. 解压

```bash
tar -zxvf privoxy.tar.gz
```

3. 创建用户

```bash
useradd privoxy
```

4. 构建

```bash
autoheader & autoconf
```

5. 配置

```bash
./configure
```

6. 在上诉过程中发生错误，原因是没有安装zlib，下面来安装zlib

```bash
yum install zlib-devel
yum install zlib
```

7. 安装

```bash
make
make install
```

8. 安装成功之后会弹出如下所示的提示

```bash
The Privoxy configuration files have been installed in /usr/local/etc/privoxy
```

9. 修改配置文件

```bash
vi /usr/local/etc/privoxy/config
在命令行模式下输入 /listen-address
点击n查找下一个，直到找到listen-address 127.0.0.1:8118，保证这一句话没有被注释

在命令行模式下输入 /forward-socks5t
点击n查找下一个，直到找到/forward-socks5t / 127.0.0.1:1080 .
保证这一句话没有被注释
```

10. 启动

```bash
privoxy --user privoxy /usr/local/etc/privoxy/config

或者

service privoxy start
```

# 如何翻墙及翻墙的检测

1. 打开ss

```bash
nohup sslocal -c /etc/shadowsocks.json
```

2. 打开privoxy

```bash
service privoxy start
```

3. 设置代理

```bash
export http_proxy=http://127.0.0.1:8118
export https_proxy=http://127.0.0.1:8118
```

4. 检测

```bash
curl httpbin.org/ip
或者
curl ip.gs
```

如果输出的ip是你自己代理服务器的ip，则说明翻墙成功

# 参考资料

https://www.jianshu.com/p/824912d9afda

https://www.cnblogs.com/jiangtu/p/6877776.html

