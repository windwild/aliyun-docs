### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[快速入门](https://help.aliyun.com/zh/cdn/getting-started/)快速接入阿里云CDN

# 快速接入阿里云CDN

更新时间：2026-01-18 21:48:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：新手指引](https://help.aliyun.com/zh/cdn/getting-started/getting-started)[下一篇：CDN概览页](https://help.aliyun.com/zh/cdn/user-guide/cdn-overview-dashboard)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

阿里云CDN是如何帮助加速的

一、基本的请求过程

二、引入阿里云CDN的请求过程

快速接入阿里云CDN

一、添加域名和源站

二、推荐配置

三、配置CNAME

四、资源预热

五、验证阿里云CDN缓存是否生效

参考文档

本文将通过直观的示例，详细介绍阿里云CDN的工作机制，以及配置过程中所需的关键设置及其功能。旨在帮助您更高效、快捷地完成阿里云CDN服务的配置与启用。

**说明**

本文以`www.example.com`作为示例中用户访问的域名，`10.10.10.1`作为示例中域名对应的服务器IP。

## **阿里云CDN是如何帮助加速的**

如果您对阿里云CDN的工作原理尚不明确，建议您花费两分钟时间阅读“阿里云CDN是如何帮助加速的”这一部分内容。当然，如果您已掌握CDN的原理，您可以直接跳过该部分，开始进行阿里云CDN的配置。

阿里云CDN是如何帮助加速的

当我们通过浏览器输入一个URL时，最终会在屏幕上显示一个网页、一段视频、一首音乐或一张图片。这一过程背后涉及了多种软件和硬件的解析与转发操作，实际上相当复杂。接下来，本文将通过一个简单的请求示例，介绍阿里云CDN是如何在这个请求流程中起到加速作用的。

### **一、基本的请求过程**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1880978671/CAEQURiBgICD5PKjmhkiIDYzNjEzMGNkY2U4MDQxNzBhNDNlNmU5MzJjNmE2NDll4745623_20241105103251.122.svg)

现在，我们希望通过访问`www.example.com`这一域名获取一张图片。然而，浏览器无法直接通过该域名定位到图片所在服务器的地址。在这种情况下，浏览器首先需要访问DNS服务器，以获取与该域名对应的IP地址`10.10.10.1`。接着，浏览器将通过该IP地址找到相应的服务器，最终从服务器中获取所需的图片。

**说明**

- 域名可以比作一个人的名字，而IP则可视为一个人的地址。当我们希望找到某个个体时，需通过其名字获取相应的地址，进而通过该地址找到此人。网络请求的过程与此场景高度相似。

- DNS服务器可以理解为一个存储域名和IP映射关系的大型数据库。更多关于DNS服务器和域名的信息，敬请参考 [DNS基本概念](https://help.aliyun.com/zh/dns/basic-concepts "")。


### **二、引入阿里云CDN的请求过程**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1880978671/CAEQURiBgIDV3_ejmhkiIDY2ZTE1NThiMDM3YjQzOWVhMjdlNjNmYWUwOGZiYWUw4745623_20241105112446.830.svg)

随着越来越多的用户通过`www.example.com`这一域名访问图片，访问请求的数据量不断增加。由于服务器配置、网络环境等多种因素的影响，图片的访问速度将日益变慢。在此背景下，阿里云CDN作为一种有效的解决方案，能够显著加速请求速度。

阿里云CDN可视作一个庞大的缓存服务，该服务在网络拓扑逻辑中位于服务器和用户之间（图中紫色部分就是引入的阿里云CDN）。当用户发起请求并到达阿里云CDN时，系统将首先查询是否存在对应的缓存图片。如果缓存中存在该图片，则将直接返回缓存的图片给浏览器，而无需访问服务器；若缓存中不存在对应的图片，则会通过阿里云CDN向服务器发起请求，获取到图片后返回给用户，并且将其存储在阿里云CDN中，以便于下一个访问该图片的请求能够快速获取。

**说明**

- 加速请求的访问速度只是阿里云CDN的基础功能，更多关于阿里云CDN的介绍和高阶功能，敬请参见 [什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn "")。

- 阿里云CDN是在目标服务器的架构之外进行加速，对目标服务器不会产生任何侵入，也无需修改任何业务代码。

- 正常的请求流程远比上述流程复杂，此处为了方便用户理解阿里云CDN的工作原理，简化了大部分的细节。


## 快速接入 **阿里云CDN**

阿里云CDN的一大核心优势在于其 **对服务器的非侵入性**，用户无需修改任何业务代码，只需通过简单的几步配置即可快速实现内容加速。接下来，本文将以两个典型场景为例，详细讲解阿里云CDN的配置流程，并解读每个配置项的具体作用，帮助您轻松上手。如果您更倾向于视频学习，也可以直接观看我们的 [快速入门](https://help.aliyun.com/zh/cdn/videos/quick-start/ "")，跟随步骤一步步完成配置。

**说明**

在正式开始接入阿里云CDN之前，需要先完成以下两个步骤：

1. 您需要拥有一个阿里云账号并完成 [实名认证](https://account.console.aliyun.com/#/auth/home)，如果您尚未注册阿里云账号，可以通过 [账号注册](https://account.aliyun.com/register/register.htm) 页面完成注册。

2. 在阿里云账号中 [开通CDN服务](https://help.aliyun.com/zh/cdn/activate-alibaba-cloud-cdn "")。


### **一、添加域名和源站**

1. #### **配置域名**


为了使您的域名享受到加速服务，需要将您的域名作为 **加速域名** 配置在阿里云CDN里。只有完成这一步骤，阿里云CDN才能识别并加速您配置的域名。



**添加域名**






1. [CDN控制台](https://cdn.console.aliyun.com/)

2. 在左侧导航栏，单击 **域名管理**。

3. 单击 **添加域名**，配置 **加速区域**、 **加速域名** 和 **业务类型**，其他参数均可保持默认。

      ![添加加速域名-cn.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2570262371/p869139.jpg)


**说明**

   - **加速域名** 是指接入阿里云CDN、用于加速的网站域名或资源域名，也是终端用户实际访问的域名。在上述示例的场景下，此处填写`www.example.com`。

   - **加速区域** 请根据 [加速区域](https://help.aliyun.com/zh/cdn/user-guide/change-the-accelerated-region "") 的描述，选择合适自身业务的区域，本次演示选择**仅中国内地**作为加速区域。当加速区域包含 **中国内地** 时，域名必须进行 [ICP备案](https://help.aliyun.com/zh/icp-filing/basic-icp-service/user-guide/icp-filing-application-overview "")，否则域名无法正常访问。

   - **业务类型** 根据 [应用场景](https://help.aliyun.com/zh/cdn/product-overview/scenarios "") 的描述，选择适合您自身业务的场景，本次演示选择 **图片小文件**。

   - 当 **加速区域** 为 **全球（不包含中国内地）** 时，可以开启 **全球资源计划**。开启后，您的域名可以享受更丰富的节点资源，但是支持的功能会受到限制，请查看 [开启全球资源计划后支持的配置功能](https://help.aliyun.com/zh/cdn/user-guide/configure-global-resource-planning#3d759eb014mqy "")，谨慎评估之后使用。


2. #### **验证域名归属权**


为了确保您添加的域名确实归您所有，阿里云CDN需要进行域名归属权验证。如果您之前已经完成过该验证，或在配置加速域名时没有收到验证提示，可以跳过此步骤。



**验证域名归属权**








**重要**





不论选择哪种验证方法，在验证完成之前，请不要关闭验证页签。











DNS解析验证（推荐）



文件验证



















1. 在添加域名页面的验证页签，单击 **方法1：DNS解析验证**，获取主机值、记录值。


      ![归属权-cn.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2570262371/p869245.jpg)

2. 在您的域名解析服务商处，添加TXT记录（以下以阿里云的云解析为例介绍TXT记录的添加方法，其他域名解析服务商（例如：腾讯云、新网等）的配置方法类似）。



      **配置TXT记录**






      2. 登录[云解析DNS控制台](https://dnsnext.console.aliyun.com/authoritative)。

      3. 在 **公网权威解析** 页面，找到加速域名的主域名`example.com`，并单击右侧的 **解析设置**。

      4. 单击 **添加记录**， **记录类型** 选择为 **TXT**，填写步骤1中阿里云CDN提供的 **主机记录**、 **记录值**，其余参数保持为默认填写即可。

         ![txt-cn.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2570262371/p869321.jpg)


      2. 单击 **确定**，完成添加。


**说明**

您可以参考 [域名基本概念](https://help.aliyun.com/zh/dns/basic-concepts "")，快速了解主域名和子域名的相关定义与区别。

3. 等待TXT解析生效，返回CDN控制台的验证页签，单击 **点击验证**，完成验证。


      如果系统提示“验证失败”，请检查TXT记录的填写是否正确，并在DNS记录生效后重新进行验证。




      **检查TXT记录是否生效**






      以加速域名`www.example.com`为例，检查TXT记录是否生效或正确的方法如下：







      Windows系统



      macOS/Linux系统



















      在系统内打开cmd命令界面，输入nslookup -type=TXT verification.example.com，根据当前的TXT结果，可以查看解析记录是否生效或正确。



      ![image](<Base64-Image-Removed>)



      在命令界面内，输入nslookup -type=TXT verification.example.com，根据当前的TXT结果，可以查看解析记录是否生效或正确。



      ![image](<Base64-Image-Removed>)





      **说明**





      - 在nslookup命令中，类型是TXT，验证的域名则是将原域名的主机名替换为verification。例如，如果您的加速域名是`www.example.com`，那么您需要验证的域名则是`verification.example.com`。

      - 域名首次配置TXT解析记录后将会实时生效，修改TXT解析记录通常会在10分钟后生效（具体生效时间长短取决于域名DNS解析配置的TTL时长，默认为10分钟）。

      - 如果Linux系统没有安装nslookup命令程序，centos系：yum install bind-utils；Ubuntu系：apt-get install dnsutils 执行命令自动安装。


1. 在验证页面，单击 **方法2: 文件验证**。

      ![txt2-cn.jpg](<Base64-Image-Removed>)

2. 单击`verification.html`，下载验证文件。

3. 手动将验证文件上传到您主域名服务器（例如您的ECS、OSS、CVM、COS、EC2等）的根目录。例如：当前加速域名为`www.example.com`，您需要将该文件上传至 `example.com` 的根目录下。

4. 确保可通过`http://example.com/verification.html`访问到该文件后，即可 **点击验证** 进行验证.



      阿里云CDN后台将访问您服务器中`http://example.com/verification.html`文件链接进行验证。



      - 如果文件内的记录值与验证文件记录值一致，则通过验证。

      - 如果验证失败，请确保上述文件链接可访问，并且您上传的文件正确。


3. #### **配置源站信息**


源站是指您运行业务的网站服务器。您需要在阿里云CDN中配置源站信息，以便在阿里云CDN未缓存数据时，能够访问您的服务器以获取资源。



**配置源站信息**






1. 完成域名业务信息配置后，在 **源站信息** 区域单击 **新增源站信息**。

2. 在对话框中，选择源站的类型，并填写源站地址。

3. 根据您源站的实际情况填写 **端口**，默认使用HTTP协议的80端口。

      ![源站-cn.jpg](<Base64-Image-Removed>)


**说明**

   - 本示例以`10.10.10.1`作为源站服务器的IP来 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server "")。

     - 如果您要加速OSS的资源， **源站信息** 请选择 **OSS域名**；

     - 如果您要加速的资源部署在ECS， **源站信息** 请选择 **IP**，IP请填写ECS服务器的公网IP。

     - 如果您要加速的资源在服务器上并且不能使用IP访问， **源站信息** 请选择 **源站域名**，域名填写源站服务器的域名。但请注意，源站域名不能和加速域名相同，否则会造成循环解析。

     - 如果您要加速的资源是阿里云的函数计算， **源站信息** 请选 **函数计算域名**，区域和域名根据您账号的函数计算资源进行选择。
   - 如果您的源站上托管了多个网站，在您配置完成源站之后，还需要配置 [指定源站回源HOST](https://help.aliyun.com/zh/cdn/user-guide/specify-an-origin-host-for-each-origin "")。

   - 更多关于源站配置项的说明，敬请参见 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server "")。

   - 关于CDN与OSS的最佳实践，敬请参见 [CDN加速OSS资源](https://help.aliyun.com/zh/cdn/use-cases/accelerate-the-retrieval-of-resources-from-an-oss-bucket-in-the-alibaba-cloud-cdn-console "")。


4. #### **验证加速域名**


成功添加加速域名后，为保证DNS解析可以顺利切换而不影响现有业务，建议您先在本地测试加速域名，验证加速域名访问正常后，再将加速域名的DNS解析记录指向CNAME域名。



**说明**





模拟访问等同于正常的CDN访问，因此也会产生CDN基础服务和增值服务费用（如果测试的是增值服务），计费方式与正常使用CDN的计费方式相同。详细信息，请参见 [计费组成](https://help.aliyun.com/zh/cdn/product-overview/billing-overview#section-ypl-yah-5oz "")。







**验证加速域名**






1. 获取加速域名的CNAME地址。

      1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

      2. 在左侧导航栏，单击 **域名管理**。

      3. 在 **域名管理** 页面，复制加速域名对应的CNAME地址。





         **说明**





         请复制状态为 **正常运行** 的CNAME地址。







         ![image](<Base64-Image-Removed>)
2. 获取CNAME对应的IP地址。在命令行（CMD，PowerShell或终端）中使用`nslookup`命令查询CNAME地址，得到IP地址。例如：















      ```plaintext
      nslookup www.example.com.w.kunlunle.com
      ```



      ![image](<Base64-Image-Removed>)

3. 在本地电脑绑定hosts文件。



      您需要将步骤2得到的IP地址和加速域名绑定到电脑本地hosts文件中，绑定顺序为IP地址在前，加速域名在后，顺序不能颠倒。接下来将以IP地址为 **192.168.0.1** 为例，为您介绍绑定方法。








      Windows系统



      macOS系统



















      1. 进入路径`C:\Windows\System32\drivers\etc`，使用记事本以管理员身份打开`hosts`文件。

      2. 编辑`hosts`文件。文件内容可能类似如下：















         ```plaintext
         # localhost name resolution is handled within DNS itself.
         # 127.0.0.1       localhost
         # ::1             localhost
         ```



         在文件末尾添加获取到的IP地址和加速域名，例如：















         ```plaintext
         192.168.0.1   www.example.com
         ```

      3. 保存更改。编辑完成后，选择**文件** \> **保存** 或按`Ctrl + S`保存更改。

      4. **（可选）** 刷新DNS缓存是为了确保DNS解析的更改立即生效。

         打开命令提示符（以管理员身份运行），输入以下命令并按回车：















         ```powershell
         ipconfig /flushdns
         ```


      1. 打开Terminal终端，使用以下命令以管理员权限打开`hosts`文件。















         ```bash
         sudo vim /etc/hosts
         ```

      2. 编辑`hosts`文件。文件内容可能类似如下：















         ```plaintext
         ##
         # Host Database
         #
         # localhost is used to configure the loopback interface
         # when the system is booting.  Do not change this entry.
         ##
         127.0.0.1   localhost
         255.255.255.255 broadcasthost
         ::1         localhost
         ```



         在文件末尾添加获取到的IP地址和加速域名，例如：















         ```plaintext
         192.168.0.1   www.example.com
         ```

      3. 保存更改并退出。

         按`Esc`键退出插入模式，然后输入`:wq`按回车，保存文件并退出vim。

      4. **（可选）** 刷新DNS缓存是为了确保DNS解析的更改立即生效。

         在终端中输入以下命令并按回车：















         ```bash
         sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
         ```


4. 测试加速域名是否访问正常。



      成功绑定hosts文件后，您可以打开浏览器，在本地访问加速域名进行连通性测试，测试结果可通过浏览器自带的开发者工具查看。



      - 如果 **Remote Address** 的IP和您在hosts文件中绑定的IP一致，表示配置正确，您可以在域名解析服务商处配置CNAME。![测试网页连通性](<Base64-Image-Removed>)

      - 如果 **Remote Address** 的IP和您在hosts文件中绑定的IP不一致，表示配置不正确，您需要检查hosts文件中绑定的IP地址是否正确，确保该IP地址是CNAME地址的IP。


成功访问加速域名后，如果您需要验证其他功能，可在电脑本地进行相应的验证。

### **二、推荐配置**

完成域名和源站的配置之后，点击 **下一步** 即可进入 **推荐配置** 页面。

**推荐配置** 中提供了 **提升缓存命中率**、 **提升访问性能**、 **防止费用超额**、 **提升访问安全** 四种配置，可以提升CDN的缓存命中率、访问性能以及安全性。

您可以根据自身业务配置合适的功能，也可以先跳过推荐配置，然后在 **域名管理** 页的 **操作** 栏点击 **快捷配置** 再次进入。

#### **提升缓存命中率**

**缓存过期时间**

合理的缓存规则能最大化 CDN 性能，减少不必要的回源请求。缓存规则按顺序匹配，首个命中的规则生效。根据资源的特性， [配置合理的缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time "")。以下为参考的推荐配置：

| **文件类型** | **文件后缀名** | **过期时间** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **文件类型** | **文件后缀名** | **过期时间** | **说明** |
| 图片/音视频 | `jpg,png,gif,mp3,mp4` | 30天 | 资源内容不经常变更 |
| 静态脚本 | `js,css` | 1小时 | 可能随版本发布而频繁变更 |
| 网站首页 | `html` | 不缓存（0秒） | 确保用户始终获取最新页面结构 |

**忽略参数**

开启 [忽略参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters "") 功能后，CDN节点在生成缓存hashkey时会去除URL中`?`之后的参数，这样客户端在携带不同的参数访问同一个资源文件的时候，都能够命中到同一个缓存文件，有助于提高缓存命中率，减少回源流量。

![image](<Base64-Image-Removed>)

#### **提升访问性能**

**Range回源**

[Range回源](https://help.aliyun.com/zh/cdn/user-guide/object-chunking "") 指HTTP请求通过Range头指定下载文件的字节范围。CDN中使用Range回源时，可针对大文件仅回源未缓存部分，避免重复传输完整文件，可以提升资源响应速度并减少回源流量。

如果客户端配置了Range回源参数，可以选择 **跟随客户端Range请求**，图片资源推荐使用512KB的分片大小，如果是视频或大文件，可以根据文件的大小选择1MB、2MB和4MB的分片大小。CDN节点第一次回源请求会按照用户请求中的Range大小向上取整来请求用户源站，后面全部按照用户指定的分片大小来请求用户源站。

如果加速的资源为视频或大文件，可以选择 **开启Range回源（大文件场景推荐配置）**，可以根据文件的大小选择1MB、2MB和4MB的分片大小。无论客户端是否使用Range请求CDN节点，CDN节点的所有回源Range请求都按照用户指定的分片大小来请求用户源站。

**Gzip压缩**

加速文件大小在1 KB~10 MB及之间时，可以使用Gzip压缩来降低传输数据大小，提升文件传输效率，减少带宽消耗。

该功能对于1 KB以下和10 MB以上大小的文件CDN不做压缩。常见的图片类型文件和视频类型文件，已经做了内容的压缩处理，开启Gzip压缩没有效果。在开启该功能之前，请仔细阅读 [Gzip压缩](https://help.aliyun.com/zh/cdn/user-guide/use-the-gzip-compression-feature "") 的注意事项。

![智能压缩](<Base64-Image-Removed>)

#### **防止费用超额**

为防止域名被攻击或盗刷产生突发高带宽，导致产生高额账单，可通过配置用量封顶，控制用户访问该域名的带宽、流量、HTTPS请求数上限值，减少因突发流量导致的损失。详细信息可以参考 [配置用量封顶](https://help.aliyun.com/zh/cdn/user-guide/configure-usage-cap "")。

**重要**

- 触发规则之后，加速域名将会被暂时下线，下线期间域名将无法访问。如果您希望在用量超过阈值以后只发送告警通知，可以 [设置流量监控告警](https://help.aliyun.com/zh/cdn/user-guide/set-an-alert-rule "")。

- 这三项配置需要根据网站的历史流量、历史带宽和历史HTTPS请求数来设置阈值。如果您不清楚网站的流量、带宽和HTTPS请求数信息，您可以先行跳过该配置，待系统稳定运行之后，使用CDN的 [用量查询](https://help.aliyun.com/zh/cdn/user-guide/query-resource-usage-1 "") 查看加速域名的用量信息，然后再来 [配置用量封顶](https://help.aliyun.com/zh/cdn/user-guide/configure-usage-cap "")。


**流量封顶**

如果计费方式是默认的 **按流量** 计费，推荐配置该功能。可以根据历史流量来设置阈值，系统会统计域名在指定周期内产生的总流量。当累计流量超过您设定的阈值时，将触发封顶规则，下线域名，当到达解封时间后，重新上线加速域名。

**带宽封顶**

如果计费方式是 **按带宽峰值** 计费，推荐配置该功能，能有效控制计费带宽的上限。当系统实时监控到的带宽值超过您设定的阈值时，将触发封顶规则，下线域名，当到达解封时间后，重新上线加速域名。

**HTTPS请求数封顶**

如果您的加速域名需要开启HTTPS访问，并且对HTTPS请求量有明确预算控制，推荐配置该功能。当加速累计请求数超过您设定的阈值时，将触发封顶规则，下线域名，当到达解封时间后，重新上线加速域名。

#### **提升访问安全**

**HTTPS证书**

如果您的应用在配置阿里云CDN之前已经支持HTTPS访问，请务必进行HTTPS证书的配置，否则您的域名将不再支持HTTPS访问。

如果您的域名之前就不支持HTTPS访问，并且暂时也不打算支持HTTPS访问，那么您可以直接跳过该配置。

**重要**

开启HTTPS将产生HTTPS请求数，静态HTTPS请求数每月前500万次免费，超过500万次后，开始计费。HTTPS请求数计费不能使用CDN流量包抵扣，请确保您的账户余额充足，或购买HTTPS请求包，避免欠费导致CDN停止服务。详情敬请参见 [静态HTTPS请求数](https://help.aliyun.com/zh/cdn/product-overview/billing-of-https-requests-for-static-content "")。

- 已在阿里云数字证书管理服务中购买了证书，请选择 **云盾（SSL）证书中心**，并在 **证书名称** 中选择已购买的证书，如果无法选择您购买的证书，请检查已购买证书绑定的域名和加速域名是否相同。

- 使用的是第三方服务商签发的证书，请选择 **自定义上传（证书+私钥）**，您需要在设置 **证书名称** 后，上传 **证书（公钥）** 和 **私钥**，该证书将在阿里云数字证书管理服务中保存。您可以在 [我的证书](https://yundun.console.aliyun.com/?spm=5176.2020520110.all.12.16df56a1u1IhI6&p=cas#/cas/home) 中查看。


![HTTPS-cn.jpg](<Base64-Image-Removed>)

**Referer黑/白名单**

Referer黑/白名单基于HTTP请求头中的Referer字段，通过设置黑名单/白名单来控制访问，防止资源被非法盗用，黑、白名单互斥，同一时间只支持其中一种方式生效。更多配置详情可以参考 [配置Referer黑/白名单](https://help.aliyun.com/zh/cdn/user-guide/configure-a-referer-whitelist-or-blacklist-to-enable-hotlink-protection "")。

**说明**

您可以提前打开 [定制和订阅运营报表](https://help.aliyun.com/zh/cdn/user-guide/customize-an-operations-report-template-and-create-a-tracking-task "") 功能，运营报表会统计并展示用户访问的 **PV/UV**、 **地区和运营商**、 **域名排行**、热门Referer、 **热门URL**、 **回源热门URL** 和 **Top客户端IP** 等内容。然后根据热门Referer再来配置 **Referer黑/白名单**。

### **三、配置CNAME**

在未接入阿里云CDN之前，当用户输入域名后，请求会直接流向指定的服务器；接入阿里云CDN之后，用户的请求首先会被发送到最近的阿里云CDN节点，再由阿里云CDN确定是否需要调用服务器回源。为了确保请求链路能够从直接连接源服务器顺利切换到通过阿里云CDN进行访问，您需要进行CNAME配置。

CNAME记录是一种DNS记录类型，用于将一个域名指向另一个域名，更多关于CNAME的介绍，敬请参考 [CNAME记录简介](https://help.aliyun.com/zh/cdn/what-is-a-dns-cname-record "")。

**在DNS服务中配置CNAME**

1. 前往阿里云CDN控制台的 [域名管理列表](https://cdn.console.aliyun.com/domain/list)，找到之前添加的域名，复制域名对应的CNAME值（如果此处值为空，请稍等五秒之后刷新重试）。

![CANME-cn.jpg](<Base64-Image-Removed>)

2. 在DNS服务器中配置CNAME记录。不同DNS服务商配置CNAME域名解析的方法不同，请以实际情况为准。本文以阿里云和腾讯云两大DNS服务商为例。






阿里云配置CNAME方法



腾讯云配置CNAME方法



















如果您的DNS服务商是阿里云，您可以根据以下步骤完成CNAME配置。



1. 使用 **加速域名所在的阿里云账号**，登录 [云解析DNS控制台](https://dns.console.aliyun.com/)

2. 在 **公网权威解析** 页面，找到加速域名的主域名`example.com`，并单击右侧的 **解析设置**。

3. 单击 **添加记录**，添加CNAME记录。

4. **记录类型** 选择CNAME。

      ![addCname-cn.jpg](<Base64-Image-Removed>)


**重要**

   - 主机记录就是域名的前缀。`www.example.com`的主机记录是`www`；如果您的加速域名就是主域名`example.com`，那么对应的主机记录填写@。

   - 对于同一个主机名，CNAME记录和A记录是相互冲突，只能有一个存在。如果您要加速的域名存在相同主机记录的A记录，需要将A记录暂停或删除，才能配置CNAME记录。

   - 暂停A记录，配置CNAME的时候，会导致域名短暂的不可访问，为减少对您域名的影响，请根据您日常流量的变化情况，在合适的时间进行配置。


5. 单击 **确认**，完成添加。


如果您的DNS服务商是腾讯云，您可以根据以下步骤完成CNAME配置。

1. 登录DNSPod控制台。

2. 在对应域名的域名解析页，单击 **添加记录**，添加CNAME记录。


      |     |     |     |
      | --- | --- | --- |
      | **参数** | **说明** | **填写样例** |
      | **主机记录** | - 加速域名为子域名的情况下，主机记录为子域名的前缀。<br>        <br>      - 加速域名为泛域名的情况下，主机记录为`*`。<br>        <br>      - 加速域名为根域名自身时，主机记录为`@`。 | - 子域名示例：<br>        <br>        - 加速域名为`www.example.com`，主机记录为`www`。<br>          <br>        - 加速域名为`www.example.aliyundoc.com`，主机记录为`www.example`。<br>      - 泛域名示例：<br>        <br>        - 加速域名为`.example.com`，主机记录为`*`。<br>          <br>        - 加速域名为`*.example.aliyundoc.com`，主机记录为`*.example`。<br>      - 根域名示例：根域名为`example.com`且配置加速域名为`example.com`时，主机记录填写`@`。<br>        <br>**说明**<br>域名解析设置是针对您注册的域名（如`example.com`）或域名的左侧部分进行解析设置。配置主机记录时，您仅需要填写要解析的部分（如解析`www.example.com`时填写`www`）。 |
      | **记录类型** | 选择CNAME。 | CNAME |
      | **线路类型** | 选择“默认”类型。 | 推荐保持默认 |
      | **记录值** | 输入加速域名对应的CNAME记录值。<br>**说明**<br>一级域名（如`www.example.com`）和二级域名（如`www.example.aliyundoc.com`）对应的CNAME值不同。如果您要加速二级域名，需要将二级域名也添加到CDN上并解析到对应的CNAME记录值，或者在CDN上添加泛域名，泛域名的CNAME可以被二级域名使用。添加泛域名或二级域名，请参见 [添加加速域名](https://help.aliyun.com/zh/cdn/add-a-domain-name#task-678836 "")。 | `www.example.com.w.kunlunsl.com` |
      | **权重** | 无需填写。 | 不涉及 |
      | **MX** | 无需填写。 | 不涉及 |
      | **TTL** | TTL为缓存时间，数值越小，修改记录后各地生效时间越快。 | 推荐保持默认 |

3. 单击 **保存**，完成添加。


3. 验证配置的CNAME是否生效。






CNAME状态



通过nslookup命令验证



















1. 前往阿里云CDN控制台的 [域名管理列表](https://cdn.console.aliyun.com/domain/list)。

2. 选择目标域名，将鼠标指向加速域名的 **CNAME状态** 处，状态为 **已配置** 时，则表示CNAME配置已生效。

      ![CnameCheck-cn.jpg](<Base64-Image-Removed>)


**说明**

   - 在配置CNAME之后，控制台中 **CNAME状态** 可能仍会显示 **待配置**，请刷新页面或等5分钟再来验证。


1. 打开cmd程序（Windows）、终端（macOS/Linux）。

2. 输入nslookup -type=CNAME **加速域名**（例如nslookup -type CNAME www.example.com ），如果返回的解析结果和CDN控制台上该 **加速域名** 的CNAME值一致，则表示配置的CNAME已经生效。

      ![nsCheckCname.jpg](<Base64-Image-Removed>)


### **四、资源预热**

当您首次接入CDN后，可选择将热点静态资源提前预热至CDN边缘节点。用户访问时可直接由CDN边缘节点响应，避免初次访问速度慢的问题，提升用户体验。

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **刷新预热**。

3. 在 **刷新缓存/预热缓存** 页签，选择操作类型为 **预热**。

4. 在预热内容输入框中，输入需要预热的完整文件 URL，每行一个。不支持预热目录。例如：`https://www.example.com/install/package.zip`。

5. 单击 **提交**，系统将开始执行预热任务。

6. 在操作记录页签中查看资源刷新或预热的详细记录和进度。进度为100%，表示任务执行完成。


**说明**

- 刷预热任务一旦提交成功，将无法中止。

- 预热任务的完成时间取决于文件大小、数量和源站性能，通常需要 5-30 分钟。


### **五、验证阿里云CDN缓存是否生效**

**验证阿里云CDN缓存是否生效**

1. Windows系统 ：按下Windows键+R键，在弹出的运行输入框里，输入cmd，点击确定，打开cmd命令行。

macOS系统 ：打开“终端”。

2. 在窗口中输入 "curl -I" + 加速域名资源，例如`curl -I www.example.com/10.JPG`。

![image](<Base64-Image-Removed>)

3. 当响应头结果中有`Age`、`X-Cache`、`X-Swift-SaveTime`、`X-Swift-CacheTime`时，证明阿里云CDN已经生效。



**说明**





   - `X-Cache`：字段为MISS，则表示未命中缓存，需要进行回源处理；X-Cache字段为HIT，则表示命中了CDN缓存，会直接读取缓存数据。

   - `Age`: 表示文件在CDN节点上缓存的时间（秒）。文件被刷新或首次访问无此字段。`Age`为0表示缓存过期，需回源校验。

   - `X-Swift-SaveTime`：表示资源首次被缓存到CDN节点上的时间（GMT）。转换为中国北京时间需加上8小时。

   - `X-Swift-CacheTime`：字段值表示CDN节点上的允许缓存时间，即该文件可以在CDN节点上缓存多久。如果是0，则表示该请求无法缓存。


**说明**

如果您按照上述流程配置完成之后，仍然出现无法访问或访问异常，敬请参见 [无法访问/访问异常排查](https://help.aliyun.com/zh/cdn/support/faq#section-8ru-2us-33z "")。

至此，阿里云CDN的主要配置已完成，您的网站现在可以通过阿里云CDN实现访问加速。

## **参考文档**

[阿里云CDN常见问题排查](https://help.aliyun.com/zh/cdn/support/faq "")

[什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn "")

[阿里云CDN的五大竞争力](https://help.aliyun.com/zh/cdn/product-overview/competitive-advantages-of-alibaba-cloud-cdn "")

[CDN防范流量盗刷最佳实践](https://help.aliyun.com/zh/cdn/use-cases/best-practices-for-preventing-traffic-theft "")

[提高CDN缓存命中率](https://help.aliyun.com/zh/cdn/use-cases/increase-the-cache-hit-ratios-of-alibaba-cloud-cdn "")

[客户案例](https://help.aliyun.com/zh/cdn/product-overview/customer-use-cases "")