### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[服务支持](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/)[故障排除](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/troubleshooting-10/)Service异常问题排查

# Service异常问题排查

更新时间：2026-01-12 22:47:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用OpenAPI诊断工具进行故障排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/use-the-openapi-diagnostics-tool-to-diagnose-issues)[下一篇：Nginx Ingress异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/troubleshooting-nginx-ingress-exceptions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

诊断流程

Service异常事件及处理方式

排查思路

CLB负载不均

应用更新过程中访问CLB出现503报错

集群内无法访问CLB

集群外无法访问CLB

无法连接到后端HTTPS服务

相关文档

本文介绍LoadBalancer类型Service的异常问题诊断流程和排查思路。

## 背景信息

当Service的类型设置为`Type=LoadBalancer`时，容器服务ACK的CCM（Cloud Controller Manager）组件会自动为该Service创建或配置阿里云传统型负载均衡CLB（Classic Load Balancer），包括CLB、监听、后端服务器组等资源。关于CLB的自动更新策略，请参见 [Service的负载均衡配置注意事项](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/considerations-for-configuring-a-loadbalancer-type-service-1#section-sm9-gly-kmn "")。

## 诊断流程

执行排查前，请确保CCM组件版本不低于V1.9.3.276-g372aa98-aliyun。关于如何升级CCM，请参见 [升级CCM组件](https://help.aliyun.com/zh/ack/product-overview/update-the-ccm#section-lkb-uza-33p "")。关于CCM的发布记录，请参见 [Cloud Controller Manager](https://help.aliyun.com/zh/ack/product-overview/cloud-controller-manager#concept-wk1-grd-qfb "")。

1. 执行以下命令，确定CLB关联的Service。

















```bash
kubectl get svc -A |grep -i LoadBalancer|grep {XXX.XXX.XXX.XXX}  # XXX.XXX.XXX.XXX是loadbalancer IP。
```

2. 执行以下命令，检查对应Service是否存在报错事件。

















```bash
kubectl -n {your-namespace} describe svc {your-svc-name}
```





   - 有异常事件：请参见 [Service异常事件及处理方式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#section-lzw-o22-ajy "")。

   - 无异常事件：请参见 [排查思路](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#section-pbd-avq-kbo "")。

## Service异常事件及处理方式

不同报错信息的解决方法如下表所示。

| **报错信息** | **说明及解决方法** |
| --- | --- |

|     |     |
| --- | --- |
| **报错信息** | **说明及解决方法** |
| `The backend server number has reached to the quota limit of this load balancers` | 指CLB的后端服务器配额不足。<br>解决方案：您可以采取以下方式，优化配额消耗。<br>- 默认情况下一个CLB实例可以挂载200个后端服务器，请申请提升配额。关于如何查询和提升配额，请登录 [负载均衡SLB配额管理](https://slbnew.console.aliyun.com/slb/quota)。<br>  <br>- 建议您设置CLB外部流量策略为Local模式（设置`externalTrafficPolicy: Local`），因为Cluster模式会快速消耗配额。如果需要使用Cluster模式，建议通过标签`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-backend-label`来指定使用的虚拟服务器，从而减少配额消耗。关于如何在注解中添加标签关联后端的虚拟服务器的操作，请参见 [通过Annotation配置传统型负载均衡CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#task-1425948 "")。<br>  <br>- 由于多个Service复用一个CLB时，后端服务器数是累加的。建议您创建Service时，新建CLB。 |
| `The loadbalancer does not support backend servers of eni type` | 共享型CLB不支持ENI。<br>解决方案：如果CLB后端使用的是ENI，您需要选择性能保障型CLB实例。在Service中添加注解`annotation: service.beta.kubernetes.io/alibaba-cloud-loadbalancer-spec: "slb.s1.small"`。<br>**重要**<br>添加注解需要注意是否符合CCM的版本要求。关于注解和CCM的版本对应关系，请参见 [通过Annotation配置传统型负载均衡CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#section-3pu-lhe-9wm "")。 |
| `There are no available nodes for LoadBalancer` | CLB无后端服务器，请确认Service是否已关联Pod且Pod正常运行。<br>解决方案：<br>- 若未关联Pod，请将Service关联至应用Pod。<br>  <br>- 若关联的Pod运行异常，请定位解决Pod异常，具体操作请参见 [Pod异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/pod-troubleshooting#task-2187029 "")。<br>  <br>- 如果CLB无后端服务器但Pod正常运行，请检查Pod所在节点是否为Master节点。如果是，请将业务Pod驱逐到Worker节点。 |
| - `alicloud: not able to find loadbalancer named [%s] in openapi, but it's defined in service.loaderbalancer.ingress. this may happen when you removed loadbalancerid annotation`<br>  <br>- `alicloud: can not find loadbalancer, but it's defined in service` | 无法根据Service关联CLB。<br>解决方案：登录[负载均衡管理控制台](https://slb.console.aliyun.com/slb)，根据Service的`EXTERNAL-IP`，在其所在的地域搜索CLB。<br>1. 如果搜索不到CLB，且该Service无需再使用，则删除对应的Service即可。<br>   <br>2. 如果CLB存在，执行以下步骤。<br>   <br>1. 如果CLB是手动在CLB控制台创建，在Service中添加注解`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`。详情请参见 [通过Annotation配置传统型负载均衡CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#task-1425948 "")。<br>      <br>2. 如果CLB是由CCM自动创建，确认该CLB是否有标签 **kubernetes.do.not.delete**。如果没有，请添加标签。具体操作，请参见 [旧版本CCM如何支持SLB重命名？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-61e-9ty-sgk "")。 |
| `ORDER.ARREARAGE Message: The account is arrearage.` | 账号欠费。 |
| `PAY.INSUFFICIENT_BALANCE Message: Your account does not have enough balance.` | 账号余额少于100元，请充值。 |
| `Status Code: 400 Code: Throttlingxxx` | CLB OpenAPI限流。<br>解决方案：<br>1. 请登录 [负载均衡SLB配额管理](https://slbnew.console.aliyun.com/slb/quota)，查看并确保CLB配额充足。<br>   <br>2. 执行以下命令，查看集群Service是否存在异常。如果存在，请参照此表处理异常事件。<br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>```bash<br>kubectl -n {your-namespace} describe svc {your-svc-name}<br>``` |
| `Status Code: 400 Code: RspoolVipExist Message: there are vips associating with this vServer group.` | 无法删除虚拟服务器组关联的监听。<br>解决方案：<br>1. 确认Service中的注解是否带有CLB实例的ID（例如`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id: {your-clb-id}`）。<br>   <br>如果注解带有CLB实例ID，说明是复用的CLB。<br>   <br>2. 在CLB控制台中删除Service中port对应的监听。关于如何删除CLB监听，请参见 [配置监听转发规则](https://help.aliyun.com/zh/slb/application-load-balancer/user-guide/manage-forwarding-rules-for-a-listener#task-2021459 "")。 |
| `Status Code: 400 Code: NetworkConflict` | 复用内网CLB时，该CLB和集群不在同一个VPC内。<br>解决方案：请确保您的CLB和集群在同一个VPC内。 |
| `Status Code: 400 Code: VSwitchAvailableIpNotExist Message: The specified VSwitch has no available ip.` | 虚拟交换机不足。<br>解决方案：通过`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-vswitch-id: "${YOUR_VSWITCH_ID}"`指定同VPC下另一个虚拟交换机。 |
| `Message：The specified VSwitch does not exist.` | 虚拟交换机不存在。<br>解决方案：<br>- 如果Service中配置了注解`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-vswitch-id`请确认对应的vSwitch是否存在。<br>  <br>- 如果Service中未配置`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-vswitch-id`，请确认集群默认的vSwitch ID是否存在。您可以在集群默认节点池（default-nodepool）的 **基本信息** 页签查看 **节点虚拟交换机**。具体操作请参见 [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#task-2457443 "")。<br>  <br>如果不存在，请通过上述注解指定其他vSwitch。 |
| `The specified Port must be between 1 and 65535.` | ENI模式不支持String类型的`targetPort`。<br>解决方案：将Service YAML中的`targetPort`字段改为INT类型或者升级CCM。关于如何升级CCM，请参见 [升级CCM组件](https://help.aliyun.com/zh/ack/product-overview/update-the-ccm#section-lkb-uza-33p "")。 |
| `Status Code: 400 Code: ShareSlbHaltSales Message: The share instance has been discontinued.` | 低版本CCM默认创建共享型CLB，但该类型CLB已停止售卖。<br>解决方案： [升级CCM组件](https://help.aliyun.com/zh/ack/product-overview/update-the-ccm#section-lkb-uza-33p "")。 |
| `can not change ResourceGroupId once created` | CLB资源组一旦创建后不支持修改。<br>解决方案：移除Service中的注解`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-resource-group-id:"rg-xxxx"`。 |
| `can not find eniid for ip x.x.x.x in vpc vpc-xxxx` | 无法在VPC内找到指定的ENI IP。<br>解决方案：确认Service中是否配置了注解`service.beta.kubernetes.io/backend-type：eni`。如果已配置，请确认集群网络插件是否为Flannel。Flannel网络模式不支持ENI模式，移除Service中对应的注解即可。 |
| - `The operation is not allowed because the instanceChargeType of loadbalancer is PayByCLCU.`<br>  <br>- `User does not have permission modify InstanceChargeType to spec.` | CLB计费类型不支持从按量付费转为按规格计费。<br>解决方案：<br>- 移除service中的Annotation：`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-spec`。<br>  <br>- 如果service中有`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-instance-charge-type`，取值需设置为`PayByCLCU`。 |
| `SyncLoadBalancerFailed the loadbalancer xxx can not be reused，can not reuse loadbalancer created by kubernetes.` | 复用了CCM创建的CLB。<br>解决方案：<br>1. 查看Service YAML中的annotation`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`对应的CLB ID。<br>   <br>2. 根据Service状态处理报错。<br>   <br>   - 如果Service为Pending状态，您需要替换annotation`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`中的CLB ID，更改为手动在 [传统型负载均衡CLB控制台](https://slb.console.aliyun.com/slb) 创建的CLB。<br>     <br>   - 如果Service不是pending状态，根据以下实际情况处理。<br>     <br>     - 如果CLB对应的IP与Service的external IP一致，删除annotation`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`即可。<br>       <br>     - 如果CLB对应的IP与Service的external IP不一致，您需要登录 [传统型负载均衡CLB控制台](https://slb.console.aliyun.com/slb)，找到集群对应Region，根据Service的external IP查找对应的CLB，更改annotation`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`中的CLB ID。如果没有找到对应的CLB，更改annotation`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`中的CLB ID为手动在CLB控制台创建的CLB，然后重建Service。 |
| `alicloud: can not change LoadBalancer AddressType once created. delete and retry` | CLB的类型一旦创建后不可更改，创建Service后更改了CLB的类型会导致该报错。<br>解决方案：删除重建Service。 |
| `the loadbalancer lb-xxxxx can not be reused, service has been associated with ip [xxx.xxx.xxx.xxx], cannot be bound to ip [xxx.xxx.xxx.xxx]` | Service已经绑定一个CLB，不能再绑定另一个CLB。<br>解决方案：不支持通过更改`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id`的CLB ID的方式复用已有CLB。如果需要更改绑定的CLB，需要删除重建Service。 |

## 排查思路

对于非Service报错类的异常问题，请参考下表进行排查。

| **问题类别** | **问题现象** | **解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **问题类别** | **问题现象** | **解决方案** |
| CLB访问类 | CLB负载不均 | [CLB负载不均](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#1 "") |
| 应用更新过程中访问CLB出现503报错 | [应用更新过程中访问CLB出现503报错](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#2 "") |
| 集群内无法访问CLB | [集群内无法访问CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#3 "") |
| 集群外无法访问CLB | [集群外无法访问CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#4437a37022v5v "") |
| 访问HTTPS端口报错`The plain HTTP request was sent to HTTPS port` | [无法连接到后端HTTPS服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#4 "") |
| CLB配置类 | Serivce注解未生效 | [Service注解不生效如何处理？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-slc-3sk-7vf "") |
| CLB配置被修改 | [为何CLB的配置被修改？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-g0s-3ac-8p8 "") |
| 复用已有CLB未生效 | [Service FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#test "") |
| 复用已有CLB未配置监听 | [为什么复用已有CLB时没有配置监听？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-a33-ozj-j1k "") |
| CLB后端不一致 | [SLB虚拟服务器组未更新如何处理？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-nmr-gvy-po3 "") |
| CLB删除类 | CLB被删除 | [什么情况下会自动删除SLB？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-nff-cbv-3de "") |
| Service删除后CLB未删除 | [什么情况下会自动删除SLB？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#section-nff-cbv-3de "") |

### CLB负载不均

**问题原因**

CLB的调度算法设置不合理。

**问题现象**

CLB后端服务器负载不均。

**解决方案**

Local模式Service（即`externalTrafficPolicy: Local`）需要将CLB调度算法设置为加权轮询算法，即为Service添加注解`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-scheduler:"wrr"`。

> 关于如何抓取容器内部的网络报文来判断负载是否不均衡的更多步骤，请参考 [阿里云开发者社区](https://developer.aliyun.com/article/775829)。

### 应用更新过程中访问CLB出现503报错

**问题原因**

没有对CLB监听设置连接优雅中断，或没有对Pod设置优雅终止。

**问题现象**

应用更新过程中访问CLB出现503报错。

**解决方案**

1. 通过`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-connection-drain`等注解为CLB监听设置连接优雅中断。关于注解的详细说明，请参见 [监听的典型操作](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#section-ynz-cbo-l0h "")。

2. 根据容器网络模式，设置Pod的`preStop`和`readinessProbe`。


   - `readinessProbe`为就绪检查。只有就绪检查通过后，Pod才会被加入到Endpoint中。容器服务ACK监控到Endpoint变化后才会将Node挂载到CLB后端。需要合理设置就绪检测（`readinessProbe`）的探测频率、延时时间、不健康阈值等数据，部分应用启动时间本身较长，如果设置的时间过短，会导致Pod反复重启。

   - `preStop`时间建议设置为业务处理完所有剩余请求所需的时间，`terminationGracePeriodSeconds` 时间建议设置为`preStop`的时间再加30秒以上。


Pod配置示例：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  containers:
    - name: nginx
      image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6
      ports:
        - containerPort: 8080
          protocol: TCP
      # 存活检测
      livenessProbe:
        failureThreshold: 3
        initialDelaySeconds: 30
        periodSeconds: 30
        successThreshold: 1
        tcpSocket:
          port: 8080
        timeoutSeconds: 1
      # 就绪检测
      readinessProbe:
        failureThreshold: 3
        initialDelaySeconds: 30
        periodSeconds: 30
        successThreshold: 1
        tcpSocket:
          port: 8080
        timeoutSeconds: 1
      # 优雅退出
      lifecycle:
        preStop:
          exec:
            command:
              - sleep
              - "30"
  terminationGracePeriodSeconds: 60
```

### 集群内无法访问CLB

**问题原因**

CLB设置了`externalTrafficPolicy: Local`类型，这种类型的CLB地址只有在Node中部署了对应的后端Pod，才能被访问。因为CLB的地址是集群外使用，如果集群节点和Pod不能直接访问，请求不会到达CLB，会被当作Service的扩展IP地址，被kube-proxy的iptables或ipvs转发。

如果刚好集群节点或者Pod所在的节点上没有相应的后端服务Pod，就会发生网络不通的问题，而如果有相应的后端服务Pod，是可以正常访问。相关问题的更多信息请参见 [kube-proxy将external-lb的地址添加到节点本地iptables规则](https://github.com/kubernetes/kubernetes/issues/66607?spm=a2c4g.171437.0.0.62e175f4OloUv5)。

**问题现象**

集群内无法访问CLB。

**解决方案**

- 在Kubernetes集群内通过ClusterIP或者服务名访问。

其中Ingress的服务名为：`nginx-ingress-lb.kube-system`

- 将LoadBalancer的Service中的externalTrafficPolicy修改为Cluster，但是在应用中会丢失原IP，Ingress的服务修改命令如下。



**说明**





若是Ingress的CLB，只有Ingress的Pod所在节点上，Pod才能访问通过Ingress或CLB暴露出去的服务。



















```bash
kubectl edit svc nginx-ingress-lb -n kube-system
```

- 若是Terway的ENI或者ENI多IP的集群，将LoadBalancer的Service中的externalTrafficPolicy修改为Cluster，并且添加ENI直通的annotation，例如`annotation： service.beta.kubernetes.io/backend-type："eni"`，具体格式如下，可以保留源IP，并且在集群内访问也没有问题。详细信息，请参见 [通过Annotation配置传统型负载均衡CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances "")。















```yaml
apiVersion: v1
kind: Service
metadata:
    annotations:
      service.beta.kubernetes.io/backend-type: eni
    labels:
      app: nginx-ingress-lb
    name: nginx-ingress-lb
    namespace: kube-system
spec:
    externalTrafficPolicy: Cluster
```


### 集群外无法访问CLB

**问题原因**

CLB设置了ACL或CLB未正常运行。

**问题现象**

集群外无法访问CLB。

**解决方案**

1. 执行以下命令，查看Service事件信息，并处理异常事件。具体操作，请参见 [Service异常事件及处理方式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/service-troubleshooting#section-lzw-o22-ajy "")。















```bash
kubectl -n {your-namespace} describe svc {your-svc-name}
```

2. 确认CLB是否配置了ACL。

如果配置了ACL，请确认ACL是否允许客户端IP访问。关于CLB的ACL配置，请参见 [访问控制](https://help.aliyun.com/zh/slb/classic-load-balancer/user-guide/overview-3#concept-2167216 "")。

3. 确认CLB虚拟服务器组是否为空。

如果虚拟服务器组为空，请检查业务Pod是否关联了Service以及业务Pod是否正常运行。如果关联的Pod运行异常，请定位解决Pod异常。具体操作，请参见 [Pod异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/support/pod-troubleshooting#task-2187029 "")。

4. 确认CLB监听的健康检查是否正常。

如果CLB健康检查异常，请检查业务Pod是否正常运行。关于CLB的健康检查的相关问题，请参见 [CLB健康检查FAQ](https://help.aliyun.com/zh/slb/classic-load-balancer/user-guide/faq-about-health-checks "")。


### 无法连接到后端HTTPS服务

**问题原因**

CLB上配置证书后将会在CLB侧进行解密，导致实际发送到后端Pod的请求为HTTP请求。

**问题现象**

无法连接到后端HTTPS服务。

**解决方案**

将Service中HTTPS端口对应的Target Port配置为HTTP端口。以Nginx为例，HTTPS端口为443，其对应的`targetPort`需要改为`80`。

配置示例：

```yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/alibaba-cloud-loadbalancer-protocol-port: "https:443"
    service.beta.kubernetes.io/alibaba-cloud-loadbalancer-cert-id: "${YOUR_CERT_ID}"
  name: nginx
  namespace: default
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 80
  - name: https
    port: 443
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  type: LoadBalancer
```

## 相关文档

- [Service FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-faq#task-2039653 "")

- [通过Annotation配置传统型负载均衡CLB](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#task-1425948 "")

- [Service的负载均衡配置注意事项](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/considerations-for-configuring-a-loadbalancer-type-service-1#task-1941987 "")