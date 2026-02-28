### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/)[使用代码包部署应用](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/)部署静态网站

# 部署静态网站

更新时间：2026-01-12 03:43:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：部署.NET Core应用](https://help.aliyun.com/zh/sae/deploy-net-core-applications-using-zip-packages)[下一篇：使用YAML部署应用](https://help.aliyun.com/zh/sae/use-yaml-to-deploy-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

步骤一：制作代码包

步骤二：创建应用

步骤三：访问应用

高级设置

运行环境和生命周期管理

应用访问和流量管理

数据持久化

日志与监控

微服务治理

其他功能

基于SAE提供的Nginx环境，仅需将静态网站资源（如HTML、CSS、JavaScript等）打包上传到SAE，即可实现静态网站的部署。

## **快速开始**

### **步骤一：制作代码包**

1. **调整目录结构：** 确保静态资源的目录结构如下。

















```plaintext
.
└── app
       └── index.html
       └── 其他静态资源文件/文件夹
```

2. **打包项目**：在`app`所在路径，执行以下命令，将所有静态资源文件打包成ZIP包。

















```shell
zip -r demo.zip app
```







**重要**





为确保上传到SAE的代码包能够运行，需遵循以下规范：



   - 静态资源文件所在目录名称应为`app`。如果原目录名称为`dist`，需要重命名为`app`。

   - 必须打包`app`文件夹，切勿打包外层目录。


### **步骤二：创建应用**

1. 在 [SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro) 中，在顶部选择目标地域和命名空间，点击 **创建应用**。

2. **选择应用版本**：不同版本的差异，请参见 [应用版本](https://help.aliyun.com/zh/sae/product-overview/application-version "")。





**说明**





**轻量版** 和 **专业版** 目前处于邀约测试阶段。未参与邀约测试的用户，创建的应用为 **标准版**，无需选择应用版本。

3. **基础信息设置**：



   - **应用名称**：可自定义。

   - **命名空间类型**：命名空间相当于K8s的Namespace，可用于不同环境的资源隔离。创建应用后不支持更改其所属的命名空间，请提前做好规划。

     - **系统创建** **：** 使用当前地域下系统创建的默认命名空间、交换机和安全组。

     - **选择已有命名空间** **：** 选择您提前创建的 [命名空间](https://help.aliyun.com/zh/sae/manage-namespaces-2-0#7a8122b058hro "")、 [交换机](https://help.aliyun.com/zh/vpc/user-guide/create-and-manage-vswitch "") 和 [安全组](https://help.aliyun.com/zh/ecs/user-guide/create-a-security-group-1 "")。
   - **应用部署方式**：选择 **代码包部署**，点击 **设置代码包部署**。

     - **技术栈语言**：选择 **HTML**。

     - **代码包类型**：选择 **ZIP 包部署**。

     - **Nginx 环境**：选择与您的代码兼容的环境，详见 [HTML - Nginx环境介绍](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/#d0f9aa0fbasr9 "")。

     - **文件上传方式**：可以上传本地代码包，或者输入代码包的地址。

     - **版本**：输入应用版本号或者 **使用时间戳为版本号**。

     - **时区设置**：选择当前应用所在时区。

4. **容量设置** **：**



   - **资源类型**：选择 **默认**。





     **说明**





     **资源类型** 分为 **默认** 和 **海光（Hygon）**， **海光（Hygon）** 目前处于邀约测试阶段。未参与邀约测试的用户， **资源类型** 自动设置为 **默认**，无需手动选择。

   - **单实例规格**：选择每个实例所需的CPU和内存。

   - **实例数**：设置初始实例数。


5. 单击 **一键创建应用**，等待应用创建完成。


### **步骤三：访问应用**

接下来，通过为应用 [绑定NLB](https://help.aliyun.com/zh/sae/bind-an-nlb-instance-to-an-application-for-application-service-access-test-invitation "")、 [绑定CLB](https://help.aliyun.com/zh/sae/sae-2-bind-clb-for-application "") 或 [配置网关路由](https://help.aliyun.com/zh/sae/configuring-gateway-routing-ingress-access/ "") 实现从外部访问应用。以NLB为例，配置步骤如下。

1. 在 [SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro) 中，在顶部选择目标地域和命名空间，点击目标 **应用 ID** 跳转到应用详情页。

2. 在 **应用访问设置** 区域，选择 **基于 NLB 访问** 页签，点击 **添加 NLB 访问**。



   - **实例来源**：选择 **新建实例**。

   - **网络类型**：选择 **公网**。

   - **虚拟交换机**：指定NLB实例所在的可用区和虚拟交换机。





     **说明**





     - 为保障业务高可用，请至少选择2个或以上可用区和虚拟交换机。

     - 如果没有虚拟交换机，则点击 **去创建**，新建一台虚拟交换机。创建完成后，点击旁边的刷新按钮，选取已创建的虚拟交换机。


   - **协议类型**：选择 **TCP**。

   - **监听端口**：用来接收请求并向后端服务器进行请求转发的监听端口。可自定义，本例填写`80`。

   - **容器端口**：进程监听端口，由程序定义。对于SAE的Nginx环境，默认配置为`80`。


3. 点击 **确定**，等待创建完成。

4. **验证效果**：



1. 点击已创建的NLB实例ID，跳转到实例详情页。在 **可用区** 区域，获取NLB实例的任意 **弹性公网IP**。

2. 通过浏览器访问应用，URL格式为`http://<弹性公网IP>:<监听端口>`。


## **高级设置**

在创建应用和部署应用时，可以根据需求配置如下高级功能。

### 运行环境和生命周期管理

- 通过 [设置环境变量](https://help.aliyun.com/zh/sae/configure-environment-variables-2-0 "")、 [设置Hosts绑定](https://help.aliyun.com/zh/sae/configure-host-bindings-1 "")、 [注入配置信息](https://help.aliyun.com/zh/sae/injection-configuration-information-new "") 和 [注入保密信息](https://help.aliyun.com/zh/sae/inject-secret "")，可以在应用部署后灵活变更运行环境中的变量或配置文件，而无需重新构建镜像。

- 通过 [设置健康检查](https://help.aliyun.com/zh/sae/set-health-check-2-0 "") 来监测应用实例是否正常运行并准备好处理业务请求，未正常运行的实例会被自动重启，并且直到实例准备就绪后才会分配业务请求。

- 通过 [应用生命周期管理](https://help.aliyun.com/zh/sae/configure-application-lifecycle-management-new "") 来自定义应用启动后和停止前执行的命令，并实现优雅下线。


### **应用访问和流量管理**

- 通过 [服务注册与发现](https://help.aliyun.com/zh/sae/service-registration-and-discovery/ "") 实现应用之间的服务调用。

- 通过为应用 [绑定NLB](https://help.aliyun.com/zh/sae/bind-an-nlb-instance-to-an-application-for-application-service-access-test-invitation "")、 [绑定CLB](https://help.aliyun.com/zh/sae/sae-2-bind-clb-for-application "") 或 [配置网关路由](https://help.aliyun.com/zh/sae/configuring-gateway-routing-ingress-access/ "") 实现从外部访问应用。

- 通过 [配置NAT网关](https://help.aliyun.com/zh/sae/configure-a-nat-gateway-for-an-sae-application-to-access-internet "") 或 [为应用实例绑定EIP](https://help.aliyun.com/zh/sae/configure-public-network-access-and-public-network-access-capabilities-of-sae-instances-based-on-eip "") 实现应用主动访问外部资源或服务。


### **数据持久化**

将应用数据存储到 [NAS](https://help.aliyun.com/zh/sae/configure-nas-storage-2-0 "")、 [OSS](https://help.aliyun.com/zh/sae/copnfigure-oss-storage-2-0 "") 或 [数据库](https://help.aliyun.com/zh/sae/application-access-to-alibaba-cloud-database/ "")，避免应用变更或停止导致数据丢失。

### **日志与监控**

- 部署应用后即可 [查看实时日志](https://help.aliyun.com/zh/sae/view-real-time-logs-new "")、 [查看资源使用情况和负载](https://help.aliyun.com/zh/sae/view-basic-monitoring-data "")，无需额外配置。此外，还可以将日志输出到 [SLS](https://help.aliyun.com/zh/sae/set-log-collection-to-sls-2-0 "") 或 [Kafka](https://help.aliyun.com/zh/sae/collect-logs-to-apsaramq-for-kafka-new "")，便于统一管理和分析。

- ARMS监控能够帮助您全面掌控应用运行状态，快速定位出错接口和慢接口，洞察性能瓶颈，重现调用参数，从而大幅提升线上问题诊断的效率。

  - 对于 **标准版** 应用，部署后即可 [查看ARMS基础版监控数据](https://help.aliyun.com/zh/sae/application-overview-new "")，无需额外配置。此外，还可以开通购买 [ARMS高级版监控](https://help.aliyun.com/zh/sae/advanced-monitoring-new "")。

  - 对于 **专业版** 应用，在 **高级设置** 中启用 **应用监控** 并完成应用部署后，即可查看ARMS高级版监控数据。无需额外付费。

### **微服务治理**

**微服务治理** 能够实现Java应用的无损上下线、流量防护、全链路灰度、同可用区路由优先。

- 对于 **标准版** 应用，需要在完成应用部署后，前往应用详情页开通购买MSE微服务治理功能。

- 对于 **专业版** 应用，在 **高级设置** 中启用 **微服务治理** 后，即可配置无损上下线。更多功能，可以在完成应用部署后，前往应用详情页配置。无需额外付费。


### **其他功能**

- 通过 [开启CPU Burst功能（仅适用于标准版、专业版）](https://help.aliyun.com/zh/sae/enable-cpu-burst-function-only-applicable-to-standard-edition-and-professional-edition "") 解决启动加载阶段所需的CPU规格高于平时导致的资源浪费问题。

- 通过 [添加Sidecar容器](https://help.aliyun.com/zh/sae/add-a-sidecar-container "") 实现非业务功能从主容器中解耦与标准化。

- 通过 [启用RRSA身份认证](https://help.aliyun.com/zh/sae/configure-authentication-service "") 实现应用实例级API权限管控，避免传统密钥认证方式存在的密钥泄露风险。