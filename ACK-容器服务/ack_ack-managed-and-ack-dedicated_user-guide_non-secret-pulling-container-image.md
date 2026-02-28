### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[工作负载](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/workloads/)[管理镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-images/)同账号拉取镜像

# 使用免密组件同账号拉取ACR企业版实例镜像

更新时间：2026-02-23 22:57:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

免密组件对比

前提条件

使用托管免密组件

步骤一：安装组件

步骤二：拉取镜像

使用自行运维免密组件

步骤一：安装组件

步骤二：变更组件配置（添加ACR实例）

步骤三：拉取镜像

常见问题

如何开启ServiceAccount创建即时使用功能？

配置免密组件后为什么仍然拉取失败？

如何使用imagePullSecrets？

相关文档

免密组件可自动化完成拉取镜像时的认证流程，跳过配置imagePullSecrets的重复操作。本文介绍免密组件安装、配置、使用的流程及注意事项。

## **工作原理**

使用ACR作为镜像来源时，若未配置公开匿名拉取功能，ACK集群在每次拉取镜像时需提供用户名和密码以完成认证。常用的解决方案是将用户名和密码存储在 Secret 中，但这会带来以下问题：

- Secret是经过Base64编码的明文，存在泄露风险。

- 需要为每个工作负载手动填入`imagePullSecrets`。

- Secret不支持跨命名空间（Namespace）使用。


免密组件的工作流程如下：

1. 免密组件从ACR实例获取临时账号和临时密码。

2. 组件将临时账号和密码保存到Secret中。

3. 组件将Secret关联到组件配置中指定的ServiceAccount。

4. 使用这些ServiceAccount的工作负载，默认会使用Secret中保存的临时账号和密码拉取镜像。


免密组件支持同时管理多个命名空间的ServiceAccount，并根据配置定时更新临时账号和密码，以降低泄露风险，且无需手动在工作负载中填入`imagePullSecrets`，免密组件不收取费用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1245091771/CAEQYRiBgICwr9GDxxkiIDNmNmRiN2ZkZjJlNjQ1ZDM5ZGM4ZDdhNTVmNWM1Y2Uz4831013_20250205151328.320.svg)

## **免密组件对比**

目前ACK提供了 aliyun-acr-credential-helper 组件，该组件有托管与自行运维两种形态，同时只能安装其中一种。两种版本的详细对比，请参见下表。

| **差异项** | **aliyun-acr-credential-helper（托管）** | **aliyun-acr-credential-helper（自行运维）** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **差异项** | **aliyun-acr-credential-helper（托管）** | **aliyun-acr-credential-helper（自行运维）** |
| 支持集群版本 | 1.22及以上版本的ACK托管集群、ACK Serverless集群、ACK Edge集群 | 1.20及以上版本的ACK托管集群、ACK专有集群 |
| 功能特性 | - 无需自行运维<br>  <br>- 支持通过RRSA跨账号拉取镜像 | - 支持查询组件日志<br>  <br>- 支持通过Worker Role、RRSA、AK/SK跨账号拉取镜像 |

> 如需升级集群，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

## **前提条件**

- 集群版本受到免密组件的支持，请参见上方的表格。

- 容器镜像服务ACR实例为企业版。



**重要**





  - 免密组件目前仅支持与ACR企业版及2024年09月08日及更早创建的ACR个人版配合使用。如无法使用免密组件，请参见 [如何使用imagePullSecrets？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/non-secret-pulling-container-image#1dcf6f7876w83 "")。


- 已为免密组件使用的RAM角色 [授权](https://ram.console.aliyun.com/role/authorization?request=%7B%22Services%22%3A%5B%7B%22Service%22%3A%22CS%22%2C%22Roles%22%3A%5B%7B%22RoleName%22%3A%22AliyunCSManagedAcrRole%22%2C%22TemplateId%22%3A%22AliyunCSManagedAcrRole%22%7D%5D%7D%5D%2C%22ReturnUrl%22%3A%22https%3A%2F%2Fcs.console.aliyun.com%2F%22%7D)。

- 打通ACR企业版实例与ACK集群的网络连接。



**配置网络连接**






在拉取镜像前，需要确保ACR企业版实例与ACK集群双方的网络连通和相关域名可解析。在同账号拉取镜像时，有下列实现方式：



  - **ACR VPC访问控制**：当ACR企业版实例与ACK集群处于同一地域时，ACK集群可通过VPC访问ACR实例。具体操作，请参见 [网络访问控制](https://help.aliyun.com/zh/acr/user-guide/configure-network-access-control/ "")。

  - **VPC对等连接**：如果ACR实例与ACK集群不处于同一VPC，可使用VPC对等连接打通两个VPC，使ACK集群可以访问ACR企业版实例。VPC处于同一地域时，对等连接功能不收取费用，处于不同地域时收费，请参见 [计费说明](https://help.aliyun.com/zh/vpc/vpc-peer-to-peer-connection#e693e3fc303wy "")。但使用功能需要两个VPC网段不能重叠，如果两个VPC中已使用的网段大量重叠，需要对现存网络架构进行改造。



    **VPC对等连接操作步骤**






    1. [为ACR实例绑定VPC内网域名解析](https://help.aliyun.com/zh/acr/user-guide/configure-access-over-vpcs#context-vfd-5l0-tf6 "")


       > 打通ACR企业版实例与VPC后，才能在VPC内通过内网域名访问企业版实例。完成配置后需要获取VPC ID和ACR企业版实例内网访问IP地址。

    2. [获取ACR实例相关域名信息和IP地址](https://help.aliyun.com/zh/acr/use-cases/access-enterprise-edition-instances-across-regions-or-from-idc#1d057a4680ogk "")


       > 获取访问ACR企业版实例使用的认证服务域名和IP地址、关联OSS Bucket域名和IP地址。

    3. [创建VPC对等连接并配置路由表](https://help.aliyun.com/zh/vpc/vpc-peer-to-peer-connection "")


       > 需要在VPC对等连接的两端添加指向对端的路由条目以实现ACK集群绑定的VPC和ACR企业版实例绑定的VPC私网互通。ACK集群绑定的VPC对等连接端还需要配置认证服务IP地址、关联OSS BucketIP地址的路由条目。

    4. 为ACK集群解析ACR实例域名


       > 通过 [添加内网DNS解析](https://help.aliyun.com/zh/dns/introduction-to-intranet-analysis "")、 [节点池自定义数据脚本](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#8613b8ae0bsra "") 批量修改`/etc/hosts`文件等方式，为ACK集群将ACR实例域名解析为ACR实例内网访问IP地址，从而通过VPC对等连接路由条目转发到ACR实例绑定的VPC。


  - **公网**：ACR企业版实例与ACK集群获得公网访问能力后，也可通过公网传输镜像。具体操作，请参见 [配置ACR公网访问控制](https://help.aliyun.com/zh/acr/user-guide/configure-access-over-the-internet "")， [为集群开启访问公网的能力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-an-existing-ack-cluster-to-access-the-internet "")。


## **使用托管免密组件**

### **步骤一：安装组件**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 在 **组件管理** 页面，选择 **安全** 页签，找到 **aliyun-acr-credential-helper托管** 卡片，单击 **安装** **。**

4. 在 **安装组件 aliyun-acr-credential-helper** 页面，可以看到 **AcrInstanceInfo** 配置以及一些其他选项。 **AcrInstanceInfo** 对应的是组件关联的每个ACR实例相关的配置。其他选项为组件配置，如无需修改组件监听命名空间或ServiceAccount，保持默认即可。


> 组件安装完成后，在 **组件管理** 页面，单击 **aliyun-acr-credential-helper托管** 卡片上的 **配置**，可变更组件配置。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8292288371/p901995.png)

关联ACR实例配置：




| **AcrInstanceInfo** | **说明** |
| --- | --- |



|     |     |     |
| --- | --- | --- |
| **AcrInstanceInfo** | **说明** |
| **InstanceId** | ACR实例ID，可通过[容器镜像服务控制台](https://cr.console.aliyun.com/)获取。<br>**重要**<br>使用个人版ACR实例时请留空，使用企业版ACR实例时必填。 |
| **regionId** | ACR实例所在地域的RegionId，可通过[容器镜像服务控制台](https://cr.console.aliyun.com/)获取。<br>**重要**<br>跨地域拉取镜像时必填。 |
| **domains** | 免密插件访问ACR实例所使用的域名。默认为上方填入的ACR实例的所有域名（公网、VPC）。若要指定个别域名，多个以英文半角逗号（,）分隔。 |
| 跨账号拉取镜像场景配置<br>> 适用于跨账号拉取镜像的场景。如无需求，请留空。 | **assumeRoleARN** | 同账号拉取时无需配置，如需跨账号拉取请参见 [跨账号拉取镜像](https://help.aliyun.com/zh/acr/user-guide/use-secret-free-components-to-pull-images-across-accounts "")。 |
| **expireDuration** |
| **rrsaRoleARN** |
| **rrsaOIDCProviderRoleARN** |





**组件配置**






|     |     |
| --- | --- |
| **配置项** | **说明** |
| **是否开启RRSA** | 勾选后即可开启RRSA，同账号拉取时无需配置，如需跨账号拉取请参见 [跨账号拉取镜像](https://help.aliyun.com/zh/acr/user-guide/use-secret-free-components-to-pull-images-across-accounts "")。 |
| **watchNamespace** | 期望能免密拉取镜像的命名空间，默认值`default`。当取值为`all`时，表示期望所有命名空间均能免密拉取。如需指定多个命名空间，请使用英文半角逗号（,）分隔。推荐配置业务命名空间，尽量避免配置`all`或者集群系统组件相关的命名空间，以免影响集群系统组件镜像的拉取。 |
| **serviceAccount** | 使免密组件托管版作用于指定的Service Account。默认值`Default`。取值为`Default`时，会作用于所有指定命名空间的默认Service Account。如果设置为（\*）， 表示支持指定命名空间下的所有ServiceAccount。如果需要配置多个，请使用以英文半角逗号（,）分隔。 |
| **expiringThreshold** | 组件内凭证过期阈值，默认值为`15m`。 |
| **notifyEmail** | 无需配置。 |


### **步骤二：拉取镜像**

安装并配置完成免密组件后，在创建工作负载时指定免密组件已关联的ServiceAccount，即可实现免密拉取镜像。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      serviceAccountName: my-service-account # 指定免密组件已经关联的ServiceAccount
      containers:
      - name: nginx
        image: "******.cn-hangzhou.cr.aliyuncs.com/nginx/nginx:latest" # 指定ACR镜像地址
        ports:
        - containerPort: 80
```

## **使用自行运维免密组件**

### **步骤一：安装组件**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 在 **组件管理** 页面，单击 **安全** 页签，找到 **aliyun-acr-credential-helper**，单击 **安装**。

4. 在 **参数配置** 页面，通过 **tokenMode** 选择组件权限模式，然后单击 **确认**。组件安装完成后，在拉取镜像前，请参见 [步骤二：变更组件配置（添加ACR实例）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/non-secret-pulling-container-image#d69c0aa102487 "") 完成组件配置。




| **tokenMode** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **tokenMode** | **说明** |
| **auto** | （推荐）组件会检测集群创建时间，并自动决定权限模式。集群在2023年04月03日之前创建将使用workerRole模式，集群在2023年04月03日及之后创建将使用managedRole模式。<br>**重要**<br>aliyun-acr-credential-helper在2023年04月03日后发布的版本中提供了配置项，支持自定义组件依赖的RAM角色。详细信息，请参见 [【产品变更】关于变更aliyun-acr-credential-helper组件依赖权限的公告](https://help.aliyun.com/zh/ack/product-overview/product-changes-revoke-the-permissions-on-which-aliyun-acr-credential-helper-relies#task-2292520 "")。 |
| **managedRole** | 组件将使用 [前提条件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/non-secret-pulling-container-image#26463d5141htp "") 中授权的AliyunCSManagedAcrRole角色获取权限。 |
| **workerRole** | 组件将使用集群Worker RAM角色获取权限。需为Worker RAM角色授予特定权限。<br>**组件模式选择workerRole**<br>组件权限模式选择workerRole时，集群Worker RAM角色必须拥有以下权限。授权具体操作，请参见 [管理RAM角色的权限](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-role "")。<br>```json<br>{<br>    "Version": "1",<br>    "Statement": [<br>        {<br>            "Action": [<br>                "cr:GetAuthorizationToken",<br>                "cr:ListInstanceEndpoint",<br>                "cr:PullRepository"<br>            ],<br>            "Resource": "*",<br>            "Effect": "Allow"<br>        }<br>    ]<br>}<br>```<br>**重要**<br>如需通过角色扮演跨账号拉取镜像，请选择此模式。 |


### **步骤二：变更组件配置（添加ACR实例）**

免密组件安装完成后，在拉取镜像前，需要通过控制台或kubectl对免密组件配置项 **acr-configuration** 进行配置以添加ACR实例。

控制台

kubectl

1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**配置管理** \> **配置项**。

2. 在 **配置项** 页面顶部的 **命名空间** 下拉列表，选择 **kube-system**，然后单击配置项 **acr-configuration**，参考下列说明修改配置。


|     |     |
| --- | --- |
| **组件配置** | **说明** |
| **watch-namespace** | 期望能免密拉取镜像的命名空间。默认值为 **default**。当取值为 **all** 时，表示期望所有命名空间均能免密拉取。配置多个命名空间时以英文半角逗号（,）分隔。推荐配置生效命名空间为业务命名空间，尽量避免配置`all`或者集群系统组件相关的命名空间，以免影响集群系统组件镜像的拉取。 |
| **acr-api-version** | 保持默认。 |
| **expiring-threshold** | 组件内凭证过期阈值，默认值为`15m`（15分钟）。 |
| **acr-registry-info** | 容器镜像的实例信息数组，YAML多行字符串格式，每个实例以三元组方式配置。<br>   - `instanceId`：ACR实例ID，可通过[容器镜像服务控制台](https://cr.console.aliyun.com/)获取。<br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     使用个人版ACR实例时请留空，使用企业版ACR实例时必填。<br>     <br>   - `regionId`：ACR实例所在地域的RegionId。可通过[容器镜像服务控制台](https://cr.console.aliyun.com/)获取。<br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     跨地域拉取镜像时必填，请参见下方的配置示例。<br>     <br>   - `domains`：免密插件访问ACR实例所使用的域名。默认填入`instanceId`中ACR实例的所有域名。若要指定个别域名，多个以英文半角逗号（,）分隔。<br>     <br>**跨地域拉取配置示例**<br>使用多个不同地域的ACR实例时，需为每个ACR实例指定ID与地域。<br>```yaml<br>data:<br>    service-account: "default"<br>    watch-namespace: "all"<br>    expiring-threshold: "15m"<br>    notify-email: "c*@aliyuncs.com"<br>    acr-registry-info: |<br>      - instanceId: "cri-instanceId"<br>        regionId: "cn-beijing"<br>      - instanceId: "cri-instanceId"<br>        regionId: "cn-hangzhou"      <br>``` |
| **service-account** | 免密组件关联的ServiceAccount，多个ServiceAccount以英文半角逗号（,）分隔。取值为 **default** 时，组件会关联每个watch-namespace中填入的指定命名空间的默认ServiceAccount。取值为`“*”`时，组件会关联指定命名空间的所有ServiceAccount。 |


![12](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0995435271/p843709.gif)

1. 执行以下命令，参考下列配置说明，编辑`acr-configuration`。















```shell
kubectl edit cm acr-configuration -n kube-system
```




|     |     |     |
| --- | --- | --- |
| **配置项键** | **配置项键说明** | **配置项值** |
| service-account | 使免密组件作用于指定的服务账号。 | 默认为 **default**。<br>**说明**<br>如果要配置多个请以英文半角逗号（,）分隔。如果设置为`“*”`， 表示支持指定命名空间下的所有ServiceAccount。 |
| acr-registry-info | 容器镜像的实例信息数组，YAML多行字符串格式，每个实例以三元组方式配置。<br>**说明**<br>实例信息三元组：<br>   - instanceId：实例ID，企业版实例必须配置此项。<br>     <br>   - regionId：可选，默认为本地地域。<br>     <br>   - domains：可选，默认为相应实例的所有域名。若要指定个别域名，多个以英文半角逗号（,）分隔。 | 企业版容器镜像实例，配置示例如下：<br>```json<br>- instanceId: <cri-instanceId><br>  regionId: "cn-hangzhou"<br>  domains: "xxx.com,yyy.com"<br>``` |
| watch-namespace | 期望能免密拉取镜像的Namespace。 | 默认值为 **default**。当取值为 **all** 时，表示期望所有Namespace均能免密拉取。如需配置多个Namespace时，以英文半角逗号（,）分隔。<br>**说明**<br>推荐配置生效Namespace为您的业务Namespace，尽量避免配置 **all** 或者集群系统组件相关Namespace，以免影响集群系统组件镜像的拉取。 |
| expiring-threshold | 本地缓存凭证过期阈值。 | 默认值为`15m`（15分钟）。 |


### **步骤三：拉取镜像**

安装并配置完成免密组件后，在创建工作负载时指定免密组件已关联的ServiceAccount，即可实现免密拉取镜像。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      serviceAccountName: my-service-account # 指定免密组件已经关联的ServiceAccount
      containers:
      - name: nginx
        image: "******.cn-hangzhou.cr.aliyuncs.com/nginx/nginx:latest" # 指定ACR镜像地址
        ports:
        - containerPort: 80
```

## **常见问题**

### **如何开启ServiceAccount创建即时使用功能？**

**重要**

开启ServiceAccount创建即时使用功能需要将免密组件升级到v23.02.06.1-74e2172-aliyun或以上版本。

启用ServiceAccount创建即时使用功能后，免密组件会通过Webhook监测集群内ServiceAccount变化。当新的ServiceAccount被创建后，组件会立即为其注入免密Secret。这个功能适用于ServiceAccount创建后需要立即使用的场景，例如，通过Helm Chart同时创建ServiceAccount和Deployment的场景。因对组件性能有一定影响，其他场景中不推荐开启该功能。

托管组件

自行运维组件

需要在集群中安装acr-credential-helper-webhook组件：

1. 在[ACK集群列表](https://cs.console.aliyun.com/)页面，单击目标集群名称，在集群详情页左侧导航栏，单击 **组件管理**。

2. 在 **组件管理** 页面，选择 **安全** 页签，找到 **acr-credential-helper-webhook托管** 卡片，单击 **安装** **。**


需要开启此功能，请在 **acr-configuration** 中添加下列字段：

```yaml
data:
  webhook-configuration: |
    enable: true
    failure-policy: Ignore
    timeout-seconds: 10
```

|     |     |
| --- | --- |
| **配置项** | **说明** |
| `enable` | 是否开启Webhook功能。<br>- `true`：开启。<br>  <br>- `false`：不开启。 |
| `failure-policy` | 当本功能出现异常时，对ServiceAccount的处理策略。<br>- `Ignore`：忽略异常，ServiceAccount正常创建完成（但可能不会附上可拉取镜像的Secret）。<br>  <br>- `Fail`：异常时中断ServiceAccount的创建（不推荐，可能导致业务部署失败）。<br>  <br>**重要**<br>受集群API Server的限制，当`timeout-seconds`设置为`15`，`failure-policy`设置为`Fail`，持续每秒创建10个ServiceAccount时，会出现创建ServiceAccount失败的情况。 |
| `timeout-seconds` | 本功能的单个ServiceAccount创建请求处理超时时长，超出该时长则按照`failure-policy`配置进行反馈。默认值为10，单位秒（s）。 |

### **配置免密组件后为什么仍然拉取失败？**

一个可能的原因是免密组件配置错误，例如：

- 免密组件中的实例信息与ACR实例不符。

- 拉取镜像使用的镜像地址与免密组件中实例信息的域名不符。


请按照本文中的操作进行排查。

如组件配置正确时，仍出现了拉取失败情况，可能是因工作负载YAML中手动填入的`imagePullSecrets`与免密组件产生冲突。请手动删除`imagePullSecrets`字段，并删除旧Pod重建以解决此问题。

### **如何使用imagePullSecrets？**

2024年09月09日及之后新建的ACR个人版不支持使用免密组件。使用新建的ACR个人版实例时，建议通过Secret保存用户名与登录密码的方式，在`imagePullSecrets`字段中使用。

**重要**

- 免密组件不支持与手动填入`imagePullSecrets`字段同时使用。

- Secret需与工作负载处于同一命名空间。


**使用imagePullSecrets示例**

执行以下命令并替换其中的参数，即可通过用户名和密码创建密钥Secret。

```bash
kubectl create secret docker-registry image-secret-1 \
  --docker-server=<registry-server> \
  --docker-username=<name> \
  --docker-password=<password> \
  --docker-email=<email>
```

在工作负载中使用密钥

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-test
  namespace: default
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      imagePullSecrets:
      - name: image-secret-1  # 使用上一步创建的Secret
      containers:
      - name: nginx
        image: <acrID>.cr.aliyuncs.com/<repo>/nginx:latest  # 替换为ACR链接
```

## **相关文档**

- 使用免密组件跨账号拉取镜像的操作，请参见 [跨账号拉取镜像](https://help.aliyun.com/zh/acr/user-guide/use-secret-free-components-to-pull-images-across-accounts "")。

- 免密组件变更记录，请参见 [aliyun-acr-credential-helper](https://help.aliyun.com/zh/ack/product-overview/aliyun-acr-credential-helper "")。