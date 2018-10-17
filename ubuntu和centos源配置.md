
# Ubuntu替换为西电源

1. 查看Ubuntu版本
* bionic (18.04 LTS)
* artful (17.10)
* zesty (17.04)
* yakkety (16.10)
* xenial (16.04 LTS)
* trusty (14.04 LTS)
* precise (12.04 LTS)
```bash
# 查看你的Ubuntu版本
lsb_release -a
```
2. 备份/etc/apt/sources.list
```bash
# 做好备份
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```
3. 修改/etc/apt/sources.list，以xenial为例，其它版本替换成相应版本号即可。
```cmd
deb http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial main restricted universe multiverse
deb-src http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial main restricted universe multiverse

deb http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-security main restricted universe multiverse

deb http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-updates main restricted universe multiverse

deb http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-backports main restricted universe multiverse

deb http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://linux.xidian.edu.cn/mirrors/ubuntu/ xenial-proposed main restricted universe multiverse
```
也可以直接下载
```bash
curl https://raw.githubusercontent.com/zhangzhongjun/MyDoc/master/sources-precise.list -o /etc/apt/sources.list
```
4. 更新源
```bash
sudo apt-get update
```

# Centos替换为西电源

1. 查看Centos的版本号

```bash
cat /etc/redhat-release
```

2. 备份

```bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

3. 修改配置文件（以cnetos7为例）

```bash
vi /etc/yum.repos.d/CentOS-Base.repo
```

```conf
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
baseurl=https://linux.xidian.edu.cn/mirrors/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-$releasever - Updates
baseurl=https://linux.xidian.edu.cn/mirrors/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
baseurl=https://linux.xidian.edu.cn/mirrors/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
baseurl=https://linux.xidian.edu.cn/mirrors/centos/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```

4. 生成缓存

```bash
yum makecache
```

# CentOS替换为阿里源

1. 加入文件夹

```bash
cd /etc/yum.repos.d
```

2. 备份旧的配置文件：

```bash
mv CentOS-Base.repo CentOS-Base.repo.bak 
```

3. 下载阿里源的文件

```bash
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo 
```

```bash
curl -o CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo 
```

4. 清理缓存

```bash
yum clean all
```

5. 重新生成缓存 

```bash
yum makecache
```
