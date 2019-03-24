# Lombok

[TOC]

>  Project Lombok是一个java库，可以自动插入编辑器并构建工具，为您的java增添色彩。
> 永远不要再写另一个getter或equals方法，只使用一个注释，类就能具有一个功能齐全的构建器，自动化日志记录变量等等。

具体使用看[官方注解文档示例](https://projectlombok.org/features/all)

#### 注解

- **@Getter / @Setter**：标记在属性上，自动实现Get和Set方法
- **@ToString**：标记在类上，自动实现toString方法，可以通过**@ToString(exclude = {"id","name"})**设置包含哪些属性
- **@EqualsAndHashCode**：生成hashCode()和equals()方法

- **@NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor**：无参构造，有参构造，全参构造

- **@Data：包含下面全部，All together now: A shortcut for **@ToString`, `@EqualsAndHashCode, @Getter**` on all fields, and **@Setter** on all non-final fields, and **@RequiredArgsConstructor**!

- `val`：用在局部变量前面，相当于将变量声明为final
- `@NonNull`：给方法参数增加这个注解会自动在方法内对该参数进行是否为空的校验，如果为空，则抛出NPE（NullPointerException）
- `@Cleanup`：自动管理资源，用在局部变量之前，在当前变量范围内即将执行完毕退出之前会自动清理资源，自动生成try-finally这样的代码来关闭流
- `@Value`：用在类上，是@Data的不可变形式，相当于为属性添加final声明，只提供getter方法，而不提供setter方法
- `@Builder`：用在类、构造器、方法上，为你提供复杂的builder APIs
- `@SneakyThrows`：自动抛受检异常，而无需显式在方法上使用throws语句
- `@Getter(lazy=true)`：可以替代经典的Double Check Lock样板代码
- @Log：根据不同的注解生成不同类型的log对象，但是实例名称都是log，有六种可选实现类
  - `@CommonsLog` Creates log = org.apache.commons.logging.LogFactory.getLog(LogExample.class);
  - `@Log` Creates log = java.util.logging.Logger.getLogger(LogExample.class.getName());
  - `@Log4j` Creates log = org.apache.log4j.Logger.getLogger(LogExample.class);
  - `@Log4j2` Creates log = org.apache.logging.log4j.LogManager.getLogger(LogExample.class);
  - `@Slf4j` Creates log = org.slf4j.LoggerFactory.getLogger(LogExample.class);
  - `@XSlf4j` Creates log = org.slf4j.ext.XLoggerFactory.getXLogger(LogExample.class);

- **@Synchronized**：同步

- **@Accessors**： 主要用于控制生成的getter和**setter**

  - fluent boolean值，默认为false。此字段主要为控制生成的getter和setter方法前面是否带get/set
  - chain boolean值，默认false。如果设置为true，setter返回的是此对象，方便链式调用方法

  - prefix 设置前缀 例如：@Accessors(prefix = "abc") private String abcAge  当生成get/set方法时，会把此前缀去掉

    ```java
    @Accessors(fluent=true, chain=true, prefix="abc")
    ```

- **@Wither**: 提供了给final字段赋值的一种方法

- **@Delegate**:会该类生成一些列的方法，这些方法都来自与List接口

- **@onX**:在注解里面添加注解的方式

  ```java
  @Getter(onMethod = @_(@Column(name="school_id")))
      @Setter
      private Integer schoolId;
  ```

  