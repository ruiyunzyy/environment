# 拷贝程序

将程序拷贝到/root下

# 创建虚拟环境

```bash
$ cd /root/QJCX_YSBH
$ virtualenv --no-site-packages django
$ source django/bin/activate
[django]$ pip3 install -r requirements.txt
```

```bash
[django]$ deactivate
$ ...
```

# 处理静态文件

```bash
mkdir -p /var/www/QJCX_YSBH/
sudo chmod 777 /var/www/QJCX_YSBH
cd /var/www/QJCX_YSBH/
mkdir static
```

这里/root/QJCX_YSBH/QJCX_YSBH/settings.py中的部分设置如下

```python
DEBUG=False
ALLOWED_HOSTS = ['*']
STATIC_URL = '/static/'

# python manage.py collectstatic 将收集所有静态文件到STATIC_ROOT指定目录
STATIC_ROOT = '/var/www/QJCX_YSBH/static/'

# 设置静态文件查找目录
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, "static"),
)

# FileSystemFinder 在文件系统里搜索STATICFILES_DIRS指定目录。默认不包含任何目录
# AppDirectoriesFinder 是默认查找器中的一个，它会在每个 INSTALLED_APPS 中指定的应用的子文件中寻找名称为 static 的特定文件夹
STATICFILES_FINDERS = (
    "django.contrib.staticfiles.finders.FileSystemFinder",
    "django.contrib.staticfiles.finders.AppDirectoriesFinder"
)
```

```bash
[django]$ python manage.py collectstatic
```

# uwsgi

```bash
pip install uwsgi
```

创建uwsgi.ini，在/root/QJCX_YSBH/QJCX_YSBH/uwsgi.ini下

将以下内容填入uwsgi.ini文件，项目名和目录请修改为自己的项目。

```ini
[uwsgi]
# Django-related settings
# Django项目本地端口
socket = :8000
# 项目根目录位置
chdir = /root/QJCX_YSBH/
# wsgi.py文件在项目的中的相对位置
wsgi-file = /QJCX_YSBH/wsgi.py
module =QJCX_YSBH.wsgi
# 进程设置，无需变动
# master
master = true
# maximum number of worker processes
# 启动4个uwsgi进程
processes = 4
# ... with appropriate permissions - may be needed
# chmod-socket    = 664
# clear environment on exit
vacuum = true
#进程号
pidfile=uwsgi.pid
#日志文件
daemonize=uwsgi.log
```

uwsgi在哪个目录启动，就会在哪个目录生成uwsgi.pid和uswgi.log文件。 
启动：uwsgi --ini uwsgi.ini 
停止：uwsgi --stop uwsgi.pid 
重启：uwsgi --reload uwsgi.pid 
强制停止：killall -9 uwsgi 
这里我们启动uwsgi服务，可以通过ps -ef | grep uwsgi看到已经有四个uwsgi服务启动。

------------------------------------------------------------------------------------
在修改了python源文件之后，需要重启uwsgi

下面是重启uwsgi的脚本

```bash
$ cat /root/QJCX_YSBH/QJCX_YSBH/uwsgi.pid
15742
$ kill -9 15742;
$ source /root/QJCX_YSBH/django/bin/activate
$ uwsgi --ini /root/QJCX_YSBH/QJCX_YSBH/uwsgi.ini
$ nginx -s reload;
```

# nginx

安装nginx请参考仓库 prepareenvironment

修改/etc/nginx/conf/中打开nginx.conf，加入以下内容

```bash
server {
    listen 8996; #暴露给外部访问的端口
    server_name localhost;
        charset utf-8;
    location / {
        include uwsgi_params;
        # 这里的8000对应于uwsgi.ini中的端口
        uwsgi_pass 127.0.0.1:8000; #外部访问8996就转发到内部8000
    }
    location /static/ {
        alias /var/www/QJCX_YSBH/static/; #项目静态路径设置
    }
}
```

执行./nginx -t命令先检查配置文件是否有错，没有错就执行以下命令：

```bash
$ ./nginx
```


终端没有任何提示就证明nginx启动成功，可以通过链接查看nginx是否启动成功:
http://192.168.1.111:8996 （请将该ip替换成你的服务器ip）

# 参考文献

https://blog.csdn.net/weixin_39198406/article/details/79277580

https://www.cnblogs.com/levelksk/p/7921066.html

