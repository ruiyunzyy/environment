# 引入打war包的插件

将所有的依赖，资源文件，类等都打包到一个压缩文件中

```xml
 <plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-war-plugin</artifactId>
	<version>3.2.0</version>
	<configuration>
		<!-- 这里改变了Exploded的输出路径-->
		<webappDirectory>${project.basedir}/target/artifacts/QWSS Exploded</webappDirectory>
	</configuration>
</plugin>
```


# 打包

```bash
$ mvn compile war:war
$ mvn compile war:exploded
```