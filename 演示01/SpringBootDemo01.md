### 使用Maven创建SpringBoot项目-快速入门

##### 1、准备工作

（1）、Spring Boot 2.X 版本，需要最低的 Java 版本是 8。

（2）、对Maven有一定了解

（3）拥有IDEA

##### 2、创建Maven项目

步骤一：打开IDEA，点击菜单File-->New-->Project创建项目,如下图

[![jUFKdP.md.png](https://s1.ax1x.com/2022/07/06/jUFKdP.md.png)](https://imgtu.com/i/jUFKdP)


步骤二：填入项目名称，选择项目保存目录点击Finish，完成Maven项目创建。

[![jUF1JS.md.png](https://s1.ax1x.com/2022/07/06/jUF1JS.md.png)](https://imgtu.com/i/jUF1JS)


#####  3、引入依赖

在Pom.xml文件中，引入相关依赖

```xml

<!-- 引入依赖 -->
<!-- 引入Spring-boot-starter-parent作为父Pom，从而继承其默认配置-->
    <parent>
        <artifactId>spring-boot-starter-parent</artifactId>
        <groupId>org.springframework.boot</groupId>
        <version>2.3.4.RELEASE</version>
        <relativePath></relativePath>
    </parent>

<!--引入 spring-boot-starter-web 依赖，实现对 SpringMVC 的自动化配置。
        同时该依赖会自动帮我们引入 SpringMVC 等相关依赖。-->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.24</version>
        </dependency>
    </dependencies>
```



##### 4、创建配置文件

在 Spring Boot 项目中，约定通过 `application.yaml` 配置文件，进行 Spring Boot 自动配置的 Bean 的自定义。

在 `resource` 目录下，创建 `application.yaml` 配置文件，内容如下：

```yaml
#在 Spring Boot 项目中，约定通过 application.yaml 配置文件，
# 进行 Spring Boot 自动配置的 Bean 的自定义。
#在 resource 目录下，创建 application.yaml
#内嵌的Tomcat端口号，默认位8080端口
server:
  port: 80

```

##### 5、创建SpringBoot启动类Application

创建 Application 类，提供 Spring Boot 应用的启动类。代码如下：

```java
package com.demo;
import lombok.extern.slf4j.Slf4j;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

/**
 * @author **
 * @version 1.0
 * @SpringBootApplication 注解声明这是一个SpringBoot应用
 * 通过该注解，可以带来 Spring Boot 自动配置等等功能
 * */
@Slf4j
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class,args);
        log.info("项目启动成功");

    }
}

```

##### 6、创建Controller类，提供一个简单的HTTP API。代码如下

```java
package com.demo.test.Controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

/**
 * @author **
 * @version 1.0
 */
@RestController
@RequestMapping("/demo")
public class HelloController {


    @GetMapping("/hello")
    public String hello(){
        return "hello springboot";
    }
}
```

**目录结构如下：**

[![jUFJMj.png](https://s1.ax1x.com/2022/07/06/jUFJMj.png)](https://imgtu.com/i/jUFJMj)
##### 7、简单测试

运行Application启动类中的Maim()方法,就可以启动该项目了。
SpringBoot内部继承了Tomcat，不需要手动配置Tomcat，只需要关注具体的业务逻辑即可。

因为我们这边配置类中端口设置的是80端口，所以直接在项目栏中访问 http://localhost/demo/hello

返回结果
[![jUFYss.png](https://s1.ax1x.com/2022/07/06/jUFYss.png)](https://imgtu.com/i/jUFYss)

