# Spring Boot

基于java的开源框架，减少了人工去配置xml文件，便于快速搭建SpringWeb，用于创建微服务 (micro service)，自动配置嵌入式Tomcat。默认大于配置

详细教程请参考[官方文档](https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/htmlsingle/#getting-started-first-application-dependencies)

[TOC]

## 一、Spring Boot入门

### Spring Boot工作原理

#### @SpringBootApplication

​	程序入口，包含了以下等内容：@Configuration、@EnableAutoconfiguration、@ComponentScan、@SpringBootConfiguration等

#### `@Configuration` 

​	标记该类作为应用程序上下文的bean定义的来源。

#### @EnableAutoconfiguration

​	能够自动注入项目中的**依赖**

![Snipaste_2019-03-14_11-08-11](./images/Snipaste_2019-03-14_11-08-11.png)

#### @ComponentScan

​	自动扫描项目中的**组件**

#### @AutoConfigurationPackage

​	自动配置包 (注：@SpringBootApplication默认是将配置类所在的包及其子包的所有组件扫描到Spring容器)

### Spring Boot Starters启动器

Spring Boot Starters启动器用于解决依赖问题，开发**不同场景的项目**选择不同的依赖。具体参考官方文档[**表13.1。Spring Boot应用程序启动器**](https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/htmlsingle/#using-boot-starter)。下面的截图列出了一部分，使用的是chrome翻译，对于翻译的准确性不做保证.

![Snipaste_2019-03-14_11-10-54](./images/Snipaste_2019-03-14_11-10-54.png)

#### @RestController

​	用于Spring MVC处理WEB请求，@Controller`和`@ResponseBody的组合

#### @RequestMapping

​	**返回纯文本**，@RestController`**返回数据**而**不是视图。**

#### @Bean

​	给容器添加一个组件，将方法的返回值添加到容器中，并且方法名就是id

#### Spring Boot运行器


​	应用程序运行器(Runner)和命令行Runner接口允许在Spring Boot应用程序启动后执行代码。可以使用这些接口在应用程序启动后立即执行一些操作。 如ApplicationRunner 和CommandLineRunner 接口。
### 打包

1. 打包成jar

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

2. 打包成jar并运行

```
mvn package && java -jar target / spring-boot-0.1.0.jar
```

### 快速创建

- IDEA——New Project——Sprign Initializr

- 文件说明:

  - staitc: 静态资源

  - templates：保存所有的模板页面

  - application.properties: **spring配置文件**，可直接修改，IDEA会提示

  - **application.yml: **Spring配置文件的另一种格式。Spring Boot支持基于YAML的属性配置来运行应用程序。可以使用application.yml文件代替application.properties。

    ```yml
    server:
    	port: 4000
    ```

## 二、YAML

#### YAML简介

YAML是"YAML Ain't a Markup Language"（YAML不是一种标记语言）的递归缩写。**以数据做为中心**

#### YAML基本语法

- 严格缩进

- 不允许使用**Tab键**，只能用空格。

- 空格数不重要，但是要对齐。

- 大小写敏感

- #表示注释

- 数据结构：key-Value（支持单行写法和多行写法, 又称行内写法和多行写法）

  - 对象：mapping / hashes / dictionary

    ```yaml
    server: mio
    	name: foo
    	age: bar
    # 另一种写法
    server: {name: foo, age: bar}
    ```

  - 数组：sequence / list

    ```yaml
    list:
    	- list1
    	- list2
    # 另一种写法
    list: [list1, list2]
    ```

  - 纯量：scalars

    - 字符串

      - 默认不使用引号
      - 使用单引号 **''**，**会转义**
      - 使用双引号**""**，**不会转义**

      ```yaml
      
      ```

    - 布尔值

      ```yaml
      isRed: true
      使用true和false
      ```

    - 整数

      ```yaml
      number: 1314
      ```

    - 浮点数

      ```yaml
      number: 13.14
      ```

    - Null

      ```yaml
      parent: ~
      比较特殊的表示，使用~符合
      ```

    - 时间

      ```yaml
      iso8601: 2001-12-14t21:59:43.10-05:00
      使用ISO8601 格式
      ```

    - 日期

      ```yaml
      date: 2019-03-14
      采用复合 iso8601 格式
      ```

  - 数据转换

  使用两个感叹号

  ```yaml
  a: !!str 123
  ```

  多行字符串可以使用 `|` 保留换行符，也可以使用 `>` 折叠换行

  `+`表示保留文字块末尾的换行，`-`表示删除字符串末尾的换行

  引用：建立锚点&，引用锚点*，<<合并到当前数据

  ```yaml
  defaults: &defaults
    adapter:  postgres
    host:     localhost
  
  development:
    database: myapp_development
    <<: *defaults
  
  ```

- 例子

  ```yaml
  person:
    name: Akane
    age: 233
    birth: 2019/03/14
    girlFriend: true
    map: {k1: v1, k2: 2}
    list:
      - eat
      - shop
    girl:
      name: YTing
      age: 18
  ```

## 三、Spring Boot配置文件

application.properties为Spring Boot的配置文件，里面包含了spring的很多配置信息，可以在这里直接修改配置信息。里面能够配置的信息，来源于properties类

#### 从application.yml或application.properties读取属性值自动配置注入

- 在pom.xml中配置处理器

- IDEA——Enalbe annotation processing
- 配置bean```@ConfigurationProperties(prefix = "person")```
- 配置applicatjon.yml
- 单元测试

解决properties乱码问题：

```
Settings——File encodings——Transparent native-to-ascii conversion
```

#### 配置多个Profile文件

可以创建多个配置文件，不同的生产环境选择不同的配置文件。默认使用application.properties

![](/images/Snipaste_2019-03-15_10-13-34.png)

示例如下：

方法一：使用application.properties的形式

```properties
spring.profiles.active=dev
```



方法二：YAML文件使用文档块的模式的形式

```yml
server:
  port: 8080
spring:
  profiles: 
    active: test # 激活
# ---表示文档块模式
---
server:
  port: 4000
spring:
  profiles: production

---
server:
  port: 9999
spring:
  profiles: test
```

方法三：

其实在IDEA中有很好的支持显示， 手动选择即可

![](/images/Snipaste_2019-03-15_10-26-06.png)

方法四：

用命令行的方式，优先级最高

```
java -jar /xxx.jar --spring.profiles.active= 
```



#### spring.config.location=——Spring Boot配置文件的加载顺序

```
# 注: file:./为application.properties所在的目录
file:./config/
file:./
# 注： classpath:./为项目的根路径，即项目名所在的路径
classpath:./config/
classpath:./
优先级由高到低，高优先级的会覆盖低的
```

当然，你也可以手动设置

```xml
spring.config.location=
```



---



#### @Value("")与@ConfigurationProperties(prefix = "")的比较

@Value标注在属性上，@ConfigurationProperties标注在类上并且批量注入

|                |              |                                       |
| -------------- | ------------ | ------------------------------------- |
|                | Value("")    | @ConfigurationProperties(prefix = "") |
| 功能           | 一个一个指定 | 批量                                  |
| 松散绑定       | 不支持       | 支持                                  |
| SpEL           | 支持         | 不支持                                |
| JSR303数据校验 | 不支持       | 支持                                  |
| 复杂类型封装   | 不支持       | 支持                                  |

```java
//@Value("${person.name}")
private String name;
// JSR303数据校验
@Email
private String email;
@Value("#{10*10}")
private Integer age;
```

#### @PropertySource()与@ImportResource

@PropertySource(): 加载指定的配置文件

```
@PropertySource(value = "classpath:person.properties")
@Component // 添加到组件中
@ConfigurationProperties(prefix = "person")
public class Person {
```

@ImportResource: 导入Spring配置文件，让配置文件内容生效。(Spring Boot没有spring 配置文件，我们自己写的也不自动导入)

```java
@ImportResource(locations = "classpath:")
@SpringBootApplication
public class SpringdemoApplication implements ApplicationRunner {	
```

SpringBoot推荐做法

```java
// 标明是一个配置类
@Configuration
public class MyAppConfig {

    /**
     * 将方法的返回值添加到容器中，并且方法名就是id
     */
    @Bean
    public HelloService helloService() {
        return new HelloService();
    }
}

```

#### 配置文件占位符

在application.properties文件中配置

```properties
person.age=${random.int} # 随机数
person.name=Akane${person.age} #占位符
person.name=Akane${person.hello:hello} #如果没有可以使用:指定默认值
```

#### @Conditionnal派生注解

**自动配置类必须在一定的条件下才能生效**

```properties
# 在application.properties可以用debug属性，用于查看哪些自动配置类生效
debug=true
```

conditionnal: 有条件的

prefix: 前缀，字首

#### 重点

![](/images/Snipaste_2019-03-15_11-19-39.png)



## 四、Spring Boot构建RESTful Web服务

1. 配置*pom.xml*，添加*spring-boot-starter-web*启动器

#### @RestController——Rest控制器

​	作用：定义RESTful Web服务，@Controller`和`@ResponseBody的组合

#### @RequestMapping——请求映射

​	作用：用于定义访问REST端点的Request URI

```java
RequestMapping(value = "/getNotice", method = RequestMethod.GET)
```

#### @RequestBody——请求主体

​	作用：用于定义请求返回的内容类型

#### @PathVariable——路径变量

​	作用：用于定义自定义或动态请求URI。 请求URI中的Path变量定义为花括号`{}`

```java
    @RequestMapping("/{name}")
    public String index(@PathVariable("name") String name) {
        return "Hello ! " + name;
    }
```

#### @RequestParam——请求参数

​	作用：用于从请求URL读取请求参数

```java
@RequestMapping(value = "/upLoadAvatar", method = RequestMethod.POST)
	public String uploadAvatarImg(@RequestParam(value = "id") Integer id,
			@RequestParam(value = "upload-avatar") MultipartFile avatarFile, HttpServletRequest request) {
```

#### HTTP请求方法

GET API: 默认.  method = RequestMethod.GET

POST API:  用于创建资源.  method = RequestMethod.POST

PUT API: 用于更新现有资源.  method = RequestMethod.PUT

DELETE API: 用于删除现有资源. method = RequestMethod.DELETE

```java
//  REST风格的Mapping，底层其实就是method = RequestMethod.PUT
	@PostMapping
    @GetMapping
	@DeleteMapping
	@PutMapping
```







## 五、Spring Boot Log

Spring Boot使用Apache Commons日志记录进行所有内部日志记录。默认打印在控制台，存在日志到文件可以通过*logging.file* 或*logging.path* 设置

```xml
logging.path=/user/local/log
logging.level.com.favorites=DEBUG
logging.level.com.example=TRACE # 设置日志级别
logging.level.org.springframework.web=INFO
logging.level.org.hibernate=ERROR
logging.pattern.console= # 设置控制台显示的格式
logging.pattern.file= # 设置保存文件的显示格式
```

- 提供日志日期和时间的日期和时间。

- 日志级别显示有：INFO，ERROR或WARN。

- 进程ID。

- `---`是一个分隔符。

- 线程名称括在方括号`[]`中。

- 记录器名称，显示源类名称。

- 日志消息。

  ```
  2019-03-14 17:16:02.001  INFO 11376 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 4 ms
  ```

SpringBoot日志使用和级别

注: SpringBoot默认输出的是Info级别，如需要修改则到application.properties修改。

![](D:/Akane-Note/images/Snipaste_2019-03-17_12-33-31.png)



#### 日志框架

Spring Boot的默认配置支持使用Java Util Logging，Log4j2和Logback。

**1. 开发中使用SFL4J**

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorld {
  public static void main(String[] args) {
    Logger logger = LoggerFactory.getLogger(HelloWorld.class);
    logger.info("Hello World");
  }
}
```

2. 导包

![](/images/concrete-bindings.png)

3. 编写配置文件

---



#### SpringBoot日志依赖关系

![](/images/Snipaste_2019-03-17_12-14-23.png)

#### 自定义日志配置

![](/images/Snipaste_2019-03-17_14-56-10.png)

logback.xml：直接被日志框架识别

**logback-spring.xml**：不直接别识别，由SpringBoot解析日志配置，可以使用SpringBoot的高级profile功能



## 六、SpringBoot开发WEB

SpringBoot简化了WEB开发，集成了很多框架，SpringBoot自动配置了SpringMCVC。在开发一个WEB应用时，只需要如下：

1. 创建应用的时候，选择需要的模块
2. 在配置文件*appplication.properties*配置指定的配置信息
3. 编写业务

#### SpringBoot对静态资源的映射规则

```java
// 负责映射管理的类
@ConfigurationProperties(
    prefix = "spring.resources",
    ignoreUnknownFields = false
)
public class ResourceProperties {
```

配置文件中属性

```yaml
spring.resources.static-locations=
```

#### 几种映射形式

1.通过WebJars导入的形式的，资源在*classpath/:META-INF/resources/webjars/*

[**WebJars](https://www.webjars.org/)**: 指的是可以通过打包JAR(Java Archive)的形式引入到WEB应用程序中，并且可以基于Maven，Gradle等构建工具进行下载依赖。

![](/images/Snipaste_2019-03-17_17-47-52.png)

2. /**的形式可以访问当前目录的任何资源

```xml
classpath:/META-INF/resources/",
"classpath:/resources/", 
"classpath:/static/", 
"classpath:/public/
"classpath:/
```

3.配置首页，静态资源文件夹下的index.html

4.站点图标，静态资源文件夹下的favicon.icon

#### Thymeleaf模板引擎

```properties
spring.thymeleaf
```

**SpringBoot使用的是嵌入式Servlet容器，不支持JSP模板引擎**，但是支持Thymeleaf模板引擎。Thymeleaf是一个现代服务器端Java模板引擎，适用于Web和独立环境，能够处理HTML，XML，JavaScript，CSS甚至纯文本。

## 七、Thymeleaf的基本语法和使用

#### Thymeleaf的基本使用

1.Thymeleaf基本配置属性

```java
@ConfigurationProperties(
    prefix = "spring.thymeleaf"
)
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;    
	public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    private boolean checkTemplate = true;
    private boolean checkTemplateLocation = true;
    private String prefix = "classpath:/templates/";
    private String suffix = ".html";
    private String mode = "HTML";
```

2.在*classpath:/templates/*文件下的HTML页面会被Thymeleaf自动渲染

---



#### Thymeleaf的基本语法

1.导入thymeleaf的名称空间

```html
<html lang="en"  xmlns:th="http://www.thymeleaf.org">
```

###### 1) th:text，改变元素里面的文本内容

​	th:任意html属性。th：thymeleaf

| Order | Feature                         | 说明                        | Attributes                                                 |
| :---- | :------------------------------ | --------------------------- | :--------------------------------------------------------- |
| 1     | Fragment inclusion              | 片段包含，jsp:include       | `th:insert` <br />`th:replace`                             |
| 2     | Fragment iteration              | 遍历，c:forEach             | `th:each`                                                  |
| 3     | Conditional evaluation          | t条件判断，c:if             | `th:if` <br />`th:unless` <br />`th:switch`<br />`th:case` |
| 4     | Local variable definition       | 声明变量，c:set             | `th:object`<br /> `th:with`                                |
| 5     | General attribute modification  | 任意属性修改                | `th:attr` <br />`th:attrprepend` <br />`th:attrappend`     |
| 6     | Specific attribute modification | 修改指定属性的默认值        | `th:value` <br />`th:href` <br />`th:src` `...`            |
| 7     | Text (tag body modification)    | 修改标签体内容，utext不转义 | `th:text` <br />`th:utext`                                 |
| 8     | Fragment specification          | 声明片段                    | `th:fragment`                                              |
| 9     | Fragment removal                |                             | `th:remove`                                                |

###### 2) 表达式语法

**${....}**

获取对象属性，还可以调用方法，使用内置基本对象，内置对象如下：

- `#ctx`: the context object.
- `#vars:` the context variables.
- `#locale`: the context locale.
- `#request`: (only in Web Contexts) the `HttpServletRequest` object.
- `#response`: (only in Web Contexts) the `HttpServletResponse` object.
- `#session`: (only in Web Contexts) the `HttpSession` object.
- `#servletContext`: (only in Web Contexts) the `ServletContext` object.

```
Established locale country: <span th:text="${#locale.country}">US</span>.
```

***{...}**

​	功能上和$一样，但是有时候更便捷

```html
  <div th:object="${session.user}">
    <p>Name: <span th:text="*{firstName}">Sebastian</span>.</p>
    <p>Surname: <span th:text="*{lastName}">Pepper</span>.</p>
    <p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
  </div>
```

​	此时*就代表了当前父类的这个属性，就相当于下面$的作用

```html
<div>
  <p>Name: <span th:text="${session.user.firstName}">Sebastian</span>.</p>
  <p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
  <p>Nationality: <span th:text="${session.user.nationality}">Saturn</span>.</p>
</div>
```

**#{...}**

​	获取国际内容

**@{...}**

​	定义url链接

**~{...}**

​	片段引用表达式

###### 3) 行内写法

使用 `[[...]]` or `[(...)]`

```html
<p>Hello, [[${session.user.name}]]!</p>
```

---



##### 配置国际化内容

1）、SpringBoot中自动配置了管理国际化资源文件的组件

```java
public class MessageSourceAutoConfiguration {
    private static final Resource[] NO_RESOURCES = new Resource[0];

    public MessageSourceAutoConfiguration() {
    }

    @Bean
    @ConfigurationProperties(
        prefix = "spring.messages"
    )
```

2）、使用**#{...}**获取国际内容

关于乱码问题：properties文件最后需要转换为ascii码，所以需要将IDEA转换为自动转换为ascii。setting——file Encoding

![](/images/Snipaste_2019-03-18_09-14-59.png)	

##### Thymeleaf设置公共页面元素

```HTML
    <!-- 声明片段-->
	<div th:fragment="copy">
      &copy; 2011 The Good Thymes Virtual Grocery
    </div>
    <!-- 引入片段-->
    <div th:insert="~{footer :: copy}">	</div> 模板名：片段名
三种不同方式
  <div th:insert="footer :: copy"></div>

  <div th:replace="footer :: copy"></div>

  <div th:include="footer :: copy"></div>
```

##### 	   REST风格的请求

```html
    <form th:action="@{/emp/}+${emp.id}" method="post">
        <input type="hidden" name="_method" method="delete"/>
        <button type="submit">删除</button>
    </form>
```





## 八、SpringBoot开发WEB的一些问题

1）、自定义区域信息解析器：

通过实现LocaleResolver，并@Bean添加到组件中即可

```JAVA
public class MyLocaleResolver implements LocaleResolver {
    @Override
    public Locale resolveLocale(HttpServletRequest httpServletRequest) {
        Locale locale = Locale.getDefault();
        String language = httpServletRequest.getParameter("l");
        if(!language.isEmpty()){
            String[] split = language.split("_");
            locale = new Locale(split[0], split[1]);
        }

        return locale;
    }
```

2）、开发的过程，可以禁用Thymeleaf模板缓存，实时生效。修改配置后重新编译

```properties
spring.thymlaef.cache=false
```

3）、防止重复提交表单，设置为重定向

4）、自定义映射规则

```java
WebMvcAutoConfigurationAdapter
```

5）、拦截器

```java
HandlerInterceptor
```

## 九、SpringData

SpringData为我们提供了统一的API来对数据访问层进行操作

#### JPA

Java Persistence API，Java持久层API

![](/images/Snipaste_2019-03-19_14-47-04.png)

## 十、SpringBoot启动顺序

断点查看