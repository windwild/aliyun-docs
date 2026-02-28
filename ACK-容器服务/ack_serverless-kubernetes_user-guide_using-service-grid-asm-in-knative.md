### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/)[Knative](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/knative/)[Knative服务管理](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/service-management-3/)使用ASM网关

# 在Knative中使用ASM网关

更新时间：2025-08-14 07:31:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用ALB网关](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/use-alb-ingresses-in-knative)[下一篇：添加自定义路由](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/add-a-custom-route)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

步骤一：部署ASM网关

步骤二：通过ASM入口网关访问部署的服务

（可选）步骤三：查看服务监控数据

相关文档

在大规模分布式系统、微服务应用流量管理等场景下，特别是已采用或计划采用Istio作为服务网格框架的业务场景中，推荐使用ASM网关实现Knative服务的流量分发和路由。ASM网关兼容社区Istio规范，控制面组件由ACK托管，简化了服务治理，包括服务调用之间的流量路由与拆分管理、服务间通信的认证安全以及网格的可观测性能力。

## **前提条件**

已创建ASM实例，且ASM实例版本为1.21.6.84及以上，请参见 [创建ASM实例](https://help.aliyun.com/zh/asm/sidecar/create-an-asm-instance "")。

创建ASM实例时，在 **Kubernetes集群** 区域，将已创建的ACK托管集群或ACK Serverless集群添加到ASM实例中，并选中 **启用数据面集群KubeAPI访问Istio资源**。

## 步骤一：部署ASM网关

您可以在首次部署Knative时直接选择使用ASM（Istio）服务网关，也可以在Knative部署完成后修改配置文件，实现ASM网关配置。

新安装Knative

已安装Knative

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**应用** \> **Knative**。

3. 在 **Knative** 页面的 **组件管理** 页签下，单击 **一键部署Knative**，然后在 **服务网关** 处选择 **ASM**，然后单击 **一键部署** **。**

部署成功后，可在Knative中使用服务网格ASM。


1. 编辑config-network文件。















```bash
kubectl -n knative-serving edit configmap config-network
```

2. 修改`ingress.class`为`istio.ingress.networking.knative.dev`，然后保存config-network文件。















```yaml
apiVersion: v1
data:
     ...
     ingress.class: istio.ingress.networking.knative.dev # 使用ASM服务网关
     ...
kind: ConfigMap
metadata:
     name: config-network
     namespace: knative-serving
```


## 步骤二：通过ASM入口网关访问部署的服务

本小节结合一个Knative Service示例演示如何通过ASM完成服务部署。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**应用** \> **Knative**。

3. 在 **Knative** 页面的 **服务管理** 页签，选择 **命名空间** 为 **default**，单击 **使用模板创建**，将以下YAML示例粘贴至模板，然后单击 **创建**，创建一个名为helloworld-go的服务。



**重要**





请将下方代码中的`{REGION-ID}`替换为您集群的所在地域（例如`cn-beijing`），以确保可以正确访问和使用镜像。



















```yaml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
     name: helloworld-go
spec:
     template:
       spec:
         containers:
      - image: registry.{REGION-ID}.aliyuncs.com/knative-sample/helloworld-go:73fbdd56 # 请将{REGION-ID}替换为您集群所在地域。
        env:
        - name: TARGET
          value: "Knative"
```

4. 在 **服务管理** 页面的 **访问网关** 列，获取helloworld-go服务的网关地址。

5. 执行以下命令，访问helloworld-go服务。















```bash
curl -H "Host: helloworld-go.default.example.com" http://39.XX.XX.XX # 网关的IP和域名请以您的实际数据为准。
```



预期输出：















```bash
Hello Knative!
```



预期输出表明，服务访问成功。


## （可选）步骤三：查看服务监控数据

Knative提供开箱即用的可观测能力，在 **Knative** 页面，单击 **监控大盘** 页签，即可查看目标Knative服务的监控数据情况。如何开启Knative监控大盘，请参见[查看Knative服务监控大盘](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/view-the-knative-dashboard-in-prometheus-service-1 "")。

## **相关文档**

- 您可以为Knative服务启用自定义域名，请参见 [使用自定义域名](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/set-a-custom-domain-name-for-knative-serving "")。

- 您可以为Knative服务配置HTTPS证书访问，请参见 [配置HTTPS证书访问](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-access-over-https "")。

- 您可以在Knative中部署gRPC服务，提升网络效率，请参见 [在Knative中部署gRPC服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-grpc-service-in-knative "")。

- 您可以配置探针（Probe），监测Knative服务的健康状态和可用性，请参见 [在Knative中配置端口探测](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-port-probing-in-knative "")。

- 如果您的ECI实例有连接公网的需求，您需要绑定EIP，请参见 [为ECI绑定EIP实现公网访问](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/associate-an-eip-with-the-elastic-container-instance-on-which-a-knative-service-runs "")。