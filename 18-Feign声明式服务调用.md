# Feign声明式服务调用



Spring cloud feign





在feign上使用hystrix

1. 在application.yml添加hystrix开启
2. 创建Fallback类，实现feign客户端接口
3. 在feign客户端上给你添加fallback属性



## Feign工作机制

`Feign` 通过注解注入一个模板化请求进行工作。只需在发送之前关闭它，参数就可以被直接的运用到模板中。然而这也限制了 `Feign`，只支持文本形式的API，它在响应请求等方面极大的简化了系统。同时，它也是十分容易进行单元测试的。