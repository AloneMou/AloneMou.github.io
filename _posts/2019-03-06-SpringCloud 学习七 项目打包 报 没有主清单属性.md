---
layout:     post
title:      SpringCloud 学习七 项目打包 报 没有主清单属性
subtitle:   SpringCloud
date:       2019-03-06
author:     BY
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - SpringCloud
    - JAVA
    - MAVEN
---

# SpringCloud 学习七 项目打包 报 没有主清单属性

项目通过MVN打包，发现打包的文件很小,大概几十KB，
估计打包有问题，执行JAVA -JAR 的时候发现果然报错，报没有主清单属性，网上找了一堆，都说加

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	        </plugin>
	    </plugins>
	</build>


>加了之后还是报一样的错误，终于在有一个网上找到

	<build>
	    <plugins>
	        <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
	            <executions>
	                <execution>
	                    <goals>
	                        <goal>repackage</goal>
	                    </goals>
	                </execution>
	            </executions>
	        </plugin>
	        <plugin>
	            <groupId>org.apache.maven.plugins</groupId>
	            <artifactId>maven-compiler-plugin</artifactId>
	            <configuration>
	                <source>1.8</source>
	                <target>1.8</target>
	            </configuration>
	        </plugin>
	    </plugins>
	</build>

这样加了以后，生成的JAR包有40多M,把项目的一些依赖包都加载进来了，这样打包后的文件就可以直接用java -jar 执行了

--------------------- 
作者：shrek11 

来源：CSDN 

原文：[https://blog.csdn.net/shrek11/article/details/86594617](https://blog.csdn.net/shrek11/article/details/86594617) 

版权声明：本文为博主原创文章，转载请附上博文链接！


	分享文档，经供参考。切勿用于商业用途。
    如果你有好的文章可以投递到博主邮箱:2627045617@qq.com

