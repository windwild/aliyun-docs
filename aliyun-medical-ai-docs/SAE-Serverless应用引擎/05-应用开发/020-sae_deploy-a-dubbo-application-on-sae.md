### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用开发](https://help.aliyun.com/zh/sae/sae-2-application-development/)[使用Dubbo开发应用](https://help.aliyun.com/zh/sae/use-dubbo-to-develop-applications/)将Dubbo应用托管到SAE

# 将Dubbo应用托管到SAE

更新时间：2025-02-20 22:40:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Dubbo开发概述](https://help.aliyun.com/zh/sae/dubbo-development-overview)[下一篇：使用Spring Boot开发Dubbo应用](https://help.aliyun.com/zh/sae/use-spring-boot-to-develop-dubbo-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么托管到SAE

准备工作

版本说明

步骤一：创建服务提供者

步骤二：创建服务消费者

步骤三：部署到SAE

本文以包含服务提供者（本文简称Provider）和服务消费者（本文简称Consumer）的Dubbo微服务应用为例，介绍如何在本地通过XML配置的方式，开发Dubbo微服务示例应用，并部署到Serverless 应用引擎 SAE（Serverless App Engine）。

## 为什么托管到SAE

将Dubbo应用托管到SAE，您仅需关注Dubbo应用自身的逻辑，无需再关注注册中心和配置中心搭建和维护，托管后还可以使用SAE提供的弹性伸缩、一键启停和监控等功能，有效降低开发和运维成本。

当您的微服务应用较多时，注册中心按推荐程度由高到低依次排序如下：

- 商业版的服务注册中心（MSE）

- 自建服务注册中心

- SAE内置服务注册中心


如果您选择商业版的服务注册中心，即使用MSE的Nacos作为服务注册中心，具体操作，请参见 [使用MSE的Nacos注册中心](https://help.aliyun.com/zh/sae/sae-2-microservices-use-an-mse-nacos-registry "")。

如果您选择使用自建Nacos作为服务注册中心，具体操作，请参见 [使用自建Nacos服务注册中心](https://help.aliyun.com/zh/sae/sae-2-microservices-use-a-self-managed-nacos-service-registry "")。

您需要确认以下内容：

- 确保SAE的网络与自建Nacos的网络互通。

- 确保`-D`和`-XX`参数未交替使用，以免命令失效。示例代码如下：

  - 修改前：















    ```plaintext
    java -Dalicloud.deployment.mode=EDAS_MANAGED -XX:+UseContainerSupport -XX:InitialRAMPercentage=70.0 -XX:MaxRAMPercentage=70.0 -XX:+UnlockExperimentalVMOptions -XX:+UseWisp2 -Dio.netty.transport.noNative=true -XX:+UseG1GC -Dspring.profiles.active=yace -Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false -jar /home/admin/app/xx-server.jar
    ```

  - 修改后：















    ```plaintext
    java -XX:+UseContainerSupport -XX:InitialRAMPercentage=70.0 -XX:MaxRAMPercentage=70.0 -XX:+UnlockExperimentalVMOptions -XX:+UseWisp2 -Dio.netty.transport.noNative=true -XX:+UseG1GC -Dspring.profiles.active=yace -Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false -jar /home/admin/app/xx-server.jar
    ```
- 建议在部署应用时，使用镜像或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。



**重要**





启动参数需要放在`-jar`之前，否则可能会导致无法使用非SAE自带的注册中心。





  - 如果采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件的程序启动命令中。Docker镜像制作方法，请参见 [制作Java镜像](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/use-cases/create-an-image-to-deploy-a-java-application#concept-98492-zh "")。

    示例代码如下：















    ```plaintext
    RUN echo 'eval exec java -Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false -jar $CATALINA_OPTS /home/admin/app/hello-edas-0.0.1-SNAPSHOT.jar'> /home/admin/start.sh && chmod +x /home/admin/start.sh
    ```

  - 如果采用JAR包方式，请在控制台 **启动命令设置** 区域的 **options设置** 文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。图示为 **Open JDK 8** 运行环境下的Java应用。具体操作，请参见 [设置启动命令](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configure-a-startup-command#concept-96677-zh "")。![sc_configure_a_startup_command_for_nacos](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5025813461/p378414.png)

## 准备工作

- 下载 [Maven](https://maven.apache.org/download.cgi) 并设置环境变量。

- 启动Nacos Server。

1. 下载并解压 [Nacos Server](https://github.com/alibaba/nacos/releases)。

2. 进入nacos/bin目录，启动Nacos Server。


     - Linux、Unix、macOS系统：执行命令`sudo sh startup.sh -m standalone`。

     - Windows系统：执行命令`startup.cmd -m standalone`。


**说明**

`standalone`表示单机模式运行，非集群模式。startup.cmd文件默认以集群模式启动，因此您在使用Windows系统时，如果直接双击执行startup.cmd文件会导致启动失败，此时需要在startup.cmd文件内设置`MODE="standalone"`。 更多信息，请参见[Nacos快速开始](https://nacos.io/zh-cn/docs/v2/quickstart/quick-start.html)。

## 版本说明

Dubbo 2.7.x、Dubbo 3.0.x 版本的生命周期已于2023年03月结束，请使用新版本开发您的应用。本文以Dubbo 3.2.15版本为例，介绍如何将Dubbo应用托管到SAE。

## 步骤一：创建服务提供者

在本地创建一个提供者应用工程，添加依赖、配置服务注册与发现，并将注册中心指定为Nacos。

1. 创建Maven项目并引入依赖。

1. 使用IDE（如IntelliJ IDEA或Eclipse）创建一个Maven项目。

2. 在`pom.xml`文件中添加dubbo、dubbo-registry-nacos和nacos-client依赖。

















      ```xml
      <dependencies>

          <dependency>
              <groupId>org.apache.dubbo</groupId>
              <artifactId>dubbo</artifactId>
              <version>3.2.15</version>
          </dependency>

          <dependency>
              <groupId>org.apache.dubbo</groupId>
              <artifactId>dubbo-registry-nacos</artifactId>
              <version>3.2.15</version>
          </dependency>

          <dependency>
              <groupId>com.alibaba.nacos</groupId>
              <artifactId>nacos-client</artifactId>
              <version>1.1.1</version>
          </dependency>
      </dependencies>
      ```
2. 开发Dubbo服务提供者。



Dubbo中服务都是以接口形式提供。



1. 在src/main/java路径下创建一个package`com.alibaba.edas`。

2. 在`com.alibaba.edas`下创建一个接口（interface）`IHelloService`，里面包含一个`sayHello`方法。

















      ```plaintext
        package com.alibaba.edas;

        public interface IHelloService {
            String sayHello(String str);
        }
      ```

3. 在`com.alibaba.edas`下创建一个类`IHelloServiceImpl`，实现此接口。

















      ```plaintext
        package com.alibaba.edas;

        public class IHelloServiceImpl implements IHelloService {
            public String sayHello(String str) {
                return "hello " + str;
            }
        }
      ```
3. 配置Dubbo服务。

1. 在src/main/resources路径下创建`provider.xml`文件并打开。

2. 在`provider.xml`中，添加Spring相关的XML Namespace（xmlns）和XML Schema Instance（xmlns:xsi），以及Dubbo相关的Namespace（xmlns:dubbo）和Schema Instance（xsi:schemaLocation）。

















      ```xml
      <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
      xmlns="http://www.springframework.org/schema/beans"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
      http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
      ```

3. 在`provider.xml`中将接口和实现类暴露成Dubbo服务。

















      ```plaintext
        <dubbo:application name="demo-provider"/>

        <dubbo:protocol name="dubbo" port="28082"/>

        <dubbo:service interface="com.alibaba.edas.IHelloService" ref="helloService"/>

        <bean id="helloService" class="com.alibaba.edas.IHelloServiceImpl"/>
      ```

4. 在`provider.xml`中将注册中心指定为本地启动的Nacos Server。

















      ```xml
      <dubbo:registry address="nacos://127.0.0.1:8848" />
      ```





      - `127.0.0.1`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的IP地址。当将应用部署到SAE后，无需做任何修改，注册中心会替换成SAE上的注册中心的地址。

      - `8848`为Nacos Server的端口号，不可修改。
4. 启动服务。

1. 在`com.alibaba.edas`中创建类Provider，并按下面的代码在Provider的main函数中加载Spring Context，将配置好的Dubbo服务暴露。

















      ```java
      package com.alibaba.edas;

      import org.springframework.context.support.ClassPathXmlApplicationContext;

      public class Provider {
          public static void main(String[] args) throws Exception {
              ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"provider.xml"});
              context.start();
              System.in.read();
          }
      }
      ```

2. 执行Provider的main函数，启动服务。
5. 登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击 **服务列表**，查看提供者列表。



可以看到服务提供者里已经包含了`com.alibaba.edas.IHelloService`，且可以查询该服务的 **服务分组** 和 **提供者IP**。


## 步骤二：创建服务消费者

在本地创建一个消费者应用工程，添加依赖、订阅服务的配置。

1. 创建Maven项目并引入依赖。

1. 使用IDE（如IntelliJ IDEA或Eclipse）创建一个Maven项目。

2. 在`pom.xml`文件中添加dubbo、dubbo-registry-nacos和nacos-client依赖。

















      ```xml
      <dependencies>

          <dependency>
              <groupId>org.apache.dubbo</groupId>
              <artifactId>dubbo</artifactId>
              <version>3.2.15</version>
          </dependency>

          <dependency>
              <groupId>org.apache.dubbo</groupId>
              <artifactId>dubbo-registry-nacos</artifactId>
              <version>3.2.15</version>
          </dependency>

          <dependency>
              <groupId>com.alibaba.nacos</groupId>
              <artifactId>nacos-client</artifactId>
              <version>1.1.1</version>
          </dependency>
      </dependencies>
      ```
2. 开发Dubbo服务消费者。



Dubbo中服务都是以接口形式提供。



1. 在src/main/java路径下创建Package，命名为`com.alibaba.edas`。

2. 在`com.alibaba.edas`下创建一个接口（interface）`IHelloService`，里面包含一个`SayHello`方法。





      **说明**





      通常是在一个单独的模块中定义接口，服务提供者和服务消费者都通过Maven依赖来引用此模块。本文为了简便，服务提供者和服务消费者分别创建两个完全一模一样的接口，实际使用中不推荐这样使用。





















      ```plaintext
        package com.alibaba.edas;

        public interface IHelloService {
            String sayHello(String str);
        }
      ```
3. 配置Dubbo服务。

1. 在src/main/resources路径下创建`consumer.xml`文件并打开。

2. 在`consumer.xml`中，添加Spring相关的XML Namespace（xmlns）和XML Schema Instance（xmlns:xsi），以及Dubbo相关的Namespace（xmlns:dubbo）和Schema Instance（xsi:schemaLocation）。

















      ```xml
      <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
      xmlns="http://www.springframework.org/schema/beans"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
      http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
      ```

3. 在`consumer.xml`中添加如下配置，订阅Dubbo服务。

















      ```plaintext
        <dubbo:application name="demo-consumer"/>

        <dubbo:registry address="nacos://127.0.0.1:8848"/>

        <dubbo:reference id="helloService" interface="com.alibaba.edas.IHelloService"/>
      ```
4. 启动并验证服务。

1. 在`com.alibaba.edas`下创建类Consumer，并按下面的代码在Consumer的main函数中加载Spring Context，订阅并消费Dubbo服务。

















      ```java
          package com.alibaba.edas;

          import org.springframework.context.support.ClassPathXmlApplicationContext;

          import java.util.concurrent.TimeUnit;

          public class Consumer {
              public static void main(String[] args) throws Exception {
                  ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"consumer.xml"});
                  context.start();
                  while (true) {
                      try {
                          TimeUnit.SECONDS.sleep(5);
                          IHelloService demoService = (IHelloService)context.getBean("helloService");
                          String result = demoService.sayHello("world");
                          System.out.println(result);
                      } catch (Exception e) {
                          e.printStackTrace();
                      }
                  }
              }
          }
      ```

2. 执行Consumer的main函数，启动服务。
5. 验证结果。



启动后，可以看到控制台不断地输出`hello world`，表明服务消费成功。



登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击 **服务列表**，再在 **服务列表** 页面选择 **调用者列表**。



可以看到包含了`com.alibaba.edas.IHelloService`，且可以查看该服务的 **服务分组** 和 **调用者IP**。


## 步骤三：部署到SAE

1. 分别在Provider和Consumer的pom.xml文件中添加如下配置，配置完成后执行mvn clean package将本地程序编译为可执行的JAR包。



   - Provider















     ```xml
     <build>
      <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                        <configuration>
                            <classifier>spring-boot</classifier>
                            <mainClass>com.alibaba.sae.Provider</mainClass>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
      </plugins>
     </build>
     ```

   - Consumer















     ```xml
     <build>
      <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                        <configuration>
                            <classifier>spring-boot</classifier>
                            <mainClass>com.alibaba.sae.Consumer</mainClass>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
      </plugins>
     </build>
     ```


2. 将编译好的Provider和Consumer应用包部署至SAE。具体操作，请参见 [使用JAR包部署Java应用](https://help.aliyun.com/zh/sae/deploy-java-applications-by-using-a-jar-package "")。