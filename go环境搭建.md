# Centos下安装GO环境

1. 下载安装包

官网为：https://studygolang.com/dl

```bash
wget https://studygolang.com/dl/golang/go1.11.linux-amd64.tar.gz
```

2. 解压到指定目录

```bash
tar -C /usr/local -xzf go1.11.linux-amd64.tar.gz
```

3. 配置环境变量

```bash
vi /etc/profile

export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin

source /etc/profile
```

4. 验证

```bash
go version
```