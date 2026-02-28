### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 添加加速域名

# 添加加速域名

更新时间：2025-02-20 04:01:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

准备工作

步骤一：配置域名信息

步骤二：配置源站

步骤三：完成域名审核

后续步骤

如果您想通过CDN加速指定网站的业务，需要将目标网站配置为源站，并为其设置一个加速域名。CDN会通过该加速域名将源站内容缓存至全球分布的边缘节点，从而显著降低内容传输延迟，提升用户的访问速度。

添加加速域名

## 准备工作

1. 您已经拥有稳定运行的源站（即业务服务器或OSS）。如果没有源站，请参见 [通过控制台使用ECS实例](https://help.aliyun.com/zh/ecs/getting-started/create-and-manage-an-ecs-instance-by-using-the-ecs-console "") 或 [创建存储空间](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4 "") 创建。

2. 您已经拥有用于加速的域名。



**说明**





当目标加速区域为 **仅中国内地** 或 **全球** 时，域名需要完成备案。如果域名未备案，您可以登录 [阿里云ICP代备案管理系统](https://beian.aliyun.com/pcContainer/myorder) 完成备案。

3. 您已经开通了CDN服务。如果未开通，请参见 [开通CDN服务](https://help.aliyun.com/zh/cdn/activate-alibaba-cloud-cdn#task-187531 "") 进行开通。


## 步骤一：配置域名信息

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 单击 **添加域名**，在 **域名信息** 页面，配置 **加速区域**、 **加速域名** 和 **业务类型**，其他参数均保持默认。

![china](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9581397861/p94748.png)




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **加速区域** | - **仅中国内地**：所有用户访问均会调度至中国内地就近节点提供加速服务（海外地区和中国香港、中国澳门、中国台湾地区的访问流量将会被调度至华东电信的CDN节点）。<br>     <br>   - **全球**：所有用户访问将会择优调度至全球就近节点提供服务。<br>     <br>   - **全球（不包含中国内地）**：非中国内地用户访问会被调度至就近节点服务；中国内地用户访问会被调度至日本、新加坡和中国香港的CDN加速节点服务。<br>     <br>**重要**<br>   - 加速区域为 **仅中国内地** 或 **全球** 时，加速域名要求 **必须备案**，您可以登录 [阿里云ICP代备案管理系统](https://beian.aliyun.com/pcContainer/myorder) 完成备案。由于工信部备案系统存在数据延迟，刚完成备案的域名请在8小时后再配置。<br>     <br>   - 加速区域为 **全球（不包含中国内地）** 时，对加速域名 **备案不作要求**。<br>     <br>   - 不同的加速区域价格不一样，请根据您的实际需求选择。计费详情，请参见[CDN定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.10.1b444ee22Dxy8y#/cdn/detail)。 |
| **加速域名** | 填写 [加速域名](https://help.aliyun.com/zh/cdn/product-overview/terms#section-obn-stb-p2b "") 名称，填写要求请参见 [使用限制](https://help.aliyun.com/zh/cdn/product-overview/limits "")。<br>**说明**<br>首次在CDN控制台添加一个新域名时，需要完成域名归属权验证。具体操作，请参见 [验证域名归属权](https://help.aliyun.com/zh/cdn/verify-domain-name-ownership#task-2511469 "")。如果之前已经验证通过根域名的归属权，请忽略。 |
| **业务类型** | - [图片小文件](https://help.aliyun.com/zh/cdn/product-overview/scenarios#section-mnp-tw0-fz3 "")：适用于电商类、网站类、游戏图片类等小型的静态资源加速场景。<br>     <br>   - [大文件下载](https://help.aliyun.com/zh/cdn/product-overview/scenarios#section-9n4-tgj-a76 "")：适用于大于20 MB的静态文件加速场景。<br>     <br>   - [视音频点播](https://help.aliyun.com/zh/cdn/product-overview/scenarios#section-zuc-giw-6og "")：适用于音频或视频文件加速场景。<br>     <br>   - [全站加速](https://help.aliyun.com/zh/edge-security-acceleration/dcdn/product-overview/what-is-dcdn#concept-hdt-3t2-xdb "")：适用于含有大量动态和静态内容混合，且多为动态资源请求的加速场景。<br>     <br>     当业务类型选择 **ESA边缘安全加速** 时，您需根据界面提示，前往全站加速控制台添加域名并进行相关配置。具体操作，请参见 [添加服务域名](https://help.aliyun.com/zh/edge-security-acceleration/dcdn/getting-started/add-a-domain-name#task-alv-1fk-xdb "")。<br>     <br>**说明**<br>配置后业务类型不可修改。 |


## 步骤二：配置源站

1. 完成域名业务信息配置后，在 **源站信息** 区域单击 **新增源站信息**。

2. 在 **新增源站信息** 对话框中，选择源站的类型，并填写源站地址，其他参数均保持默认。



![配置源站信息](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3869438171/p278368.png)






| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **源站信息** | 选择 [源站](https://help.aliyun.com/zh/cdn/product-overview/terms#section-fce-wpt-1bf "") 的类型，并填写源站地址。源站类型支持 **OSS域名**、 **IP**、 **源站域名** 和 **函数计算域名**。此处以 **OSS域名** 举例说明，其他类型的源站配置，详情请参见 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server "")。<br>**源站信息** 选择 **OSS域名**，并在下方的 **域名** 列表中选择同账号下的OSS Bucket，或选择输入阿里云OSS Bucket的外网域名作为源站（不支持OSS内网域名作为源站），示例值为`***.oss-cn-hangzhou.aliyuncs.com`。 |
| **优先级** | 源站优先级支持设置主备，主优先级大于备优先级。用户请求通过阿里云CDN回源时，会优先回源到优先级为主的源站地址。主源站出现故障的情况下，将会回源到备源站。源站优先级的取值范围为0~127，数值越小，优先级越高。主源站的优先级默认值为20，备源站的优先级默认值为30。如需配置其他值，请[填写信息](https://page.aliyun.com/form/act2017566026/index.htm)申请。<br>例如，有A、B两个源站，A源站的优先级为主，B源站的优先级为备，则用户请求通过阿里云CDN回源时会优先回源到A源站，如果A源站出现故障，将会回源到B源站，当A源站恢复正常后会从B源站切换回A源站。 |
| **权重** | 当多个源站的优先级相同时，阿里云CDN会按照源站的权重分配用户请求回源到不同源站的比例，实现按权重的负载均衡。您可以根据业务需求，自行设置权重值。<br>   - 取值范围：1~100，数值越大，源站分配到的用户请求比例越高。<br>     <br>   - 默认值：10。<br>     <br>例如：有A、B两个源站，两个源站的优先级都是主，A源站的权重为80，B源站的权重为20，则用户请求将会按照8:2的比例在A、B两个源站之间分配。 |
| **端口** | 表示CDN节点回到源站哪个端口请求资源。默认为80，根据您源站的支持情况，可自定义设置回源端口，允许设置的端口范围为1~65535。<br>   - 默认值：80。<br>     <br>   - 端口值为443时，以HTTPS协议回源；80或其他自定义端口，以HTTP协议回源。<br>     <br>**说明**<br>   - 如果需要以HTTPS协议回源到其他自定义端口，请参见 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy#task-261642 "")。<br>     <br>   - 如果配置了 **回源协议** 功能（默认为关闭状态），这里配置的端口会失效。关闭回源协议的方法，请参见 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy#task-261642 "")。<br>     <br>   - 当源站选择OSS域名时，回源端口是否支持自定义端口，取决于OSS产品。 |

3. 配置完成后，单击 **确定**。


## 步骤三：完成域名审核

1. 完成源站配置后，阅读并勾选合规承诺，单击 **下一步**。

2. 页面跳转至 **推荐配置** 页面，请根据实际需要配置缓存过期时间、忽略参数、页面优化、Range回源、Gzip压缩等基础配置，有效提升CDN的缓存命中率和访问性能，请参见 [推荐配置（可选）](https://help.aliyun.com/zh/cdn/configure-system-recommended-features "")。

您可以单击页面下方的 **一键配置** 按钮，CDN会快速帮您完成相关配置；您也可以单击 **返回域名管理** 在域名列表页的操作栏单击 **推荐配置** 再次进入。

3. 等待人工审核。



审核通过后，域名状态显示为 **正常运行**，表示添加成功。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3869438171/p810612.png)





**说明**





   - 如果您的加速域名无需人工审核，将直接进入下一个配置环节，您可根据实际业务需求，完成推荐配置。

   - 新增域名的生效时长通常在10分钟以内，偶尔会因为系统波动延长到30分钟，如果超过30分钟仍未完成域名新增，那么将会有阿里云的工程师介入处理。


## 后续步骤

[配置CNAME](https://help.aliyun.com/zh/cdn/add-a-cname-record-for-a-domain-name#task-187531 "")：添加域名后，阿里云CDN会为您分配对应的CNAME域名，您需要完成CNAME配置，CDN服务才能生效。

**说明**

同时，建议您在 [配置CNAME](https://help.aliyun.com/zh/cdn/add-a-cname-record-for-a-domain-name#task-187531 "") 前，完成以下操作：

- [推荐配置（可选）](https://help.aliyun.com/zh/cdn/configure-system-recommended-features#task-187634 "")：为域名配置缓存过期时间、带宽封顶等功能，提升CDN的缓存命中率、安全性和访问性能。

- [模拟访问测试（可选）](https://help.aliyun.com/zh/cdn/test-whether-a-domain-name-is-accessible#task-2520721 "")：保证DNS解析顺利切换而不影响现有业务。