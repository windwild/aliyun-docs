### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 验证域名归属权

# 验证域名归属权

更新时间：2025-12-22 01:39:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

方法一：DNS解析验证（推荐）

方法二：文件验证

常见问题

您首次将一个域名添加到CDN系统中时，需要完成域名归属权验证。验证通过后您再次添加该域名或子域名时，无需再次验证。

验证域名归属权

## 方法一：DNS解析验证（推荐）

本文以加速域名`image.example.com`为例，为您介绍如何通过DNS解析验证来验证域名归属权。

1. 在验证页面，单击 **方法1：DNS解析验证**，获取主机记录、记录值。





**重要**





在验证完成前请不要关闭验证页面。DNS解析验证偶尔会出现验证失败的情况，您还可以尝试使用 **方法二：文件验证**。







![DNS解析验证](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2109057961/p581805.png)

2. 在您的域名解析服务商，添加 **TXT** 记录。



下文以阿里云的云解析为例介绍如何添加 **TXT** 记录，在其他域名解析服务商（例如：腾讯云、新网等）的配置方法类似。



1. 登录[云解析DNS控制台](https://dns.console.aliyun.com/)。

2. 在 **公网权威解析** 页面，找到加速域名的根域名`example.com`，并单击右侧的 **解析设置**。

3. 单击 **添加记录**， **记录类型** 选择为 **TXT**，填写步骤1中阿里云CDN提供的 **主机记录**、 **记录值**，其余参数保持默认即可。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2855836671/p1037029.png)

4. 单击 **确定**，完成添加。
3. 等待TXT解析生效，返回CDN控制台，单击 **点击验证**，完成验证。



如果系统提示“验证失败”，请检查TXT记录是否正确填写，并等待DNS记录生效后重新验证。



以加速域名`image.example.com`为例，检查TXT记录是否正确方法：





**说明**





   - 域名首次配置TXT解析记录后将会实时生效，修改TXT解析记录通常会在10分钟后生效（具体生效时间长短取决于域名DNS解析配置的TTL时长，默认为10分钟）。

   - 如果Linux系统没有安装nslookup命令程序，centos系：`yum install bind-utils`Ubuntu系：`apt-get install dnsutils` 执行命令自动安装。


Windows系统

Linux系统

在系统内打开cmd命令界面，输入`nslookup -type=TXT verification.example.com`，根据当前的TXT结果，可以查看解析记录是否生效或正确。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3336734171/p795450.png)

在命令界面内，输入`nslookup -type=TXT verification.example.com`，根据当前的TXT结果，可以查看解析记录是否生效或正确。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3336734171/p795449.png)

## 方法二：文件验证

1. 在验证页面，单击 **方法2: 文件验证**。



**重要**





在验证完成前请不要关闭验证页面。





![文件验证](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4512768761/p581806.png)

2. 单击`verification.html`，下载验证文件。

3. 手动将验证文件上传到您主域名服务器（例如您的ECS、OSS、CVM、COS、EC2等）的根目录。例如：当前加速域名为`image.example.com`，您需要将该文件上传至 `example.com` 的根目录下。

4. 确保可通过`http://example.com/verification.html`访问到该文件后，即可 **点击验证** 进行验证。



阿里云CDN后台将访问您服务器中`http://example.com/verification.html`文件链接进行验证。



   - 如果文件内的记录值与验证文件记录值一致，则通过验证。

   - 如果验证失败，请确保上述文件链接可访问，并且您上传的文件正确。


## 常见问题

在添加新的加速域名时，您可能会遇到如下问题：

- Q：为什么要做域名归属权验证？






A：为了确保域名只被真正的拥有者添加，避免出现用户A的域名被用户B添加导致域名冲突及安全隐患问题。

- Q：我有多个阿里云账号，每个账号首次添加新域名时都要做归属权验证吗？






A：是的。多个账号视为多个不同的独立用户，每个账号都需要对新域名进行一次归属权验证。

- Q：我已完成DNS验证或文件验证，是否可以删除用作验证的DNS记录或文件？






A：可以。要求您添加的DNS解析或文件，只用作添加域名时的归属权验证，验证通过后您可以删除记录或文件。

- Q：已经添加到阿里云CDN控制台的存量域名，需要做域名归属权验证吗？






A：不需要。例如您已经添加了example.aliyundoc.com，且配置了CDN分配的CNAME在正常使用中，则视为您拥有aliyundoc.com的解析权。您后续再添加\*\*.aliyundoc.com、\*\*\*.aliyundoc.com等任意aliyundoc.com的子域名，都无需再验证。

- Q：通过API接口AddCdnDomain添加域名是否需要域名归属权验证？






A：需要。和控制台添加一样，您可以选择DNS解析验证或文件验证，先配置好DNS或在源站根目录放置好验证文件，然后调用AddCdnDomain接口添加加速域名。

- Q：我无法完成DNS验证或文件验证，怎么办？






A：您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)说明无法完成域名归属权验证的原因，并提交可以证明您持有该域名的资料，我们将进行人工审核。