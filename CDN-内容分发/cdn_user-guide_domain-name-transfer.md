### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[域名迁移](https://help.aliyun.com/zh/cdn/user-guide/domain-name-transfer-1/)跨账号迁移CDN域名

# 跨账号迁移CDN域名

更新时间：2025-04-22 21:34:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：复制配置](https://help.aliyun.com/zh/cdn/user-guide/copy-configurations-to-domain-names)[下一篇：设置报警](https://help.aliyun.com/zh/cdn/user-guide/set-an-alert-rule)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用场景

前提条件

注意事项

操作步骤

当您需要将阿里云CDN域名跨账号迁移至另一个阿里云账号时， 可以使用域名迁移工具完成迁移操作。

## 使用场景

- 域名迁移工具仅适用于不同阿里云账号之间的CDN加速域名迁移，主要用于以下场景：

  - 您有多个阿里云账号，希望将账号A中的加速域名迁移至账号B。

  - 您在添加加速域名时，有提示该加速域名已经被添加过，您不清楚该加速域名归属于哪个账号，希望将该加速域名迁移至您正在操作的账号中。
- 如果目标域名已被添加在其他云产品上（例如视频直播），需要迁移至CDN服务时，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)处理。


## **前提条件**

- 域名迁移前，若加速域名的原账号或目标账号其中任意一个处于欠费状态，则无法完成域名迁移，您需要结清欠费后再进行自助迁移。

- 如果您使用RAM用户（子账号），RAM用户必须具有指定资源的**AliyunCDNFullAccess**权限才能执行迁移操作。具体操作，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user#task-187800 "")。


## 注意事项

- 为了确保您的域名运行安全，仅支持单个域名迁移，不支持批量迁移。

- 若迁移时，目标账号中的CDN域名已达到上限，您可以先在配额中心提升域名上限后，再进行迁移，详情请参见 [配额管理](https://help.aliyun.com/zh/cdn/user-guide/quota-management#concept-2086246 "")。

- 请保证同一个根域名的泛域名和精确域名在同一个账号下（例如`.aliyundoc.com`和`example.aliyundoc.com`），否则可能出现配置冲突，实际配置都会以精确域名的配置为准。

- 您迁移的域名若有线上业务正在运行，迁移前请务必确认好以下两点，避免影响业务：

  - 如果待迁移域名的源站为阿里云OSS，并且CDN域名开启了 [OSS私有Bucket回源](https://help.aliyun.com/zh/cdn/user-guide/grant-alibaba-cloud-cdn-access-permissions-on-private-oss-buckets#task-187634 "") 功能，同时配置使用STS安全令牌回源到阿里云同账号下的OSS私有Bucket，那么域名跨账号迁移后可能会导致回源鉴权失效，导致回源失败，因此需要在迁移域名之前，将域名的鉴权方式切换到使用永久安全令牌。

  - 如果待迁移域名已经配置了SSL证书，支持HTTPS访问，那么迁移到新账号以后，该域名依旧支持HTTPS访问。但是新账号将无法收到域名的证书过期提醒，您需要在新账号重新上传证书，才能收到该提醒。
- 域名迁移前，需先关闭在原账号下开启的监控数据、日志数据、运营报表数据等功能。如未操作，这些功能将持续向原账号投递日志、报表等信息并产生计费。域名迁移后，这些功能也需在新账号中重新配置。

- 域名迁移到新账号以后：

  - 域名产生的流量，将无法使用原账号下的资源包抵扣（资源包不可被迁移）。

  - 域名关联的资源组和标签也会发生变化，若您使用了资源组或者标签来管理域名，请在新账号中重新调整。
- 若您的域名被限制迁移，迁移时会有提醒，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)咨询。


## 操作步骤

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面右上角单击 **迁入域名**。

4. 阅读并勾选迁入须知后，单击 **确定**。

5. 输入待迁移的加速域名，参考如下方式完成域名归属校验。






方式一：DNS解析验证



方式二：文件验证



















1. 在 **域名归属校验** 区域，单击 **方法1：DNS解析验证**。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5820892471/p933889.png)

2. 登录[云解析DNS控制台](https://dns.console.aliyun.com/)。

3. 在 **权威域名解析** 页面，找到加速域名的根域名`example.com`，并单击右侧的 **解析设置**。

4. 单击 **添加记录**， **记录类型** 选择为 **TXT**，填写步骤1中阿里云CDN提供的 **主机记录**、 **记录值**，其余参数保持为默认填写即可。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6330967271/p855492.png)

5. 单击 **确定**，完成添加。


1. 在验证页面，单击 **方法2: 文件验证**。

2. 单击`verification.html`，下载验证文件。

3. 手动将验证文件上传到您主域名服务器（例如您的ECS、OSS、CVM、COS、EC2等）的根目录。例如：当前加速域名为`image.example.com`，您需要将该文件上传至 `example.com` 的根目录下。



      **说明**





      阿里云CDN后台将访问您服务器中`http://example.com/verification.html`文件链接进行验证。



      - 如果文件内的记录值与验证文件记录值一致，则通过验证。

      - 如果验证失败，请确保上述文件链接可访问，并且您上传的文件正确。


6. 返回CDN控制台，单击 **确认迁入**，完成迁移。



**说明**





若迁入失败，请先检查第五步配置是否正确。如有误，修改后重新确认迁入；若配置正确仍失败，您可以联系我们帮您处理。可以前往[阿里云提交工单页面](https://smartservice.console.aliyun.com/service/create-ticket)提交工单。