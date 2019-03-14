# Spring Boot

基于java的开源框架，减少了人工去配置xml文件，便于快速搭建SpringWeb，用于创建微服务 (micro service)，自动配置嵌入式Tomcat。

详细请参考[官方文档](https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/htmlsingle/#getting-started-first-application-dependencies)

### Spring Boot工作原理

#### @SpringBootApplication

​	程序入口，包含了以下等内容：@Configuration、@EnableAutoconfiguration、@ComponentScan、@SpringBootConfiguration等

#### `@Configuration` 

​	标记该类作为应用程序上下文的bean定义的来源。

#### @EnableAutoconfiguration

​	能够自动注入项目中的**依赖**

![Snipaste_2019-03-14_11-08-11](.\images\Snipaste_2019-03-14_11-08-11.png)

#### @ComponentScan

​	自动扫描项目中的**组件**

#### @AutoConfigurationPackage

​	自动配置包 (注：@SpringBootApplication默认是将配置类所在的包及其子包的所有组件扫描到Spring容器)

### Spring Boot Starters启动器

Spring Boot Starters启动器用于解决依赖问题，开发**不同场景的项目**选择不同的依赖。具体参考官方文档[**表13.1。Spring Boot应用程序启动器**](https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/htmlsingle/#using-boot-starter)。下面的截图列出了一部分，使用的是chrome翻译，对于翻译的准确性不做保证.

![Snipaste_2019-03-14_11-10-54](.\images\Snipaste_2019-03-14_11-10-54.png)

#### @RestController

​	用于Spring MVC处理WEB请求

#### @RequestMapping

​	**返回纯文本**，@RestController`组合`@Controller`和`@ResponseBody`两个注释会导致Web请求**返回数据**而**不是视图。**

#### @Bean

打包运行

```
mvn package && java -jar target / spring-boot-0.1.0.jar
```

### 打包成jar

*pom.xml*配置插件

```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

### 单元测试

