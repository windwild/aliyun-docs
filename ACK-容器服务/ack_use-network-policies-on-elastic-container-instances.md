### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 在ECI上使用网络策略

# 在ECI上使用网络策略

更新时间：2025-01-09 01:11:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

注意事项

步骤一：开启网络策略

步骤二：使用网络策略

注册集群网络策略（Network Policy）提供基于策略的网络控制。如果您希望在IP地址或者端口层面控制网络流量，可以为集群中特定应用使用网络策略。本文介绍如何使用ACK One注册集群的网络策略及常见的使用场景。

## 前提条件

- 自建Kubernetes集群版本需在1.20.0及以上。

- 已创建注册集群，并将自建Kubernetes集群接入注册集群。具体操作，请参见 [创建注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-ack-one-registered-clusters#task-skz-qwk-qfb "")。


## 注意事项

- Network Policy功能仅支持在ACK One注册集群的弹性容器实例ECI中使用。

- 暂不支持IPv6地址的网络策略。

- 暂不支持NetworkPolicy中EndPort配置。

- NetworkPolicy规则允许通过LabelSelector选择Namespace或者Pod。但当Pod中的NetworkPolicy数量增大时，不仅会使规则生效时间延长，而且大量的NetworkPolicy规则也会对您的集群管理、问题排查带来困扰，因此建议您集群内的NetworkPolicy数量小于100个。


## 步骤一：开启网络策略

1. 安装组件Poseidon。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **组件管理**。

3. 在 **组件管理** 页面，单击 **网络** 页签，在 **Poseidon** 组件所在卡片的右下方，单击 **安装**。

4. 在 **安装组件Poseidon** 页面，选中 **为ECI实例启用NetworkPolicy**，然后单击 **确认**。
2. 安装组件ack-virtual-node。


1. 在 **组件管理** 页面，单击 **核心组件** 页签，在 **ack-virtual-node** 组件所在卡片的右下方，单击 **安装**。

2. 在 **安装组件ack-virtual-node** 页面，根据实际网络接入情况选择 **是否启用VPC内网访问**，然后单击 **确认**。

      组件安装成功后，会在卡片右上角出现 **已安装** 字样。


**说明**

若您之前已安装 **ack-virtual-node** 组件，需要将该组件升级至2.10.0及以上版本。具体操作，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components "")。

## 步骤二：使用网络策略

1. 执行如下命令，创建网络策略。该策略描述在`default`命名空间中，允许带有`app: busybox`标签的Pod通过TCP的80端口向具有`app: nginx`标签的Pod发送流量。除非具有其他网络策略，否则将阻止来自其他Pod的流量。















```bash
kubectl apply -f - <<EOF
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
     name: test-network-policy
     namespace: default
spec:
     podSelector:
       matchLabels:
         app: nginx
     policyTypes:
    - Ingress
ingress:
    - from:
        - podSelector:
            matchLabels:
              app: busybox
      ports:
        - protocol: TCP
          port: 80
EOF
```

2. 执行如下命令，创建标签为`app: nginx`的应用。















```bash
kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
     labels:
       app: nginx
     name: nginx-deployment
     namespace: default
spec:
     replicas: 1
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         labels:
           alibabacloud.com/eci: 'true'
           app: nginx
       spec:
         containers:
        - image: 'registry.cn-hangzhou.aliyuncs.com/eci_open/nginx:1.14.2'
          imagePullPolicy: IfNotPresent
          name: nginx
          ports:
            - containerPort: 80
              protocol: TCP
          resources:
            limits:
              cpu: 500m

EOF
```

3. 执行如下命令，查看Nginx应用状态并记录Pod IP地址。















```bash
kubectl get pod -owide | grep nginx-deployment
```



预期输出：















```bash
NAME                                   READY   STATUS    RESTARTS   AGE   IP                NODE                     NOMINATED NODE   READINESS GATES
nginx-deployment-698d746d4c-nXXXXXXx   1/1     Running   0          35s   192.168.XXX.XXX   cn-heyuan.10.108.XX.XX   <none>           <none>
```

4. 执行如下命令，创建标签为`app: busybox`的应用。















```bash
kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
     labels:
       app: busybox
     name: busybox-deployment
     namespace: default
spec:
     replicas: 1
     selector:
       matchLabels:
         app: busybox
     template:
       metadata:
         labels:
           alibabacloud.com/eci: 'true'
           app: busybox
       spec:
         containers:
        - args:
            - '-c'
            - ' sleep 360000000'
          command:
            - /bin/sh
          image: 'registry-cn-hangzhou.ack.aliyuncs.com/dev/busybox:1'
          imagePullPolicy: IfNotPresent
          name: busybox
          ports:
            - containerPort: 80
              protocol: TCP
          resources:
            limits:
              cpu: 500m
EOF
```

5. 登录到busybox容器内执行如下命令，访问Nginx应用的Pod IP地址。
















   ```bash
   wget http://192.168.XXX.XXX
   ```



    预期输出：
















   ```bash
   Connecting to 192.168.XXX.XXX:80... connected.
   HTTP request sent, awaiting response... 200 OK
   Length: 612 [text/html]
   Saving to: 'index.html'

   index.html                                               100%[================================================================================================================================>]     612  --.-KB/s    in 0s

   2024-11-19 20:12:09 (1.66 MB/s) - 'index.html' saved [612/612]
   ```



    连接Nginx的进度为100%时，说明请求成功，可以正常访问Nginx服务。

6. 执行如下命令，创建标签为`app: busybox-demo`的应用。















   ```bash
   kubectl apply -f - <<EOF
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     labels:
       app: busybox-demo
     name: busybox-deployment-demo
     namespace: default
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: busybox-demo
     template:
       metadata:
         labels:
           alibabacloud.com/eci: 'true'
           app: busybox-demo
       spec:
         containers:
        - args:
            - '-c'
            - ' sleep 360000000'
          command:
            - /bin/sh
          image: 'registry-cn-hangzhou.ack.aliyuncs.com/dev/busybox:1'
          imagePullPolicy: IfNotPresent
          name: busybox-demo
          ports:
            - containerPort: 80
              protocol: TCP
          resources:
            limits:
              cpu: 500m
kubectl apply -f - <<EOF
```

7. 登录到busybox-demo容器执行如下命令，访问Nginx应用的Pod IP地址。
















```bash
wget http://192.168.XXX.XXX
```



预期输出：















```bash
Connecting to 192.168.XXX.XXX:80...
failed: Connection timed out.
```



    连接Nginx超时，说明网络策略生效。