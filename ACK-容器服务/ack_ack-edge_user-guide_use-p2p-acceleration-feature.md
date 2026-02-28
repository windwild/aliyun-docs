### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)[容器镜像](https://help.aliyun.com/zh/ack/ack-edge/user-guide/container-mirrors/)使用P2P加速

# 使用P2P加速

更新时间：2025-07-17 04:29:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：在ACK Edge集群中安装P2P加速套件](https://help.aliyun.com/zh/ack/ack-edge/user-guide/install-p2p-acceleration-kit-in-ack-clusters)[下一篇：部署DeepSeek蒸馏模型推理服务](https://help.aliyun.com/zh/ack/ack-edge/use-cases/deploy-deepseek-distilled-model-inference-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

使用限制

启用P2P加速

验证P2P加速

（可选）启用客户端指标采集

P2P Metrics说明

打开Metrics

访问方式

指标说明

审计日志

（可选）关闭按需加载镜像使用P2P加速

附录

P2P 加速效果参考

P2P加速功能可以提升镜像拉取速度，减少应用部署时间。当大规模容器集群批量下载镜像时，您可以使用P2P加速功能提升镜像拉取速度。本文介绍如何使用P2P加速功能提升镜像拉取速度。

## **背景信息**

当大规模容器集群批量下载镜像时，容器镜像存储的网络带宽会成为性能瓶颈，导致镜像拉取缓慢。P2P加速功能可以利用您计算节点的带宽资源，进行节点之间的镜像分发，以减少对容器镜像存储的压力，可以大幅提升镜像拉取速度，减少应用部署时间。经过测试，1000节点规模下拉取1 GB大小的镜像，相比普通镜像拉取方式（以带宽为10 Gbps为例），P2P加速方式可以减少95%以上的镜像拉取时间。此外，新版的P2P加速方案相较于旧版的P2P有30%~50%的性能提升，且新版的P2P方案默认支持按需加载容器镜像使用P2P加速，具体操作，请参见 [按需加载容器镜像](https://help.aliyun.com/zh/acr/user-guide/load-resources-of-a-container-image-on-demand "")。

您可以在以下场景使用P2P加速功能。

- ACK集群

- IDC或其他云厂商集群


## **前提条件**

安装P2P加速套件。

- 若您需要在ACK集群中使用P2P加速功能。关于如何安装P2P加速套件的具体操作，请参见 [在ACK集群中安装P2P加速套件](https://help.aliyun.com/zh/acr/user-guide/use-p2p-acceleration-in-an-ack-cluster "")。

- 若您需要在IDC或其他云厂商集群中使用P2P加速功能。关于如何安装P2P加速套件的具体操作，请参见 [在IDC或其他云厂商集群中安装P2P加速套件](https://help.aliyun.com/zh/acr/user-guide/install-p2p-acceleration-suite-in-idc-or-other-cloud-vendor-clusters "")。


## **使用限制**

开启P2P加速后，P2P加速套件会将您的容器镜像地址通过Webhook替换为P2P的镜像地址，例如，您的原始镜像地址为`test****vpc.cn-hangzhou.cr.aliyuncs.com/docker-builder/nginx:latest`，替换后的P2P加速镜像地址为`test****vpc.distributed.cn-hangzhou.cr.aliyuncs.com:65001/docker-builder/nginx:latest`。

同时，Webhook会帮您自动生成一个用于加速镜像地址的镜像拉取密钥（基于原始镜像的镜像拉取密钥复制生成），由于该P2P镜像拉取密钥的创建和P2P镜像地址的替换是异步逻辑，因此建议您在下发工作负载前优先下发容器镜像拉取需要的镜像拉取密钥，或手动创建一个用于P2P镜像拉取（domain为`test-registry-vpc.distributed.cn-hangzhou.cr.aliyuncs.com:65001`）的镜像拉取密钥，然后再下发工作负载，避免由于镜像地址的替换而导致镜像拉取失败。

## 启用P2P加速

您可以通过添加标签的方式启用P2P加速，可以为应用负载添加P2P加速标签，例如Pod、Deployment等。也可以为ACK集群的命名空间设置P2P加速标签。为命名空间设置P2P加速标签后，该命名空间内的所有符合加速条件的应用负载都会启用P2P加速，无需再修改应用负载的YAML文件。根据实际情况选择任一方式添加P2P加速标签。

**说明**

标签的名称为`k8s.aliyun.com/image-accelerate-mode`，值为`p2p`。

- 为应用负载添加P2P加速标签。



以下以Deployment为例设置标签。执行以下命令，为Deployment设置标签。

















```shell
kubectl edit deploy <Deployment名称>
```





在Deployment文件中添加标签`k8s.aliyun.com/image-accelerate-mode: p2p`。

















```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: test
    labels:
      app: nginx
spec:
    replicas: 1
    selector:
      matchLabels:
        app: nginx
    template:
      metadata:
        labels:
          # enable P2P
          k8s.aliyun.com/image-accelerate-mode: p2p
          app: nginx
      spec:
        # your ACR instacne image pull secret
        imagePullSecrets:
      - name: test-registry
      containers:
      # your ACR instacne image
      - image: test-registry-vpc.cn-hangzhou.cr.aliyuncs.com/docker-builder/nginx:latest
        name: test
        command: ["sleep", "3600"]
```

- 为命名空间添加P2P加速标签

  - 通过控制台添加P2P加速标签。

    1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

    2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择 **命名空间与配额**。

    3. 在 **命名空间** 页面单击目标命名空间 **操作** 列的 **编辑**。

    4. 在 **编辑命名空间** 对话框中，单击 **+命名空间标签**，配置 **变量名称** 为`k8s.aliyun.com/image-accelerate-mode`， **变量值** 为`p2p`，然后单击 **确定**。
  - 通过命令行添加P2P加速标签。















    ```shell
    kubectl label namespaces <YOUR-NAMESPACE> k8s.aliyun.com/image-accelerate-mode=p2p
    ```

## 验证P2P加速

启用P2P加速后，P2P组件会自动为Pod注入P2P相关 **annotation**、P2P加速镜像地址以及对应的镜像拉取凭证。

**重要**

P2P镜像拉取凭证与您原先配置的非P2P镜像地址拉取凭证仅镜像仓库域名不一样，其他凭证信息一致。因此，若您原先镜像拉取凭证用户信息配置错误，也会导致P2P镜像拉取失败。

执行以下命令，查看Pod。

```shell
kubectl get po <Pod的名称> -oyaml
```

预期输出：

```yaml
apiVersion: v1
kind: Pod
metadata:
annotations:
    # inject p2p-annotations automatically
    k8s.aliyun.com/image-accelerate-mode: p2p
    k8s.aliyun.com/p2p-config: '...'
spec:
containers:
# inject image to p2p endpoint
   - image: test-registry-vpc.distributed.cn-hangzhou.cr.aliyuncs.com:65001/docker-builder/nginx:latest
imagePullSecrets:
  - name: test-registry
# inject image pull secret for p2p endpoint
  - name: acr-credential-test-registry-p2p
```

可以看到，Pod已注入P2P相关 **annotation**、P2P加速镜像地址以及对应的镜像拉取凭证，说明启用P2P加速成功。

## （可选） **启用客户端指标采集**

### **P2P Metrics说明**

### **打开Metrics**

安装P2P时，打开Metrics配置。

```yaml
p2p:

v2:
    # Component for P2P v2
    image: registry-vpc.__ACK_REGION_ID__.aliyuncs.com/acs/dadi-agent
    imageTag: v0.1.2-72276d4-aliyun

    # Concurrency limit number of layers downloading by each node proxy
    proxyConcurrencyLimit: 128

    # The server port to communicate with P2P nodes
    p2pPort: 65002

    cache:
      # Disk cache capacity in bytes, default 4GB
      capacity: 4294967296
      # Set to 1 if you are using high-performance disks on your ECS, e.g. ESSD PL2/PL3
      aioEnable: 0
    exporter:
      # Set to true if you want to collect component metrics
      enable: false
      port: 65003

    # limit for downstream throughput
    throttleLimitMB: 512
```

### 访问方式

P2P YAML中关于`exporter`字段定义了Metrics的端口。

```yaml
ExporterConfig:
enable: true # 是否开启
port: 65006  # 监听端口
standaloneExporterPort: true # 是否采用独立端口暴露，如果为false，则通过http服务端口吐出
```

`curl 127.0.0.1:$port/metrics`可以得到Metrics结果如下。

```bash
# HELP DADIP2P_Alive
# TYPE DADIP2P_Alive gauge
DADIP2P_Alive{node="192.168.69.172:65005",mode="agent"} 1.000000 1692156721833

# HELP DADIP2P_Read_Throughtput Bytes / sec
# TYPE DADIP2P_Read_Throughtput gauge
DADIP2P_Read_Throughtput{node="192.168.69.172:65005",type="pread",mode="agent"} 0.000000 1692156721833
DADIP2P_Read_Throughtput{node="192.168.69.172:65005",type="download",mode="agent"} 0.000000 1692156721833
DADIP2P_Read_Throughtput{node="192.168.69.172:65005",type="peer",mode="agent"} 0.000000 1692156721833
DADIP2P_Read_Throughtput{node="192.168.69.172:65005",type="disk",mode="agent"} 0.000000 1692156721833
DADIP2P_Read_Throughtput{node="192.168.69.172:65005",type="http",mode="agent"} 0.000000 1692156721833

# HELP DADIP2P_QPS
# TYPE DADIP2P_QPS gauge
DADIP2P_QPS{node="192.168.69.172:65005",type="pread",mode="agent"} 0.000000 1692156721833
DADIP2P_QPS{node="192.168.69.172:65005",type="download",mode="agent"} 0.000000 1692156721833
DADIP2P_QPS{node="192.168.69.172:65005",type="peer",mode="agent"} 0.000000 1692156721833
DADIP2P_QPS{node="192.168.69.172:65005",type="disk",mode="agent"} 0.000000 1692156721833
DADIP2P_QPS{node="192.168.69.172:65005",type="http",mode="agent"} 0.000000 1692156721833

# HELP DADIP2P_MaxLatency us
# TYPE DADIP2P_MaxLatency gauge
DADIP2P_MaxLatency{node="192.168.69.172:65005",type="pread",mode="agent"} 0.000000 1692156721833
DADIP2P_MaxLatency{node="192.168.69.172:65005",type="download",mode="agent"} 0.000000 1692156721833
DADIP2P_MaxLatency{node="192.168.69.172:65005",type="peer",mode="agent"} 0.000000 1692156721833
DADIP2P_MaxLatency{node="192.168.69.172:65005",type="disk",mode="agent"} 0.000000 1692156721833
DADIP2P_MaxLatency{node="192.168.69.172:65005",type="http",mode="agent"} 0.000000 1692156721833

# HELP DADIP2P_Count Bytes
# TYPE DADIP2P_Count gauge
DADIP2P_Count{node="192.168.69.172:65005",type="pread",mode="agent"} 0.000000 1692156721833
DADIP2P_Count{node="192.168.69.172:65005",type="download",mode="agent"} 0.000000 1692156721833
DADIP2P_Count{node="192.168.69.172:65005",type="peer",mode="agent"} 0.000000 1692156721833
DADIP2P_Count{node="192.168.69.172:65005",type="disk",mode="agent"} 0.000000 1692156721833
DADIP2P_Count{node="192.168.69.172:65005",type="http",mode="agent"} 0.000000 1692156721833

# HELP DADIP2P_Cache
# TYPE DADIP2P_Cache gauge
DADIP2P_Cache{node="192.168.69.172:65005",type="allocated",mode="agent"} 4294967296.000000 1692156721833
DADIP2P_Cache{node="192.168.69.172:65005",type="used",mode="agent"} 4294971392.000000 1692156721833

# HELP DADIP2P_Label
# TYPE DADIP2P_Label gauge
```

### 指标说明

#### **指标名**

- DADIP2P\_Alive：服务是否存活。

- DADIP2P\_Read\_Throughtput：P2P服务吞吐，单位：byte/s。

- DADIP2P\_QPS：QPS。

- DADIP2P\_MaxLatency：延迟统计，单位：us。

- DADIP2P\_Count：流量统计，单位：bytes。

- DADIP2P\_Cache：单机Cache用量，单位：bytes。


#### **Tag**

- node：P2P Agent/Root的服务IP和端口。

- type：指标类型。

  - pread：处理下游请求。

  - download：回源。

  - peer：P2P网络分发。

  - disk：处理磁盘。

  - http：处理HTTP请求。

  - allocated：缓存分配空间。

  - used：缓存使用空间。

**指标示例**

```yaml
DADIP2P_Count{node="11.238.108.XXX:9877",type="http",mode="agent"} 4248808352.000000 1692157615810
Agent服务累计处理HTTP请求流量：4248808352字节。

DADIP2P_Cache{node="11.238.108.XXX:9877",type="used",mode="agent"} 2147487744.000000 1692157615810
当前Agent缓存用量：2147487744字节。
```

### **审计日志**

#### **开启审计日志**

修改`p2p configmap`里 **audit** 字段为`true`。

```yaml
DeployConfig:
mode: agent
logDir: /dadi-p2p/log
logAudit: true
logAuditMode: stdout # 输出到控制台, file为输出到日志目录/dadi-p2p/log/audit.log
```

#### **审计日志格式**

格式如下，其含义为：从接收到请求至结果返回的处理耗时，单位：us。

```bash
2022/08/30 15:44:52|AUDIT|th=00007FBA247C5280|download[pathname=/https://cri-pi840la*****-registry.oss-cn-hangzhou.aliyuncs.com/docker/registry/v2/blobs/sha256/dd/dd65726c224b09836aeb6ecebd6baf58c96be727ba86da14e62835569896008a/data][offset=125829120][size=2097152][latency=267172]
....
2022/08/30 15:44:55|AUDIT|th=00007FBA2EFEAEC0|http:pread[pathname=/https://cri-pi840lacia*****-registry.oss-cn-hangzhou.aliyuncs.com/docker/registry/v2/blobs/sha256/dd/dd65726c224b09836aeb6ecebd6baf58c96be727ba86da14e62835569896008a/data][offset=127467520][size=65536][latency=21]
```

主要字段为：时间、 AUDIT、线程指针、操作码\[pathname=\]\[size=\]\[latency=\]。

其中AUDIT和线程指针一般不用关心， **size** 为单次请求大小，若为负数则表示异常； **latency** 为单次请求延迟，单位：us。

常见操作码如下：

- http:pread：表示HTTP Proxy处理下游数据请求。

- rpc:stat：表示P2P Agent获取文件长度。

- rpc:pread：表示P2P Agent处理下游数据请求。

- download：表示P2P Agent从上游下载数据。

- filewrite：表示P2P Agent写入当前数据分片到缓存。

- fileread：表示P2P Agent从缓存读取数据分片。


**日志示例**

```yaml
download[pathname=mytest][offset=0][size=65536][latency=26461]
## P2P Agent从上游下载mytest文件[0,65536)这段数据的延迟为26461us\
rpc:pread[pathname=mytest][offset=0][size=65536][latency=2]\
## P2P Agent向下游返回mytest文件[0,65536)这段数据的延迟为2us\
http:pread[pathname=mytest][offset=0][size=65536][latency=26461]\
## 代理向从上游下载mytest文件[0,65536)这段数据的延迟为26461us\
```\
\
## （可选）关闭按需加载镜像使用P2P加速\
\
**说明**\
\
以下是集群内修改单节点配置的参考步骤。您需关注节点的后续运维操作，是否会覆盖此配置。\
\
1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。\
\
2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点**。\
\
3. 在 **节点** 页面，单击目标节点IP地址下的 **实例ID**。\
\
4. 在实例详情页面，使用 **远程连接**，登录节点。\
\
5. 使用`vi`命令编辑`/etc/overlaybd/overlaybd.json`文件中的 **p2pConfig**，将 **enable** 改为 **false**。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```json\
{\
        "p2pConfig": {\
           "enable": false,\
           "address": "https://localhost:6****/accelerator"\
       },\
... ...\
}\
```\
\
6. 执行如下命令，重新按需加载的组件。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```shell\
service overlaybd-tcmu restart\
```\
\
\
## **附录**\
\
### **P2P 加速效果参考**\
\
#### **不同规格镜像拉取**\
\
**测试镜像规格如下**\
\
- 4 GB（512 MB \* 8层）\
\
- 10 GB（10 GB \* 1层）\
\
- 20 GB（4 GB \* 5层，10 GB \* 2层，512 MB \* 40层， 20 GB \* 1层，2 GB \* 10层）\
\
\
**测试环境如下**\
\
- ACK集群：1000节点\
\
- ECS规格：4核8 GB内存\
\
- 云盘规格：200 GB ESSD PL1\
\
- P2P Agent规格：1核1 GB内存，缓存4 GB\
\
\
**测试场景**\
\
1000 节点拉取相同镜像（含镜像下载后解压完成）\
\
**测试结果（P95耗时）**\
\
| **镜像规格** | **耗时** | **回源（Bucket）峰值吞吐（Gbps）** |\
| --- | --- | --- |\
\
|     |     |     |\
| --- | --- | --- |\
| **镜像规格** | **耗时** | **回源（Bucket）峰值吞吐（Gbps）** |\
| 512 MB \* 8层 | 116秒 | 2 |\
| 10 GB \* 1层 | 6分20秒 | 1.2 |\
| 4 GB \* 5层 | 9分15秒 | 5.1 |\
| 10 GB \* 2层 | 9分50秒 | 6.7 |\
| 512 MB \* 40层 | 7分55秒 | 3.8 |\
| 20 GB \* 1层 | 11分 | 2.5 |\
| 2 GB \* 10层 | 8分13秒 | 3.2 |