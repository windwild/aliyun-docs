### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 超时配置

# 超时配置

更新时间：2024-02-21 02:13:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

客户端超时配置

服务端方法超时配置

本文介绍开发HSF应用过程中如何进行超时配置。

## 前提条件

在开发应用前，您已经完成以下工作：

- [配置SAE的私服地址和轻量级配置及注册中心](https://help.aliyun.com/zh/sae/configure-the-internal-repository-path-and-the-lightweight-configuration-center-of-sae#task-1938002 "")

- [启动轻量级配置及注册中心](https://help.aliyun.com/zh/sae/start-the-lightweight-configuration-center#task-2310117 "")


## 背景信息

有关网络调用的请求，都需要配置超时，HSF的默认超时时间是3000ms。客户端和服务端都可以设置超时，默认优先采用客户端的配置，如果客户端没有配置，使用服务端的超时配置。 在服务端设置超时时，需要考虑到业务本身的执行耗时，加上序列化和网络通讯的时间。所以推荐服务端给每个服务都配置个默认的时间。当然客户端也可以根据自己的业务场景配置超时时间，例如一些前端应用，需要用户快速看到结果，可以把超时时间设置小一些。

配置的作用范围、作用域，按照优先级由高到低如下表所示。

| **优先级** | **API** | **范围** | **作用域** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **优先级** | **API** | **范围** | **作用域** |
| 0 | com.taobao.hsf.util.RequestCtxUtil#setRequestTimeout | 客户端 | 单次调用 |
| 1 | HSFApiConsumerBean#setMethodSpecials | 客户端 | 方法 |
| 2 | HSFApiConsumerBean#setClientTimeout | 客户端 | 接口 |
| 3 | defaultHsfClientTimeout | 客户端 | 所有接口 |
| 4 | HSFApiProviderBean#setMethodSpecials | 服务端 | 方法 |
| 5 | HSFApiProviderBean#setClientTimeout | 服务端 | 接口 |

**说明**

客户端配置优先于服务端，方法优先于接口。

## 客户端超时配置

- API形式配置HSF服务。

配置HSFApiConsumerBean的clientTimeout属性，单位是ms，我们把接口的超时配置为1000ms，方法queryOrder配置为100ms, 代码如下。















```java
HSFApiConsumerBean consumerBean = new HSFApiConsumerBean();
// 接口级别超时配置
consumerBean.setClientTimeout(1000);
MethodSpecial methodSpecial = new MethodSpecial();
methodSpecial.setMethodName("queryOrder");
// 方法级别超时配置，优先于接口超时配置
methodSpecial.setClientTimeout(100);
consumerBean.setMethodSpecials(new MethodSpecial[]{methodSpecial});
```

- Spring配置HSF服务。



Spring框架是在应用中广泛使用的组件，如果不想通过API的形式配置HSF服务，可以使用Spring XML的形式进行配置，上述例子中的API配置等同于如下XML配置。

















```xml
<bean id="CallHelloWorld" class="com.taobao.hsf.app.spring.util.HSFSpringConsumerBean">
      ...
      <property name="clientTimeout" value="1000" />
      <property name="methodSpecials">
        <list>
          <bean class="com.taobao.hsf.model.metadata.MethodSpecial">
            <property name="methodName" value="queryOrder" />
            <property name="clientTimeout" value="100" />
          </bean>
        </list>
      </property>
      ...
</bean>
```

- 注解配置。



SpringBoot广泛使用的今天，使用注解装配SpringBean也成为一种选择，HSF也支持使用注解进行配置，用来订阅服务。



1. 在项目中增加依赖starter。















     ```xml
     <dependency>
         <groupId>com.alibaba.boot</groupId>
         <artifactId>pandora-hsf-spring-boot-starter</artifactId>
     </dependency>
     ```

2. 在代码中注解配置。

     通常一个HSF Consumer需要在多个地方使用，但并不需要在每次使用的地方都用 @HSFConsumer来标记。只需要写一个统一Config类，然后在其他需要使用的地方，直接@Autowired注入即可。上述例子中的API配置等同于如下注解配置。















     ```java
      @HSFConsumer(clientTimeout = 1000, methodSpecials = @HSFConsumer.ConsumerMethodSpecial(methodName = "queryOrder", clientTimeout = "100"))
      private OderService orderService;
     ```


- 客户端全局接口超时配置。

  - 在启动参数中添加`-DdefaultHsfClientTimeout=100`

  - 在代码中添加`System.setProperty("defaultHsfClientTimeout", “100”)`

## 服务端方法超时配置

- API配置HSF服务。

配置HSFApiProviderBean的clientTimeout属性，单位是ms，代码如下。















```java
HSFApiProviderBean providerBean = new HSFApiProviderBean();
// 接口级别超时配置providerBean.setClientTimeout(1000);
MethodSpecial methodSpecial = new MethodSpecial();
methodSpecial.setMethodName("queryOrder");
// 方法级别超时配置，优先于接口超时配置methodSpecial.setClientTimeout(100);
providerBean.setMethodSpecials(new MethodSpecial[]{methodSpecial});
```

- Spring配置HSF服务。

Spring框架是在应用中广泛使用的组件，如果不想通过API的形式配置HSF服务，可以使用Spring XML的形式进行配置，上述例子中的API配置等同于如下XML配置。















```xml
<bean class="com.taobao.hsf.app.spring.util.HSFSpringProviderBean" init-method="init">
      ...
      <property name="clientTimeout" value="1000" />
      <property name="methodSpecials">
        <list>
          <bean class="com.taobao.hsf.model.metadata.MethodSpecial">
            <property name="methodName" value="queryOrder" />
            <property name="clientTimeout" value="2000" />
          </bean>
        </list>
      </property>
      ...
</bean>
```

- 注解配置HSF服务。

上述例子中的API配置等同于如下注解配置。















```java
@HSFProvider(serviceInterface = OrderService.class, clientTimeout = 3000)
public class OrderServiceImpl implements OrderService {
      @Autowired
      private OrderDAO orderDAO;

      @Override
      public OrderModel queryOrder(Long id) {
          return orderDAO.queryOrder(id);
      }
}
```