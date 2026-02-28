在HSF框架中开发RESTful应用，并实现服务注册与发现。由于SAE已经支持原生Spring Cloud框架的应用，新用户不推荐使用该开发方式。


## 背景信息

原生Spring Cloud框架下的服务开发请参考[将Spring Cloud应用托管到SAE](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "本文以包含服务提供者（Provider）和服务消费者（Consumer）的Spring Cloud微服务应用为例，指导您将原依赖Eureka、Consul、ZooKeeper等组件实现服务注册与发现的Spring Cloud应用部署到中，并实现应用的服务注册与发现，以及Consumer对Provider的调用。")。


## 服务注册与发现

通过一个简单的示例详细介绍如何在本地开发RESTful应用并实现注册与发现。

Demo源码下载：


- [sc-vip-server](https://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/sc-vip-server.zip)
- [sc-vip-client](https://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/sc-vip-client.zip)

1. 创建服务提供者。
此服务提供者提供了一个简单的echo服务，并将自身注册到服务发现中心。

1. 创建命名为sc-vip-server的RESTful应用工程。
2. 在pom.xml中添加需要的依赖。
















      ```xml
          <parent>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>1.5.8.RELEASE</version>
              <relativePath/>
          </parent>

          <dependencies>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-starter-vipclient</artifactId>
                  <version>1.3</version>
              </dependency>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-starter-pandora</artifactId>
                  <version>1.3</version>
              </dependency>
          </dependencies>

          <dependencyManagement>
              <dependencies>
                  <dependency>
                      <groupId>org.springframework.cloud</groupId>
                      <artifactId>spring-cloud-dependencies</artifactId>
                      <version>Dalston.SR4</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
              </dependencies>
          </dependencyManagement>
      ```





      如果您的工程不想将parent设置为`spring-boot-starter-parent`，也可以通过添加`dependencyManagement`并设置`scope=import`来达到依赖管理的效果。


















      ```xml
      <dependencyManagement>
                  <dependencies>
                      <dependency>
                          <groupId>org.springframework.boot</groupId>
                          <artifactId>spring-boot-dependencies</artifactId>
                          <version>1.5.8.RELEASE</version>
                          <type>pom</type>
                          <scope>import</scope>
                      </dependency>
                  </dependencies>
      </dependencyManagement>
      ```

3. 创建服务提供者应用，其中@EnableDiscoveryClient 注解表明此应用需开启服务注册与发现功能。
















      ```less
      @SpringBootApplication
          @EnableDiscoveryClient
          public class ServerApplication {

              public static void main(String[] args) {
                  PandoraBootstrap.run(args);
                  SpringApplication.run(ServerApplication.class, args);
                  PandoraBootstrap.markStartupAndWait();
              }
          }
      ```

4. 创建EchoController，提供简单的echo服务。
















      ```less
      @RestController
          public class EchoController {
              @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
              public String echo(@PathVariable String string) {
                  return string;
              }
          }
      ```

5. 在resources下的application.properties文件中配置应用名与监听端口号。
















      ```ini
      spring.application.name=service-provider
      server.port=18081
      ```
2. 创建服务消费者。
本示例中将创建一个服务消费者，通过RestTemplate、AsyncRestTemplate、FeignClient这三个客户端去调用服务提供者。

1. 创建名为sc-vip-client的RESTful应用工程。
2. 在pom.xml中引入需要的依赖。
















      ```xml
      <parent>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>1.5.8.RELEASE</version>
              <relativePath/>
          </parent>

          <dependencies>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-starter-vipclient</artifactId>
                  <version>1.3</version>
              </dependency>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-starter-pandora</artifactId>
                  <version>1.3</version>
              </dependency>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-starter-feign</artifactId>
              </dependency>
          </dependencies>

          <dependencyManagement>
              <dependencies>
                  <dependency>
                      <groupId>org.springframework.cloud</groupId>
                      <artifactId>spring-cloud-dependencies</artifactId>
                      <version>Dalston.SR4</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
              </dependencies>
          </dependencyManagement>
      ```





      本示例需要通过FeignClient进行演示，与sc-vip-server（服务提供者）相比，pom.xml文件中的依赖增加了`spring-cloud-starter-feign`。


3. 与sc-vip-server相比，除了开启服务与注册外，还需要添加下面两项配置才能使用RestTemplate、AsyncRestTemplate、FeignClient这三个客户端。


      - 添加@LoadBalanced注解将RestTemplate和AsyncRestTemplate与服务发现结合。

      - 使用@EnableFeignClients注解激活FeignClient。















        ```less
        @SpringBootApplication
            @EnableDiscoveryClient
            @EnableFeignClients
            public class ConsumerApplication {

                @LoadBalanced
                @Bean
                public RestTemplate restTemplate() {
                    return new RestTemplate();
                }

                @LoadBalanced
                @Bean
                public AsyncRestTemplate asyncRestTemplate(){
                    return new AsyncRestTemplate();
                }

                public static void main(String[] args) {
                    PandoraBootstrap.run(args);
                    SpringApplication.run(ConsumerApplication.class, args);
                    PandoraBootstrap.markStartupAndWait();
                }

            }
        ```


4. 在使用EchoService的FeignClient之前，还需要配置服务名以及方法对应的HTTP请求。在sc-vip-server工程中配置服务名service-provider。
















      ```less
      @FeignClient(name = "service-provider")
          public interface EchoService {
              @RequestMapping(value = "/echo/{str}", method = RequestMethod.GET)
              String echo(@PathVariable("str") String str);
          }
      ```

5. 创建一个Controller用于调用测试。
















      ```typescript
      @RestController
      public class Controller {
         @Autowired
         private RestTemplate restTemplate;
         @Autowired
         private AsyncRestTemplate asyncRestTemplate;
         @Autowired
         private  EchoService echoService;
         @RequestMapping(value = "/echo-rest/{str}", method = RequestMethod.GET)
         public String rest(@PathVariable String str) {
             return restTemplate.getForObject("http://service-provider/echo/" + str, String.class);
         }
         @RequestMapping(value = "/echo-async-rest/{str}", method = RequestMethod.GET)
         public String asyncRest(@PathVariable String str) throws Exception{
             ListenableFuture<ResponseEntity<String>> future = asyncRestTemplate.
                     getForEntity("http://service-provider/echo/"+str, String.class);
             return future.get().getBody();
         }
         @RequestMapping(value = "/echo-feign/{str}", method = RequestMethod.GET)
         public String feign(@PathVariable String str) {
             return echoService.echo(str);
         }
      }
      ```





      代码说明如下：


      - `/echo-rest/`验证通过RestTemplate去调用服务提供者。

      - `/echo-async-rest/`验证通过AsyncRestTemplate去调用服务提供者。

      - `/echo-feign/`验证通过FeignClient去调用服务提供者。


6. 配置应用名以及监听端口号。
















      ```ini
      spring.application.name=service-consumer
      server.port=18082
      ```
3. 本地开发调试。
1. 启动轻量级配置中心。
      本地开发调试时，需要使用轻量级配置中心，轻量级配置中心包含了SAE服务注册发现服务端的轻量版，详情请参见 [启动轻量级配置及注册中心](https://help.aliyun.com/zh/edas/developer-reference/start-the-lightweight-configuration-center-1#task-2310117 "开发者可以在本地使用轻量级配置及注册中心实现应用的注册、发现和配置管理，完成应用的开发和测试。在将应用部署到后，这些功能仍然可以正常使用。本文介绍如何下载、启动和验证轻量级配置及注册中心。")。


2. 启动应用。


      - IDE中启动

        在IDE中启动，通过VM options配置启动参数`-Dvipserver.server.port=8080`（注意：该参数仅在本地开发且使用轻量级配置中心时需要添加，当应用部署到SAE时，须移除此参数，否则会使应用无法正常发布或订阅），通过main方法直接启动。


        轻量级配置中心与应用部署在不同的机器上，需要绑定hosts，详情请参见 [启动轻量级配置及注册中心](https://help.aliyun.com/zh/edas/developer-reference/start-the-lightweight-configuration-center-1#task-2310117 "开发者可以在本地使用轻量级配置及注册中心实现应用的注册、发现和配置管理，完成应用的开发和测试。在将应用部署到后，这些功能仍然可以正常使用。本文介绍如何下载、启动和验证轻量级配置及注册中心。")。


      - FatJar启动

        1. 添加FatJar打包插件。

           使用Maven将pandora-boot工程打包成FatJar， 需要在pom.xml中添加如下插件。为避免与其他打包插件发生冲突，请勿在build的plugin中添加其他FatJar插件。















           ```xml
           <build>
               <plugin>
                   <groupId>com.taobao.pandora</groupId>
                       <artifactId>pandora-boot-maven-plugin</artifactId>
                       <version>2.1.9.1</version>
                       <executions>
                          <execution>
                             <phase>package</phase>
                             <goals>
                                 <goal>repackage</goal>
                             </goals>
                          </execution>
                        </executions>
               </plugin>
           </build>
           ```

        2. 添加完插件后，在工程的主目录下，使用Maven命令`mvn clean package`进行打包，即可在target目录下找到打包好的FatJar文件。

        3. 通过Java命令启动应用。















           ```awk
           java -Dvipserver.server.port=8080 -Dpandora.location=/Users/{$username}/.m2/repository/com/taobao/pandora/taobao-hsf.sar/dev-SNAPSHOT/taobao-hsf.sar-dev-SNAPSHOT.jar  -jar sc-vip-server-0.0.1-SNAPSHOT.jar
           ```





           **说明**



           `-Dpandora.location`指定的路径必须是全路径，且必须放在sc-vip-server-0.0.1-SNAPSHOT.jar之前。

启动服务，分别进行调用，可以看到调用都成功了。![EDAS应用开发HSF开发RESTful](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6345559951/p64676.png)
4. 常见问题处理。


   - AsyncRestTemplate无法接入服务发现。

     AsyncRestTemplate接入服务发现的时间比较晚，需要在Dalston之后的版本才能使用，相关内容，请参见 [pull request](https://github.com/spring-cloud/spring-cloud-commons/pull/149)。


   - FatJar打包插件冲突。

     为避免与其他打包插件发生冲突，请勿在build的plugin中添加其他FatJar插件。

   - 打包时可不可以不排除taobao-hsf.sar？

     可以，但是不建议这么做。

     通过修改pandora-boot-maven-plugin插件，把excludeSar设置为false，打包时就会自动包含taobao-hsf.sar。
















     ```xml
     <plugin>
         <groupId>com.taobao.pandora</groupId>
         <artifactId>pandora-boot-maven-plugin</artifactId>
         <version>2.1.9.1</version>
         <configuration>
         <excludeSar>false</excludeSar>
         </configuration>
            <executions>
                <execution>
                   <phase>package</phase>
                   <goals>
                       <goal>repackage</goal>
                   </goals>
                 </execution>
         </executions>
     </plugin>
     ```





     这样打包后可以在不配置Pandora地址的情况下启动。
















     ```apache
     java -jar  -Dvipserver.server.port=8080 sc-vip-server-0.0.1-SNAPSHOT.jar
     ```





     请在将应用部署到SAE前恢复到默认排除SAR包的配置。



### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 开发RESTful应用（不推荐）

# 开发RESTful应用（不推荐）

更新时间：2022-08-25 22:21:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

服务注册与发现