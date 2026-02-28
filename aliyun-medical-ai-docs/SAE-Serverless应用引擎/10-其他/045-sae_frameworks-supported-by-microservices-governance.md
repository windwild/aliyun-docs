### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用访问和流量管理](https://help.aliyun.com/zh/sae/sae-network-related-concepts-and-capabilities/)[微服务治理](https://help.aliyun.com/zh/sae/microservice-governance/)[微服务治理探针说明](https://help.aliyun.com/zh/sae/microservices-governance-agent/)微服务治理支持的框架

# 微服务治理支持的框架

更新时间：2025-03-31 23:19:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Golang探针版本](https://help.aliyun.com/zh/sae/release-notes-for-the-go-agent)[下一篇：基于MSE云原生网关实现全链路灰度](https://help.aliyun.com/zh/sae/full-link-gray-scale-based-on-mse-cloud-native-gateway)

该文章对您有帮助吗？

反馈

本文将介绍SAE微服务治理对Java和Golang应用的支持，包括可选择的JDK和框架版本，以及Golang应用所支持的操作系统、语言版本和第三方组件。

根据您的需要，您可以选择合适的技术栈进行微服务治理。

微服务治理支持的Java框架

微服务治理支持的Golang框架

## **支持的JDK版本**

- JDK 1.8




**说明**





对于Kubernetes集群应用部署，建议使用JDK 8u212及以上版本。

- JDK 11




**说明**





SAE微服务治理于2.9.x探针版本后支持，建议使用JDK 11.0.17及以上版本。

- JDK 17




**说明**





SAE微服务治理于2.9.x探针版本后支持，建议您使用JDK 17.0.9及以上版本。

- JDK 21




**说明**





SAE微服务治理于3.2.x探针版本后支持。


## **支持的JDK发行版**

- OpenJDK（推荐）

- Alibaba Dragonwell（推荐）

- Temurin

- AdoptOpenJDK

- Amazon Corretto

- Azul

- Java HotSpot VM


**说明**

Eclipse OpenJ9与SAE微服务治理存在一定的兼容性问题，不建议使用。

## **支持的框架**

### **流量防护和指标监控**

|     |     |     |
| --- | --- | --- |
| **分类** | **框架名称** | **框架版本** |
| Web | Spring MVC | 对应Spring Cloud关联版本 |
| Spring Boot | 2.x.x ~ 3.2.3 |
| Spring Cloud | E、F、G、H、2020.x、2021.x、2022.x、2023.x |
| Feign | 对应Spring Cloud关联版本 |
| Java网关 | Spring Cloud Zuul | 1.3.x ~ 2.1.3 |
| Spring Cloud Gateway | 2.0.2 ~ 4.1.0 |
| RPC | Dubbo | 2.7.x、3.0.x、3.1.x、3.2.x |

### **全链路灰度**

|     |     |     |
| --- | --- | --- |
| **分类** | **框架名称** | **框架版本** |
| Spring | Spring Boot | 2.x.x ~ 3.2.3 |
| Spring Cloud | E、F、G、H、2020.x、2021.x、2022.x、2023.x |
| Java网关 | Spring Cloud Zuul | 1.3.x ~ 2.1.3 |
| Spring Cloud Gateway | 2.1.x ~ 4.1.0 |
| 负载均衡 | Spring Cloud LoadBalancer | 对应Spring Cloud关联版本 |
| Ribbon | 对应Spring Cloud关联版本 |
| 注册中心 | Nacos | 对应Spring Cloud关联版本 |
| Eureka |
| ZooKeeper |
| RPC | Dubbo | 2.7.x、3.0.x、3.1.x、3.2.x |
| Web | Tomcat | 7.x ~ 10.x |
| Undertow | 1.4.x ~ 2.2.x |
| 消息 | RocketMQ | 4.x |
| RocketMQ ONS | 1.x及以上版本 |

### **无损上下线**

|     |     |     |
| --- | --- | --- |
| **分类** | **框架名称** | **框架版本** |
| Spring | Spring Boot | 2.x.x ~ 3.2.3 |
| Spring Cloud | E、F、G、H、2020.x、2021.x、2022.x、2023.x |
| Java 网关 | Spring Cloud Zuul | 1.3.x ~ 2.1.3 |
| Spring Cloud Gateway | 2.1.x ~ 4.1.0 |
| 注册中心 | Nacos | 对应Spring Cloud关联版本 |
| Eureka |
| ZooKeeper |
| RPC | Dubbo | 2.7.x、3.0.x、3.1.x、3.2.x |

## **支持的Golang版本**

Golang 1.18 及以上版本。

## **支持的操作系统**

|     |     |     |
| --- | --- | --- |
| **编译工具名** | **操作系统** | **架构** |
| instgo\_linux\_amd64 | Linux | amd64 |
| instgo\_linux\_arm64 | Linux | arm64 |
| instgo\_darwin\_amd64 | Darwin/macOS | amd64 |
| instgo\_darwin\_arm64 | Darwin/macOS | arm64 |
| instgo\_windows\_amd64.exe | Windows | amd64 |

## **支持的框架和组件**

### **流量防护和指标监控**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **框架/组件名称** | **仓库地址** | **最低版本** | **最高版本** | **备注** |
| Net/HTTP | [https://pkg.go.dev/net/http](https://pkg.go.dev/net/http) | v1.18 | v1.24 | 支持基于Net/Http自研和魔改框架。 |
| Gin | [https://github.com/gin-gonic/gin](https://github.com/gin-gonic/gin) | v1.7.0 | v1.10.0 |  |
| Grpc-go | [https://github.com/grpc/grpc-go](https://github.com/grpc/grpc-go) | v1.44.0 | v1.69.2 | 支持基于Grpc-go自研和魔改框架。 |
| Kratos | [https://github.com/go-kratos/kratos](https://github.com/go-kratos/kratos) | v2.5.2 | v2.8.3 |  |
| Go-Zero | [https://github.com/zeromicro/go-zero](https://github.com/zeromicro/go-zero) | v1.4.0 | v1.8.0 |  |
| Kitex | [https://github.com/cloudwego/kitex](https://github.com/cloudwego/kitex) | v0.5.1 | v0.12.1 |  |
| Sentinel-Golang | [https://github.com/alibaba/sentinel-golang](https://github.com/alibaba/sentinel-golang) | v1.0.0 | v1.4.0 | 支持业务代码中的自定义埋点。 |

### **全链路灰度**

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **框架/组件名称** | **仓库地址** | **最低版本** | **最高版本** | **支持的服务发现方式** | **备注** |
| Net/HTTP | [https://pkg.go.dev/net/http](https://pkg.go.dev/net/http) | v1.18 | v1.24 | K8s Svc、Nacos | 支持基于Net/Http自研和魔改框架。 |
| Gin | [https://github.com/gin-gonic/gin](https://github.com/gin-gonic/gin) | v1.7.0 | v1.10.0 | K8s Svc、Nacos |  |
| Grpc-go | [https://github.com/grpc/grpc-go](https://github.com/grpc/grpc-go) | v1.44.0 | v1.69.2 | K8s Svc、Nacos | 支持基于Grpc-go自研和魔改框架。 |
| Kratos | [https://github.com/go-kratos/kratos](https://github.com/go-kratos/kratos) | v2.5.2 | v2.8.3 | K8s Svc、Nacos |  |
| Go-Zero | [https://github.com/zeromicro/go-zero](https://github.com/zeromicro/go-zero) | v1.4.0 | v1.8.0 | K8s Svc、Nacos |  |