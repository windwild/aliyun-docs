### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/)注入配置信息

# 注入配置信息

更新时间：2025-06-27 10:34:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开启CPU Burst功能（仅适用于标准版、专业版）](https://help.aliyun.com/zh/sae/enable-cpu-burst-function-only-applicable-to-standard-edition-and-professional-edition)[下一篇：注入保密信息](https://help.aliyun.com/zh/sae/inject-secret)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作入口

配置指引

场景示例

将配置项（ConfigMap）注入容器可以将其转换为容器中的文件，应用可以读取注入的文件作为配置文件，这使得您可以灵活修改应用的配置而无需重新构建应用的镜像。

## 操作入口

1. 操作入口在不同场景下有差异：







创建应用



对正在运行的应用进行变更



对已停止的应用进行变更



















1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击 **创建应用**。

2. 在 **应用基本信息** 向导页面进行配置后，单击 **下一步：高级设置**。


**警告**

重新部署应用后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **部署应用**。


1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **修改应用配置**。


2. 展开 **配置管理** 区域，按需进行配置。


## 配置指引

注入配置项前，您需要先创建配置项。您可以在应用的 **命名空间** 中 [创建配置项](https://help.aliyun.com/zh/sae/manage-and-use-configuration-items-k8s-configmap#section-ji2-r1r-iht "")，也可以在当前区域单击 **创建配置项（ConfigMap）**，在 **创建配置项** 面板进行创建，创建的配置项会同步到应用的 **命名空间**。

单击 **+添加**，您可以将特定配置项（ConfigMap）的单个键或全部键注入容器，以将其转换为容器中的文件。配置项的值将作为文件的内容，您可以自定义文件的挂载路径。

**说明**

应用可以读取注入的文件作为配置文件，这使得您可以灵活修改应用的配置而无需重新构建应用的镜像。修改应用配置时，请先将容器内的原配置文件内容复制到本地，修改后将其保存为配置项（ConfigMap）的值，再参考以下步骤将配置项（ConfigMap）注入容器。您需要重新部署应用，并单击 **配置项名称** 旁的刷新按钮，以确保改动生效。

将单个键注入容器

将全部键注入容器

选择已创建的 **配置项名称** 和该配置项中的 **键**，并输入 **挂载路径**。 **挂载路径** 是注入的文件在容器环境中的绝对路径（含文件名）。如果路径不存在将自动创建 。如果路径下存在同名文件，则注入的文件会覆盖原有文件。注入的文件在容器中是只读的。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5800210471/p919455.png)

选择已创建的 **配置项名称**，从 **键** 下拉列表选择 **全部**，并输入 **挂载路径**。 **挂载路径** 是注入的文件在容器环境中的绝对路径（不含文件名，且不能以`/`结尾），注入的文件以键名作为文件名。如果路径不存在将自动创建 。如果路径下存在同名文件，则注入的文件会覆盖原有文件。注入的文件在容器中是只读的。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5800210471/p919510.png)

### **场景示例**

[通过注入配置项修改Nginx配置文件](https://help.aliyun.com/zh/sae/use-sae-to-deploy-an-nginx-application#4263e739f61if "")