# cas单点登录

[TOC]



> CAS是Central Authentication Service的缩写，**中央认证服务**，一种独立开放指令协议。CAS 是 [Yale](https://baike.baidu.com/item/Yale/10754982) 大学发起的一个开源项目，旨在为 Web 应用系统提供一种可靠的单点登录方法，CAS 在 2004 年 12 月正式成为 JA-SIG 的一个项目。



非对称加密

> 对称加密[算法](https://baike.baidu.com/item/%E7%AE%97%E6%B3%95)在加密和解密时使用的是同一个秘钥；而[非对称加密算法](https://baike.baidu.com/item/%E9%9D%9E%E5%AF%B9%E7%A7%B0%E5%8A%A0%E5%AF%86%E7%AE%97%E6%B3%95/1208652)需要两个[密钥](https://baike.baidu.com/item/%E5%AF%86%E9%92%A5/101144)来进行加密和解密，这两个秘钥是[公开密钥](https://baike.baidu.com/item/%E5%85%AC%E5%BC%80%E5%AF%86%E9%92%A5/7453570)（public key，简称公钥）和私有密钥（private key，简称私钥）。

**如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。**





安装证书

使用keytool，内部证书、外部证书（服务器和客户端证书）



cas shiro

1.  shiro本身通过继承realm的方式来进行登录认证 当接入cas后 则**通过cas-server来进行登录认证** 详见org.apache.shiro.cas.CasRealm
2.  通过shiroFilter来对请求路径的登录状态验证 详见org.apache.shiro.cas.CasFilter

