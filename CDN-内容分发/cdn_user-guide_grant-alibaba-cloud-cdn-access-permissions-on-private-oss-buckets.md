### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/)OSS私有Bucket回源

# OSS私有Bucket回源

更新时间：2025-12-11 03:58:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：回源概述](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-routing-overview)[下一篇：配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理与优势

操作步骤

安全加固建议

关闭OSS私有Bucket回源

常见问题

相关文档

如果加速域名的源站是阿里云对象存储OSS，并且OSS的Bucket为私有模式（可以起到访问鉴权的作用，避免非授权的请求盗刷流量），建议您给加速域名开启OSS私有Bucket回源功能，通过CDN加速OSS私有Bucket资源。

## **工作原理与优势**

- **工作原理**：功能开启后，CDN向您的私有OSS Bucket发起回源请求时，会自动在请求头（Header）中添加一个`Authorization`字段。该字段的值是根据您授权的身份信息（STS临时令牌或AccessKey）生成的有效签名，OSS服务会据此对请求进行鉴权。

- **安全访问**：通过为CDN授予一个受限的只读权限，确保了回源请求的合法性，避免了将私有Bucket设置为公开所带来的安全风险。

- **成本优化**：终端用户访问将命中CDN缓存，其流量费用远低于直接访问OSS产生的外网流出流量。同时，CDN回源到OSS的流量会计为CDN回源流量，其单价也低于OSS外网流出流量单价，有效降低总体成本。具体请参见 [CDN加速OSS计费说明](https://help.aliyun.com/zh/cdn/product-overview/billing-of-oss-content-acceleration "")


## **操作步骤**

配置过程分为两步：首先为您的账号完成一次性授权，然后为指定的加速域名开启该功能。

1. 授权CDN访问OSS。在首次为账号下域名配置该功能前，您必须先为CDN服务授予访问OSS的权限，此为账号级别的一次性操作。如果您没有出现授权提示，则直接跳过该步骤。






（推荐）通过控制台一键授权



（备用方案）通过RAM手动授权



















1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，单击目标域名对应的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **阿里云OSS私有Bucket回源** 区域，单击 **点击授权**，在授权确认页中单击 **确认授权**。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6253445671/p1032254.png)


1. 登录 [RAM控制台](https://ram.console.aliyun.com/permissions)。

2. 在左侧导航栏，单击 **权限管理** **>** **权限策略**。

3. 在 **权限策略** 页面，单击 **创建权限策略**。

4. 在 **脚本编辑** 页签，输入以下策略内容。


```json
{
    "Version": "1",
    "Statement": [\
        {\
            "Action": [\
                "oss:List*",\
                "oss:Get*"\
            ],\
            "Resource": "*",\
            "Effect": "Allow"\
        }\
    ]
}
```

6. 单击 **确定**，在 **创建权限策略** 页面输入以下信息之后单击 **确定**。

7. **策略名称**：AliyunCDNAccessingPrivateOSSRolePolicy

8. **备注**：用于CDN/DCDN回源私有OSS Bucket角色的授权策略，包含OSS的只读权限。


在左侧导航栏，单击 **身份管理** **>** **角色**。

1. 在 **角色** 页面，单击 **创建角色**。

2. 将 **信任主体类型** 设置为 **云账号**， **信任主体名称** 选择 **当前云账号**，单击 **确定**。

3. 在 **创建角色** 阶段，输入以下信息 **。**

4. **角色名称**：AliyunCDNAccessingPrivateOSSRole


角色创建完成之后，在 **角色** 页面列表中单击 **AliyunCDNAccessingPrivateOSSRole**，进入角色编辑页面。

1. 在 **信任策略** 页签，单击 **编辑信任策略**，输入以下信息之后单击 **确定**。


```plaintext
{
  "Statement": [\
    {\
      "Action": "sts:AssumeRole",\
      "Effect": "Allow",\
      "Principal": {\
        "Service": [\
          "cdn.aliyuncs.com"\
        ]\
      }\
    }\
  ],
  "Version": "1"
}
```

3. 切换到 **权限管理** 页签，在 **授权** 页签中，单击 **新增授权**。

4. 资源范围：账号级别

5. 授权主体：选择之前创建的AliyunCDNAccessingPrivateOSSRole

6. 权限策略：选择 **自** **定义策略**，选择之前创建的AliyunCDNAccessingPrivateOSSRolePolicy，单击 **确认新增授权**。


**确认新增授权** 之后，回到CDN控制台的 **回源配置** 页面，可以看到 **阿里云OSS私有Bucket回源** 功能已经完成授权，

2. 开启 **阿里云OSS私有Bucket回源** 并配置回源类型。

1. 找到 **阿里云OSS私有Bucket回源** 区域，打开其开关。

2. 在弹出的 **阿里云OSS私有Bucket回源** 对话框中，选择回源类型，单击 **确定**。

      ![回源类型](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7078127761/p572918.png)




      | **回源类型** | **推荐场景与说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **回源类型** | **推荐场景与说明** |
      | **同账号回源** | **（推荐）** 适用于CDN和OSS Bucket在同一个阿里云账号下的场景。系统将自动使用STS临时安全令牌进行鉴权，配置简单，无需管理密钥，安全性更高。 |
      | **跨账号回源或同账号回源** | 适用于CDN和OSS Bucket分属不同阿里云账号的场景，也支持同账号。此方式需要您手动提供回源目标OSS私有Bucket所属阿里云账号的AccessKey ID和AccessKey Secret。具体请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair#task-2245479 "")。 |





      **说明**





      - **访问范围说明**：开启后，该加速域名将可以访问其源站私有Bucket内的 **所有** 资源，无法在CDN侧对Bucket内的部分资源做访问限制。

      - **签名冲突说明**：为避免OSS鉴权失败，请确保回源请求的URL参数中不携带签名信息。单个请求不能同时在Header和URL中携带签名。

      - **功能冲突说明**：本功能与OSS的静态网站托管功能的默认首页配置存在冲突。如需同时使用，请参考 [说明文档](https://help.aliyun.com/zh/cdn/you-are-forbidden-to-list-buckets-after-access-to-private-oss-buckets-is-enabled#concept-2120076 "")。

## **安全加固建议**

开启私有Bucket回源后，您的源站数据是安全的，但缓存在CDN边缘节点上的资源默认是公开访问的。为防止CDN流量被盗刷，强烈建议您结合使用CDN提供的其他安全功能：

- [配置Referer黑/白名单](https://help.aliyun.com/zh/cdn/user-guide/configure-a-referer-whitelist-or-blacklist-to-enable-hotlink-protection#task-187634 "")：限制只有特定来源网站的请求才能访问您的CDN资源。

- [配置URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-url-signing#task-2106935 "")：为您的资源URL设置动态签名和过期时间，有效抵御恶意下载。


## 关闭OSS私有Bucket回源

如果您不希望加速域名能够访问您同账号下的私有Bucket内资源，您可以通过访问控制RAM（Resource Access Management）控制台，取消对应角色名称的授权，关闭CDN回源OSS私有Bucket的权限。

1. 在CDN控制台关闭该功能。

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，单击目标域名对应的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **阿里云OSS私有Bucket回源** 区域，关闭 **阿里云OSS私有Bucket回源** 开关。
2. 在RAM控制台彻底删除授权。

1. 登录 [RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏，单击**身份管理** \> **角色**。

3. 在 **角色名称** 列表下，单击 **AliyunCDNAccessingPrivateOSSRole** 角色。



      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7008884671/p820303.png)

4. 移除角色 **AliyunCDNAccessingPrivateOSSRole** 中的所有权限。

      1. 单击权限对应的 **解除授权**。

      2. 在移除权限的确认对话框中，单击 **解除授权**。
5. 返回**身份管理** \> **角色**页面，删除 **AliyunCDNAccessingPrivateOSSRole** 角色。

      1. 单击 **AliyunCDNAccessingPrivateOSSRole** 角色对应的 **删除角色**。

      2. 在 **删除角色** 的确认对话框中，单击 **删除角色**。
6. 返回**权限管理** \> **权限策略**页面，删除 **AliyunCDNAccessingPrivateOSSRolePolicy** 策略。

      1. 单击**AliyunCDNAccessingPrivateOSSRolePolic**策略对应的 **删除权限策略** 按钮。

      2. 在 **删除权限策略** 的确认对话框中，输入策略名称，单击 **删除权限策略**。

## **常见问题**

**CDN访问OSS资源提示**`This request is forbidden by kms.` **错误如何解决？**

如果您的OSS Bucket中使用了密钥管理服务KMS（Key Management Service）进行加密，您需要为CDN的回源角色额外授予使用KMS密钥的权限，否则CDN将无法解密和访问这些文件，出现`This request is forbidden by kms.`报错。

1. 登录 [RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏，选择**身份管理** \> **角色**。

3. 在 **角色名称** 列表下，找到 **AliyunCDNAccessingPrivateOSSRole** 角色。

4. 单击 **新增授权**， **授权主体** 会自动填入。

5. 在 **权限策略** 下选择 **系统策略**，搜索 **AliyunKMSCryptoUserAccess**，并单击 **AliyunKMSCryptoUserAccess**，将其添加到 **已选择权限策略** 区域框中。

6. 单击 **确认新增授权**，显示 **已完成**。

7. 单击 **关闭**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8616301271/p820217.png)

8. 使用 [刷新资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#17007093c7uba "") 功能，待刷新任务完成后，重新访问资源。


## **相关文档**

[CDN加速OSS资源最佳实践](https://help.aliyun.com/zh/cdn/use-cases/accelerate-the-retrieval-of-resources-from-an-oss-bucket-in-the-alibaba-cloud-cdn-console "")