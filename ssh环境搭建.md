
# 开启SSH Server

1. 安装openssh-server

```bash
sudo  apt-get install openssh-server
```

2. 检查ssh服务开启状态

```bash
ps -s | grep ssh
```

3. 通过以下命令启动ssh服务

```cmd
service ssh start
/etc/init.d/ssh start
```

# 允许使用root账户ssh登录ubuntu

1. 激活ubuntu的root用户

重置root账户密码：

```cmd
sudo passwd root
```

根据提示，连续输入两次root账户的密码即可

2. 修改 root 密码

```bash
sudo passwd root
```

3. 以其他账户登录，通过 sudo nano 修改 /etc/ssh/sshd_config

```bash
vi /etc/ssh/sshd_config
```

4. 注释掉 #PermitRootLogin without-password，添加 PermitRootLogin yes
```bash
# Authentication:
LoginGraceTime 120
#PermitRootLogin without-password
PermitRootLogin yes
StrictModes yes
```
4. 重启ssh服务
```bash
service ssh restart
```

## 使用ssh登录远程服务器

打开cmd，输入如下的指令
```cmd
ssh -p6000 root@zzj.red
```

## 使用scp下载和上传文件

上传：打开cmd，输入如下的指令
```bash
# 文件
scp -P6000 F:\a.txt root@zzj.red:/root/a.txt
# 目录
scp -r -P6000 F:\aaa root@zzj.red:/root/aaa
```

下载：打开cmd，输入如下的指令
```bash
# 文件
scp -P6000 root@zzj.red:/root/b.txt F:\b.txt
# 目录
scp -r -P6000 root@zzj.red:/root/bbb F:\bbb
```




