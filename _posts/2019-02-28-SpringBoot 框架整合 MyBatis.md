---
layout:     post
title:      SpringBoot 框架整合 MyBatis
subtitle:   spring-boot、MyBatis
date:       2019-02-28
author:     BY
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - SpringBoot
    - 开发利器
    - JAVA
---

# SpringBoot 框架整合 MyBatis
>本文讨论使用 mybatis-spring-boot-starter 的方式整合进 spring-boot 框架中
>
>本文也只详细讨论基于 xml 的配置，基于注解的方式比 xml 要简单，不再做详细讲解。

### 1、将 MyBatis 加入 pom.xml 配置
```
	<dependency>
	    <groupId>org.mybatis.spring.boot</groupId>
	    <artifactId>mybatis-spring-boot-starter</artifactId>
	    <version>1.3.1</version>
	</dependency>
```

```
    此文章转自：http://www.spring4all.com/article/320
    如果您有更好的文章推荐，请投稿可以投递到博主邮箱:2627045617@qq.com
```