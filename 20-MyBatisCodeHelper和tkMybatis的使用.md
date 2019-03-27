# MyBatisCodeHelper和tkMybatis的使用

[TOC]



### MyBatisCodeHelper

| **功能点**                                                   | **未激活版** | **激活版** |
| ------------------------------------------------------------ | ------------ | ---------- |
| **接口与xml互相跳转 更换图标**                               | ✔            | ✔          |
| 接口方法名重构                                               | ✔            | ✔          |
| 一键添加param                                                | ✔            | ✔          |
| xml中的 param的自动提示 if test的自动提示 resultMap refid 等的自动提示 | ✔            | ✔          |
| resultMap中的property的自动提示                              | ✔            | ✔          |
| 检测没有使用的xml 可一键删除                                 | ✔            | ✔          |
| 检测mybatis接口中方法是否有实现，没有则报红 可创建一个空的xml方法块 | ✔            | ✔          |
| 检测resultmap的property是否有误                              | ✔            | ✔          |
| 支持spring 将mapper注入到spring中 intellij的spring注入不再报错 支持springboot | ✔            | ✔          |
| 一键生成分页查询                                             | ✔            | ✔          |
| 代码模版，生成cdata和collection语句                          | ✔            | ✔          |
| 一键添加resultMap中未被使用的属性                            | ✔            | ✔          |
| 一键生成mybatis接口的testcase                                | ✘            | ✔          |
| 通过方法名生成sql                                            | ✘            | ✔          |
| 通过数据库生成crud代码                                       | ✘            | ✔          |
| **通过java类生成crud代码**                                   | ✘            | ✔          |
| xml collection中的 param提示                                 | ✘            | ✔          |
| 识别mybatis的标签 全自动sql补全                              |              |            |

#### 总结

1. xml和Mapper之间相互跳转，代码提示，检查
2. 在model或者Mapper类中,右键可以自动生成
3. 在Mapper类中，输入关键字，比如getByUsername，之后ALT+Enter会自动提示实现XML文件
4. 在数据库中可以右键表一键generator



### TkMybatis

好处: 基于注解，无需编写xml文件

#### 基本使用

1. 在model中配置注解，其中

   ```
   @Table指定表名，@Id指定id，@Column指定对应的数据库字段名，
   @GeneratedValue中strategy表示使用数据库自带的主键生成策略.
   @GeneratedValue中generator配置为"JDBC",在数据插入完毕之后,会自动将主键id填充到实体类中.类似普通mapper.xml中配置的selectKey标签
   ```

   例子：

   ```
   @Data
   @Table(name = "test_person")
   public class Person implements Serializable {
   
       /**
        * id
        */
       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY, generator = "JDBC")
       @Column(name = "tid")
       private Integer id;
   
       /**
        * 用户名
        */
       @Column(name = "username")
       private String username;
   ```

   2.  在Mapper接口中配置@Mapper注解，或者在Application类配置@MapperScan注解扫描Mapper接口。并且在Mapper接口中继承tk.mybatis.mapper.common.Mappe和MysqlMapper.
   3. 无需编写Mapper.xml，直接测试即可

Q: 关于Mapper层中@Param的作用

```
Person get(@Param("id")Integer id);
```

A: 为了传递多个参数，解决的是可读性和直观性