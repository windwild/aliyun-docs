### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [快速入门](https://help.aliyun.com/zh/sae/getting-started/) 部署第一个Serverless应用

# 部署第一个Serverless应用

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：准备工作](https://help.aliyun.com/zh/sae/sae-2-preparations)[下一篇：周期性执行或手动触发执行Job 任务](https://help.aliyun.com/zh/sae/quick-start-with-job-tasks)

该文章对您有帮助吗？

反馈

您仅需将代码或镜像上传到SAE，即可部署应用服务。SAE会代您管理底层的计算资源，通过简单配置即可实现根据访问量自动扩缩容、跨可用区部署。

## **方案概览**

您将部署一组微服务应用，实现服务的注册与发现、服务之间的方法调用，并且通过公网来访问应用。示例应用的架构如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6518927471/CAEQVRiBgIC2k8y1rRkiIDkyZTNhODQ0MDhkZjRmYjBiMjI1NWIzOGM4MjliODJh4982129_20250318094750.578.svg)

> 尽管本文以Java微服务应用为例， **但SAE对应用的技术栈语言和架构没有限制**，能够适配多种业务场景，例如 **静态网站**、 **前后端分离的网站**、 **单体应用**、 **微服务应用**。

为实现本方案，您将：

1. **部署应用：** 使用示例镜像部署provider应用与consumer应用。通过SAE内置的Nacos实现服务注册与发现，使得consumer应用可以调用provider应用提供的服务。

2. **通过公网访问应用**： 为consumer应用配置公网访问地址并访问应用。


## **准备工作**

领取免费试用额度

首次使用SAE，您可以领取 [免费试用额度](https://help.aliyun.com/zh/sae/trial-quota "")。

开通SAE服务并授权

建议您使用阿里云账号开通SAE服务，并通过RAM用户来管理SAE相关的资源。

### **为阿里云账号开通服务**

进入[SAE产品主页](https://www.aliyun.com/product/sae)，点击免费开通。登录阿里云账号，根据页面提示开通SAE服务并创建服务关联角色。

**重要**

SAE服务开通后，超出 [免费试用](https://help.aliyun.com/zh/sae/trial-quota "") **额度** 和 **期限** 的部分将 [按量计费](https://help.aliyun.com/zh/sae/charge-by-volume-2-0 "")。为节省费用，您可以购买 [资源包（预付费）](https://help.aliyun.com/zh/sae/resource-plans-1/ "")。

### 为RAM用户授权

您需要通过阿里云账号 [为RAM用户授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-user-2-0 "")，授予 [SAE所需权限策略](https://help.aliyun.com/zh/sae/policies-and-examples-2-0 "")，RAM用户才能管理SAE服务相关的资源。

## **操作指引**

SAE支持 **控制台**、 **saectl工具**（兼容kubectl）等多种操作方式，从中选择您熟悉的方式来完成本教程。

### **控制台**

#### **1\. 部署应用**

1. **部署provider应用**：登录 [SAE控制台](https://saenext.console.aliyun.com/)，在左侧选择**应用管理** \> **应用列表**，在顶部选择应用部署的地域（本文以 **杭州** 为例），点击 **创建应用**。配置以下参数，其余保持默认。点击 **一键创建应用**（跳过 **高级设置**）。


> 如果导航栏中没有**应用管理** \> **应用列表**，请选择**应用管理** \> **微服务应用**。



> 如果提示选择应用版本，请选择 **标准版**。**轻量版** 和 **专业版** 目前处于邀约测试阶段。完成本教程无需考虑应用版本间的差异。


1. 自定义 **应用名称**，例如`provider`。

2. 设置 **命名空间类型** 为`系统创建`，表示应用将会创建于当前地域的默认命名空间，且自动创建并关联VPC、交换机、安全组等网络资源，无需用户关注。

3. 设置 **应用部署方式** 为`选择镜像部署`。点击 **设置镜像**，在 **Demo镜像** 标签页，找到 **微服务应用-提供者**， **选择镜像版本** 为`microservice-java-provider-v1.0`，点击 **确定**。

4. 在 **容量设置** 区域，自定义 **单实例规格** 和 **实例数**，这决定了应用初始运行的实例数量、系统为每个实例分配多少计算资源。
2. **部署consumer应用**：重复上述步骤并调整以下参数来部署Consumer应用。

1. 自定义 **应用名称**，例如`consumer`。

2. **设置镜像** 时，找到 **微服务应用-消费者**， **选择镜像版本** 为`microservice-java-consumer-v1.0`。
3. **查看应用部署结果**：请耐心等待应用创建完成，大约需要1分钟。

1. 您可以在 **应用列表** 中查看已创建的应用，点击其中某个应用可以进入其详情页面。

2. 在左侧导航栏选择 **基础信息**，在 **实例列表** 页签中，可以查看已创建的应用实例。

#### **2\. 通过公网访问应用**

为了实现从公网访问consumer应用，一种简便的方式是为该应用绑定公网CLB实例。

1. **为consumer应用绑定公网CLB实例**：进入consumer应用的详情页面。在 **应用信息** 页签中，在 **应用访问设置** 区域选择 **基于CLB访问**。点击 **添加公网CLB访问**，配置如下参数，然后点击 **确定**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6518927471/p931638.png)

1. 在 **CLB实例** 中，选择 **新建CLB实例**。

2. 在 **HTTP协议** 页签中，设置 **HTTP端口** 为`80`， **容器端口** 为`18082`。
2. **验证结果**：SAE将为您代购一个CLB实例并绑定到当前应用。等待创建完成，控制台将显示应用的 **公网访问地址**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6518927471/p930955.png)

1. 通过浏览器访问`http://<公网访问地址>/consumer-echo/hello`（其中`<公网访问地址>`需要替换为实际值），验证能够通过公网来访问应用。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6518927471/p931041.png)

2. 在**应用监控** \> **应用详情** \> **拓扑视图**中，您可以查看consumer应用调用provider应用的拓扑视图。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6518927471/p931031.png)

#### **3\. 清理资源**

在完成本教程后，建议清理相关资源，避免持续产生费用。

1. **删除应用**：进入provider应用和consumer应用的详情页面，点击**更多** \> **删除应用**，并按照指引操作来删除上述应用。


> SAE代购的CLB实例将随应用删除而自动释放。

2. **（可选）删除网络资源**：在部署应用的过程中，系统自动创建了VPC、交换机、安全组。

1. 查看VPC：在左侧导航栏选择**命名空间**，点击 **默认**，在 **基础信息** 页面查看VPC，点击链接跳转到VPC详情页。

2. 查看交换机、安全组：在VPC的 **资源管理** 标签页点击链接跳转到相应资源的详情页。

3. 在各资源的详情页执行删除操作。

### **saectl工具**

#### **1\.** [安装与配置saectl工具](https://help.aliyun.com/zh/sae/install-and-configure-saectl-tool "")

#### **2\. 部署应用**

1. **创建资源配置文件**：在同一路径中创建以下文件。 **注意**：将配置文件中的`image: ...cn-hangzhou...`替换为您的应用部署地域。

1. `deployment-provider.yaml`用于配置provider应用：


      ```yaml
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        annotations:
          sae.aliyun.com/new-sae-version: std # 选择应用版本，std表示标准版。轻量版和专业版目前处于邀约测试阶段。完成本教程无需考虑应用版本间的差异。
        name: provider # 应用名称可自定义
        namespace: default # 选择系统创建的默认命名空间，自动创建并关联VPC、交换机、安全组等网络资源，无需用户关注。
      spec:
        replicas: 2 # 应用实例的数量
        selector:
          matchLabels:
            sae.aliyun.com/app-name: provider # 必须与metadata中定义的应用名称保持一致
        template:
          metadata:
            labels:
              sae.aliyun.com/app-name: provider # 必须与metadata中定义的应用名称保持一致
          spec:
            containers:
      - name: main # 建议将containers的名称固定设置为main，避免冲突。
        image: registry.cn-hangzhou.aliyuncs.com/sae-serverless-demo/sae-demo:microservice-java-provider-v1.0 # 使用provider应用的示例镜像，其中，cn-hangzhou需要替换为您部署应用的地域。
        resources: # 单个应用实例的规格。limits和requests需要保持相同的配置。
          limits:
            cpu: "2"
            memory: 4Gi
          requests:
            cpu: "2"
            memory: 4Gi
```

   2. `deployment-consumer.yaml`用于配置consumer应用：


      ```yaml
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        annotations:
          sae.aliyun.com/new-sae-version: std # 选择应用版本，std表示标准版。轻量版和专业版目前处于邀约测试阶段。完成本教程无需考虑应用版本间的差异。
        name: consumer # 应用名称可自定义
        namespace: default # 选择系统创建的默认命名空间，自动创建并关联VPC、交换机、安全组等网络资源，无需用户关注。
      spec:
        replicas: 2 # 应用实例的数量
        selector:
          matchLabels:
            sae.aliyun.com/app-name: consumer # 必须与metadata中定义的应用名称保持一致
        template:
          metadata:
            labels:
              sae.aliyun.com/app-name: consumer # 必须与metadata中定义的应用名称保持一致
          spec:
            containers:
      - name: main # 建议将containers的名称固定设置为main，避免冲突。
        image: registry.cn-hangzhou.aliyuncs.com/sae-serverless-demo/sae-demo:microservice-java-consumer-v1.0 # 使用consumer应用的示例镜像，其中，cn-hangzhou需要替换为您部署应用的地域。
        resources: # 单个应用实例的规格。limits和requests需要保持相同的配置。
          limits:
            cpu: "2"
            memory: 4Gi
          requests:
            cpu: "2"
            memory: 4Gi
```
2. **执行部署**：在上述配置文件所在路径执行`saectl apply -f deployment-provider.yaml -f deployment-consumer.yaml`。

3. **验证结果**：

1. **查看应用**：执行`saectl get deployments -n default`。其中，`-n default`表示查询默认命名空间。返回结果中：

      1. `STATE`字段显示`RUNNING`表示应用正常运行；如果显示`PUBLISHING`表示应用正在部署，请等待部署完成后再查看。

      2. `READY`字段显示`n/m`代表`已就绪的实例数/期望部署的实例数`。
2. **查看应用实例**：执行`saectl get pods -n default`。返回结果中：

      1. `STATUS`字段显示`RUNNING`表示实例中的容器正常运行；如果显示`ContainerCreating`表示容器正在创建，请等待创建完成后再查看。

      2. `READY`字段显示`n/m`代表`已就绪的容器数/总容器数`。

#### **3\. 通过公网访问应用**

为了实现从公网访问consumer应用，一种简便的方式是为该应用绑定公网CLB实例。

1. **创建资源配置文件**：创建`svc.yaml`用于配置 **Service**，即通过为consumer应用绑定公网CLB对外提供服务：


```yaml
apiVersion: v1
kind: Service
metadata:
     annotations:
       sae.aliyun.com/loadbalancer-address-type: internet # 公网或私网类型, internet表示公网类型，intranet表示私网类型。
     name: internet-consumer # 固定格式 ${公网或私网类型}-${应用名}
spec:
     ports:
  - name: port-80 # 固定格式 port-${对外端口}
    port: 80
    protocol: HTTP
    targetPort: 18082 # consumer应用的容器端口
selector:
    sae.aliyun.com/app-name: consumer # 应用名称
type: LoadBalancer
```

2. **执行部署**：在上述配置文件所在路径执行`saectl apply -f svc.yaml`。

3. **验证结果**：

1. **查看服务**：执行`saectl get services -n default`。返回结果中：

      1. `EXTERNAL-IP`字段显示访问应用的公网IP；如果显示`<pending>`表示服务正在创建，请等待创建完成后再查看。

      2. `PORT(S)`字段显示您配置的应用访问端口。
2. **从公网访问应用**：执行`curl http://<公网访问地址>:<访问端口>/consumer-echo/hello`（其中`<公网访问地址>`、`<访问端口>`需要替换为实际值）。从返回结果中，能够看到consumer应用通过调用provider应用来处理请求的过程。

#### **4\. 清理资源**

在完成本教程后，建议清理相关资源，避免持续产生费用。

**删除应用**：执行`saectl delete -f deployment-provider.yaml -f deployment-consumer.yaml`。

> SAE代购的CLB实例将随应用删除而自动释放。

## **后续步骤**

- 您已通过Demo镜像体验了部署应用的流程。SAE为您提供以下方式来 **部署实际的应用**：

  - [使用镜像部署应用（推荐）](https://help.aliyun.com/zh/sae/use-an-image-to-deploy-an-application/ "")：您可以将任何应用制作成镜像，然后将其推送到镜像仓库，最后将其部署到SAE。

  - [使用代码包部署应用](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/ "")：SAE提供Java、PHP、Python、.NET Core特定版本的 [运行环境](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/ "")，如果与您的代码兼容，则可以使用代码包部署应用。您需要先 [制作符合SAE要求的代码包](https://help.aliyun.com/zh/sae/create-sae-compatible-packages "")，然后将其部署到SAE。
- 本示例通过 [SAE内置Nacos](https://help.aliyun.com/zh/sae/sae-2-microservices-use-the-sae-built-in-nacos-registry "") 实现了服务注册与发现，使得consumer应用能够访问provider应用并调用其方法。SAE还提供以下方式来 **实现应用间的互访**，您可以根据实际情况灵活选取：

  - [使用MSE的Nacos注册中心（推荐）](https://help.aliyun.com/zh/sae/sae-2-microservices-use-an-mse-nacos-registry "")：如果您不希望自建服务注册中心，且追求注册中心的性能、扩展性、高可用性等方面，建议使用MSE的Nacos注册中心。

  - [使用自建服务注册中心](https://help.aliyun.com/zh/sae/sae-2-microservices-use-a-self-managed-nacos-service-registry "")：如果您当前已部署了自建的服务注册中心（例如Nacos、Zookeeper等），且已能够满足使用需求，在您部署应用到SAE后，可以继续使用自建的服务注册中心。前提是确保应用和注册中心之间的网络联通性，并且需要手动在程序中配置注册中心的地址。

  - [基于K8s ServiceName配置应用服务访问](https://help.aliyun.com/zh/sae/sae-2-microservices-configure-application-access-based-on-kubernetes-services "")：在SAE集群内，为应用配置一个可以供其他应用访问的固定域名。
- 本示例通过 [为应用绑定CLB实例](https://help.aliyun.com/zh/sae/sae-2-bind-clb-for-application "") 实现了从外部访问应用。您也可以通过 [为应用绑定NLB实例](https://help.aliyun.com/zh/sae/bind-an-nlb-instance-to-an-application-for-application-service-access-test-invitation "") 或 [配置网关路由](https://help.aliyun.com/zh/sae/configuring-gateway-routing-ingress-access/ "") 来 **实现从外部访问应用**。如果需要 **应用主动访问外部的资源和服务**，则需要 [配置NAT网关](https://help.aliyun.com/zh/sae/configure-a-nat-gateway-for-an-sae-application-to-access-internet "") 或者 [为应用实例绑定EIP](https://help.aliyun.com/zh/sae/configure-public-network-access-and-public-network-access-capabilities-of-sae-instances-based-on-eip "")。

- 本示例使用系统创建的默认命名空间来部署应用。您也可以通过 [自定义命名空间](https://help.aliyun.com/zh/sae/manage-namespaces-2-0 "") 来 **实现不同应用之间、开发/测试/生产环境之间的隔离**。每个命名空间需要绑定一个VPC。部署应用时，需要为应用实例绑定该VPC中的交换机，选择不同可用区的交换机即可 **实现应用的跨可用区部署**。

- 创建应用后，可以 [手动调整实例数量](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling "") 与 [实例规格](https://help.aliyun.com/zh/sae/change-the-instance-specifications-of-an-application-2-0 "")，或通过 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "") **实现根据访问量、资源使用情况自动调整实例数量**。还可以通过 [开启闲置模式](https://help.aliyun.com/zh/sae/idle-mode-new "") 来降低成本。