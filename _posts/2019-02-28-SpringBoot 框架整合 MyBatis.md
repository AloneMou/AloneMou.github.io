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
    - MyBatis
---

# SpringBoot 框架整合 MyBatis
>本文讨论使用 mybatis-spring-boot-starter 的方式整合进 spring-boot 框架中
>
>本文也只详细讨论基于 xml 的配置，基于注解的方式比 xml 要简单，不再做详细讲解。



**SpringBoot2.x的Maven依赖配置：**

	 <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.6.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

### 1、将 MyBatis 加入 pom.xml 配置
    <dependency>
	    <groupId>org.mybatis.spring.boot</groupId>
	    <artifactId>mybatis-spring-boot-starter</artifactId>
	    <version>1.3.1</version>
	</dependency>

### 2、application.yml 配置
	spring:
  	  datasource:
		driver-class-name: com.mysql.jdbc.Driver
 		url: jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf-8
    	username: 用户名
    	password: 密码

	server:
	  port: 8080

	mybatis:
	  config-location: classpath:config/mybatis-config.xml
	  mapper-locations: classpath:mapper/*.xml

MyBatis 配置项解读：

     config-location：指定 MyBatis 主配置文件的位置
     mapper-locations：指定 mapper 文件的位置。如果在项目中你的 mapper 文件是按目录来放置，那么对应的配置就变成：mapper-locations: classpath:mapper/*/*.xml
这时候假设我们的 resources 结构是这样的：

    |-resources
	|--config
	|---application.yml
	|---mybatis-config.xml
	|--mapper
	|---CityMapper.xml

### 3、mybatis-config.xml 配置
    <?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE configuration
	        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
	        "http://mybatis.org/dtd/mybatis-3-config.dtd">
	<configuration>
	    <typeAliases>
	        <package name="com.mybatis.domain"/>
	    </typeAliases>

	    <!--<mappers>-->
	        <!--<mapper resource="sample/mybatis/mapper/CityMapper.xml"/>-->
	        <!--<mapper resource="sample/mybatis/mapper/HotelMapper.xml"/>-->
	    <!--</mappers>-->
	</configuration>
这个配置见仁见智，在它里面我就配置了一个 <code>typeAliases</code>。不了解的同学可以移步文档查看相关解释。

你也可以把mapper配置在此处，有多少个mapper就配置多少次,我们已经在application.yml中批量指定了就很方便，就不用在此处一个个写。

### 4、接下来就是业务代码部分了
这时候假设我们的 resources 结构是这样的：

   	|-com.mybatis
	|--controller
	|---CityRestController.java (控制器)
	|--domain
	|---City.java (实体类)
	|--mapper
	|---CityMapper.java (mybatis的mapper)
	|--service
	|---CityService.java (service 接口)
	|---CityServiceImpl.java (service 实现)
	|--MyApplication.java (入口)

首先我们定义城市这个实体类：

	public class City implements Serializable {
	    private static final long serialVersionUID = 1L;
	
	    private Long id;
	
	    private Long provinceId;
	
	    private String cityName;
	
	    ....此处省略getter/setter方法
	}

接着我们来定义mapper：

	//@Mapper
	public interface CityMapper {
	
	    City findByProvinceId(Long provinceId);
	
	    List<City> findAll();
	}
定义这个 mapper 的作用是用来跟数据库进行交互的。

请注意，这里我把 <code>@Mapper</code> 注解给注释掉了，大家先把这个注释打开，待会再来解释。

另外，如果你想使用注解的方式来操作数据库，那么可以这样来定义 mapper：

	//@Mapper
	public interface CityMapper {
	    @Select("select * from city where province_id = #{provinceId}")
	    // 返回结果实体属性与数据库字段转换
	    @Results({
	            @Result(property = "provinceId", column = "province_id"),
	            @Result(property = "cityName", column = "city_name")
	    })
	    City findByProvinceId(@Param("provinceId") Long provinceId);
	}
>对于选择使用注解还是使用 xml 的方式，大家可以灵活选择，比如简单的语句可以使用注解，复杂的语句使用 xml，当然，还是需要跟团队保持一致。

**还记得我们 resources 的结构吗？**

里面有一个mapper目录，我们配置了在这个目录里面寻找 mapper 文件。

这里我定义了一个 <code>CityMapper.xml</code> 文件，用来跟数据库进行交互：

	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper
	        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	<mapper namespace="com.mybatis.mapper.CityMapper">

	    <resultMap id="BaseResultMap" type="com.mybatis.domain.City" >
	        <result column="province_id" property="provinceId" />
	        <result column="city_name" property="cityName" />
	    </resultMap>

	    <select id="findByProvinceId" resultMap="BaseResultMap">
	        select * from city where province_id = #{provinceId}
	    </select>

	    <select id="findAll" resultMap="BaseResultMap">
	        select * from city
	    </select>
	</mapper>

文件解读：
	<ul>
		<li>namespace 属性用于跟咱们业务中的那个 mapper 进行关联</li>
		<li>resultMap 标签用来定义字段映射和结果字段返回类型</li>
		<li>select 中的 id 属性用来跟咱们业中 mapper 的方法进行关联，查询到的结果就会返回给该方法</li>
		<li>
		<code>#{}</code>是占位符，表示需要动态获取的数据</li>
	</ul>

**最后定义 service 来处理咱们的业务：**

	public interface CityService {
	
	    City getByProvinceId(Long provinceId);
	
	    List<City> getAll();
	
	}
>

	@Service
	public class CityServiceImpl implements CityService {
	
	    @Resource
	    private CityMapper cityMapper;
	
	    @Override
	    public City getByProvinceId(Long provinceId) {
	        return cityMapper.findByProvinceId(provinceId);
	    }
	
	    @Override
	    public List<City> getAll() {
	        return cityMapper.findAll();
	    }
	}

**在controller里面进行验证：**

	@RestController
	@RequestMapping("/api")
	public class CityRestController {
	
	    @Resource
	    private CityService cityService;
	
	    @GetMapping("/cities")
	    public List<City> cities () {
	        return cityService.getAll();
	    }
	
	    @GetMapping("/city/{provinceId}")
	    public City city(@PathVariable long provinceId) {
	        return cityService.getByProvinceId(provinceId);
	    }	
	}

**最后**

还记得我定义 <code>CityMapper.java</code> 的时候，为什么把 <code>@Mapper</code> 给注释掉了吗？是因为我在入口文件这里定义了到哪里去找 mapper 文件，所以就不用再在每个 mapper 文件中再写个注解了：
	
	@SpringBootApplication
	@MapperScan("com.mybatis.mapper") // 定义了在哪里扫描mapper文件
	public class MyApplication {
	
	    public static void main(String[] args) {
	        SpringApplication.run(MyApplication.class, args);
	    }
	}

至此，spring-boot 与 mybatis 整合完毕。

### 5、附上三个 MyBatis 链接，分别是：
<p>1、<a href="http://www.mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/" rel="nofollow noreferrer" target="_blank">mybatis-spring-boot-starter 配置项手册</a></p>
2、<a href="https://github.com/mybatis/spring-boot-starter" rel="nofollow noreferrer" target="_blank">GitHub仓库地址，包含代码示例</a></p>
<p>3、<a href="http://www.mybatis.org/mybatis-3/zh/index.html" rel="nofollow noreferrer" target="_blank">中文官方文档</a></p>

```
    此文章转自：https://segmentfault.com/a/1190000014064512
    如果您有更好的文章推荐，请投稿可以投递到博主邮箱:2627045617@qq.com
```