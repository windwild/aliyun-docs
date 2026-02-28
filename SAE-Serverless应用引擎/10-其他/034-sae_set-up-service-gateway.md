### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [应用开发](https://help.aliyun.com/zh/sae/sae-2-application-development/) [使用Spring Cloud开发应用](https://help.aliyun.com/zh/sae/spring-cloud-development/) 搭建服务网关

# 搭建服务网关

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实现配置管理](https://help.aliyun.com/zh/sae/manage-application-configurations)[下一篇：使用Dubbo开发应用](https://help.aliyun.com/zh/sae/use-dubbo-to-develop-applications/)

该文章对您有帮助吗？

反馈

本文介绍如何基于Spring Cloud Gateway和Spring Cloud Netflix Zuul使用Nacos搭建应用的服务网关。

## 为什么使用SAE服务注册中心

SAE服务注册中心提供了开源Nacos Server的商用版本，使用开源版本`Spring Cloud Alibaba Nacos Discovery`开发的应用可以直接使用SAE提供的商业版服务注册中心。

SAE服务注册中心与Nacos、Eureka和Consul相比，具有以下优势：

- 共享组件，节省了部署、运维Nacos、Eureka或Consul的成本。
- 在服务注册和发现的调用中都进行了链路加密，保护您的服务，无需再担心服务被未授权的应用发现。
- SAE服务注册中心与SAE其他组件紧密结合，为您提供一整套的微服务解决方案，包括环境隔离、灰度发布等。

您在SAE部署应用时，SAE服务注册中心以高优先级自动设置Nacos Server服务端地址和服务端口，以及命名空间、AccessKey等信息，无需进行任何额外的配置。

## 基于Spring Cloud Gateway搭建服务网关

介绍如何使用Nacos基于Spring Cloud Gateway从零搭建应用的服务网关。

1. 创建服务网关。

1. 创建命名为`spring-cloud-gateway-nacos`的Maven工程。

2. 在`pom.xml`文件中添加Spring Boot和Spring Cloud的依赖。



      以Spring Boot 2.1.4.RELEASE和Spring Cloud Greenwich.SR1版本为例。



      ```xml
       <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.1.4.RELEASE</version>
           <relativePath/>
       </parent>

       <dependencies>
           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-gateway</artifactId>
           </dependency>
           <dependency>
               <groupId>com.alibaba.cloud</groupId>
               <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
               <version>2.1.1.RELEASE</version>
           </dependency>
       </dependencies>

       <dependencyManagement>
           <dependencies>
               <dependency>
                   <groupId>org.springframework.cloud</groupId>
                   <artifactId>spring-cloud-dependencies</artifactId>
                   <version>Greenwich.SR1</version>
                   <type>pom</type>
                   <scope>import</scope>
               </dependency>
           </dependencies>
       </dependencyManagement>

       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
      ```

3. 开发服务网关启动类`GatewayApplication`。



      ```java
          @SpringBootApplication
          @EnableDiscoveryClient
          public class GatewayApplication {
              public static void main(String[] args) {
                  SpringApplication.run(GatewayApplication.class, args);
              }
          }
      ```

4. 在`application.yaml`中添加如下配置，将注册中心指定为Nacos Server的地址。



      其中`127.0.0.1:8848`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的地址。



      其中routes配置了Gateway的路由转发策略，这里我们配置将所有前缀为`/provider1/`的请求都路由到服务名为`service-provider`的后端服务中。



      ```yaml
      server:
       port: 18012

      spring:
       application:
              name: spring-cloud-gateway-nacos
       cloud:
              gateway: # config the routes for gateway
                routes:
          - id: service-provider          #将/provider1/开头的请求转发到provider1
            uri: lb://service-provider
            predicates:
            - Path=/provider1/**
            filters:
            - StripPrefix=1               #表明前缀/provider1需要截取掉
        nacos:
          discovery:
            server-addr: 127.0.0.1:8848
```

   5. 执行启动类`GatewayApplication`中的main函数，启动Gateway。

   6. 登录本地启动的Nacos Server控制台http://127.0.0.1:8848/nacos（本地Nacos控制台的默认用户名和密码同为nacos），在左侧导航栏中选择**服务管理** \> **服务列表**，可以看到服务列表中已经包含了spring-cloud-gateway-nacos，且在详情中可以查询该服务的详情。表明网关已经启动并注册成功，接下来我们将通过创建一个下游服务来验证网关的请求转发功能。
2. 创建服务提供者。



   创建一个服务提供者的应用，请参见[将应用的服务注册与发现中心更改为Nacos](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "")。





   服务提供者示例：



   ```java
   @SpringBootApplication
   @EnableDiscoveryClient
   public class ProviderApplication {

       public static void main(String[] args) {

           SpringApplication.run(ProviderApplication, args);
       }

       @RestController
       public class EchoController {
           @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
           public String echo(@PathVariable String string) {
               return string;
           }
       }
   }
   ```

3. 结果验证。

   - 本地验证。

     本地启动开发好的服务网关和服务提供者，通过访问Spring Cloud Gateway将请求转发给后端服务，可以看到调用成功的结果。

     ![EDAS SpringCloud应用开发之搭建服务网管](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2398561961/p66814.png)

   - 在SAE中验证。

     SAE服务注册中心提供了正式商用版本Nacos。当您将应用部署到SAE的时候，SAE会直接替换本地Nacos Server的地址和服务端口，以及namespace、access-key、secret-key、context-path信息。您无需进行任何额外的配置，原有的配置内容可以选择保留或删除。

## 基于Zuul搭建服务网关

介绍如何基于Zuul使用Nacos作为服务注册中心从零搭建应用的服务网关。

1. 创建服务网关。

   1. 创建命名为`spring-cloud-zuul-nacos`的Maven工程。

   2. 在`pom.xml`文件中添加Spring Boot、Spring Cloud和Spring Cloud Alibaba的依赖。



      请添加Spring Boot 2.1.4.RELEASE、Spring Cloud Greenwich.SR1和Spring Cloud Alibaba 0.9.0版本依赖。



      ```xml
       <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.1.4.RELEASE</version>
           <relativePath/>
       </parent>

       <dependencies>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-webflux</artifactId>
           </dependency>

           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
           </dependency>
           <dependency>
               <groupId>com.alibaba.cloud</groupId>
               <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
               <version>2.1.1.RELEASE</version>
           </dependency>
       </dependencies>

       <dependencyManagement>
           <dependencies>
               <dependency>
                   <groupId>org.springframework.cloud</groupId>
                   <artifactId>spring-cloud-dependencies</artifactId>
                   <version>Greenwich.SR1</version>
                   <type>pom</type>
                   <scope>import</scope>
               </dependency>
           </dependencies>
       </dependencyManagement>

       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
      ```

   3. 开发服务网关启动类`ZuulApplication`。



      ```java
          @SpringBootApplication
          @EnableZuulProxy
          @EnableDiscoveryClient
          public class ZuulApplication {
              public static void main(String[] args) {
                  SpringApplication.run(ZuulApplication.class, args);
              }
          }
      ```

   4. 在`application.properties`中添加如下配置，将注册中心指定为Nacos Server的地址。



      其中`127.0.0.1:8848`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的地址。



      其中routes配置了Zuul的路由转发策略，这里我们配置将所有前缀为`/provider1/`的请求都路由到服务名为`service-provider`的后端服务中。



      ```properties
       spring.application.name=spring-cloud-zuul-nacos
       server.port=18022

       spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848

       zuul.routes.opensource-provider1.path=/provider1/**
       zuul.routes.opensource-provider1.serviceId=service-provider
      ```

   5. 执行spring-cloud-zuul-nacos中的main函数`ZuulApplication`，启动服务。

   6. 登录本地启动的Nacos Server控制台http://127.0.0.1:8848/nacos （本地Nacos控制台的默认用户名和密码同为nacos），在左侧导航栏中选择服务管理 > 服务列表，可以看到服务列表中已经包含了spring-cloud-zuul-nacos，且在详情中可以查询该服务的详情。表明网关已经启动并注册成功，接下来我们将通过创建一个下游服务来验证网关的请求转发功能。
2. 创建服务提供者。



   如何快速创建一个服务提供者，请参见[将应用的服务注册与发现中心更改为Nacos](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "")。





   服务提供者启动类示例：



   ```java
   @SpringBootApplication
   @EnableDiscoveryClient
   public class ProviderApplication {

       public static void main(String[] args) {

           SpringApplication.run(ProviderApplication, args);
       }

       @RestController
       public class EchoController {
           @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
           public String echo(@PathVariable String string) {
               return string;
           }
       }
   }
   ```

3. 结果验证。

   - 本地验证。

     本地启动开发好的服务网关Zuul和服务提供者，通过访问Spring Cloud Netflix Zuul将请求转发给后端服务，可以看到调用成功的结果。

     ![EDAS SpringCloud应用开发之搭建Zuul网管](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5145559951/p66815.png)

   - 在SAE中验证。

     您将应用部署到SAE，并验证。具体操作，请参见[将应用的服务注册与发现中心更改为Nacos](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "")。

     SAE服务注册中心提供了正式商用版本Nacos。当您将应用部署到SAE的时候，SAE会直接替换本地Nacos Server的地址和服务端口，以及namespace、access-key、secret-key、context-path信息。您无需进行任何额外的配置，原有的配置内容可以选择保留或删除。

## 版本说明

- 示例中使用的Spring Cloud版本为Greenwich，对应的Spring Cloud Alibaba版本为2.1.1.RELEASE。

- Spring Cloud Finchley对应的Spring Cloud Alibaba版本为2.0.1.RELEASE。

- Spring Cloud Edgware对应的Spring Cloud Alibaba版本为1.5.1.RELEASE。


**说明**

Spring Cloud Edgware版本的生命周期已结束，不推荐使用这个版本开发应用。