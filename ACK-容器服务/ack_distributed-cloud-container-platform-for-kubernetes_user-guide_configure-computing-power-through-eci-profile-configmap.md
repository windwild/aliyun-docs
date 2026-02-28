### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/)[注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/registered-clusters/)[接入云上Serverless算力](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/integrate-serverless-computing-power-on-the-cloud/)[ACS算力](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/acs-computing-power/)[ACS算力高级配置](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/advanced-configuration-for-acs-compute-resources/)通过配置项eci-profile配置ACS算力参数

# 通过配置项eci-profile配置ACS算力参数

更新时间：2025-03-12 05:10:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：采集ACS Pod的Prometheus Metrics指标](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/collect-prometheus-metrics-from-acs-pods)[下一篇：ACS Pod Annotation功能说明](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/acs-pod-annotation-guide)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

配置说明

更新集群配置项

配置Selectors

演示示例

为了减少您对业务YAML的改动，ACS算力支持eci-profile功能，可以提供集群维度的资源视图。本文介绍如何配置eci-profile。

## 功能介绍

eci-profile支持Pod配置自动注入，其中包含了交换机、安全组、域名解析模式等集群维度的配置，您可以根据需要进行更新：

- 更新配置时无需重启acs-virtual-node组件。

- 对于新创建的ACS Pod，可以即时生效更新后的配置；对于存量ACS Pod，需要滚动发布后才能生效更新后的配置。


## 配置说明

创建Pod时，系统会读取kube-system命名空间下的eci-profile配置文件（名为eci-profile的ConfigMap），并按照文件中的配置来创建Pod。您可以通过以下命令查看eci-profile的YAML。

```bash
kubectl get cm -n kube-system eci-profile -o yaml
```

YAML内容如下：

```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: eci-profile
  namespace: kube-system
data:
  enablePrivateZone: "false"
  securityGroupId: sg-2zeeyaaxlkq9sppl****
  vSwitchIds: vsw-2ze23nqzig8inprou****,vsw-2ze94pjtfuj9vaymf****
  vpcId: vpc-2zeghwzptn5zii0w7****
  selectors: ""
```

修改eci-profile的方式如下：

- 通过kubectl edit命令















```bash
kubectl edit configmap eci-profile -n kube-system
```

- 通过容器计算服务管理控制台

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**配置管理** \> **配置项**。

3. 在 **配置项** 页面，选择 **命名空间** 为 **kube-system**，找到eci-profile，单击 **YAML编辑**。



     **说明**





     如果修改eci-profile中的某项配置后，文件存在格式错误，修改的配置将不会生效，具体的错误信息会保存到event中，您可以通过以下kubectl命令查看

















     ```shell
     kubectl -n kube-system get event --field-selector involvedObject.namespace=kube-system,involvedObject.name=eci-profile
     ```

## 更新集群配置项

eci-profile中包含了`vpcId`、`vSwitchIds`等集群配置项对应VPC、交换机等信息，您可以根据需要进行更新，更新后的配置可以即时生效（热更新）。支持更新的配置项如下：

| **配置项** | **示例值** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **配置项** | **示例值** | **说明** |
| `securityGroupId` | `sg-2ze0b9o8pjjzts4h****` | ACS Pod所属安全组。 |
| `vSwitchIds` | `vsw-2zeet2ksvw7f14ryz****` | ACS Pod所属交换机。可配置多个，用半角逗号间隔。 |
| `vpcId` | `vpc-2zeghwzptn5zii0w7****` | ACS Pod所属VPC。 |
| `enablePrivateZone` | `"false"` | 是否使用PrivateZone进行域名解析。 |

**说明**

上述配置项均为集群级别的默认配置项，如果在创建ACS Pod时没有特别修改和覆盖某些参数，系统将会采用eci-profile中预先设定的默认配置。

## 配置Selectors

创建Pod时，系统会按照Selectors去匹配Pod，对于Label能够匹配上的Pod，会自动追加Annotation和Label，以便生效ACS Pod的功能特性。

Selectors中可以包含多个Selector，在每个Selector中，您必须声明Selector的name，配置格式如下：

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| `name` | Selector名称，必填不能为空。 |
| `namespaceSelector` | 通过Namespace Label筛选Pod。 |
| `namespaceSelector.matchLabels` | 通过`{key,value}`格式描述匹配规则。 |
| `namespaceSelector.matchExpressions` | 通过选择运算符列表描述匹配规则。 <br>有效的运算符包括`In`、`NotIn`、`Exists`和`DoesNotExist`。 在`In`和`NotIn`的情况下，设置的值必须是非空的。 |
| `objectSelector` | 通过Pod Label筛选。 |
| `objectSelector.matchLabels` | 通过`{key,value}`格式描述匹配规则。 |
| `objectSelector.matchExpressions` | 通过选择运算符列表描述匹配规则。 <br>有效的运算符包括`In`、`NotIn`、`Exists`和`DoesNotExist`。 在`In`和`NotIn`的情况下，设置的值必须是非空的。 |
| `effect` | 要动态追加的Annotation和Label。 |

Selectors的配置模板如下：

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: eci-profile
  namespace: kube-system
data:
  selectors: |
    [\
      {\
        "name": "selector-demo1",\
        "namespaceSelector": {\
          "matchLabels": {\
            "kubernetes.io/metadata.name": "dev-ns"\
          }\
        },\
        "objectSelector": {\
          "matchLabels": {\
            "acs": "true"\
          },\
          "matchExpressions": [\
            {\
              "key": "usage",\
              "operator": "In",\
              "values": ["testing"]\
            }\
          ]\
        },\
        "effect": {\
          "annotations": {\
            "network.alibabacloud.com/custom-dnsconfig": "{\"servers\":[\"114.114.114.114\",\"8.8.8.8\"],\"searches\":[\"xx.com\",\"yy.com\"],\"options\":[\"ndots:2\",\"edns0\"]}"\
          },\
          "labels": {\
            "created-by-acs": "true"\
          }\
        }\
      }\
    ]
```

上述模板中，名为selector-demo1的Selector可以实现以下功能：

如果Pod所属命名空间为`dev-ns`，并且Pod本身含有`acs=true`和`usage=testing`Label，则该Pod会自动增加`network.alibabacloud.com/custom-dnsconfig="{\"servers\":[\"114.114.114.114\",\"8.8.8.8\"],\"searches\":[\"xx.com\",\"yy.com\"],\"options\":[\"ndots:2\",\"edns0\"]}"`的Annotation，以及`created-by-acs=true` 的Label。

**重要**

为了确保精确匹配，建议您在一个Selector中至少配置`namespaceSelector`或`objectSelector`中的一个。如果两者同时配置，则Pod需要同时满足两种条件才可以成功匹配；如果两者都不配置，则该`effect`将作用于集群内所有的ACS Pod，可能会导致不必要的影响。

如果同时配置了多个Selector，ACS将按照顺序匹配。成功匹配某个Selector后，会自动将该Selector中`effect`声明的Annotation和Label追加到Pod中，不会覆盖Pod原有的值。如存在重复的Annotation和Label，作用的优先级如下：

Pod原有的声明值。

最先被匹配上的Selector中`effect`声明的值。

后续匹配的Selector中`effect`声明的值。

### **演示示例**

1. 使用以下内容，创建一个符合selector-demo1条件的Deployment。















```yaml
apiVersion: v1
kind: Pod
metadata:
     name: nginx
     namespace: dev-ns
     labels:
       alibabacloud.com/acs: 'true'
       alibabacloud.com/compute-class: general-purpose
       alibabacloud.com/compute-qos: default
       acs: "true"
       usage: "testing"
spec:
     containers:
  - name: nginx
    image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6
    command: ["sleep", "infinity"]
    ports:
    - containerPort: 80
```

2. Deployment创建完成后，查看Pod信息如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6460771471/p923522.png)