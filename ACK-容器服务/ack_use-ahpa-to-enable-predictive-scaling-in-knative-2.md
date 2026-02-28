### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 在Knative中使用AHPA弹性预测

# 在Knative中使用AHPA弹性预测

更新时间：2024-07-03 23:18:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

步骤一：安装AHPA Controller

步骤二：配置Prometheus指标采集

1、设置采集规则

2、配置Prometheus数据源

步骤三：创建Knative服务

执行结果

相关文档

Knative Serverless支持AHPA（Advanced Horizontal Pod Autoscaler）的弹性能力，当应用所需资源具备周期性变化时，可通过弹性预测，预热资源，缓解您在使用Knative时遇到的冷启动问题。本文介绍如何在Knative中使用AHPA弹性预测功能。

## 前提条件

- 已部署Knative。具体操作，请参见 [部署Knative](https://help.aliyun.com/zh/ack/enable-knative-3#task-1956927 "")。

- 已开启Prometheus监控。具体操作，请参见 [阿里云Prometheus监控](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/enable-prometheus-service#task-1962610 "")。


## 步骤一：安装AHPA Controller

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **组件管理**。

3. 在 **组件管理** 页面，单击 **其他** 页签或在页面右上方搜索 **AHPA Controller**，然后在 **AHPA Controller** 卡片单击 **安装**。

4. 在安装组件对话框，单击 **确定**。


## 步骤二：配置Prometheus指标采集

通过Prometheus采集Knative服务的RT、RPS指标数据。

### **1、设置采集规则**

1. 登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。
2. 在左侧导航栏选择**Prometheus监控** \> **实例列表**，进入可观测监控 Prometheus 版的实例列表页面。

3. 在顶部菜单栏选择目标集群所在的地域。

4. 在 **实例列表** 页面，单击目标实例名称，进入目标实例页面。

5. 在左侧导航栏选择 **服务发现**，然后单击 **配置** 页签，在 **配置** 页签下，单击 **自定义服务发现**，然后单击 **添加**。

6. 在 **添加自定义服务发现** 对话框中，设置采集规则。



采集规则配置示例如下：

















```yaml
job_name: queue-proxy
scrape_interval: 3s
scrape_timeout: 3s
kubernetes_sd_configs:
- role: pod
relabel_configs:
- source_labels:
  - __meta_kubernetes_pod_label_serving_knative_dev_revision
  - __meta_kubernetes_pod_container_port_name
action: keep
regex: .+;http-usermetric
- source_labels:
  - __meta_kubernetes_namespace
target_label: namespace
- source_labels:
  - __meta_kubernetes_pod_name
target_label: pod
- source_labels:
  - __meta_kubernetes_service_name
target_label: service
```

### **2、配置Prometheus数据源**

1. 登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。
2. 在左侧导航栏选择**Prometheus监控** \> **实例列表**，进入可观测监控 Prometheus 版的实例列表页面。

3. 在顶部菜单栏选择目标集群所在的地域。

4. 在 **实例列表** 页面，单击目标实例名称，进入目标实例详情页面。

5. 在左侧导航栏单击 **设置**，复制HTTP API地址下的公网地址。

6. 在HTTP API地址下单击 **生成token**，获取Prometheus实例的鉴权Token。

7. 使用以下内容，创建application-intelligence.yaml，在集群中设置Prometheus查询地址。

















```yaml
apiVersion: v1
kind: ConfigMap
metadata:
     name: application-intelligence
     namespace: kube-system
data:
     prometheusUrl: "https://cn-hangzhou.arms.aliyuncs.com:9443/api/v1/prometheus/da9d7dece901db4c9fc7f5b9c40****/158120454317****/cc6df477a982145d986e3f79c985a****/cn-hangzhou"
     token: "****"
```







部分参数说明如下：



   - `prometheusUrl`：用于设置阿里云Prometheus的访问地址，值为第 [4](https://help.aliyun.com/zh/ack/use-ahpa-to-enable-predictive-scaling-in-knative-2#step-gfu-jzt-qzx "") 步获取的公网地址。

   - `token`：用于设置访问鉴权Token，值为第 [5](https://help.aliyun.com/zh/ack/use-ahpa-to-enable-predictive-scaling-in-knative-2#step-emi-34z-g63 "") 步获取的鉴权Token。


8. 执行以下命令，部署ConfigMap。

















```bash
kubectl apply -f application-intelligence.yaml
```


## 步骤三：创建Knative服务

在Knative Service指定使用AHPA弹性策略。

1. 使用以下内容，创建autoscale-go.yaml。

















```yaml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
     name: autoscale-go
     namespace: default
spec:
     template:
       metadata:
         labels:
           app: autoscale-go
         annotations:
           autoscaling.knative.dev/class: ahpa.autoscaling.knative.dev
           autoscaling.knative.dev/target: "500"
           autoscaling.knative.dev/metric: "rt"
           autoscaling.knative.dev/minScale: "1"
           autoscaling.knative.dev/maxScale: "30"
           autoscaling.alibabacloud.com/scaleStrategy: "observer"
       spec:
         containers:
        - image: registry.cn-hangzhou.aliyuncs.com/knative-sample/autoscale-go:0.1

```

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| `autoscaling.knative.dev/class: ahpa.autoscaling.knative.dev` | 指定弹性插件AHPA。 |
| `autoscaling.knative.dev/metric: "rt"` | 设置AHPA指标。目前仅支持响应时间RT。 |
| `autoscaling.knative.dev/target: "500` | 设置AHPA指标的阈值，本示例RT阈值为500，单位毫秒。 |
| `autoscaling.knative.dev/minScale: "1"` | 设置弹性策略实例数的最小值为1。 |
| `autoscaling.knative.dev/maxScale: "30"` | 设置弹性策略实例数的最大值为30。 |
| `autoscaling.alibabacloud.com/scaleStrategy: "observer"` | 设置弹性伸缩模式，默认值是`observer`。<br>   - `observer`：表示只观察，但不做真正的伸缩动作。您可以通过这种方式观察AHPA的工作是否符合预期。由于预测需要历史7天的数据，因此创建服务默认是`observer`模式。<br>     <br>   - `auto`：表示由AHPA负责扩容和缩容，把AHPA指标和阈值输入到AHPA，AHPA最终决定是否生效。 |

2. 执行以下命令，开启AHPA弹性策略。

















```bash
kubectl apply -f autoscale-go.yaml
```


## 执行结果

Knative Service开启AHPA弹性后，您可以看到弹性预测生效前后的RT数据对比。![AHPA效果图.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0701803461/p390912.png)

## **相关文档**

- 阿里云Prometheus监控提供一键安装AHPA组件功能，并提供开箱即用的专属监控大盘。详细信息，请参见 [为AHPA开启Prometheus大盘](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-prometheus-service-for-ahpa "")。

- 如何将Knative和AHPA结合从而拥有基于RPS定时弹性的能力，请参见 [Knative结合AHPA实现基于RPS的定时弹性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-combined-with-ahpa-to-realize-timing-elasticity-based-on "")。