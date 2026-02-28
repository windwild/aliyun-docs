### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)[Ingress管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ingress-management-2/)[ALB Ingress管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alb-ingress-management-1/)创建并使用ALB Ingress对外暴露服务

# 创建并使用ALB Ingress对外暴露服务

更新时间：2026-01-09 03:12:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ALB Ingress管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alb-ingress-management-1/)[下一篇：通过AlbConfig配置ALB实例](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-albconfigs-to-configure-alb-instances)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

Service类型限制

安装ALB Ingress Controller组件

创建示例应用

创建ALB Ingress

计费说明

应用于生产环境

配额与限制

常见问题

相关文档

ACK集群中的服务默认与外部网络隔离。ALB Ingress通过使用具备域名路由、安全防护和高可用能力的应用型负载均衡 ALB作为外部流量入口，以满足将集群内部服务暴露给用户访问的需求。

## **工作原理**

|     |     |
| --- | --- |
| 1. **资源关联**<br>   <br>   AlbConfig资源对象定义了ALB实例的具体配置（如功能版本、监听等），与ALB实例为一对一的关联关系。Ingress中定义的路径映射和关联的Service，将自动转化为ALB实例的路由规则和服务器组配置。<br>   <br>2. **动态同步**<br>   <br>   ALB Ingress Controller通过API Server动态地获取Ingress和AlbConfig资源的变化，然后动态更新ALB实例。<br>   <br>3. **流量转发**<br>   <br>   与Nginx Ingress Controller不同，ALB Ingress Controller是托管组件，作为ALB实例的控制面，不直接处理用户请求流量，用户流量的转发由ALB实例来处理，并最终转发到Service所代理的后端Pod上。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3736497671/CAEQYxiBgICTiJLIzhkiIGI5NTgwZDBkN2ZkZTQ0MGFhNzUyMzhmNDM5Y2ExMDMy4054380_20231026180318.932.svg) |

## **Service类型限制**

当使用flannel网络插件时，ALB Ingress后端Service仅支持`NodePort`和`LoadBalancer`类型。

## **安装ALB Ingress Controller组件**

创建集群时安装

为已有集群安装

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，单击 **创建集群**。

2. 在 **组件配置** 阶段的 **Ingress** 配置区域，选择安装 **ALB Ingress**。

3. 以新建ALB实例为例，然后按照页面提示创建集群。


|     |     |
| --- | --- |
| **ALB 应用型负载均衡实例** | **说明** |
| **新建** | 自动创建ALB实例、AlbConfig和IngressClass。<br>   - ALB实例：在集群VPC内自动创建一个标准版、按量付费的公网/私网ALB实例，并配置`HTTP:80`监听。<br>     <br>   - AlbConfig和IngressClass：在集群中自动创建与ALB实例关联的AlbConfig和IngressClass资源对象。 |


| **使用已有**<br>> 仅当集群网络配置为使用已有专有网络时可选 | 使用一个已有的ALB实例，并自动创建AlbConfig和IngressClass。该ALB实例的功能版本需为标准版或WAF增强版，网络类型需为与集群同VPC的公网/私网类型，且未被其他集群关联。 |
| **暂不创建** | 仅安装ALB Ingress Controller组件，后续需 [手动创建AlbConfig和IngressClass](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-and-use-alb-ingress-to-expose-services-to-the-public#564a6487e3n7s "")，适用于需要自定义ALB实例配置的场景。 |


1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 通过搜索栏或者 **网络** 页签找到组件，在 **ALB Ingress Controller** 组件卡片的右下角，单击 **安装**。

4. 以新建ALB实例为例，然后单击 **确认**。


|     |     |
| --- | --- |
| **ALB 应用型负载均衡实例** | **说明** |
| **新建** | 自动创建ALB实例、AlbConfig和IngressClass。<br>   - ALB实例：在集群VPC内自动创建一个标准版、按量付费的公网/私网ALB实例，并配置`HTTP:80`监听。<br>     <br>   - AlbConfig和IngressClass：在集群中自动创建与ALB实例关联的AlbConfig和IngressClass资源对象。 |


| **使用已有** | 使用一个已有的ALB实例，并自动创建AlbConfig和IngressClass。该ALB实例的功能版本需为标准版或WAF增强版，网络类型需为与集群同VPC的公网/私网类型，且未被其他集群关联。 |
| **暂不创建** | 仅安装ALB Ingress Controller组件，后续需 [手动创建AlbConfig和IngressClass](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-and-use-alb-ingress-to-expose-services-to-the-public#564a6487e3n7s "")，适用于需要自定义ALB实例配置的场景。 |


## **创建示例应用**

示例应用将部署一个名称为`coffee`的无状态工作负载（Deployment）以及对应的`coffee-svc`服务（Service）。

控制台

kubectl

1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **无状态**。

2. 单击 **使用YAML创建资源**， **示例模板** 选择 **自定义**。然后将以下内容复制到模板区域，单击 **创建**。



**示例应用YAML**




















```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
     name: coffee
     namespace: default
spec:
     replicas: 2
     selector:
       matchLabels:
         app: coffee
     template:
       metadata:
         labels:
           app: coffee
       spec:
         containers:
      - name: coffee
        image: registry.cn-hangzhou.aliyuncs.com/acs-sample/nginxdemos:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
name: coffee-svc
namespace: default
spec:
ports:
  - port: 80
    targetPort: 80
    protocol: TCP
selector:
    app: coffee
type: ClusterIP  # 当使用flannel网络插件时，ALB Ingress后端Service仅支持NodePort和LoadBalancer类型
```

3. 在弹窗提示中单击 **查看**，确认Pod状态为`Running`。


1. [获取集群KubeConfig并通过kubectl工具连接集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/obtain-the-kubeconfig-file-of-a-cluster-and-use-kubectl-to-connect-to-the-cluster "")。

2. 使用以下内容创建`coffee-deployment-service.yaml`文件。



**示例应用YAML**




















```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
     name: coffee
     namespace: default
spec:
     replicas: 2
     selector:
       matchLabels:
         app: coffee
     template:
       metadata:
         labels:
           app: coffee
       spec:
         containers:
      - name: coffee
        image: registry.cn-hangzhou.aliyuncs.com/acs-sample/nginxdemos:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
name: coffee-svc
namespace: default
spec:
ports:
  - port: 80
    targetPort: 80
    protocol: TCP
selector:
    app: coffee
type: ClusterIP  # 当使用flannel网络插件时，ALB Ingress后端Service仅支持NodePort和LoadBalancer类型
```

3. 创建示例应用的Deployment和Service。

















```shell
kubectl apply -f coffee-deployment-service.yaml
```

4. 确认Pod状态为`Running`。















```shell
    kubectl get pod -l app=coffee
```



预期输出：















```plaintext
NAME                      READY   STATUS    RESTARTS   AGE
coffee-84bd6*****-*****   1/1     Running   0          4m22s
coffee-84bd6*****-*****   1/1     Running   0          4m22s
```


## **创建ALB Ingress**

通过配置ALB Ingress的域名和路径映射，实现访问`ingress-demo.com/coffee`域名即可路由至集群内部`coffee-svc`服务的功能。

> 在ACK专有集群中使用ALB Ingress，需要 [授予ALB Ingress Controller访问权限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/grant-permissions-to-the-alb-ingress-controller#task-2118820 "")。

控制台

kubectl

1. 在左侧导航栏，选择**网络** \> **路由**。选择`default`命名空间，单击 **创建 Ingress**。

2. 添加以下Ingress配置，单击 **确定**。

   - **名称**：`coffee-ingress`

   - **域名**：`ingress-demo.com`

   - **路径映射**： **路径**：`/coffee`， **匹配规则**：`前缀匹配（Prefix）`， **服务名称**：`coffee-svc`， **端口**：`80`。


     |     |     |
     | --- | --- |
     | **匹配规则（pathType）** | **说明** |
     | 前缀匹配（Prefix） | 匹配请求URL路径的前缀部分。例如，可匹配`/coffee/1`或`/coffee/buy/1`路径，但不能匹配`/cof`或`/coffeebuy/1`。 |
     | 完整匹配（Exact） | 完全匹配请求URL路径。仅`/coffee`路径可匹配。 |
     | 默认（ImplementationSpecific） | 由Ingress Controller实现的具体逻辑决定。在ALB Ingress Controller中为完整匹配（Exact）。 |
3. 获取 **端点** 地址。


> ALB Ingress生效过程耗时约10秒，可稍后单击刷新按钮获取端点信息。若长时间未更新端点信息，可单击路由名称，进入 **事件** 页签，进行 [异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/troubleshooting-alb-ingress-exceptions "")。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5285101671/p1012808.png)

4. 测试访问域名和端点地址，若HTTP状态码为`200`即表示ALB Ingress已创建成功。















```bash
curl -H "Host:ingress-demo.com" http://<端点地址>/coffee -s -o /dev/null -w "%{http_code}\n"
```


1. 创建ALB Ingress。将以下YAML内容保存为`coffee-ingress.yaml`文件，然后执行`kubectl apply -f coffee-ingress.yaml`命令。















```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
     name: coffee-ingress
     namespace: default
spec:
     ingressClassName: alb
     rules:
  - host: ingress-demo.com
    http:
      paths:
      - path: /coffee
        backend:
          service:
            name: coffee-svc
            port:
              number: 80
        pathType: Prefix
```

|     |     |
| --- | --- |
| **匹配规则（pathType）** | **说明** |
| 前缀匹配（Prefix） | 匹配请求URL路径的前缀部分。例如，可匹配`/coffee/1`或`/coffee/buy/1`路径，但不能匹配`/cof`或`/coffeebuy/1`。 |
| 完整匹配（Exact） | 完全匹配请求URL路径。仅`/coffee`路径可匹配。 |
| 默认（ImplementationSpecific） | 由Ingress Controller实现的具体逻辑决定。在ALB Ingress Controller中为完整匹配（Exact）。 |

2. 查看Ingress并获取`ADDRESS`字段中的端点地址。















   ```shell
   kubectl get ingress coffee-ingress -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'
   ```



   预期输出：















   ```plaintext
   alb-******************.cn-wulanchabu.alb.aliyuncsslb.com
   ```

3. 测试访问域名和端点地址，若HTTP状态码为`200`即表示ALB Ingress已创建成功。















   ```bash
   curl -H "Host:ingress-demo.com" http://<端点地址>/coffee -s -o /dev/null -w "%{http_code}\n"
   ```


## **计费说明**

- ALB Ingress Controller组件：该组件为ACK托管组件，不涉及用户侧的资源使用和计费。

- ALB实例：每个AlbConfig资源对象会创建一个对应的ALB实例，ALB实例的计费规则为 [按量付费](https://help.aliyun.com/zh/slb/application-load-balancer/product-overview/alb-billing-rules "")。


## **应用于生产环境**

- [配置域名解析](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-and-use-alb-ingress-to-expose-services-to-the-public#c68ba52ef3dhi "")：将业务域名通过CNAME记录解析至ALB实例提供的公网访问地址，以解耦域名与ALB实例访问地址，确保服务入口的高可用与灵活配置。

- [配置HTTPS安全加密](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-and-use-alb-ingress-to-expose-services-to-the-public#122ca3373dhkc "")：在数字证书管理服务中统一管理证书，并在Ingress资源的`tls`字段中声明式地引用该证书，从而实现服务流量的HTTPS安全加密。


## **配额与限制**

- AlbConfig、Ingress、Service和Namespace的资源名称不能以`aliyun`开头。

- ALB Ingress的配额限制，请参见 [ALB配额计算方式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alb-quota-calculation-method "")。

- ALB Ingress支持的地域与可用区，请参见 [ALB支持的地域与可用区](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/regions-and-zones-supported-by-alb "")。


## **常见问题**

#### **为什么访问** Ingress域名 **返回了** 503、502、404等 **HTTP错误码**？

**问题原因**

- 503（Service Temporarily Unavailable）错误

  - 路由规则未匹配：请求路径与Ingress实际配置的路由规则不符。

  - 后端无存活Pod：Service关联的Pod全部未就绪或不存在，导致Endpoints对象为空。
- 502（Bad Gateway）错误

  HTTP或HTTPS监听接收到客户端连接请求后，ALB由于无法正常将请求转发至Pod或无法从Pod收到响应，则会向客户端发送HTTP 502 Bad Gateway状态码。

- 404（Not Found）错误

  通常原因为已匹配Ingress中定义的路由规则，但与Pod中应用实际提供服务的URL不匹配。

- 400（Bad Request）错误

  如HTTP请求发送至HTTPS监听等原因。


> 更多HTTP错误码说明，请参见 [ALB异常状态码](https://help.aliyun.com/zh/slb/application-load-balancer/support/alb-exception-status-code-description "")。

**解决方案**

1. 检查Ingress状态：执行`kubectl describe ingress <ingress-name> -n <namespace>`命令，查看Events部分是否有错误信息。如出现类似`listener is not exist in alb`的事件，请在AlbConfig中 [创建Ingress资源所需的监听](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-the-alb-listener-through-the-albconfig#8f22f7807fem3 "")。















   ```plaintext
   ...
   Events:
     Type     Reason                  Age     From     Message
     ----     ------                  ----    ----     -------
     Warning  FailedBuildModel        ****    ingress  listener is not exist in alb, port: 443, protocol: HTTPS
     Warning  FailedBuildModel        ****    ingress  listener not found for (443/HTTPS), with ingresses 1
   ...
   ```

2. 检查后端Endpoints：执行`kubectl get endpoints <service-name> -n <namespace>`命令，确认`ENDPOINTS`字段下有至少一个健康的Pod IP和端口。若为空，则排查Service的`selector`是否与Pod的`labels`匹配，以及Pod是否处于`Running`状态。

3. 检查Pod状态与日志：先执行`kubectl get pod -l <app=your-app> -n <namespace>`命令，查看Pod运行状态。获取Pod名称之后执行`kubectl logs <pod-name> -n <namespace>`命令，查看应用日志是否有启动失败或处理请求的错误信息。

4. 网络连通性测试：在Pod内或节点上尝试`curl`后端Service的ClusterIP或Pod IP，验证集群内部服务是否可达。


#### 配置Ingress TLS后，为什么HTTPS还是无法访问？

**问题原因**

- ALB实例未监听443端口：只配置了Ingress的TLS安全加密，但没有创建对应的`HTTPS:443`监听。

- 证书配置错误：Secret类型不是`kubernetes.io/tls`或`IngressTLS`，或者`data`中的`tls.crt`和`tls.key`内容不正确或不匹配。

- 证书更新不生效：在阿里云证书中心更新了证书，但未更新AlbConfig中指定的证书ID，或未触发自动发现证书调谐，导致ALB实例仍引用旧证书。


**解决方案**

1. 检查监听端口：执行`kubectl describe albconfig <alb-name> -n <namespace>`命令，检查是否缺少`spec.listeners.port: 443`和`spec.listeners.protocol: HTTPS`配置。

2. 检查Ingress配置：检查Ingress的配置中是否缺少注解`alb.ingress.kubernetes.io/listen-ports: [{"HTTP": 80}, {"HTTPS": 443}]`，该注解将Ingress关联到HTTP和HTTPS监听上。

3. 检查Secret配置：检查Ingress的配置中`spec.tls`的`secretName`字段，确认引用了正确的Secret。执行`kubectl get secret <secret-name> -n <namespace> -o yaml`命令，确认Secret类型和数据完整性。


#### **如何为Ingress配置域名解析？**

1. [注册域名](https://help.aliyun.com/zh/dws/user-guide/how-to-register-a-domain-name "")，并完成 [ICP备案](https://help.aliyun.com/zh/icp-filing/basic-icp-service/user-guide/icp-filing-application-overview "")。

2. [添加CNAME解析记录](https://help.aliyun.com/zh/slb/application-load-balancer/user-guide/configure-cname-resolution-for-alb#step-vw2-a60-5a0 "")。


   > 以添加一个记录类型为`CNAME`、主机记录为`@`（表示直接解析主域名，如`ingress-demo.com`）、记录值为Ingress端点地址的解析记录为例 **。**

3. 在浏览器中访问http://ingress-demo.com/coffee，验证域名解析生效。

   ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4161725571/p996375.png)


   > 请替换为实际注册域名进行验证。如发现解析不生效，请参考 [解析不生效问题快速排查](https://help.aliyun.com/zh/dns/pubz-quick-troubleshooting-of-problems-not-effective "")。


#### **如何为Ingress配置HTTPS安全加密？**

1. [购买正式证书](https://help.aliyun.com/zh/ssl-certificate/purchase-an-ssl-certificate "") 或 [个人测试证书](https://help.aliyun.com/zh/ssl-certificate/purchase-an-individual-test-certificate "")，并完成 [申请证书](https://help.aliyun.com/zh/ssl-certificate/apply-for-a-certificate "")，确认待使用的证书处于 **已签发** 状态。

2. [下载SSL证书](https://help.aliyun.com/zh/ssl-certificate/download-an-ssl-certificate "")。


   > 以下载`ingress-demo.com`域名、服务器类型为 **其他** 的PEM格式证书文件为例。

3. 创建Secret存储证书文件。

   1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**配置管理** \> **保密字典**。

   2. 在 **保密字典** 页面，选择`default`命名空间，单击左侧 **创建**。添加以下配置，单击 **确定**。


      - **名称**：`ingress-tls`

      - **类型**： **TLS证书**

      - **证书**：已下载并解压的证书文件（.pem）中的完整内容

      - **密钥**：已下载并解压的证书私钥文件（.key）中的完整内容


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5285101671/p1012619.png)
4. 更新AlbConfig，为ALB实例新增`HTTPS:443`监听。

   1. 在左侧导航栏，选择**工作负载** \> **自定义资源**。在 **资源对象浏览器** 页签中，搜索AlbConfig，然后单击搜索结果。

   2. 在AlbConfig资源对象列表中，找到目标资源`alb`，单击其右侧 **操作** 列下的 **YAML编辑**。

   3. 新增`spec.listeners.port: 443`和`spec.listeners.protocol: HTTPS`字段，然后单击 **确定**。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5285101671/p1012836.png)
5. 更新Ingress，添加TLS配置并关联`HTTPS:443`监听。

   1. 在左侧导航栏，选择**网络** \> **路由**。在目标路由右侧 **操作** 栏中，单击 **更新**。

   2. 添加以下配置，单击 **确定**。

      - **TLS配置**：开启

      - **域名**：`ingress-demo.com`

      - **保密字典**：`ingress-tls`

      - **注解**：`alb.ingress.kubernetes.io/listen-ports: [{"HTTP": 80}, {"HTTPS": 443}]`
6. 在浏览器中访问`https://ingress-demo.com/coffee`，验证HTTPS加密访问。

   ![image](<Base64-Image-Removed>)


   > 请替换为实际注册域名进行验证。


更多HTTPS证书的配置方式，请参见 [配置HTTPS证书以实现加密通信](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-an-alb-ingress-to-configure-certificates-for-an-https-listener "")。

#### **如何手动创建AlbConfig和IngressClass？**

**创建AlbConfig**

1. 登录[专有网络管理控制台](https://vpcnext.console.aliyun.com/vpc)，记录集群所在VPC中至少两个处于不同可用区的虚拟交换机ID。


   > 配置的虚拟交换机所属可用区需满足 [ALB支持的地域与可用区](https://help.aliyun.com/zh/slb/application-load-balancer/product-overview/supported-regions-and-zones "")。

2. 将下方代码中`zoneMappings.vSwitchId`替换为上一步中得到的交换机ID。创建并保存名为albconfig.yaml的文件，执行`kubectl apply -f albconfig.yaml`创建AlbConfig。


   > 更详细的操作步骤，请参见 [创建AlbConfig](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-albconfigs-to-configure-alb-instances#section-6su-pov-aml "")。
















   ```yaml
   apiVersion: alibabacloud.com/v1
   kind: AlbConfig
   metadata:
     name: alb # 请勿创建同名的AlbConfig资源
   spec:
     config:
       name: alb-test
       addressType: Internet
       zoneMappings:
    - vSwitchId: vsw-****cg2a9g71hx8go**** # 替换为实际虚拟交换机ID
    - vSwitchId: vsw-****un9tql5t8nh15**** # 替换为实际虚拟交换机ID
  listeners:
    - port: 80
      protocol: HTTP
```

**创建IngressClass**

IngressClass关联了AlbConfig和Ingress资源，在Ingress中填入`ingressClassName: alb`即可通过名为alb的IngressClass使用AlbConfig。

创建并保存名为IngressClass.yaml的文件，然后执行`kubectl apply -f IngressClass.yaml`创建IngressClass。

> `spec.parameters.name`中需填入AlbConfig的名称。安装组件时默认创建的AlbConfig名称为`alb`。更详细的操作说明，请参见 [使用IngressClass关联AlbConfig与Ingress](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-albconfigs-to-configure-alb-instances#section-ca6-6ol-iqb "")。

```yaml
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: alb
spec:
  controller: ingress.k8s.alibabacloud/alb
  parameters:
    apiGroup: alibabacloud.com
    kind: AlbConfig
    name: alb # 与AlbConfig的名称对应
```

## **相关文档**

[ALB Ingress服务高级用法](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/advanced-alb-ingress-configurations "")

[自定义ALB Ingress的转发规则](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-routing-rules-of-an-alb-ingress-1 "")

[通过ALB Ingress实现灰度发布](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-alb-ingresses-to-perform-canary-releases-1 "")