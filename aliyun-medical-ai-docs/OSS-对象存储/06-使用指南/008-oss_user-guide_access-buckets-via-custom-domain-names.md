### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[访问域名与网络连接](https://help.aliyun.com/zh/oss/user-guide/access-domain-name-and-network-connection/)通过自定义域名访问OSS

# 通过自定义域名访问OSS

更新时间：2025-12-24 21:26:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过Bucket域名访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-oss-via-bucket-domain-name)[下一篇：通过HTTPS协议访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-oss-by-https-protocol)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

绑定域名至外网访问域名

步骤一：绑定域名至Bucket

步骤二：配置CNAME指向外网访问域名

步骤三：验证自定义域名访问

绑定域名至传输加速域名

步骤一：绑定域名至Bucket

步骤二：开启传输加速功能

步骤三：配置CNAME指向传输加速域名

步骤四：验证自定义域名访问

绑定域名至接入点域名

步骤一：绑定域名至接入点

步骤二：配置CNAME指向接入点域名

步骤三：验证自定义域名访问

绑定域名至对象FC接入点域名

步骤一：绑定域名至对象FC接入点

步骤二：配置CNAME指向接入点域名

步骤三：验证自定义域名访问

应用于生产环境

最佳实践

风险防范

配额与限制

常见问题

通过API绑定域名时返回NeedVerifyDomainOwnership错误怎么办？

通过加速域名访问时返回 502 或 504 错误怎么办？

访问时出现网络错误（如解析失败、连接超时）如何排查？

OSS上传或下载文件时速度很慢，怎么办？

如何控制通过自定义域名访问文件时的预览或下载行为？

绑定域名时校验失败，提示域名绑定在其他Bucket上怎么办？

为何“域名B CNAME到域名A，域名A再绑定OSS”的方式会访问失败？

配置完成后访问自定义域名无效或仍访问到旧地址？

如何使用不带签名的长期有效的URL访问OSS文件？

绑定自定义域名后，之前的文件URL是否可以继续使用？

自定义域名绑定OSS后只能用外网访问域名吗？可以绑定内网域名吗？

已经正常解析到WAF且有内容的域名可以绑定至Bucket吗？

使用自定义域名，为什么HTTPS请求不了资源文件，会强制跳转HTTPS？

OSS Bucket域名访问HTML、图片等文件时，浏览器会强制下载而非在线预览，影响用户体验。通过将自定义域名绑定至Bucket，可以使用自定义域名替代OSS Bucket域名直接访问文件，实现在线预览，并获得更灵活的访问控制能力。

**重要**

- 绑定自定义域名前，请确保已拥有一个已注册的域名或 [注册一个新域名](https://wanwang.aliyun.com/domain)。若Bucket位于中国内地，绑定的域名必须完成 [ICP备案](https://beian.aliyun.com/)。


## **工作原理**

自定义域名绑定至OSS Bucket的实现机制基于DNS的CNAME（Canonical Name）记录。通过将域名指向OSS为Bucket提供的访问地址，当用户访问自定义域名时，DNS系统将其解析到对应的OSS Bucket域名，从而实现对OSS资源的直接访问。

请根据业务需求选择相应的自定义域名绑定方式：

- **常规访问**： [绑定域名至外网访问域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#1e43238a95bb6 "")

- **跨国或远距离加速**： [绑定域名至传输加速域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#cf9eef1776h0b "")

- **精细化权限管理**： [绑定域名至接入点域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#c45d7bae542oc "")

- **服务计算触发**： [绑定域名至对象FC接入点域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#05df3f5328q6y "")


## **绑定域名至外网访问域名**

如需托管网站的图片、脚本等静态文件，可将域名绑定至外网访问域名，实现基础的文件访问和在线预览功能。

### **步骤一：绑定域名至Bucket**

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称，然后在Bucket左侧菜单栏单击**Bucket配置** \> **域名管理**。

2. 单击 **绑定域名**，输入需要绑定的域名，如`oss-example.cn`，系统将自动检测是否满足绑定条件。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006236.png)

3. 检测通过后，将域名绑定至Bucket。






直接绑定



验证域名所有权并绑定



















域名属于当前账户时，可直接进行绑定。单击 **确认绑定**，将域名绑定至Bucket。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006237.png)



域名属于其他阿里云账户或其他域名服务商时，需要先验证域名所有权才能进行绑定。以下操作以其他阿里云账户为例说明域名所有权验证并绑定的完整流程。



1. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

2. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。

      - **记录类型**：选择 **TXT**。

      - **主机记录**：填写OSS控制台显示的主机记录，如`_dnsauth`，如果绑定的是子域名，还需要加上子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`_dnsauth.image`。

      - **记录值**：填写OSS控制台显示的记录值，如`21a0****************************`。
3. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**。

4. 返回OSS控制台，单击 **验证域名所有权并绑定**，将域名绑定至Bucket。域名解析记录添加后需要一段时间才能生效，如果页面报错，请等待几分钟后重试。


**说明**

TXT记录用于验证对域名的所有权，验证成功后即可删除，不影响后续使用。

### **步骤二：配置CNAME指向外网访问域名**

将域名绑定至Bucket后，自定义域名尚未生效，需要配置CNAME解析记录将自定义域名指向 [CNAME域名](https://help.aliyun.com/zh/oss/user-guide/access-oss-via-bucket-domain-name#225165999bkuj "")（推荐）或 OSS 外网访问域名，使自定义域名生效。

**重要**

在配置自定义域名 CNAME 指向 CNAME 域名（推荐）或 OSS 外网访问域名前，请务必在控制台将该自定义域名与 OSS Bucket 进行绑定，否则会导致以自定义域名访问 OSS 时无法正确识别出 Bucket ，进而返回非预期内容的情况。同时在后续解除绑定关系后，也请务必及时删除自定义域名 CNAME 到 OSS 的指向。

自动配置

手动配置

域名属于当前账户时，绑定域名后可以直接在控制台开启 **自动添加 CNAME 记录**，系统会在阿里云域名解析处自动添加当前域名的CNAME记录。

**说明**

如果提示存在相同的主机记录导致无法自动添加CNAME记录，说明之前已为该域名创建CNAME解析记录。请登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative) 确认该CNAME记录是否还在使用，如果不再使用，可以删除后重新添加正确的CNAME解析记录。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006335.png)

当前域名已存在CNAME解析记录，或域名属于其他阿里云账户或其他域名服务商时，需要在相应的域名解析服务商配置CNAME解析。以下操作以阿里云云解析DNS为例说明CNAME解析记录的配置方法。

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket/)，单击目标Bucket名称，然后在Bucket左侧菜单栏单击 **概览**，复制 **CNAME 域名**（推荐）或 **外网访问** 右侧的 **Bucket域名**。

2. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

3. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。



**说明**





如果已存在CNAME解析记录，请单击解析记录操作列的 **修改**，将记录值修改为CNAME域名（推荐）或OSS外网域名。





   - **记录类型**：选择 **CNAME**。

   - **主机记录**：如果绑定的是主域名，填写`@`，如果绑定的是子域名，填写子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`image`。

   - **记录值**：填写CNAME域名（推荐）或外网访问域名，如`p******.cn-hangzhou.taihang***.cn`或`pub******.oss-cn-hangzhou.aliyuncs.com`。
4. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**，完成域名解析配置。


**重要**

DNS解析的生效时间取决于记录的TTL（生存时间）设置，完全生效通常需要几分钟到几小时。配置后立即访问无效属于正常现象，请耐心等待或尝试清除本地DNS缓存。

### **步骤三：验证自定义域名访问**

完成域名绑定和解析配置后，可根据Bucket的读写权限设置选择相应的验证方式。

#### **公共读和公共读写Bucket**

在浏览器中通过URL：`http://your_domain_name/object_path`访问OSS中的对象文件，其中`your_domain_name`为绑定的自定义域名，`object_path`为文件在Bucket内的访问路径。例如，文件`dest.jpg`存放在Bucket的`exampledir`目录下，则`object_path`为`exampledir/dest.jpg`。访问效果如下图所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006351.png)

#### **私有Bucket**

访问读写权限为私有的Bucket时，需要在访问文件的URL中包含签名信息。以下操作说明如何通过控制台获取文件的签名URL，关于签名的详细信息和生成方式请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls "")。

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称。

2. 单击需要访问的目标文件操作列的 **详情**。

3. 选择域名为 **自定义域名** 并在下拉框中选择绑定的自定义域名，然后单击 **复制文件URL**。

4. 在浏览器中访问URL，访问效果如下图所示。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006353.png)

## **绑定域名至传输加速域名**

当需要使用自定义域名实现Bucket远距离数据传输加速，例如从中国内地向非中国内地Bucket加速上传或下载文件时，除了将域名绑定至Bucket，还需要开启传输加速功能，并修改CNAME记录指向传输加速域名。

### **步骤一：绑定域名至Bucket**

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称，然后在Bucket左侧菜单栏单击**Bucket配置** \> **域名管理**。

2. 单击 **绑定域名**，输入需要绑定的域名，如`oss-example.cn`，系统将自动检测是否满足绑定条件。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006236.png)

3. 检测通过后，将域名绑定至Bucket。






直接绑定



验证域名所有权并绑定



















域名属于当前账户时，可直接进行绑定。单击 **确认绑定**，将域名绑定至Bucket。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006237.png)



域名属于其他阿里云账户或其他域名服务商时，需要先验证域名所有权才能进行绑定。以下操作以其他阿里云账户为例说明域名所有权验证并绑定的完整流程。



1. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

2. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。

      - **记录类型**：选择 **TXT**。

      - **主机记录**：填写OSS控制台显示的主机记录，如`_dnsauth`，如果绑定的是子域名，还需要加上子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`_dnsauth.image`。

      - **记录值**：填写OSS控制台显示的记录值，如`21a0****************************`。
3. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**。

4. 返回OSS控制台，单击 **验证域名所有权并绑定**，将域名绑定至Bucket。域名解析记录添加后需要一段时间才能生效，如果页面报错，请等待几分钟后重试。


**说明**

TXT记录用于验证对域名的所有权，验证成功后即可删除，不影响后续使用。

### **步骤二：开启传输加速功能**

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称，然后在Bucket左侧菜单栏单击**Bucket配置** \> **传输加速**。

2. 启用 **开启传输加速**，在弹出的对话框中仔细阅读开通提示，然后单击 **确定**。

3. 复制 **传输加速访问域名**。


### **步骤三：配置CNAME指向传输加速域名**

以下操作以阿里云云解析DNS为例说明CNAME解析记录的配置方法。

**重要**

在配置自定义域名 CNAME 指向 OSS 传输加速域名前，请务必在控制台将该自定义域名与 OSS Bucket 进行绑定，否则会导致以自定义域名访问 OSS 时无法正确识别出 Bucket ，进而返回非预期内容的情况。同时在后续解除绑定关系后，也请务必及时删除自定义域名 CNAME 到 OSS 的指向。

1. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

2. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。



**说明**





如果已存在CNAME解析记录，请单击解析记录操作列的 **修改**，将记录值修改为 **传输加速访问域名**。





   - **记录类型**：选择 **CNAME**。

   - **主机记录**：如果绑定的是主域名，填写`@`，如果绑定的是子域名，填写子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`image`。

   - **记录值**：填写 **传输加速访问域名**。
3. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**，完成域名解析配置。


**重要**

DNS解析的生效时间取决于记录的TTL（生存时间）设置，完全生效通常需要几分钟到几小时。配置后立即访问无效属于正常现象，请耐心等待或尝试清除本地DNS缓存。

### **步骤四：验证自定义域名访问**

完成域名绑定和解析配置后，可根据Bucket的读写权限设置选择相应的验证方式。

#### **公共读和公共读写Bucket**

在浏览器中通过URL：`http://your_domain_name/object_path`访问OSS中的对象文件，其中`your_domain_name`为绑定的自定义域名，`object_path`为文件在Bucket内的访问路径。例如，文件`dest.jpg`存放在Bucket的`exampledir`目录下，则`object_path`为`exampledir/dest.jpg`。访问效果如下图所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006351.png)

#### **私有Bucket**

访问读写权限为私有的Bucket时，需要在访问文件的URL中包含签名信息。以下操作说明如何通过控制台获取文件的签名URL，关于签名的详细信息和生成方式请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls "")。

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称。

2. 单击需要访问的目标文件操作列的 **详情**。

3. 选择域名为 **自定义域名** 并在下拉框中选择绑定的自定义域名，然后单击 **复制文件URL**。

4. 在浏览器中访问URL，访问效果如下图所示。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1006353.png)

## **绑定域名至接入点域名**

当使用接入点（Access Point）为不同的应用程序或用户组提供独立的访问控制时，可以为该接入点绑定自定义域名，从而使用更具辨识度的URL进行资源访问，实现权限隔离和管理简化。

> 绑定域名至接入点域名时，需先 [创建接入点](https://help.aliyun.com/zh/oss/user-guide/create-access-point "")。

### **步骤一：绑定域名至接入点**

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket名称，然后在Bucket左侧菜单栏单击 **接入点**。

2. 单击目标接入点名称，然后单击**接入点域名管理** \> **绑定域名**。

3. 输入域名，待绑定的域名需要先验证域名所有权才能进行绑定。以下操作以其他阿里云账户为例说明域名所有权验证并绑定的完整流程。

1. 单击 **立即验证**，查看TXT解析记录配置说明。

2. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

3. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。

      - **记录类型**：选择 **TXT**。

      - **主机记录**：填写OSS控制台显示的主机记录，如`_dnsauth`，如果绑定的是子域名，还需要加上子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`_dnsauth.image`。

      - **记录值**：填写OSS控制台显示的 **CnameToken**，如`e5cd****************************`。
4. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**。

5. 返回OSS控制台，单击 **验证域名所有权并绑定**，将域名绑定至Bucket。域名解析记录添加后需要一段时间才能生效，如果页面报错，请等待几分钟后重试。

**说明**

TXT记录用于验证对域名的所有权，验证成功后即可删除，不影响后续使用。

### **步骤二：配置CNAME指向接入点域名**

将域名绑定至接入点后，自定义域名尚未生效，需要配置CNAME解析记录将自定义域名指向接入点域名，使自定义域名生效。

**重要**

在配置自定义域名 CNAME 指向 OSS 接入点域名前，请务必在控制台将该自定义域名与 OSS 接入点进行绑定，否则会导致以自定义域名访问 OSS 时无法正确识别出 Bucket ，进而返回非预期内容的情况。同时在后续解除绑定关系后，也请务必及时删除自定义域名 CNAME 到 OSS 的指向。

1. 单击绑定的自定义域名操作列的 **域名绑定配置**，复制 **OSS访问域名** 下方的记录值。

2. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

3. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。



**说明**





如果已存在CNAME解析记录，请单击解析记录操作列的 **修改**，将记录值修改为接入点域名。





   - **记录类型**：选择 **CNAME**。

   - **主机记录**：如果绑定的是主域名，填写`@`，如果绑定的是子域名，填写子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`image`。

   - **记录值**：填写复制的记录值。
4. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**，完成域名解析配置。


**重要**

DNS解析的生效时间取决于记录的TTL（生存时间）设置，完全生效通常需要几分钟到几小时。配置后立即访问无效属于正常现象，请耐心等待或尝试清除本地DNS缓存。

### **步骤三：验证自定义域名访问**

完成CNAME解析配置后，即可通过自定义域名访问接入点服务。由于接入点不支持匿名访问，以下操作以ossutil为例介绍自定义域名的访问方式。

1. 安装并配置 [ossutil](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，配置时使用接入点授权用户的AccessKey。

2. 通过`presign`命令为目标文件`dest.jpg`生成签名URL，其中`accesspoint-test-16e9******************************-ossalias`为接入点别名。















```shell
ossutil presign oss://accesspoint-test-16e9******************************-ossalias/dest.jpg
```



执行命令后将得到如下签名URL：















```shell
https://accesspoint-test-16e9******************************-ossalias.oss-ap-northeast-1.aliyuncs.com/dest.jpg?x-oss-credential=LTAI********************%2F20250916%2Fap-northeast-1%2Foss%2Faliyun_v4_request&x-oss-date=20250916T121842Z&x-oss-expires=900&x-oss-signature=f3b4************************************************************&x-oss-signature-version=OSS4-HMAC-SHA256
```

3. 将签名URL中的接入点访问域名，如`accesspoint-test-16e9******************************-ossalias.oss-ap-northeast-1.aliyuncs.com`，替换为自定义域名。

4. 通过浏览器访问修改后的签名URL，访问效果如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1007482.png)


## **绑定域名至对象FC接入点域名**

当使用对象FC接入点将OSS与函数计算（Function Compute）集成，以实现数据触发处理时，可以为该接入点绑定自定义域名，以便通过友好的URL触发函数调用，实现事件驱动的无服务器数据处理架构。

> 绑定域名至对象FC接入点域名时，需先 [创建对象FC接入点](https://help.aliyun.com/zh/oss/user-guide/create-object-fc-access-point "")。

### **步骤一：绑定域名至对象FC接入点**

1. 前往 [对象FC接入点列表](https://oss.console.aliyun.com/fc-access-point)，单击目标对象FC接入点对应的 **支持接入点** 名称。

2. 单击**接入点域名管理** \> **绑定域名**。

3. 输入域名，待绑定的域名需要先验证域名所有权才能进行绑定。以下操作以其他阿里云账户为例说明域名所有权验证并绑定的完整流程。

1. 单击 **立即验证**，查看TXT解析记录配置说明。

2. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

3. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。

      - **记录类型**：选择 **TXT**。

      - **主机记录**：填写OSS控制台显示的主机记录，如`_dnsauth`，如果绑定的是子域名，还需要加上子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`_dnsauth.image`。

      - **记录值**：填写OSS控制台显示的 **CnameToken**，如`e5cd****************************`。
4. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**。

5. 返回OSS控制台，单击 **验证域名所有权并绑定**，将域名绑定至Bucket。域名解析记录添加后需要一段时间才能生效，如果页面报错，请等待几分钟后重试。

**说明**

TXT记录用于验证对域名的所有权，验证成功后即可删除，不影响后续使用。

### **步骤二：配置CNAME指向接入点域名**

将域名绑定至接入点后，自定义域名尚未生效，需要配置CNAME解析记录将自定义域名指向接入点域名，使自定义域名生效。

**重要**

在配置自定义域名 CNAME 指向 OSS 接入点域名前，请务必在控制台将该自定义域名与 OSS 接入点进行绑定，否则会导致以自定义域名访问 OSS 时无法正确识别出 Bucket ，进而返回非预期内容的情况。同时在后续解除绑定关系后，也请务必及时删除自定义域名 CNAME 到 OSS 的指向。

1. 单击绑定的自定义域名操作列的 **域名绑定配置**，复制 **OSS访问域名** 下方的记录值。

2. 使用域名归属的阿里云账号登录 [云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)，单击目标域名操作列的 **解析设置**。

3. 单击 **添加记录**，按照下方配置列表填写记录信息，其余配置项可保持默认设置。



**说明**





如果已存在CNAME解析记录，请单击解析记录操作列的 **修改**，将记录值修改为接入点域名。





   - **记录类型**：选择 **CNAME**。

   - **主机记录**：如果绑定的是主域名，填写`@`，如果绑定的是子域名，填写子域名前缀，如绑定`image.oss-example.cn`，则主机记录填写`image`。

   - **记录值**：填写复制的记录值。
4. 单击 **确定**，然后在弹出的 **解析变更确认** 窗口，再次单击 **确定**，完成域名解析配置。


**重要**

DNS解析的生效时间取决于记录的TTL（生存时间）设置，完全生效通常需要几分钟到几小时。配置后立即访问无效属于正常现象，请耐心等待或尝试清除本地DNS缓存。

### **步骤三：验证自定义域名访问**

完成CNAME解析配置后，即可通过自定义域名访问对象FC接入点服务。由于接入点不支持匿名访问，以下操作以ossutil为例介绍自定义域名的访问方式。

1. 安装并配置 [ossutil](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，配置时使用接入点授权用户的AccessKey。

2. 通过`presign`命令为目标文件`dest.jpg`生成签名URL，其中`accesspoint-test-16e9******************************-ossalias`为接入点别名。















```shell
ossutil presign oss://accesspoint-test-16e9******************************-ossalias/dest.jpg
```



执行命令后将得到如下签名URL：















```shell
https://accesspoint-test-16e9******************************-ossalias.oss-ap-northeast-1.aliyuncs.com/dest.jpg?x-oss-credential=LTAI********************%2F20250916%2Fap-northeast-1%2Foss%2Faliyun_v4_request&x-oss-date=20250916T121842Z&x-oss-expires=900&x-oss-signature=f3b4************************************************************&x-oss-signature-version=OSS4-HMAC-SHA256
```

3. 将签名URL中的接入点访问域名，如`accesspoint-test-16e9******************************-ossalias.oss-ap-northeast-1.aliyuncs.com`，替换为自定义域名。

4. 通过浏览器访问修改后的签名URL，访问效果如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6018808571/p1007482.png)


## **应用于生产环境**

### **最佳实践**

- **安全传输：启用HTTPS**

为自定义域名 [配置SSL证书](https://help.aliyun.com/zh/oss/user-guide/access-oss-by-https-protocol#section-evp-h0m-z2e "")，强制使用HTTPS访问。HTTPS协议通过TLS/SSL加密传输数据，防止数据在传输过程中被窃取或篡改，避免浏览器显示不安全警告，提升用户信任度和品牌形象。

- **跨域访问：配置CORS规则**

当前端应用（如部署在`https://web.example.cn`）需要访问OSS资源（如`https://oss.example.cn`）时，必须 [配置CORS跨域规则](https://help.aliyun.com/zh/oss/user-guide/configure-cross-origin-resource-sharing/ "")，允许来自应用域名的跨域请求。CORS规则通过HTTP头控制跨域访问权限，确保前端应用正常访问OSS资源，同时防止未授权的跨域请求。

- **平滑上线：零停机域名切换**

当需要将Bucket域名切换到绑定的自定义域名时，采用以下分阶段切换策略可避免服务中断，确保业务连续性。

1. **准备阶段**：将自定义域名绑定至Bucket并完成CNAME解析规则设置。在测试环境中，使用`hosts`文件或测试域名完整验证新配置的自定义域名功能和性能，确保所有功能正常运行。

2. **灰度发布阶段（建议在业务低峰期）**：采用灰度发布的方式将部分业务流量切换至自定义域名，通过逐步放量降低切换风险。

3. **验证阶段**：密切监控业务访问日志和错误率，分析响应时间、成功率等关键指标，确保灰度发布服务正常且业务运行平稳。

4. **全量发布阶段**：经过充分验证后，将全量业务流量切换至自定义域名，完成域名迁移。

5. **回滚预案**：如遇问题，立即回滚至Bucket域名，并详细分析问题根因后重新部署。
- **性能与安全：通过子域名隔离用途**

根据不同业务用途分配不同子域名，如网页静态资源使用`static.example.com`，图片资源使用`images.example.com`。通过域名隔离实现浏览器并发连接数优化（绕过单域名并发限制）、独立缓存策略配置、精细化权限控制和安全策略部署，提升访问速度并增强整体安全性。

- **功能扩展：托管静态网站**

如果目标是利用OSS托管完整的静态网站（包含HTML、CSS、JS等文件），在绑定自定义域名后，还需进一步配置 [静态网站托管](https://help.aliyun.com/zh/oss/user-guide/hosting-static-websites "") 功能，实现默认首页、404错误页面等网站基础功能。

- **性能优化：配置CDN加速**

对于需要向全球用户分发静态资源的场景，建议在自定义域名的基础上，进一步配置 [CDN加速](https://help.aliyun.com/zh/oss/user-guide/cdn-acceleration "") 服务，通过全球分布的边缘节点缓存内容，获得更低的访问延迟、更高的并发能力和更优的用户体验。


### **风险防范**

- **流量盗用防护：配置Referer防盗链**

为防止图片、视频等资源被其他网站盗用，产生不必要的流量费用和带宽消耗，请 [使用防盗链策略避免非法流量盗用](https://help.aliyun.com/zh/oss/user-guide/hotlink-protection/ "")。通过白名单机制限制访问来源，有效控制成本并保护资源不被滥用。

- **行为审计与排障：启用访问日志**

启用OSS [实时日志查询](https://help.aliyun.com/zh/oss/user-guide/real-time-log-query/ "")，记录所有访问请求的详细信息，包括访问时间、来源IP、请求类型、响应状态等，便于安全审计、性能分析、异常排查和业务运营决策支持。


## **配额与限制**

- **绑定数量**：每个Bucket最多可以绑定100个自定义域名。

- **域名唯一性**：一个自定义域名在同一时间只能绑定到一个实体（Bucket、接入点）。如需改绑，必须先从原实体解绑，确保域名指向的唯一性和访问路径的明确性。



**说明**





对于部分使用旧版图片处理功能的用户，已用于图片处理的域名不能再绑定到Bucket。新版图片处理功能无此限制。

- **域名类型**：不支持绑定中文域名和泛域名（如 `*.example.cn`），确保DNS解析的稳定性和兼容性。



**说明**





通过CDN加速OSS时，允许绑定泛域名，但该域名不会在OSS管理控制台显示。

- **顶级域名要求**：绑定的自定义域名中涉及的顶级域名必须满足指定后缀的要求，否则会被视为无效域名，最终导致域名绑定失败。更多信息，请参见 [顶级域名分类解析](https://help.aliyun.com/zh/dws/product-overview/top-level-domain-name-suffix-list "")。


## **常见问题**

### **通过API绑定域名时返回**`NeedVerifyDomainOwnership` **错误怎么办？**

此错误明确指出未验证域名所有权。可通过以下方式验证域名所有权：

1. 调用 [CreateCnameToken](https://help.aliyun.com/zh/oss/developer-reference/createcnametoken#reference-2210351 "") 接口创建域名所有权验证所需的`CnameToken`。



**说明**





`CnameToken`默认在创建完成后72小时内过期。如果在过期时间内重复创建，则返回已存在的`CnameToken`。

2. 参照前述文档说明，在域名服务提供商处配置TXT记录完成域名所有权验证。

3. 调用 [PutCname](https://help.aliyun.com/zh/oss/developer-reference/putcname#reference-2210550 "") 接口绑定自定义域名。


### **通过加速域名访问时返回**`502` **或**`504` **错误怎么办？**

此问题通常是OSS传输加速的 **自动路径切换** 机制导致的正常现象。为应对远距离传输中的网络波动和链路质量变化，该服务会动态选择最优传输路径，在路径切换瞬间可能导致少量请求中断并返回`502/504`错误。这种情况无法完全避免，建议在客户端代码中实现指数退避的重试逻辑来提升访问成功率。

### **访问时出现网络错误（如解析失败、连接超时）如何排查？**

如果请求OSS时收到了响应，只需 [获取Request ID](https://help.aliyun.com/zh/oss/user-guide/obtain-request-ids "")，打开 [OSS自助诊断工具](https://oss.console.aliyun.com/tools/diagnose) 进行问题诊断检测即可。

如果请求没有到达OSS服务器就发生了中断，即`Request ID`为空，可按以下步骤排查：

- **Connection refused：** 此错误通常表示客户端与OSS同地域但端口不通，或跨地域使用了内网Endpoint。请检查并使用正确的外网Endpoint访问，同时使用`ping`和`telnet`命令检查客户端防火墙设置或网络连通性限制。

- **ConnectionTimeOut：** 通常由网络环境不佳或超时设置过短导致。建议适当增大SDK中的连接超时和读取超时时间并开启失败重传机制。对于大文件传输，应使用 [分片上传](https://help.aliyun.com/zh/oss/user-guide/multipart-upload "") 和 [断点续传上传](https://help.aliyun.com/zh/oss/user-guide/resumable-upload "") 提升传输稳定性。若为网络链路问题，可考虑使用CDN或OSS传输加速服务。

- **Socket timeout or Socket closed：** 表示与OSS的连接超时或被异常关闭。请在SDK配置中增大Socket超时时间（例如Java SDK的`ClientConfiguration.setSocketTimeout`方法）。

- **Connection reset：** 连接被重置的原因多样（如Endpoint配置错误、Bucket因安全原因被限制访问等）。请依次排查：

1. 使用`ping`或 [阿里昆仑诊断工具](https://cdn.dns-detect.alicdn.com/https/doc.html) 检查客户端网络连通性是否正常。

2. 确认代码中配置的Endpoint准确无误且包含正确的协议头（`http://`或`https://`）。

3. 确认Bucket未因安全攻击或违规内容被置入 [OSS沙箱](https://help.aliyun.com/zh/oss/user-guide/oss-sandbox "") 限制访问状态。

4. 若问题依旧，请使用Wireshark等工具抓包后联系[技术支持](https://selfservice.console.aliyun.com/ticket/createIndex)进行深入排查。

### **OSS上传或下载文件时速度很慢，怎么办？**

OSS的传输速度主要受客户端本地网络带宽、网络链路质量和传输策略配置影响。

- **通用排查**：首先，确认当前带宽使用未达到Bucket的 [带宽限制](https://help.aliyun.com/zh/oss/user-guide/limits "") 上限。其次， [使用MTR工具进行网络链路分析](https://help.aliyun.com/zh/ecs/user-guide/use-mtr-tool-for-network-analysis#fb02c53042ekt "") 检查是否存在丢包、高延迟或路由异常。对于跨国或远距离传输场景，强烈建议 [开启并使用传输加速](https://help.aliyun.com/zh/oss/user-guide/transfer-acceleration#section-gtt-hyd-vba "") 服务优化网络路径。

- **工具优化**：推荐使用 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "") 进行大文件或大量文件的传输。使用其`probe`命令可检测当前网络状态。

- **SDK优化**：对于大文件，务必使用 [分片上传](https://help.aliyun.com/zh/oss/user-guide/multipart-upload "") 和 [断点续传上传](https://help.aliyun.com/zh/oss/user-guide/resumable-upload "") 功能，并合理配置分片大小`part_size`和并发线程数`num_threads`。在网络情况良好时，可适当增大分片大小以减少请求次数。此外，在初始化SDK客户端时关闭CRC64校验（如Python中设置`enable_crc=False`），并在请求头中增加`Content-MD5`进行数据完整性校验，可在保证数据安全的前提下提升传输性能。


### **如何控制通过自定义域名访问文件时的预览或下载行为？**

文件的预览或下载行为由HTTP响应头`Content-Disposition`决定。核心机制在于：使用OSS Bucket域名访问时，OSS会为安全起见强制添加`Content-Disposition: attachment`下载头；而 **通过自定义域名访问时，OSS则不会添加此头**，从而使行为变得可控。

- **实现预览**：确保文件元数据中 **没有** 设置`Content-Disposition: attachment`并确保文件的`Content-Type`（MIME类型）正确匹配文件格式。对于浏览器原生不支持预览的文件格式，可通过以下方式扩展预览能力：

  - 对于.doc、.ppt、.pdf等办公文件，集成 [WebOffice在线预览](https://help.aliyun.com/zh/oss/user-guide/online-object-preview "") 服务实现文档预览。

  - 对于.mov等特殊格式视频文件，使用 [视频转码](https://help.aliyun.com/zh/oss/user-guide/video-transcoding "") 服务转换为Web兼容格式后实现预览。

  - 安装对应文件类型的浏览器预览插件。
- **强制下载**：为文件的元数据手动设置`Content-Disposition`为`attachment`，浏览器将忽略预览尝试并直接下载文件。



**说明**





`<video>`或`<audio>`标签会优先播放媒体，可能会忽略`attachment`的下载建议。


### **绑定域名时校验失败，提示域名绑定在其他Bucket上怎么办？**

遇到域名已被其他Bucket绑定的情况，可采用以下两种解决方案：

- 为当前业务使用一个新的子域名。如子域名`oss-example.cn`已被其他Bucket绑定，可使用`static.oss-example.cn`等新的子域名进行绑定，通过域名层级实现业务隔离。

- 将域名从原有Bucket解绑，再绑定到目标Bucket。解绑操作步骤如下：

1. 如果已开启CDN加速，需要先修改CDN加速服务的源站信息，使加速域名不再指向OSS的Bucket域名，避免CDN回源失败。修改方式请参见 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server "")。

2. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击原有绑定的Bucket名称，然后在Bucket左侧菜单栏单击**Bucket配置** \> **域名管理**。

3. 在域名列表中单击目标域名操作列的 **解绑**，在弹出的对话框中单击 **确定**，完成域名解绑。

### **为何“域名B CNAME到域名A，域名A再绑定OSS”的方式会访问失败？**

因为OSS会严格校验HTTP请求头中的`Host`字段，要求其必须与Bucket中实际绑定的域名（域名A）完全一致。当访问域名B时，`Host`头为"域名B"，与绑定域名不匹配导致校验失败。因此，必须将实际公网访问的域名（域名B）直接绑定到Bucket，而不能通过域名间的CNAME转发实现。

### **配置完成后访问自定义域名无效或仍访问到旧地址？**

这很可能是由于本地及运营商DNS缓存导致的解析延迟。建议等待十分钟后再尝试。

为提升解析效率，DNS系统各层级节点会依据TTL（Time-To-Live）值将域名解析结果缓存一段时间。当CNAME记录变更后，若缓存尚未过期，访问请求仍可能被指向旧的地址。请尝试清除本地DNS缓存，或等待缓存自动刷新后重试。不同操作系统清除本地DNS缓存的方式如下：

Windows

macOS

Linux

```shell
ipconfig /flushdns
```

```shell
 sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

```shell
 sudo systemd-resolve --flush-caches
```

### **如何使用不带签名的长期有效的URL访问OSS文件？**

实现长期有效URL访问有以下两种方式：

- [设置文件为公共读](https://help.aliyun.com/zh/oss/user-guide/object-acl#concept-blw-yqm-2gb "")：文件将可被任何人无限制访问。为防止资源被恶意盗用产生额外费用，务必在OSS中配置 [防盗链](https://help.aliyun.com/zh/oss/user-guide/hotlink-protection/ "") 策略限制访问来源。

- [通过CDN加速访问OSS](https://help.aliyun.com/zh/cdn/use-cases/accelerate-the-retrieval-of-resources-from-an-oss-bucket-in-the-alibaba-cloud-cdn-console "")：保持OSS文件的权限为私有，通过开启CDN的私有Bucket回源功能提供公共读访问。CDN可提供更好的访问性能和缓存能力，为防止资源被盗用，需要在CDN层面配置 [防盗链](https://help.aliyun.com/zh/cdn/user-guide/configure-a-referer-whitelist-or-blacklist-to-enable-hotlink-protection "") 规则。


### **绑定自定义域名后，之前的文件URL是否可以继续使用？**

可以继续使用。绑定自定义域名不会影响原有的OSS Bucket域名访问方式，两者可以并存。获取之前的文件URL方法，请参见 [使用预签名URL下载文件](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects "")。

### **自定义域名绑定OSS后只能用外网访问域名吗？可以绑定内网域名吗？**

自定义域名绑定OSS后，只能用于公网（外网）访问，不能用于内网访问。

OSS的自定义域名功能是通过在DNS服务商处配置CNAME记录，将您的自有域名指向OSS Bucket的外网Endpoint（如 `examplebucket.oss-cn-hangzhou.aliyuncs.com`）来实现的。该机制设计初衷是面向公网用户通过自有域名访问OSS资源。

而内网访问必须使用阿里云提供的内网Endpoint（如 `oss-cn-hangzhou-internal.aliyuncs.com`），且仅限于与OSS同地域的阿里云资源（如ECS、函数计算等）在VPC内通过私网调用。由于内网Endpoint不支持被外部DNS解析，也无法通过CNAME绑定到自定义域名，因此无法将自定义域名用于内网访问。

### **已经正常解析到WAF且有内容的域名可以绑定至Bucket吗？**

可以绑定。WAF（Web应用防火墙）与OSS的CNAME解析在不同的网络层面工作，两者功能互不冲突。WAF主要负责应用层安全防护，而CNAME解析负责域名指向，可以同时配置。将WAF接入OSS的具体方法，请参见 [CDN回源OSS私有Bucket场景下串接WAF最佳实践](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/use-cases/best-practice-of-concatenating-waf-in-cdn-back-to-source-oss-private "")。

### **使用自定义域名，为什么HTTPS请求不了资源文件，会强制跳转HTTPS？**

这是因为您在自定义域名上开启了强制HTTPS跳转功能，导致所有HTTP请求被自动重定向为HTTPS请求。

OSS 本身不支持强制跳转，但当您通过CDN绑定自定义域名并配置了HTTPS证书后，可在CDN的HTTPS配置中开启强制跳转（HTTP → HTTPS），此时系统会返回 301/302 重定向响应，使浏览器将HTTP请求转为HTTPS。

如果您希望允许HTTP访问资源文件，请进入CDN控制台，找到对应域名，将 **跳转类型** 改为 **默认**（即同时支持HTTP和HTTPS）。具体操作，请参见 [配置强制跳转](https://help.aliyun.com/zh/cdn/user-guide/configure-url-redirection "")。