# 概念

spring在简化：会达成一个jar包：内嵌tomcat；微服务架构

### 什么是Spring

Spring是一个开源框架，2003 年兴起的一个轻量级的Java 开发框架，作者：Rod Johnson 。

**Spring是为了解决企业级应用开发的复杂性而创建的，简化开发。**

### Spring是如何简化Java开发的

为了降低Java开发的复杂性，Spring采用了以下4种关键策略：

1、基于POJO的轻量级和最小侵入性编程；

2、通过IOC，依赖注入（DI）和面向接口实现松耦合；

3、基于切面（AOP）和惯例进行声明式编程；

4、通过切面和模版减少样式代码；

### 什么是SpringBoot

学过javaweb的同学就知道，开发一个web应用，从最初开始接触Servlet结合Tomcat, 跑出一个Hello Wolrld程序，是要经历特别多的步骤； 后来就用了框架Struts，再后来是SpringMVC，到了现在的SpringBoot，过一两年又会有其他web框架出现；不知道你们有没经历过框架不断的演进，然后自己开发项目所有的技术也再不断的变化、改造，反正我是都经历过了，哈哈。言归正传，什么是SpringBoot呢，就是一个javaweb的开发框架，和SpringMVC类似，对比其他javaweb框架的好处，官方说是简化开发，约定大于配置， you can "just run"，能迅速的开发web应用，几行代码开发一个http接口。

所有的技术框架的发展似乎都遵循了一条主线规律：从一个复杂应用场景 衍生 一种规范框架，人们只需要进行各种配置而不需要自己去实现它，这时候强大的配置功能成了优点；发展到一定程度之后，人们根据实际生产应用情况，选取其中实用功能和设计精华，重构出一些轻量级的框架；之后为了提高开发效率，嫌弃原先的各类配置过于麻烦，于是开始提倡“约定大于配置”，进而衍生出一些一站式的解决方案。

是的这就是Java企业级应用->J2EE->spring->springboot的过程。

随着 Spring 不断的发展，涉及的领域越来越多，项目整合开发需要配合各种各样的文件，慢慢变得不那么易用简单，违背了最初的理念，甚至人称配置地狱。Spring Boot 正是在这样的一个背景下被抽象出来的开发框架，目的为了让大家更容易的使用 Spring 、更容易的集成各种常用的中间件、开源软件；

Spring Boot 基于 Spring 开发，Spirng Boot 本身并不提供 Spring 框架的核心特性以及扩展功能，只是用于快速、敏捷地开发新一代基于 Spring 框架的应用程序。也就是说，它并不是用来替代 Spring 的解决方案，而是和 Spring 框架紧密结合用于提升 Spring 开发者体验的工具。Spring Boot 以**约定大于配置的核心思想**，默认帮我们进行了很多设置，多数 Spring Boot 应用只需要很少的 Spring 配置。同时它集成了大量常用的第三方库配置（例如 Redis、MongoDB、Jpa、RabbitMQ、Quartz 等等），Spring Boot 应用中这些第三方库几乎可以零配置的开箱即用，

简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，spring boot整合了所有的框架 。

Spring Boot 出生名门，从一开始就站在一个比较高的起点，又经过这几年的发展，生态足够完善，Spring Boot 已经当之无愧成为 Java 领域最热门的技术。

**Spring Boot的主要优点：**

- 为所有Spring开发者更快的入门
- **开箱即用**，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

使用 Spring Boot 到底有多爽，用下面这幅图来表达

![1569859952418.png](https://blog.kuangstudy.com/usr/uploads/2019/10/3278965235.png)

## 微服务

### 什么是微服务？

微服务是一种架构风格，它要求我们在开发一个应用的时候，这个应用必须构建成一系列小服务的组合；可以通过http的方式进行互通。要说微服务架构，先得说说过去我们的单体应用架构。

### 单体应用架构

所谓单体应用架构（all in one）是指，我们将一个应用的中的所有应用服务都封装在一个应用中。

无论是ERP、CRM或是其他什么系统，你都把数据库访问，web访问，等等各个功能放到一个war包内。

- 这样做的好处是，易于开发和测试；也十分方便部署；当需要扩展时，只需要将war复制多份，然后放到多个服务器上，再做个负载均衡就可以了。
- 单体应用架构的缺点是，哪怕我要修改一个非常小的地方，我都需要停掉整个服务，重新打包、部署这个应用war包。特别是对于一个大型应用，我们不可能吧所有内容都放在一个应用里面，我们如何维护、如何分工合作都是问题。

### 微服务架构

all in one的架构方式，我们把所有的功能单元放在一个应用里面。然后我们把整个应用部署到服务器上。如果负载能力不行，我们将整个应用进行水平复制，进行扩展，然后在负载均衡。

所谓微服务架构，就是打破之前all in one的架构方式，把每个功能元素独立出来。把独立出来的功能元素的动态组合，需要的功能元素才去拿来组合，需要多一些时可以整合多个功能元素。所以微服务架构是对功能元素进行复制，而没有对整个应用进行复制。

这样做的好处是：

1. 节省了调用资源。
2. 每个功能元素的服务都是一个可替换的、可独立升级的软件代码。

![1569860054088.png](https://blog.kuangstudy.com/usr/uploads/2019/10/3173282649.png)

Martin Flower 于 2014 年 3 月 25 日写的《Microservices》，详细的阐述了什么是微服务。

- 原文地址：http://martinfowler.com/articles/microservices.html
- 翻译：https://www.cnblogs.com/liuning8023/p/4493156.html

### 如何构建微服务

一个大型系统的微服务架构，就像一个复杂交织的神经网络，每一个神经元就是一个功能元素，它们各自完成自己的功能，然后通过http相互请求调用。比如一个电商系统，查缓存、连数据库、浏览页面、结账、支付等服务都是一个个独立的功能服务，都被微化了，它们作为一个个微服务共同构建了一个庞大的系统。如果修改其中的一个功能，只需要更新升级其中一个功能服务单元即可。

但是这种庞大的系统架构给部署和运维带来很大的难度。于是，spring为我们带来了构建大型分布式微服务的全套、全程产品：

- 构建一个个功能独立的微服务应用单元，可以使用springboot，可以帮我们快速构建一个应用；
- 大型分布式网络服务的调用，这部分由spring cloud来完成，实现分布式；
- 在分布式中间，进行流式数据计算、批处理，我们有spring cloud data flow。
- spring为我们想清楚了整个从开始构建应用到大型分布式应用全流程方案。

![1569860149218.png](https://blog.kuangstudy.com/usr/uploads/2019/10/1647528912.png)

## HelloWorld

**准备工作**

我们将学习如何快速的创建一个Spring Boot应用，并且实现一个简单的Http请求处理。通过这个例子对Spring Boot有一个初步的了解，并体验其结构简单、开发快速的特性。

我的环境准备：

- java version "1.8.0_181"
- Maven-3.6.1
- SpringBoot 2.x 最新版

开发工具：

- IDEA

### 创建基础项目

Spring官方提供了非常方便的工具

Spring Initializr：https://start.spring.io/ 来帮助我们创建Spring Boot应用。

【目标一：**使用Spring Initializr页面创建项目**】

步骤：

1. 打开 https://start.spring.io/
2. 填写项目信息
3. 点击”Generate Project“按钮生成项目；下载此项目
   ![1570257132310.png](https://blog.kuangstudy.com/usr/uploads/2019/10/2278667781.png)
4. 解压项目包，并用编译器以Maven项目导入，以IntelliJ IDEA为例：
5. 导入这个Maven项目，一路下一步即可，直到项目导入完毕。**如果是第一次使用，可能速度会比较慢，需要耐心等待一切就绪**
   ![1570257159884.png](https://blog.kuangstudy.com/usr/uploads/2019/10/3059404183.png)

### 项目结构分析

通过上面步骤完成了基础项目的创建。就会自动生成以下文件。

- 程序的主程序类
- 一个 application.properties 配置文件
- 一个测试类

生成的`DemoApplication`和测试包下的`DemoApplicationTests`类都可以直接运行来启动当前创建的项目，由于目前该项目未配合任何数据访问或Web模块，程序会在加载完Spring之后结束运行。

![1570257265158.png](https://blog.kuangstudy.com/usr/uploads/2019/10/2439611141.png)

### pom.xml 分析

打开`pom.xml`，看看Spring Boot项目的依赖：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.9.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.kuang</groupId>
    <artifactId>springboot-01-helloworld</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot-01-helloworld</name>
    <description>springboot-01-helloworld</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
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

</project>
```

如上所示，主要有四个部分：

- 项目元数据信息：创建时候输入的Project Metadata部分，也就是Maven项目的基本元素，包括：groupId、artifactId、version、name、description等
- parent：继承`spring-boot-starter-parent`的依赖管理，控制版本与打包等内容
- dependencies：项目具体依赖，这里包含了`spring-boot-starter-web`用于实现HTTP接口（该依赖中包含了Spring MVC），官网对它的描述是：使用Spring MVC构建Web（包括RESTful）应用程序的入门者，使用Tomcat作为默认嵌入式容器。；`spring-boot-starter-test`用于编写单元测试的依赖包。更多功能模块的使用我们将在后面逐步展开。
- build：构建配置部分。默认使用了`spring-boot-maven-plugin`，配合`spring-boot-starter-parent`就可以把Spring Boot应用打包成JAR来直接运行。

### 编写HTTP接口

1. 在主程序的同级目录下，新建一个controller包【一定要在同级目录下，否则识别不到】
   ![1570257676939.png](https://blog.kuangstudy.com/usr/uploads/2019/10/2566396584.png)

2. 在包中新建一个Controller类

   ```java
   package com.kuang.springboot.controller;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   
   @RestController
   public class HelloController {
   
       @RequestMapping("/hello")
       public String hello() {
           return "Hello World";
       }
       
   }
   ```

3. 编写完毕后，从主程序启动项目，浏览器发起请求，看页面返回；

   - 控制台输出了SpringBoot 的 banner
   - 控制条输出了 Tomcat 访问的端口号！
   - 访问 hello 请求，字符串成功返回！
     ![1570257840889.png](https://blog.kuangstudy.com/usr/uploads/2019/10/1251448510.png)

4. 将项目打成jar包
   ![1570258568981.png](https://blog.kuangstudy.com/usr/uploads/2019/10/1772691465.png)

5. 打成了jar包后，就可以在任何地方运行了！OK

   ### 在cmd中运行

   利用打好的jar包在cmd中控可以直接部署在服务器上，示例命令如下

   ![image-20200219143406292](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200219143406292.png)

### 小结

- 简单几步，就完成了一个web接口的开发，SpringBoot就是这么简单。所以我们常用它来建立我们的微服务项目！

### 彩蛋

如何更改启动时显示的字符拼成的字母，SpringBoot呢？

[点击这个链接](http://patorjk.com/software/taag/#p=display&f=Graffiti&t=Kuangshen) ，直接输入要生成的字母，系统会自动转换，然后复制下面转换好的字符；

到项目下的 resources 目录下新建一个txt文件就可以，banner.txt

```
 /\/\/\                            /  \                   
| \  / |                         /      \                 
|  \/  |                       /          \               
|  /\  |----------------------|     /\     |              
| /  \ |                      |    /  \    |              
|/    \|                      |   /    \   |              
|\    /|                      |  | (  ) |  |              
| \  / |                      |  | (  ) |  |              
|  \/  |                 /\   |  |      |  |   /\         
|  /\  |                /  \  |  |      |  |  /  \        
| /  \ |               |----| |  |      |  | |----|       
|/    \|---------------|    | | /|   .  |\ | |    |       
|\    /|               |    | /  |   .  |  \ |    |       
| \  / |               |    /    |   .  |    \    |       
|  \/  |               |  /      |   .  |      \  |       
|  /\  |---------------|/        |   .  |        \|       
| /  \ |              /   NASA   |   .  |  NASA    \      
|/    \|              (          |      |           )     
|/\/\/\|               |    | |--|      |--| |    |       
------------------------/  \-----/  \/  \-----/  \--------
                        \\//     \\//\\//     \\//        
                         \/       \/  \/       \/      
```

然后重启试试吧！

![1570258914089.png](https://blog.kuangstudy.com/usr/uploads/2019/10/758786077.png)

### 使用IDEA快速构建项目

**之前，我们在官网上直接快速构建了一个springboot项目，IDEA也可以做到，我们来看下具体步骤：**

1. 创建一个新项目

2. 选择spring initalizr ， 可以看到默认就是去官网的快速构建工具那里实现

3. 填写项目信息

4. 选择初始化的组件

5. 填写项目路径

6. 等待项目构建成功

7. 我们在SpringBootApplication的同路径下，建一个包 controller ，建立一个类HelloSpringBoot

8. 编写代码

   ```java
   //@RestController 的意思就是 Controller 里面的方法都以 json 格式输出
   @RestController
   public class HelloSpringBoot {
   
       @RequestMapping("/hello")
       public String hello(){
           return "Hello,SpringBoot!";
       }
   }
   ```

9. **启动主程序，打开浏览器访问 [http://localhost](http://localhost/):8080/hello，就可以看到效果了！**
   ![1570259079467.png](https://blog.kuangstudy.com/usr/uploads/2019/10/2365050656.png)

**我们在之后的学习中，直接使用IDEA创建项目即可，方便快捷！这么简单的东西背后一定有故事，我们之后去进行一波源码分析！**

## 运行原理探究

### pom.xml

我们之前写的HelloSpringBoot，到底是怎么运行的呢，我们来看pom.xml文件

其中它主要是依赖一个父项目

```xml
<parent>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-parent</artifactId>
   <version>2.1.9.RELEASE</version>
   <relativePath/> <!-- lookup parent from repository -->
</parent>
```

进入父项目

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-dependencies</artifactId>
  <version>2.1.9.RELEASE</version>
  <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
```

这里才是真正管理SpringBoot应用里面所有依赖版本的地方，SpringBoot的版本控制中心；

**以后我们导入依赖默认是不需要写版本；但是如果导入的包没有在依赖中管理着就需要手动配置版本了；**

### 启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**springboot-boot-starter：就是spring-boot的场景启动器**

**spring-boot-starter-web 帮我们导入了web模块正常运行所依赖的组件；**

SpringBoot将所有的功能场景都抽取出来，做成一个个的starter （启动器），只需要在项目中引入这些starter即可，所有相关的依赖都会导入进来 ， 我们要用什么功能就导入什么样的场景启动器即可 ；

### 主程序

```java
//@SpringBootApplication 来标注一个主程序类 ， 说明这是一个Spring Boot应用
@SpringBootApplication
public class Springboot01HelloworldApplication {

   public static void main(String[] args) {
     //将SpringBoot应用启动起来
      SpringApplication.run(Springboot01HelloworldApplication.class, args);
   }

}
```

但是**一个简单的启动类并不简单！**我们来分析一下这些注解都干了什么

#### **1、@SpringBootApplication**

意义：SpringBoot应用标注在某个类上说明这个类是SpringBoot的主配置类 ， SpringBoot就应该运行这个类的main方法来启动SpringBoot应用；

进入这个注解：可以看到上面还有很多其他注解！

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
    //.....
}
```

#### **2、@ComponentScan**

 这个注解在Spring中很重要 ， 它对应XML配置中的元素。@ComponentScan的功能就是自动扫描并加载符合条件的组件或者bean ， 将这个bean定义加载到IOC容器中 ；

#### **3、@SpringBootConfiguration**

意义：SpringBoot的配置类 ；标注在某个类上 ， 表示这是一个SpringBoot的配置类；

我们继续进去这个注解查看

```java
@Configuration //点进去得到下面的 @Component
public @interface SpringBootConfiguration {
}
@Component
public @interface Configuration {
}
```

@Configuration：配置类上来标注这个注解，说明这是一个配置类 ，配置类---即----配置文件；

我们继续点进去，发现配置类也是容器中的一个组件。@Component 。这就说明，启动类本身也是Spring中的一个组件而已，负责启动应用！

#### **4、@EnableAutoConfiguration**

我们回到 SpringBootApplication 注解中继续看。

![1570275600891.png](https://blog.kuangstudy.com/usr/uploads/2019/10/3676838154.png)

**@EnableAutoConfiguration ：开启自动配置功能**

 以前我们需要自己配置的东西，而现在SpringBoot可以自动帮我们配置 ； @EnableAutoConfiguration告诉SpringBoot开启自动配置功能，这样自动配置才能生效；

**我们点击去查看**。**发现注解@AutoConfigurationPackage ： 自动配置包**

```java
@AutoConfigurationPackage //自动配置包
@Import({AutoConfigurationImportSelector.class}) //导入哪些组件的选择器
public @interface EnableAutoConfiguration {
}
```

**再点进去看到一个 @Import({Registrar.class})**

```java
@Import({Registrar.class})
public @interface AutoConfigurationPackage {
}
```

**@import** ：Spring底层注解@import ， 给容器中导入一个组件

**Registrar.class 将主配置类 【即@SpringBootApplication标注的类】的所在包及包下面所有子包里面的所有组件扫描到Spring容器 ；**

退到上一步，继续看：**@Import({AutoConfigurationImportSelector.class})** ：给容器导入组件 ；

AutoConfigurationImportSelector ： 自动配置导入选择器，那么它会导入哪些组件的选择器呢？ ;

我们点击去这个类看源码：

1. 这个类中有一个这样的方法

   ```java
   // 获得候选的配置
   protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
       //这里的getSpringFactoriesLoaderFactoryClass（）方法
       //返回的就是我们最开始看的启动自动导入配置文件的注解类；EnableAutoConfiguration
       List<String> configurations = SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader());
       Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you are using a custom packaging, make sure that file is correct.");
       return configurations;
   }
   ```

2. 这个方法又调用了 SpringFactoriesLoader 类的静态方法！我们进入SpringFactoriesLoader类loadFactoryNames() 方法

   ```java
   public static List<String> loadFactoryNames(Class<?> factoryClass, @Nullable ClassLoader classLoader) {
       String factoryClassName = factoryClass.getName();
       //这里它又调用了 loadSpringFactories 方法
       return (List)loadSpringFactories(classLoader).getOrDefault(factoryClassName, Collections.emptyList());
   }
   ```

3. 我们继续点击查看 loadSpringFactories 方法

   ```java
   private static Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader) {
       //获得classLoader ， 我们返回可以看到这里得到的就是EnableAutoConfiguration标注的类本身
       MultiValueMap<String, String> result = (MultiValueMap)cache.get(classLoader);
       if (result != null) {
           return result;
       } else {
           try {
               //去获取一个资源 "META-INF/spring.factories"
               Enumeration<URL> urls = classLoader != null ? classLoader.getResources("META-INF/spring.factories") : ClassLoader.getSystemResources("META-INF/spring.factories");
               LinkedMultiValueMap result = new LinkedMultiValueMap();
   
               //将读取到的资源遍历，封装成为一个Properties
               while(urls.hasMoreElements()) {
                   URL url = (URL)urls.nextElement();
                   UrlResource resource = new UrlResource(url);
                   Properties properties = PropertiesLoaderUtils.loadProperties(resource);
                   Iterator var6 = properties.entrySet().iterator();
   
                   while(var6.hasNext()) {
                       Entry<?, ?> entry = (Entry)var6.next();
                       String factoryClassName = ((String)entry.getKey()).trim();
                       String[] var9 = StringUtils.commaDelimitedListToStringArray((String)entry.getValue());
                       int var10 = var9.length;
   
                       for(int var11 = 0; var11 < var10; ++var11) {
                           String factoryName = var9[var11];
                           result.add(factoryClassName, factoryName.trim());
                       }
                   }
               }
   
               cache.put(classLoader, result);
               return result;
           } catch (IOException var13) {
               throw new IllegalArgumentException("Unable to load factories from location [META-INF/spring.factories]", var13);
           }
       }
   }
   ```

4. **我们根据源头打开spring.factories的配置文件 ， 看到了很多自动配置的文件；这就是自动配置根源所在！**

![1570276858427.png](https://blog.kuangstudy.com/usr/uploads/2019/10/1620545636.png)

**WebMvcAutoConfiguration**

我们在上面的自动配置类随便找一个打开看看，比如 ： WebMvcAutoConfiguration

![1570277345733.png](https://blog.kuangstudy.com/usr/uploads/2019/10/165245652.png)

可以看到这些一个个的都是JavaConfig配置类，而且都注入了一些Bean，可以找一些自己认识的类，看着熟悉一下！

**所以，自动配置真正实现是从classpath中搜寻所有的`META-INF/spring.factories`配置文件 ，并将其中对应的 org.springframework.boot.autoconfigure. 包下的配置项，通过反射实例化为对应标注了 @Configuration的JavaConfig形式的IOC容器配置类 ， 然后将这些都汇总成为一个实例并加载到IOC容器中。**

**结论：**

1. SpringBoot在启动的时候从类路径下的META-INF/spring.factories中获取EnableAutoConfiguration指定的值，但是不一定成立，只要导入了对应的启动器，有了驱动器，我们自动装配就能生效
2. 将这些值作为自动配置类导入容器 ， 自动配置类就生效 ， 帮我们进行自动配置工作；
3. 以前我们需要自己配置的东西 ， 自动配置类都帮我们解决了
4. 整个J2EE的整体解决方案和自动配置都在springboot-autoconfigure的jar包中；
5. **它将所有需要导入的组件以全类名的方式返回 ， 这些组件就会被添加到容器中 ；**
6. 它会给容器中导入非常多的自动配置类 （xxxAutoConfiguration）, 就是给容器中导入这个场景需要的所有组件 ， 并配置好这些组件 ；
7. **有了自动配置类 ， 免去了我们手动编写配置注入功能组件等的工作；**

### Run

我最初以为就是运行了一个main方法，没想到却开启了一个服务；

```java
@SpringBootApplication
public class SpringbootDemo02Application {

    public static void main(String[] args) {
        //该方法返回一个ConfigurableApplicationContext对象
        //参数一：应用入口的类     参数类：命令行参数
        SpringApplication.run(SpringbootDemo02Application.class, args);
    }

}
```

**SpringApplication.run分析**

分析该方法主要分两部分，一部分是SpringApplication的实例化，二是run方法的执行；

### SpringApplication

这个类主要做了以下四件事情

1. 推断应用的类型是普通的项目还是Web项目
2. 查找并加载所有可用初始化器 ， 设置到initializers属性中
3. 找出所有的应用程序监听器，设置到listeners属性中
4. 推断并设置main方法的定义类，找到运行的主类

**查看构造器**

```java
public SpringApplication(ResourceLoader resourceLoader, Class... primarySources) {
    this.sources = new LinkedHashSet();
    this.bannerMode = Mode.CONSOLE;
    this.logStartupInfo = true;
    this.addCommandLineProperties = true;
    this.addConversionService = true;
    this.headless = true;
    this.registerShutdownHook = true;
    this.additionalProfiles = new HashSet();
    this.isCustomEnvironment = false;
    this.resourceLoader = resourceLoader;
    Assert.notNull(primarySources, "PrimarySources must not be null");
    this.primarySources = new LinkedHashSet(Arrays.asList(primarySources));
    this.webApplicationType = WebApplicationType.deduceFromClasspath();
    this.setInitializers(this.getSpringFactoriesInstances(ApplicationContextInitializer.class));
    this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
    this.mainApplicationClass = this.deduceMainApplicationClass();
}
```

### run方法

![1353149994.png](https://blog.kuangstudy.com/usr/uploads/2019/10/700745206.png)

