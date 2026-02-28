### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[实践教程](https://help.aliyun.com/zh/sae/use-cases/)[AI](https://help.aliyun.com/zh/sae/sae-ai-applications/)Dify性能优化

# Dify性能优化

更新时间：2025-12-24 21:53:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Dify版本升级](https://help.aliyun.com/zh/sae/upgrade-dify)[下一篇：使用SAE部署OpenClaw](https://help.aliyun.com/zh/sae/use-sae-to-deploy-openclaw)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作步骤

各性能档位所需最小资源集合

档位1：性能要求达到10QPS

档位2：性能要求达到100QPS

档位3：性能要求达到200QPS

档位4：性能要求达到500QPS（仅适用于Dify高性能版）

通过合理配置Dify组件及外部资源的规格、数量，能够在满足生产环境性能要求的同时提高资源利用率。

## **操作步骤**

1. [使用SAE部署Dify](https://help.aliyun.com/zh/sae/deploy-dify-on-sae "")，如果要求系统性能达到500QPS及以上，在部署时需要选择 **Dify高性能版**。

2. 参考 [各性能档位所需最小资源集合](https://help.aliyun.com/zh/sae/dify-performance-optimization#56400c745b4kr "") 调整Dify组件及外部资源的配置：

1. 调整各个Dify组件的 [实例规格](https://help.aliyun.com/zh/sae/change-the-instance-specifications-of-an-application-2-0 "") 和 [数量](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling "")。

2. 调整Redis实例规格：登录 [Redis控制台](https://kvstore.console.aliyun.com/)，在左侧点击 **实例列表**，在顶部选择部署地域，点击已创建的Redis实例 **操作** 列的 **变更配置**；或者点击已创建的Redis实例 **操作** 列的 **管理**，在左侧点击 **实例信息**，按要求调整配置。

3. 调整PostgreSQL实例规格：登录 [RDS控制台](https://rdsnext.console.aliyun.com/)，在左侧点击 **实例列表**，在顶部选择部署地域，点击已创建的PostgreSQL实例 **操作** 列的 **管理**。在左侧点击 **基本信息**，按要求调整配置。

4. 调整公网NAT网关实例规格：登录 [NAT网关控制台](https://vpc.console.aliyun.com/nat)，在顶部选择部署地域，点击已创建的公网NAT网关实例 **操作** 列的 **管理**。在 **绑定的弹性公网IP** 页签，点击 **实例ID** 跳转到弹性公网IP实例详情页，在右上角点击**更多操作** \> **变配**，按要求调整配置。

## **各性能档位所需最小资源集合**

### **档位1：性能要求达到10QPS**

|     |     |     |
| --- | --- | --- |
| **Dify组件** |
| **组件名称** | **实例规格** | **实例数量** |
| dify-nginx | CPU 1核 内存 2GB | 1 |
| dify-api | CPU 1核 内存 2GB | 1 |
| dify-plugin-daemon | CPU 1核 内存 2GB | 1 |
| dify-worker | CPU 1核 内存 2GB | 1 |
| dify-sandbox | CPU 1核 内存 2GB | 1 |
| dify-web | CPU 1核 内存 2GB | 1 |
| **外部资源** |
| **资源类型** | **实例规格** |
| Redis | - 架构类型：不启用集群<br>  <br>- 产品类型：开源版<br>  <br>- 版本：6.0<br>  <br>- 规格：2GB(redis.shard.mid.2.ce)<br>  <br>- 带宽：96MB/s<br>  <br>- 读写分离：未开启(1主，1备)<br>  <br>- 最大连接数：10,000<br>  <br>- 分片数：1 |
| PostgreSQL | - CPU：2核<br>  <br>- 数据库内存：8G<br>  <br>- 实例规格：pg.n4.2c.2m<br>  <br>- 规格默认连接数：800 |
| 公网NAT网关 | - 类型：增强型<br>  <br>- 公网IP带宽峰值：5 Mbps |

### **档位2：性能要求达到100QPS**

|     |     |     |
| --- | --- | --- |
| **Dify组件** |
| **组件名称** | **实例规格** | **实例数量** |
| dify-nginx | CPU 1核 内存 2GB | 1 |
| dify-api | CPU 8核 内存 8GB | 2 |
| dify-plugin-daemon | CPU 2核 内存 4GB | 4 |
| dify-worker | CPU 1核 内存 2GB | 1 |
| dify-sandbox | CPU 1核 内存 2GB | 1 |
| dify-web | CPU 1核 内存 2GB | 1 |
| **外部资源** |
| **资源类型** | **实例规格** |
| Redis | - 架构类型：不启用集群<br>  <br>- 产品类型：开源版<br>  <br>- 版本：6.0<br>  <br>- 规格：2GB(redis.shard.mid.2.ce)<br>  <br>- 带宽：96MB/s<br>  <br>- 读写分离：未开启(1主，1备)<br>  <br>- 最大连接数：10,000<br>  <br>- 分片数：1 |
| PostgreSQL | - CPU：2核<br>  <br>- 数据库内存：8G<br>  <br>- 实例规格：pg.n4.2c.2m / pg.n4.4c.2m<br>  <br>- 规格默认连接数：800 |
| 公网NAT网关 | - 类型：增强型<br>  <br>- 公网IP带宽峰值：100 Mbps |

### **档位3：性能要求达到200QPS**

|     |     |     |
| --- | --- | --- |
| **Dify组件** |
| **组件名称** | **实例规格** | **实例数量** |
| dify-nginx | CPU 1核 内存 2GB | 2 |
| dify-api | CPU 12核 内存 12GB | 5 |
| dify-plugin-daemon | CPU 2核 内存 4GB | 10 |
| dify-worker | CPU 1核 内存 2GB | 1 |
| dify-sandbox | CPU 1核 内存 2GB | 1 |
| dify-web | CPU 1核 内存 2GB | 1 |
| **外部资源** |
| **资源类型** | **实例规格** |
| Redis | - 可选配置1：非集群架构<br>  <br>  - 架构类型：不启用集群<br>    <br>  - 产品类型：开源版<br>    <br>  - 版本：6.0<br>    <br>  - 规格：16GB(redis.shard.2xlarge.ce)<br>    <br>  - 带宽：288MB/s <br>    <br>  - 读写分离：未开启(1主，1备)<br>    <br>  - 最大连接数：20,000<br>    <br>  - 分片数：1 |
| - 可选配置2：集群架构<br>  <br>  - 架构类型：启用集群<br>    <br>  - 产品类型：开源版<br>    <br>  - 版本：6.0<br>    <br>  - 规格：1GB(redis.shard.small.ce)<br>    <br>  - 带宽：288MB/s <br>    <br>  - 读写分离：未开启(1主，1备)<br>    <br>  - 最大连接数：30,000<br>    <br>  - 分片数：3 |
| PostgreSQL | - CPU：64核<br>  <br>- 数据库内存：256G<br>  <br>- 实例规格：pg.x4.8xlarge.2c<br>  <br>- 规格默认连接数：25,600 |
| 公网NAT网关 | - 类型：增强型<br>  <br>- 公网IP带宽峰值：100 Mbps |

### **档位4：性能要求达到500QPS（仅适用于** Dify高性能版 **）**

|     |     |     |
| --- | --- | --- |
| **Dify组件** |
| **组件名称** | **实例规格** | **实例数量** |
| dify-nginx | CPU 1核 内存 2GB | 2 |
| dify-api | CPU 12核 内存 12GB | 8 |
| dify-plugin-daemon | CPU 2核 内存 4GB | 16 |
| dify-worker | CPU 1核 内存 2GB | 1 |
| dify-sandbox | CPU 1核 内存 2GB | 1 |
| dify-web | CPU 1核 内存 2GB | 1 |
| **外部资源** |
| **资源类型** | **实例规格** |
| Redis | - 可选配置1：非集群架构<br>  <br>  - 架构类型：不启用集群<br>    <br>  - 产品类型：开源版<br>    <br>  - 版本：6.0<br>    <br>  - 规格：16GB(redis.shard.2xlarge.ce)<br>    <br>  - 带宽：288MB/s <br>    <br>  - 读写分离：未开启(1主，1备)<br>    <br>  - 最大连接数：20,000<br>    <br>  - 分片数：1 |
| - 可选配置2：集群架构<br>  <br>  - 架构类型：启用集群<br>    <br>  - 产品类型：开源版<br>    <br>  - 版本：6.0<br>    <br>  - 规格：1GB(redis.shard.small.ce)<br>    <br>  - 带宽：288MB/s <br>    <br>  - 读写分离：未开启(1主，1备)<br>    <br>  - 最大连接数：30,000<br>    <br>  - 分片数：3 |
| PostgreSQL | - CPU：16核<br>  <br>- 数据库内存：128G<br>  <br>- 实例规格：pg.x8.2xlarge.2c<br>  <br>- 规格默认连接数：12,800 |
| 公网NAT网关 | - 类型：增强型<br>  <br>- 公网IP带宽峰值：100 Mbps |