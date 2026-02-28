本文介绍开发HSF应用过程中如何进行服务端线程池配置。

## 前提条件

在开发应用前，您已经完成以下工作：

- [配置SAE的私服地址和轻量级配置及注册中心](https://help.aliyun.com/zh/sae/configure-the-internal-repository-path-and-the-lightweight-configuration-center-of-sae#task-1938002 "")
- [启动轻量级配置及注册中心](https://help.aliyun.com/zh/sae/start-the-lightweight-configuration-center#task-2310117 "")

## 服务线程池业务示意图

HSF服务端线程池主要分为IO线程和业务线程，其中IO线程模型就是netty reactor网络模型中使用的。我们主要讨论业务线程池的配置。业务线程池分为默认业务线程池和服务线程池，其中服务线程池是从默认线程池中分割出来的。

![服务线程业务示意图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2445559951/p65772.png)

## 默认线程池配置

服务端线程池是用来执行业务逻辑的线程池，线程池默认的core size是50，max size是720，keepAliveTime 500s。队列使用的是SynchronousQueue，没有缓存队列，不会堆积用户请求。
当服务端线程池所有线程（720）都在处理请求时，对于新的请求，会立即拒绝，返回Thread pool is full异常。可以使用下面VM参数（-D参数）进行配置。


- 线程池最小配置：`-Dhsf.server.min.poolsize`
- 线程池最大配置：`-Dhsf.server.max.poolsize`
- 线程收敛的存活时间：`-Dhsf.server.thread.keepalive`

## 服务线程池配置

对于一些慢服务、并发高，可以为其单独配置线程池，以免占用过多的业务线程，影响应用的其他服务的调用。

- API形式配置HSF服务















```abnf
HSFApiProviderBean hsfApiProviderBean = new HSFApiProviderBean();

hsfApiProviderBean.setCorePoolSize("50");
hsfApiProviderBean.setMaxPoolSize("200");
```

- Spring配置HSF服务

Spring框架是在应用中广泛使用的组件，如果不想通过API的形式配置HSF服务，可以使用Spring XML的形式进行配置，上述例子中的API配置等同于如下XML配置。















```xml
<bean class="com.taobao.hsf.app.spring.util.HSFSpringProviderBean" init-method="init">
      <!--[设置] 发布服务的接口 -->
      <property name="serviceInterface" value="com.alibaba.middleware.hsf.guide.api.service.OrderService"/>
      <property name="corePoolSize" value="50" />
      <property name="maxPoolSize" value="200" />
</bean>
```

- 注解配置HSF服务

SpringBoot广泛使用的今天，使用注解装配SpringBean也成为一种选择，HSF也支持使用注解进行配置，用来发布服务。

1. 在项目中增加依赖starter。















     ```xml
     <dependency>
         <groupId>com.alibaba.boot</groupId>
         <artifactId>pandora-hsf-spring-boot-starter</artifactId>
     </dependency>
     ```

2. 将 @HSFProvider配置到实现的类型。

     上述例子中的API配置等同于如下注解配置。
















     ```kotlin
     @HSFProvider(serviceInterface = OrderService.class, corePoolSize = 50, maxPoolSize = 200)
     public class OrderServiceImpl implements OrderService {
         @Autowired
         private OrderDAO orderDAO;

         @Override
         public OrderModel queryOrder(Long id) {
             return orderDAO.queryOrder(id);
         }
     }
     ```

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 服务端线程池配置

# 服务端线程池配置

更新时间：2022-11-22 04:21:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

服务线程池业务示意图

默认线程池配置

服务线程池配置