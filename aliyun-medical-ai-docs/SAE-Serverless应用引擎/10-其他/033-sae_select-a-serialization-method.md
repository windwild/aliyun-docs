序列化的过程是将Java对象转成byte数组在网络中传输，反序列化会将byte数组转成Java对象。

## 简介

序列化的选择需要考虑兼容性，性能等因素，HSF的序列化方式支持java、hessian2，默认是hessian2。序列化方式的对比和配置（只在服务端配置HSFApiProviderBean）如下表所示。

| 序列化方式 | Maven依赖 | 配置 | 兼容性 | 性能 |
| --- | --- | --- | --- | --- |

| 序列化方式 | Maven依赖 | 配置 | 兼容性 | 性能 |
| --- | --- | --- | --- | --- |
| hessian2 | <artifactId>hsf-io-serialize-hessian2</artifactId> | `setPreferSerializeType("hessian2")` | 好 | 好 |
| java | <artifactId>hsf-io-serialize-java</artifactId> | `setPreferSerializeType("java")` | 佳 | 一般 |

## 前提条件

在开发应用前，您已经完成以下工作：


- [配置SAE的私服地址和轻量级配置及注册中心](https://help.aliyun.com/zh/edas/developer-reference/configure-the-internal-repository-path-and-the-light-weight-configuration-center-of-edas#task-2310132 "使用Pandora Boot开发HSF应用前，需要先配置SAE的私服地址和轻量级配置及注册中心。")
- [启动轻量级配置及注册中心](https://help.aliyun.com/zh/edas/developer-reference/start-the-lightweight-configuration-center-1#task-2310117 "开发者可以在本地使用轻量级配置及注册中心实现应用的注册、发现和配置管理，完成应用的开发和测试。在将应用部署到后，这些功能仍然可以正常使用。本文介绍如何下载、启动和验证轻量级配置及注册中心。")

## API形式配置HSF服务

```abnf
HSFApiProviderBean hsfApiProviderBean = new HSFApiProviderBean();
hsfApiProviderBean.setPreferSerializeType("hessian2");
```

## Spring配置HSF服务

Spring框架是在应用中广泛使用的组件，如果不想通过API的形式配置HSF服务，可以使用Spring XML的形式进行配置，上述例子中的API配置等同于如下XML配置。

```xml
<bean class="com.taobao.hsf.app.spring.util.HSFSpringProviderBean" init-method="init">
    <!--[设置] 发布服务的接口 -->
    <property name="serviceInterface" value="com.alibaba.middleware.hsf.guide.api.service.OrderService"/>
    <!--[设置] 服务的实现对象target必须配置 [ref]，为需要发布为HSF服务的spring bean id-->
    <property name="target" ref="引用的BeanId"/>
    <!--[设置] 服务的版本 -->
    <property name="serviceVersion" value="1.0.0"/>
    <!--[设置] 服务的归组 -->
    <property name="serviceGroup" value="HSF"/>
    <!--[设置] 服务的响应时间 -->
    <property name="clientTimeout" value="3000"/>
    <!--[设置]  服务传输业务对象时的序列化类型 -->
    <property name="preferSerializeType" value="hessian2"/>
</bean>
```

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 序列化方式选择

# 序列化方式选择

更新时间：2021-05-21 04:03:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

前提条件

API形式配置HSF服务

Spring配置HSF服务