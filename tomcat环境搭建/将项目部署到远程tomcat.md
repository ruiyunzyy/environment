# 修改pom.xml

```xml
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
    <configuration>
        <url>http://localhost:8080/manager/text</url>
        <server>tomcat7</server>
        <path>/${project.artifactId}</path>
        <update>true</update>
    </configuration>
</plugin>
```

# 修改tomcat的配置文件

修改conf/server.xml文件，在port等于8080的Connector节点增加属性URIEncoding=”UTF-8”：

```xml
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443"
               URIEncoding="UTF-8" />
```

修改tomcat-users.xml文件，在tomcat-users节点中增加内容：

```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="account001" password="password001" roles="manager-gui,manager-script"/>
```


# 修改maven的配置文件

在maven安装目录下的conf文件夹中，找到settings.xml。在servers节点下面添加如下的内容

```xml
<server>
    <id>tomcat7</id>
    <username>account001</username>
    <password>password001</password>
</server>
```

这就是在tomcat的tomcat-users.xml文件中配置的用户和密码，这样执行maven插件的时候就能从此处取得对应的用户名和密码去tomcat上做操作了。

# 部署

```bash
$ mvn clean 
$ mvn package -U -Dmaven.test.skip=true 
$ mvn tomcat7:redeploy -Dmaven.test.skip=true 
```

# 其他命令

部署一个web war包

```bash
$ mvn tomcat:deploy	
```

重新加载web war包

```bash
$ mvn tomcat:reload	
```

启动tomcat

```bash
$ mvn tomcat:start
```

停止tomcat

```bash
$ mvn tomcat:stop
```
停止一个war包

```bash
$ mvn tomcat:undeploy
```

启动嵌入式tomcat ，并运行当前项目

```bash
$ mvn tomcat:run
```