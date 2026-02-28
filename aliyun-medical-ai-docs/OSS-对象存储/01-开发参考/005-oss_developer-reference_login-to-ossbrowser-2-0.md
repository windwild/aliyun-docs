### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[图形化管理工具ossbrowser 2.0（预览版）](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview/)登录ossbrowser 2.0

# 登录ossbrowser 2.0

更新时间：2026-02-01 21:57:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0)[下一篇：常用操作](https://help.aliyun.com/zh/oss/developer-reference/commonly-used-function-of-ossbrowser2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

登录账号权限配置

操作步骤

选择登录方式

配置Endpoint

配置预设OSS路径

配置Bucket地域

结果验证

更多配置

本文详细为您介绍ossbrowser 2.0的登录选择，以及相关配置项说明。

## **登录账号权限配置**

在登录前，您需要确保当前所登录账号拥有ossbrowser 2.0的相关操作权限。

- **阿里云（主账号）**：阿里云（主账号）默认拥有其账号下所有资源权限，无需额外配置权限。

- **RAM用户**：登录并查看全部Bucket列表和文件列表，至少确保其RAM用户拥有全部Bucket的`oss:ListBuckets`、`oss:ListObjects`和`oss:GetBucketInfo`权限。

- **STS临时访问凭证**：登录并查看指定Bucket下的文件列表，至少确保STS临时访问凭证拥有指定Bucket的`oss:ListObjects`和`oss:GetBucketInfo`权限。

- **授权码**：授权码权限由主账号或RAM用户管理者登录ossbrowser 2.0后，通过 [文件授权](https://help.aliyun.com/zh/oss/developer-reference/document-authorization-using-ossbrowser2-0#949eb71b93qo8 "") 操作进行配置。


使用RAM用户或STS临时访问凭证登录ossbrowser 2.0后，执行相关操作也需配置相应的权限策略。您可以根据以下表格，按照所需操作的功能分类配置使用权限。有关如何自定义权限策略以及为RAM用户授权，请参见 [创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy#title-3km-fsu-3en "") 和 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。

**ossbrowser 2.0各功能模块操作所需权限**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能模块** | **Action** | **说明** | **权限配置建议** |
| 登录ossbrowser 2.0 | oss:ListBuckets | 列举拥有的所有Bucket。 | 如果只需访问特定Bucket，无需`oss:ListBuckets`权限，但无法进入Bucket列表。 |
| oss:ListObjects | 列举Bucket中所有Object的信息。 | 如需访问文件列表，需配置`oss:ListObjects`权限。 |
| oss:GetBucketInfo | 查看Bucket相关信息。 | 若想通过预设路径访问特定Bucket，需配置`oss:GetBucketInfo`权限；若没有该权限，也可手动指定存储桶所在的地域来实现访问。 |
| 管理Bucket | oss:ListBuckets | 列举拥有的所有Bucket。 | 查看Bucket 列表，需配置`oss:ListBuckets`权限。 |
| oss:PutBucket | 创建Bucket。 | 创建Bucket，需配置`oss:PutBucket`权限。 |
| oss:GetBucketInfo | 查看Bucket相关信息。 | 获取Bucket基本信息，需配置`oss:GetBucketInfo`权限。 |
| oss:DeleteBucket | 删除某个Bucket。 | 删除Bucket，建议谨慎配置`oss:DeleteBucket`权限。 |
| 文件列表 | oss:ListObjects | 列举Bucket中所有Object的信息。 | 列举文件列表，需配置`oss:ListObjects`权限。 |
| 上传和下载 | oss:ListObjects | 列举Bucket中所有Object的信息。 | 下载文件夹，需配置`oss:ListObjects`权限。 |
| oss:GetObject | 获取某个Object。 | 上传和下载文件，需配置`oss:GetObject`权限。 |
| oss:PutObject | 上传文件。 | 上传文件，需配置`oss:PutObject`权限。 |
| 复制、移动和重命名 | oss:ListBuckets | 列举拥有的所有Bucket。 | 跨Bucket复制和移动时，需配置`oss:ListBuckets`权限。 |
| oss:ListObjects | 列举Bucket中所有Object的信息。 | 复制、移动和重命名文件夹时，需配置`oss:ListObjects`权限。 |
| oss:GetObject | 获取某个Object。 | 需有源Bucket的`oss:GetObject`权限。 |
| oss:PutObject | 上传文件。 | 需有目标Bucket的`oss:PutObject`权限 。 |
| oss:DeleteObject | 删除某个Object。 | 移动和重命名时，需有源Bucket的`oss:DeleteObject`权限，否则源文件无法删除。 |
| oss:GetBucketInfo | 查看Bucket相关信息。 | OSS的`Bucket`开启版本控制后，遇到同名文件只能覆盖。ossbrowser 2.0会调用`GetBucketInfo`来查询Bucket的版本状态，但这个权限非必需，没权限报错关掉弹窗即可。只要Bucket开了版本控制，同名策略选 **跳过** 和 **询问** 无效，最终只能覆盖。 |
| 文件删除 | oss:ListObjects | 列举Bucket中所有Object的信息。 | 删除目录，需配置`oss:ListObjects`权限。 |
| oss:DeleteObject | 删除某个Object。 | 删除文件，建议谨慎配置`oss:DeleteObject`权限。 |
| 碎片管理 | oss:ListParts | 列举指定Upload ID所属的所有已经上传成功的Part。 | 查看文件碎片，需配置`oss:ListParts`权限。 |
| oss:ListMultipartUploads | 列举所有执行中的Multipart Upload事件，即已经初始化但还未完成（Complete）或者还未中止（Abort）的Multipart Upload事件。 | 删除文件碎片，需配置`oss:ListMultipartUploads`权限。 |
| 文件解冻 | oss:RestoreObject | 解冻归档存储、冷归档存储或者深度冷归档存储类型的Object。 | 文件解冻，需配置`oss:RestoreObject`权限。 |

## **操作步骤**

1. ### **选择登录方式**


ossbrowser 2.0提供了四种登录方式，如下表所示。




| **登录方式** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **登录方式** | **说明** |
| **AK登录** | 如果您是资源拥有者，或者团队内成员需要长期操作OSS资源且要求登录长期有效，那么建议您使用 **阿里云（主账号）** 或 **RAM用户** 的AccessKey（AK）信息来登录ossbrowser 2.0。 |
| **账号登录** | 如果您是资源拥有者，或者团队内成员需要长期操作OSS资源，且需要每天进行安全登录验证，那么建议您使用 **阿里云APP**、 **支付宝**、 **钉钉** 扫码或 **阿里云（主账号）、RAM用户账号、手机验证码** 等多种方式选择登录。<br>**重要**<br>账号登录方式暂不支持 [文件授权](https://help.aliyun.com/zh/oss/developer-reference/document-authorization-using-ossbrowser2-0#949eb71b93qo8 "") 操作，若需进行此操作，请选用其他登录方式。 |
| **STS登录** | 如果需要团队内成员临时操作您的OSS资源，可以通过RAM用户扮演RAM角色的方式调用STS服务来获取STS临时访问凭证。然后，团队的其他成员可以凭借此临时访问凭证进行登录并操作您的OSS资源。 |
| **授权码登录** | 如果需要团队内成员临时或长期操作您的部分OSS资源，可以通过AK登录到ossbrowser 2.0， **对OSS资源进行授权并生成授权码**。然后，团队的其他成员可以凭借此授权码进行登录，并操作您已授权过的OSS资源。 |



请根据使用场景选择登录方式。






AK登录



账号登录



STS登录



授权码登录



















**AK登录** 方式支持阿里云（主账号）以及RAM用户的AK信息进行登录，为保障数据安全， **建议您使用RAM用户的AK信息登录**。




阿里云（主账号）登录






1. 获取AK信息。

      1. **本地获取AK**：使用您在创建AK时，保存在本地的`AccessKey ID`和`AccessKey Secret`进行登录。

      2. **创建AK**：如果您忘记了AK，请进入 [创建AccessKey](https://ram.console.aliyun.com/profile/access-keys?spm=5176.12818093_-1363046575.console-base_top-nav.dak.58c816d0tZzByx) 页面，单击 **创建AccessKey** 按钮，按照页面提示完成访问密钥（AccessKey）的创建。创建成功后，在弹出框单击 **下载CSV文件** 便可将访问密钥（AccessKey）保存到本地。最后，使用新生成的`AccessKey ID`和`AccessKey Secret`进行登录即可。
2. 单击 **AK登录**，并填写账号的`AccessKey ID`和`AccessKey Secret`进行登录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2820645471/p948511.png)


RAM用户登录：创建RAM用户并登录

创建RAM用户需使用拥有管理RAM用户权限的账号，例如阿里云（主账号）登录阿里云，执行以下步骤创建。

1. 创建RAM用户。

      1. 单击 [创建用户](https://ram.console.aliyun.com/users) 根据控制台指引完成RAM用户的创建。



         **说明**





         有关创建RAM用户的详细信息，请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user#task-187540 "")。

      2. 单击 **下载CSV文件**，此文件包含RAM用户登录所需AK信息，请务必妥善保存。
2. 为RAM用户授权。

      1. 单击 [用户](https://ram.console.aliyun.com/users) 页面，选择目标用户后单击**权限管理** \> **新增授权**。

      2. 在 **搜索框** 复制并添加 [ossbrowser 2.0操作权限](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#c42a0112c8rge "")、`AliyunRAMFullAccess`以及`AliyunSTSAssumeRoleAccess`权限。



         **说明**





         RAM用户授权的详细信息以及自定义授权，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "") 和 [创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy#title-3km-fsu-3en "")。
3. 单击 **AK登录**，并填写CSV文件中的`AccessKey ID`和`AccessKey Secret`进行登录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2820645471/p948513.png)


RAM用户登录：使用已有的RAM用户登录

1. 获取AK信息。

      1. **本地获取AK**：使用您在创建AK时，保存在本地的`AccessKey ID`和`AccessKey Secret`进行登录。

      2. **创建AK**：如果您忘记AK，请使用登录了阿里云的目标RAM用户，进入 [用户](https://ram.console.aliyun.com/users) 界面并单击目标RAM用户，在目标用户页面单击 **创建AccessKey** 按钮，按照页面提示完成访问密钥（AccessKey）的创建。创建成功后，在弹出框单击 **下载CSV文件** 便可将访问密钥（AccessKey）保存到本地。最后，使用新生成的`AccessKey ID`和`AccessKey Secret`进行登录即可。
2. 确认OSS授权。

      1. 进入 [用户](https://ram.console.aliyun.com/users) 页面，选择目标用户后单击 **权限管理**，查看是否拥有管理OSS资源的权限。例如管理对象存储服务（OSS）权限`AliyunOSSFullAccess`。

      2. 如无管理OSS资源权限，请在目标用户 **权限管理** 页面单击 **新增授权**，在 **搜索框** 复制并添加`AliyunOSSFullAccess`、`AliyunRAMFullAccess`以及`AliyunSTSAssumeRoleAccess`权限。



         **说明**





         RAM用户授权的详细信息以及自定义授权，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "") 和 [创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy#title-3km-fsu-3en "")。
3. 单击 **AK登录**，并填写RAM用户的`AccessKey ID`和`AccessKey Secret`进行登录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2820645471/p948514.png)


1. 单击 **账号登录**。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p862179.png)

2. 单击打开 **阿里云登录页**，选择对应方式登录。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p862328.png)


**重要**

**AccessKeyID** 文本框信息符合`STS.*****`格式后， **STS Token** 文本框才显示。

1. 获取STS临时访问凭证。如何获取临时访问凭证，请参见 [使用STS临时访问凭证访问OSS](https://help.aliyun.com/zh/oss/developer-reference/use-temporary-access-credentials-provided-by-sts-to-access-oss#title-zjk-bpd-5dk "")。

2. 单击 **AK登录**，并填写临时访问凭证中`AccessKey ID`、`AccessKey Secret`和`SecurityToken`进行登录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p862162.png)


1. 获取授权码。如何生成授权码，请参见 [文件授权](https://help.aliyun.com/zh/oss/developer-reference/document-authorization-using-ossbrowser2-0#949eb71b93qo8 "")。

2. 单击 **授权码登录**，填入获取到的授权码进行登录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p862815.png)


2. ### **配置** **Endpoint**




**重要**





请注意CDN域名不支持在OSS Browser 2.0中登录 。








| **Endpoint** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **Endpoint** | **说明** |
| **外网域名** | 适用于在本地使用ossbrowser 2.0的场景，此时请选择 **外网域名**。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8768486371/p899602.png) |
| **内网域名** | 阿里云内网环境中使用，例如在ECS虚拟机上安装ossbrowser 2.0，此时请选择 **内网域名**。需注意ECS虚拟机和目标Bucket需处于同一地域，关于如何创建ECS虚拟机，请参见 [创建ECS实例](https://help.aliyun.com/zh/ecs/user-guide/use-the-ecs-instance-in-the-console#ebe7d61fcapjd "")。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8768486371/p899606.png) |
| **指定域名** | **说明**<br>通过指定域名方式登录ossbrowser客户端后，暂不支持切换至其他Bucket。<br>适用于指定域名登录的场景，例如开启传输加速器服务后，可填写 **传输加速访问域名**。关于如何开通传输加速服务并获取传输加速访问域名，请参见 [通过传输加速访问OSS](https://help.aliyun.com/zh/oss/user-guide/transfer-acceleration#title-kc6-o9j-8og "")。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8768486371/p899385.png) |
| **自定义域名** | 适用于通过自定义域名访问OSS资源的场景，需填写绑定OSS后的 **自有域名**。关于如何绑定自有域名，请参见 [绑定自定义域名](https://help.aliyun.com/zh/oss/manage-a-domain-map-custom-domain-names#concept-ozw-m2r-5fb "")。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8768486371/p899596.png) |
| **私网连接** | **说明**<br>当通过私网连接方式登录ossbrowser客户端时，需在预设OSS路径中提前指定目标Bucket，并且在客户端运行期间，暂不支持切换至其他Bucket。<br>阿里云内网环境中使用，例如已有目标ECS虚拟机，且需要建立更安全稳定的私有连接场景，需确保ECS虚拟机与终端节点处于同一VPC专有网络之下，同时，ECS虚拟机和目标Bucket要处于同一地域。<br>此处请填写 **终端节点服务域名**。关于如何创建ECS虚拟机，以及创建终端节点并获取终端节点服务域名，请参见 [创建ECS实例](https://help.aliyun.com/zh/ecs/user-guide/use-the-ecs-instance-in-the-console#ebe7d61fcapjd "") 和 [创建终端节点](https://help.aliyun.com/zh/oss/user-guide/access-oss-via-privatelink-network#384a3ac157maw "")。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8768486371/p899714.png) |
| **云盒** | **说明**<br>使用云盒Endpoint登录ossbrowser 2.0后，不支持 [文件授权](https://help.aliyun.com/zh/oss/developer-reference/document-authorization-using-ossbrowser2-0#949eb71b93qo8 "") 操作。<br>适用于访问云盒环境场景，需填写云盒的 [数据域名](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#title-cwj-sn1-1vx "") 登录ossbrowser 2.0。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8828441571/p980932.png) |

3. ### **配置预设OSS路径**


当您只拥有Bucket中某部分资源权限时，需填写OSS资源路径，示例如下：

1. 访问整个Bucket空间，例如访问`bucketname`下的所有文件。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p863230.png)

2. 访问Bucket内某个目录，例如访问`bucketname`中的`folder`目录。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p863297.png)

3. 访问Bucket内某个具体文件，例如访问`bucketname`中`folder`下的`file`文件。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p863234.png)
4. ### **配置** **Bucket地域**




**重要**





如果您需要访问特定Bucket，请先配置好预设OSS路径，再进行Bucket地域的配置。








| **Endpoint类型** | **配置方式** | **示例** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **Endpoint类型** | **配置方式** | **示例** |
| **外网域名** | 单击登录页面右上角**高级设置** \> **默认地域**，选择目标Bucket地域。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5434974471/p940978.png)![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5434974471/p940990.png) |
| **内网域名** |
| **指定域名** | 在展开的 **默认地域** 下拉列表框中，选择目标Bucket地域。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2820645471/p948517.png) |
| **自定义域名** |
| **私网连接** |

5. ### **结果验证**


完成登录后界面如图所示。快速熟悉并使用ossbrowser 2.0，请参见 [常用操作](https://help.aliyun.com/zh/oss/developer-reference/commonly-used-function-of-ossbrowser2-0#77df3848adbau "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1498900371/p863401.png)


## **更多配置**

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| **请求者付费模式** | 当授权访问的Bucket开启了请求者付费模式，且您不是该Bucket拥有者的情况下，需选中 **请求者付费模式**。单击登录页面右上角**高级设置**，在高级设置界面开启 **请求者付费模式**。<br>**重要**<br>- 当授权访问的Bucket开启请求者付费模式，而您不是其拥有者且未选中 **请求者付费模式** 时，访问预设OSS路径下指定资源会报错`AccessDenied`。<br>  <br>- 选中 **请求者付费模式** 后可正常访问预设OSS路径下的指定资源，且访问该Bucket产生的流量、请求次数等费用将由您支付。有关请求者付费模式的更多信息，请参见 [请求者付费](https://help.aliyun.com/zh/oss/user-guide/enable-pay-by-requester-1#concept-yls-jm2-2fb "")。 |
| **保持登录** | 选中 **保持登录** 后ossbrowser 2.0会保持登录状态，下次打开时将自动登录。 |
| **记录会话** | 选中 **记录会话** 后可保存AK密钥。再次登录时，单击 **AK历史**，可选择指定密钥直接登录。<br>**警告**<br>为避免不必要的信息安全风险，请勿在临时使用的电脑上选中该项。 |