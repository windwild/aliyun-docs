### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/)[持久化存储](https://help.aliyun.com/zh/sae/persistent-storage/)设置OSS存储

# 设置OSS存储

更新时间：2025-05-30 03:16:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置NAS存储](https://help.aliyun.com/zh/sae/configure-nas-storage-2-0)[下一篇：设置身份认证服务功能](https://help.aliyun.com/zh/sae/configure-authentication-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

功能入口

操作步骤

挂载OSS

取消挂载OSS

结果验证

常见问题

可以使用OSS存储日志吗？

故障排查

与NAS相比，OSS提供了便捷的工具以及控制台，支持可视化管理Bucket，并在解决应用实例数据持久化和实例间数据分发问题的基础上，进一步降低成本。OSS适用于读多写少的场景，例如挂载配置文件或者前端静态文件等。

## 前提条件

- [开通OSS服务](https://help.aliyun.com/zh/oss/getting-started/activate-oss#task-njz-hf4-tdb "")

- [创建存储空间](https://help.aliyun.com/zh/oss/manage-buckets-create-buckets#task-bcz-sbz-5db "")

- [创建AccessKey](https://help.aliyun.com/document_detail/53045.html#task968 "")


## 功能入口

场景不同，操作入口也有所差异：

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


## 操作步骤

展开 **持久化存储设置** 区域， **启用OSS对象存储**。

### **挂载OSS**

1. 填写 **AccessKey ID** 和 **AccessKey Secret**。





建议您遵循阿里云安全最佳实践，使用RAM用户的AccessKey调用OSS接口，并确保授予该RAM用户访问OSS资源的最小权限。例如，您需要该RAM用户只读test-sae Bucket的oss-test/目录，那么您可以授予该RAM用户以下最小权限。

















```json
{
       "Statement": [\
           {\
               "Action": "oss:GetBucket",\
               "Effect": "Allow",\
               "Resource": "acs:oss:*:*:test-sae"\
           },\
           {\
               "Action": "oss:GetObject",\
               "Effect": "Allow",\
               "Resource": "acs:oss:*:*:/"\
           }\
       ],
       "Version": "1"
}
```

2. 配置以下OSS挂载信息。如需添加多条信息，请点击 **添加**。








| **配置项** | **说明** | **示例值** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **配置项** | **说明** | **示例值** |
| **Bucket** | 已创建的OSS Bucket。 | bucketname |
| **挂载目录** | 已创建的OSS目录或OSS对象。如果OSS挂载目录不存在，会触发异常。 | 示例如下：<br>   - /<br>     <br>     <br>     <br>     **说明**<br>     <br>     <br>     <br>     <br>     <br>     代表挂载Bucket的根目录。<br>     <br>   - tmp/oss-test/<br>     <br>   - tmp/oss-demo.log |
| **容器路径** | SAE的容器路径。如果路径已存在，会覆盖原有路径；如果路径不存在，会新建路径。 | /home/admin/app/php/ |
| **权限** | 容器路径对挂载目录资源的权限，取值如下：<br>   - 只读<br>     <br>   - 读写 | 只读 |


### 取消挂载OSS

挂载OSS后，如果您不再使用OSS存储，可以取消挂载OSS。在SAE控制台取消挂载OSS后，您在OSS中所存储的数据仍然存在，不会被删除。

具体操作为：找到需要取消挂载的OSS配置条目，在其 **操作** 列，单击![oss-mount-delete-icon](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5430549161/p268612.png)图标。

## 结果验证

- 从变更详情判断。

如果变更成功，且变更生成的新实例没有出现异常事件，则说明OSS挂载成功。

![sae挂载nas成功](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5232573661/p70176.png)

- 从容器角度判断。

[登录Webshell](https://help.aliyun.com/zh/sae/use-the-webshell-feature-to-check-the-health-status-of-applications-2-0 "")，执行以下命令查询应用中是否存在OSS挂载信息。















```shell
cat /proc/mounts | grep ossfs
```





当显示如下信息时，表示OSS挂载成功。![oss_success](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8721549161/p268614.png)

- 从业务角度判断。

[登录Webshell](https://help.aliyun.com/zh/sae/use-the-webshell-feature-to-check-the-health-status-of-applications-2-0 "")，对挂载的OSS文件系统路径进行操作，如果可以从OSS控制台同步看到结果，则说明OSS挂载成功。


## **常见问题**

### 可以使用OSS存储日志吗？

建议将日志持久化存储到 [SLS](https://help.aliyun.com/zh/sae/set-log-collection-to-sls-2-0 "") 或 [Kafka](https://help.aliyun.com/zh/sae/collect-logs-to-apsaramq-for-kafka-new "")。

不建议使用OSS作为日志持久化工具，OSS适用于互联网图片、音视频等海量文件处理场景，以及网页/应用的静态和动态资源分离的场景。

## **故障排查**

使用过程中，遇到OSS挂载失败、容器中挂载路径不存在、或缺少操作权限等问题，请参考以下步骤排查故障。

1. 确认配置的OSS Bucket是否存在。

1. 如果是通过控制台部署应用，只有 **同账号同地域** 下实际存在的OSS Bucket才能在SAE控制台选取。

2. 如果是通过除控制台外的方式（例如API、SDK、saectl工具、Jenkins插件）部署应用，需要登录 [OSS控制台](https://oss.console.aliyun.com/) 并确认 **同账号同地域** 下配置的 OSS Bucket 名称是存在的。
2. 检查挂载时配置的AccessKey ID、AccessKey Secret所对应的RAM用户的操作权限。

1. 根据配置的AccessKey ID、AccessKey Secret找到关联的 RAM 用户。

2. 确认该 RAM 用户针对配置的 OSS Bucket 有 [必要的操作权限](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies "")。
3. 检查OSS Bucket授权策略。

1. 登录 [OSS控制台](https://oss.console.aliyun.com/)，进入目标Bucket的详情页面，在左侧导航栏选择**权限控制** \> **Bucket授权策略**。

2. 检查Bucket授权策略是否拦截了SAE的访问，具体来说，就是要确认相应地域下SAE的公网地址已被添加到放行的白名单中，如下表所示。



      **说明**





      如需获取SAE详细公网地址，请在钉钉群（群号：32874633）联系相关技术人员。






      |     |     |
      | --- | --- |
      | **Region** | **IP 地址** |
      | cn-hangzhou | 47.99.xx.xx |
      | cn-shanghai | 47.101.xx.xx |
      | cn-beijing | 47.94.xx.xx |
      | cn-zhangjiakou | 121.89.xx.xx |
      | cn-wulanchabu | 8.130.xx.xx |
      | cn-shenzhen | 39.108.xx.xx |
      | cn-heyuan | 47.121.xx.xx |
      | cn-guangzhou | 8.134.xx.xx<br>8.134.xx.xx |
      | cn-chengdu | 47.108.xx.xx |
      | cn-hongkong | 47.243.xx.xx<br>8.210.xx.xx |
      | ap-southeast-1 | 8.219.xx.xx |
      | eu-central-1 | 8.211.xx.xx<br>8.211.xx.xx |
      | us-west-1 | 47.89.xx.xx |
      | us-east-1 | 47.252.xx.xx |