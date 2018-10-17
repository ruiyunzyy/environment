# linux安装tex

1. 下载texlive.iso

2. 挂载 iso并安装texlive2013
```bash
mount -o remount,rw /
sudo mount -t -iso9660 -o loop texlive2013-20130530.iso /mnt
cd /mnt/
sudo ./install-tl
```

3. 卸载iso的挂载盘

```bash
cd /
sudo umount /mnt/
```

4. 设置环境变量

在/etc/profile中添加
```bash
PATH=/usr/local/texlive/2013/bin/i386-linux:$PATH; export PATH
MANPATH=/usr/local/texlive/2013/texmf-dist/doc/man:$MANPATH; export MANPATH
INFOPATH=/usr/local/texlive/2013/texmf-dist/doc/info:$INFOPATH; export INFOPATH
```

使用如下命令使配置生效

```bash
source /etc/profile
```

5. 安装texmaker

```bash
sudo apt-get install texmaker
```