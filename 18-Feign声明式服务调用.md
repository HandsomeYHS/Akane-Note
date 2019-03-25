# Feign声明式服务调用



Spring cloud feign





在feign上使用hystrix

1. 在application.yml添加hystrix开启
2. 创建Fallback类，实现feign客户端接口
3. 在feign客户端上给你添加fallback属性