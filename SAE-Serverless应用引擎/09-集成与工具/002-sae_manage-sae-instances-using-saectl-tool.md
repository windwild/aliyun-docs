### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[开发参考](https://help.aliyun.com/zh/sae/developer-reference/)[saectl工具](https://help.aliyun.com/zh/sae/saectl-tool/)使用saectl工具管理应用实例Pod

# 使用saectl工具管理应用实例Pod

更新时间：2026-01-15 04:05:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用saectl工具管理应用](https://help.aliyun.com/zh/sae/use-saectl-tool-to-configure-an-application)[下一篇：使用saectl工具管理配置项ConfigMap](https://help.aliyun.com/zh/sae/manage-sae-configmap-using-saectl-tool)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

管理应用实例

查看应用实例列表

查看应用实例详情

查看应用实例日志

进入应用实例控制台

删除应用实例

K8s YAML配置项说明

SAE的应用实例对应于Kubernetes的Pod资源类型。本文介绍如何使用saectl工具管理SAE应用实例，并提供相关的K8s YAML配置文件示例。

## **前提条件**

已安装saectl工具，并配置AccessKey ID、AccessKey Secret、应用部署地域，详见 [安装与配置saectl工具](https://help.aliyun.com/zh/sae/install-and-configure-saectl-tool "")。

## 管理应用实例

saectl工具支持查看、删除应用实例，但不支持创建、更新应用实例。

### **查看应用实例列表**

执行以下命令，查看指定应用下的实例列表。

```bash
saectl get pod ${instance-id} -n ${namespace} -l sae.aliyun.com/app-name=${app-name}
# ${instance-id}为实例ID，如果不指定实例ID，则获取范围内所有实例。
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间。
# ${app-name}为应用名称，如果不通过-l指定应用名称，则获取范围内所有应用的实例。
```

输出结果的字段说明如下：

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| NAME | 实例ID。 |
| READY | 已准备就绪的容器数 / 总容器数，准备就绪是指已通过Readiness探针检查。 |
| STATUS | 实例的状态，Running表示实例正在运行。 |
| RESTARTS | 重启次数。 |
| AGE | 实例的存在时间。 |

### 查看应用实例详情

saectl工具支持使用`get`或`describe`命令查看应用实例详情。返回结果中包含应用实例的配置项，详情请参考 [K8s YAML配置项说明](https://help.aliyun.com/zh/sae/manage-sae-instances-using-saectl-tool#6170664743t3z "")。

#### 通过get命令查看应用实例配置信息

```bash
saectl get pod ${instance-id} -o {yaml | json} -n ${namespace}
# ${instance-id}为实例ID
# -o参数指定返回结果的格式
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间
```

#### 通过describe命令查看应用实例详情

```bash
saectl describe pod ${instance-id} -n ${namespace}
# ${instance-id}为实例ID
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间
```

### 查看应用实例日志

```bash
saectl logs ${instance-id} -n ${namespace}
# ${instance-id}为实例ID
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间
```

### 进入应用实例控制台

```bash
saectl exec -it ${instance-id} /bin/bash -n ${namespace}
# ${instance-id}为实例ID
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间
```

### 删除应用实例

```bash
saectl delete pod ${instance-id} -n ${namespace}
# ${instance-id}为实例ID
# ${namespace}为命名空间ID，如果不通过-n参数指定命名空间，则默认使用default命名空间
```

## **K8s YAML配置项说明**

SAE的应用实例对应于Kubernetes的Pod资源类型。相关K8s YAML配置项说明详见下表。

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| metadata.name | 实例ID。 |
| metadata.namespace | 实例所在的命名空间。 |
| metadata.uid | 实例ID。 |
| metadata.labels | 使用固定格式如下：<br>```yaml<br>  labels:<br>    sae.aliyun.com/app-name: ${应用名}<br>``` |
| metadata.ownerReferences | 实例所属的Deployment应用。<br>使用固定格式如下：<br>```yaml<br>  ownerReferences:<br>  - apiVersion: apps/v1<br>    kind: Deployment<br>    name: ${应用名}<br>    uid: ${应用ID}<br>``` |
| spec.containers | 实例包含的容器信息。 |
| status.podIP | 实例IP。 |