# Mavan常用操作

## 运行调试
```bash
pushd "C:\cncdr-1.0\dev\backend\app"
mvn clean -Djetty.port=8888 jetty:run
```

## 打包编译
```bash
pushd "C:\cncdr-1.0\dev\backend"
mvn clean install -Dmaven.test.skip=true
```


<plugin>
 <groupId>org.codehaus.mojo</groupId>
 <artifactId>exec-maven-plugin</artifactId>
 <executions>
	 <execution>
		 <id>----npm run build----</id>
		 <phase>generate-sources</phase>
		 <goals>
			<goal>exec</goal>
		 </goals>
		 <configuration>
			 <workingDirectory>${basedir}/../../frontend</workingDirectory>
			 <executable>npm</executable>
			 <arguments>
				 <argument>run</argument>
				 <argument>build</argument>
			 </arguments>
		 </configuration>
	</execution>
  </executions>
</plugin> 
