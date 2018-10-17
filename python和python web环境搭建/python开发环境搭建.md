# Ubuntu搭建Python环境

1. pip需要ssl环境 安装openssl* 
  
如果不安装的话，安装python时不会自动安装pip

```cmd
apt-get install openssl*
```

2. 下载python

```cmd
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
```

3. 解压下载的文件

```cmd
tar -zxvf Python-3.6.1.tgz
```

4. 创建安装的目录,最好自己创建一个，这样的话以后出了问题也能解决

```cmd
mkdir -p /usr/local/python3
```

5. 编译安装

```cmd
cd Python-3.6.1
./configure --prefix=/usr/local/python3
make && make install
```

6. 创建软连接，这一步是为了不必再设置path变量

```cmd
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3.6 /usr/bin/pip3
```

7. 测试一下是否安装成功

```cmd
python3 --version
pip3 --version
```

# Centos7安装python3环境

1. 安装工具yum-utils

```bash
$ sudo yum install yum-utils
```

2. 使用yum-builddep为Python3构建环境,安装缺失的软件依赖,使用下面的命令会自动处理.

```bash
sudo yum-builddep python
```

3. 下载Python3的源码包

```bash
$ curl -O https://www.python.org/ftp/python/3.5.0/Python-3.5.0.tgz
```

4. 编译安装

```bash
$ tar xf Python-3.5.0.tgz
$ cd Python-3.5.0
$ ./configure
$ make
$ sudo make install
```

5. 至此你已经在你的CentOS系统中成功安装了python3、pip3、setuptools，查看python版本

```bash
$ python3 -V
```

# centos7安装pip(python2环境)

```bash
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
```
