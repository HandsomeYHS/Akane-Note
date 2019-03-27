# 毁灭吧 bug

Q: IDEA中项目启动失败？Disconnected from the target VM, address: '127.0.0.1:56091', transport: 'socket'

项目依赖问题

A:当编写自动测试类的时候，IDEA自动在其他服务中导入了模块。惨，搞了一个下午。



Q: serialVersionUID的作用？

A：验证类版本的标识，用于序列化和反序列化中的对接。如果没有指定，会通过类名、方法名等众多因素计算而得到一个值。

如果我们不希望通过编译来强制划分软件版本，即实现序列化接口的实体能够兼容先前版本，未作更改的类，就需要显式地定义一个名为serialVersionUID，类型为long的变量，不修改这个变量值的序列化实体都可以相互进行串行化和反串行化。**serialVersionUID为了让该类别 Serializable向后兼容。如果你修改了此类, 要修改此值**.

```
 * If a serializable class does not explicitly declare a serialVersionUID, then
 * the serialization runtime will calculate a default serialVersionUID value
 * for that class based on various aspects of the class,
 
 * Therefore, to guarantee a consistent serialVersionUID value across different java
 * compiler implementations, a serializable class must declare an explicit
 * serialVersionUID value. 
 因此，为了保证跨不同java编译器实现的一致的serialVersionUID值，可序列化类必须声明显式的serialVersionUID值。
```





