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

#### @ComponentScan

​	自动扫描项目中的**组件**

### Spring Boot Starters启动器

- Spring Boot Starters启动器用于解决依赖问题，开发不同类型的项目选择不同的依赖
- **Spring Boot Starter Actuator**依赖关系用于监视和管理应用程序
- **Spring Boot Starter Security**依赖项用于Spring Security
- **Spring Boot Starter Web**依赖项用于编写Rest端点
- **Spring Boot Starter Thyme Leaf**依赖项用于创建Web应用程序
- **Spring Boot Starter Test**依赖项用于编写测试用例

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

