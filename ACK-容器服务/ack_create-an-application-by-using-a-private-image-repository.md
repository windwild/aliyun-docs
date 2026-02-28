在很多场景下，您需要用到私有镜像仓库中的镜像进行应用的部署，本文介绍如何使用阿里云镜像仓库服务创建一个私有的镜像仓库，并且创建一个使用该私有镜像仓库的应用。

## 创建私有镜像库

如果您是首次使用阿里云容器镜像服务，会弹出提示需要您设置Registry登录密码，请单击前往开通，并根据界面提示，设置Registry登录密码。


01. 登录[容器镜像服务控制台](https://cr.console.aliyun.com/)。
02. 在顶部菜单栏，选择所需地域。
03. 在左侧导航栏，选择实例列表。
04. 在实例列表页面单击个人版实例。
05. 在个人实例管理页面选择仓库管理 \> 镜像仓库。
06. 在镜像仓库页面左上角选择创建镜像仓库。
07. 在仓库信息配置向导中设置命名空间、仓库名称、摘要和仓库类型，本例选择私有镜像仓库类型。然后单击下一步。
08. 在代码源配置向导中，将代码源设为本地仓库，然后单击创建镜像仓库。




    **说明**



    在镜像仓库列表下，单击目标镜像仓库的名称。在基本信息页面的操作指南页签，可以查看如何使用该私有镜像仓库。


09. 执行以下命令，登录镜像仓库。




    **说明**





    - 如果您使用的是阿里云账号，阿里云账号就是您的镜像仓库登录名。
    - 如果您使用的是RAM用户，去掉RAM用户账号.onaliyun.com后的名称就是您的镜像仓库登录名。例如您的RAM用户为123@1880770869021234.onaliyun.com，则您的镜像仓库登录名为123@1880770869021234。

```xml
sudo docker login --username=<镜像仓库登录名> registry.cn-<个人版实例所在的地域>.aliyuncs.com
```

返回结果中输入登录密码，然后显示`login succeeded`，表示登录成功。


10. 执行以下命令，查看镜像ID。
















    ```ebnf
    docker images
    ```

11. 执行以下命令，设置镜像标签。
















    ```pf
    sudo docker tag <镜像ID> registry.cn-hangzhou.aliyuncs.com/<命名空间名称>/<镜像仓库名称>：[镜像版本号]
    ```

12. 执行以下命令，推送镜像至镜像仓库。
















    ```stylus
    sudo docker push registry.cn-hangzhou.aliyuncs.com/<命名空间名称>/<镜像仓库名称>：[镜像版本号]
    ```





    预期输出：

















    ```yaml
    The push refers to a repository [registry.cn-hangzhou.aliyuncs.com/XXX/tomcat-private]
    9072c7b03a1b: Pushed
    f9701cf47c58: Pushed
    365c8156ff79: Pushed
    2de08d97c2ed: Pushed
    6b09c39b2b33: Pushed
    4172ffa172a6: Pushed
    1dccf0da88f3: Pushed
    d2070b14033b: Pushed
    63dcf81c7ca7: Pushed
    ce6466f43b11: Pushed
    719d45669b35: Pushed
    3b10514a95be: Pushed
    V1: digest: sha256:cded14cf64697961078aedfdf870e704a52270188c8194b6f70c778a8289**** size: 2836
    ```





    在镜像仓库详情页，单击左侧导航栏中的镜像版本，您可以看到镜像已成功上传，并可查看镜像的版本信息。



## 创建私有镜像仓库登录密钥类型的密钥

如果拉取私有镜像的话，您需要使用私有镜像仓库登录密钥类型的密钥进行拉取。


1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)。
2. 在控制台左侧导航栏中，单击集群。
3. 在集群列表页面中，单击目标集群名称或者目标集群右侧操作列下的详情。
4. 在集群管理页左侧导航栏中，选择配置管理 \> 保密字典。
5. 在保密字典页面右上角，单击创建。
6. 在创建页面配置参数，然后单击确定。





| 参数 | 描述 |
| --- | --- |




| 参数 | 描述 |
| --- | --- |
| 名称 | 保密字典名称。 |
| 类型 | 保密字典类型：<br> <br>   - Opaque：一般密钥类型。输入键、值。值必须使用Base64编码。<br>   - 私有镜像仓库登录密钥：存放拉取私有仓库镜像所需的认证信息。输入镜像仓库地址及用户名和密码。<br>      <br>     <br>     <br>     **说明**<br>     <br>     <br>     <br>     用户名和密码为阿里云账号全名和开通服务时所设密码。您可以在访问凭证页面修改密码。<br>      <br>     <br>   - TLS证书：TLS是一种用来对身份进行验证的机制。<br>      <br>     - Cert：填写TLS证书信息。<br>     - Key：填写TLS的私钥信息。 |





默认返回保密字典页面，您可看到新建的密钥出现在列表中。


**说明**

您也可以通过命令行创建私有镜像仓库登录密钥类型的密钥，请参见[通过kubectl连接Kubernetes集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/obtain-the-kubeconfig-file-of-a-cluster-and-use-kubectl-to-connect-to-the-cluster#task-ubf-lhg-vdb "")。


## 通过私有镜像仓库创建应用

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)。
2. 在控制台左侧导航栏中，单击集群。
3. 在集群列表页面中，单击目标集群名称或者目标集群右侧操作列下的详情。
4. 在集群管理页左侧导航栏中，选择工作负载 \> 无状态。
5. 在无状态页面右上角，单击使用YAML创建资源。




**说明**



您也可以通过单击使用镜像创建来创建应用。请参见[使用镜像密钥创建应用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-stateless-application-by-using-a-deployment#section-frc-gez-jd5 "")。


6. 将示例模板设置为自定义，并将以下YAML内容复制到模板中。
















```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
     name: private-image
     nameSpace: default
     labels:
       app: private-image
spec:
     replicas: 1
     selector:
       matchLabels:
         app: private-image
     template:
       metadata:
         labels:
           app: private-image
       spec:
         containers:
      - name: private-image
        image: registry.cn-hangzhou.aliyuncs.com/命名空间名称/tomcat-private:latest
        ports:
        - containerPort: 8080
      imagePullSecrets:
      - name: regsecret
```

7. 单击创建。
返回无状态应用列表，查看使用私有镜像仓库创建的应用。


更多内容请参见Kubernetes官方文档[使用私有仓库](https://kubernetes.io/docs/concepts/containers/images/?spm=a2c4g.11186623.2.1.XVyfik#using-a-private-registry)。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 使用私有镜像仓库创建应用

# 使用私有镜像仓库创建应用

更新时间：2021-05-10 05:33:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

创建私有镜像库

创建私有镜像仓库登录密钥类型的密钥

通过私有镜像仓库创建应用