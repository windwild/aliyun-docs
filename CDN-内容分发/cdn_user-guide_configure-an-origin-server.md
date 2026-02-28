### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[基本配置](https://help.aliyun.com/zh/cdn/user-guide/basic-settings/)配置源站

# 配置源站

更新时间：2025-12-03 04:58:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置全球资源计划](https://help.aliyun.com/zh/cdn/user-guide/configure-global-resource-planning)[下一篇：配置条件源站](https://help.aliyun.com/zh/cdn/user-guide/configure-a-conditional-origin)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

新增或修改源站信息

回源重试、回源超时、源站探测相关说明

相关文档

阿里云CDN支持的源站类型包括OSS域名、IP、源站域名和函数计算域名，每种源站类型都支持配置多个源站地址，多源站场景下，支持设置源站的主备优先级和权重，实现负载均衡。

## 注意事项

CDN回源从源站获取资源时，源站产生的流量宽带费用由源站来缴纳，比如源站是客户的IDC中心，产生的就是IDC中心的流量带宽费用；如果源站是OSS，产生的就是OSS的流量费。

## 新增或修改源站信息

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在 **源站信息** 区域，根据业务需求，选择新增或修改源站配置。



   - 单击 **新增源站信息**，可以增加源站。

   - 单击已有源站信息后面的 **编辑**，可以修改已有源站配置。


![域名](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9946493761/p549725.png)

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| **源站信息** | 选择源站的类型，并填写源站地址。<br>   - **OSS域名**<br>     <br>     <br>     - 在下拉列表中选择同一账号下OSS的外网域名作为源站。<br>       <br>     - 手动输入阿里云OSS的外网域名作为源站（不支持OSS内网域名作为源站），例如：`***.oss-cn-hangzhou.aliyuncs.com`，OSS外网域名可前往[OSS控制台](https://oss.console.aliyun.com/)查看。<br>       <br>**说明**<br>     - 关于加速OSS资源的实践，请参见 [CDN加速OSS资源](https://help.aliyun.com/zh/cdn/use-cases/use-alibaba-cloud-cdn-to-accelerate-the-delivery-of-resources-from-oss-buckets/ "")。<br>       <br>     - 阿里云CDN回源阿里云OSS的流量优惠说明：<br>       <br>       <br>       - 用户需要在CDN控制台上把源站类型设置为“OSS域名”，这样阿里云OSS产品会将来自阿里云CDN产品的回源流量识别为“CDN回源流出流量”，从而享受到更优惠的价格。<br>         <br>       - 如果用户在CDN控制台上把源站类型误设为“源站域名”，阿里云OSS产品会将来自阿里云CDN产品的回源流量识别为“外网流出流量”，这种情况下就享受不到优惠价格。<br>         <br>详细的费用说明，请参见 [CDN加速OSS计费说明](https://help.aliyun.com/zh/cdn/product-overview/billing-of-oss-content-acceleration#concept-2165710 "")。<br>     - 采用阿里云OSS作为源站时，必须要 [配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host "")，并且默认回源HOST的值为OSS Bucket的公网地址域名，否则会无法访问源站。<br>       <br>     - 采用阿里云OSS作为源站时，建议 [配置默认回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni "")，并且默认回源SNI的值为OSS Bucket的公网地址域名，否则可能会被OSS限流。<br>       <br>   - **IP**<br>     <br>     - 支持配置单个或者多个IP作为源站地址，不支持内网IP，支持IPv4地址和IPv6地址，不能全部配置IPv6地址，必须至少配置一个IPv4地址，使用阿里云ECS的外网IP作为源站地址可免审核。如果要配置IPv6源站地址，您需要提前开启IPv6回源功能，如果没有提前开启，那么配置的IPv6源站地址将无法生效，这会导致回源失败。详细信息，请参见 [配置IPv6回源](https://help.aliyun.com/zh/cdn/user-guide/configure-back-to-origin-routing-over-ipv6 "")。<br>       <br>     - 关于源站类型为IP的配置实践，敬请参见 [CDN加速ECS资源](https://help.aliyun.com/zh/cdn/use-cases/use-alibaba-cloud-cdn-to-accelerate-the-retrieval-of-resources-from-an-ecs-instance "")。<br>   - **源站域名**：支持配置域名作为源站地址，可配置多个域名。<br>     <br>     <br>     <br>     **说明**<br>     <br>     <br>     <br>     <br>     <br>     - 关于源站类型为域名的配置实践，敬请参见 [CDN加速ECS资源](https://help.aliyun.com/zh/cdn/use-cases/use-alibaba-cloud-cdn-to-accelerate-the-retrieval-of-resources-from-an-ecs-instance "")。<br>       <br>     - 源站域名不能与加速域名相同。若加速域名和源站域名一致，会导致请求反复解析到CDN节点上，造成循环解析，使得CDN节点无法回源。<br>       <br>     - 阿里云CDN当前支持直接将阿里云ALB产品的实例地址（例如：`example.hangzhou.alb.aliyuncs.com`）添加为CDN的源站。<br>       <br>     - 源站域名格式：<br>       <br>       - 域名长度为1~67个字符。<br>         <br>       - 支持：小写英文字母（a~z）、数字（0~9）和短划线（-），例如example.com。<br>         <br>       - 不支持：中文、英文大写字母（A~Z）和除了短划线（-）以外的其他符号，且短划线（-）不能连续出现、不能单独使用、不能出现在开头和结尾。如果域名包含中文（例如：阿里云.网址），请以中文形式进行相关备案，再通过第三方工具punycode将中文域名转换成为英文域名（例如：xn--fiq\*\*\*\*.xn--eq\*\*\*\*）后填入。<br>   - **函数计算域名**：支持将您在同一账号下的函数计算产品上配置的函数计算域名，配置为源站地址。您需要选择函数计算 **区域** 和 **域名**。操作方法，请参见 [配置自定义域名](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-a-custom-domain-name#multiTask145 "")。 |
| **优先级** | 源站优先级支持设置主备，主优先级大于备优先级。用户请求通过阿里云CDN回源时，会优先回源到优先级为主的源站地址。主源站出现故障（CDN节点和源站TCP连接失败）的情况下，将会回源到备源站。源站优先级的取值范围为0~127，数值越小，优先级越高。主源站的优先级默认值为20，备源站的优先级默认值为30。如需配置其他值，请提交工单申请。<br>例如，有A、B两个源站，A源站的优先级为主，B源站的优先级为备，则用户请求通过阿里云CDN回源时会优先回源到A源站，如果A源站出现故障（CDN节点和源站TCP连接失败），将会回源到B源站，当A源站恢复正常后会从B源站切换回A源站。 |
| **权重** | 当多个源站的优先级相同时，阿里云CDN会按照源站的权重分配用户请求回源到不同源站的比例，实现按权重的负载均衡。您可以根据业务需求，自行设置权重值。<br>   - 取值范围：1~100，数值越大，源站分配到的用户请求比例越高。<br>     <br>   - 默认值：10。<br>     <br>例如：有A、B两个源站，两个源站的优先级都是主，A源站的权重为80，B源站的权重为20，则用户请求将会按照8:2的比例在A、B两个源站之间分配。<br>**说明**<br>在某些情况下，用户实际请求回源到不同源站的比例并不一定会与域名配置中源站的权重比例相同，例如：<br>   - 回源QPS较低（例如不到10QPS），回源到不同源站的概率分布不太均匀，因此会出现实际回源权重与源站配置的权重不一致的情况。<br>     <br>   - 所有的请求均来自于某个IP地址（或者有限的某几个IP地址），由于同一个IP地址将会被调度到同一个CDN节点，并且CDN节点与源站之间存在TCP会话保持，因此很可能会出现大部分请求都回源到同一个源站的情况。<br>     <br>如果您希望验证用户请求回源权重大致等同于域名配置中的源站权重，您可以使用第三方拨测工具来发起探测任务，配置地理位置分布尽可能广、运营商分布尽可能多的探测客户端，并且探测任务需要持续一段时间，以便采集到足够多的有效探测数据。 |
| **端口** | 表示CDN节点回到源站哪个端口请求资源。默认为80，根据您源站的支持情况，可自定义设置回源端口，允许设置的端口范围为1~65535。<br>   - 默认值：80。<br>     <br>   - 端口值为443时，以HTTPS协议回源；80或其他自定义端口，以HTTP协议回源。<br>     <br>**说明**<br>   - 如果需要以HTTPS协议回源到其他自定义端口，请参见 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy#task-261642 "")。<br>     <br>   - 如果配置了 **回源协议** 功能（默认为关闭状态），这里配置的端口会失效。关闭回源协议的方法，请参见 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy#task-261642 "")。<br>     <br>   - 当源站选择OSS域名时，回源端口是否支持自定义端口，取决于OSS产品。 |

**说明**

源站健康检查策略，请参见 [回源重试、回源超时、源站探测相关说明](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server#section-3fj-o6s-p4t "")。

5. 单击 **确定**，完成配置。


## 回源重试、回源超时、源站探测相关说明

- 回源重试顺序：

  - 对域名基础信息的源站地址列表内的源站地址按优先级从高到低进行重试。

  - 如果有优先级相同的源站地址，则按权重比例进行重试。
- 回源重试的颗粒度：

  - 重试是IP地址级别的，如果源站是域名，将会对域名解析出的所有IP地址进行重试，只有域名下的所有IP都连接失败后才会访问其他可用源站。

  - 重试时系统会自动过滤dead table中不可用的源站。
- 回源重试状态码：

  - CDN节点在收到源站响应的5xx状态码的时候进行重试。
- 回源超时时间：在源站主动响应重试状态码时，CDN节点收到重试状态码之后就会重试。如果没有收到源站主动响应的重试状态码，则会遵循回源超时时间处理逻辑，达到超时时间之后就会触发CDN节点重试。

  - 源站TCP建连超时：10秒。

  - 源站写超时：默认为30秒（源站建连后写入内容超时）。

  - 源站读超时：默认为30秒（源站建连后在一定时间内没有把CDN节点请求的内容完整响应回去）。

  - 源站写超时时间和源站读超时时间可以通过配置回源HTTP请求超时时间来调整。
- 源站探测逻辑：

  - TCP连接异常：如果CDN节点与源站IP地址之间连续两次出现TCP连接不可用（建连失败或连接超时），CDN会从可用源站地址列表中剔除该源站IP地址，并将该IP地址加入dead table中，这样后续的回源请求就不会去访问这个源站IP地址；此后CDN节点会每隔5秒使用TCP建连去探测一次该源站IP地址，如果建连成功，则将该源站IP地址恢复到可用源站地址列表中。

  - TCP连接正常：如果CDN节点与源站IP地址之间TCP连接正常，但收到源站响应的重试状态码（例如：5xx），此时虽然会触发重试的逻辑，但该源站IP地址仍然还在可用源站地址列表中，下次访问还会按权重去请求该源站（即TCP四层连接正常的情况下，七层HTTP请求异常不会主动屏蔽源站IP地址，如果需要在七层HTTP请求异常的情况下主动屏蔽源站IP地址，则需要提交工单申请配置）。

## **相关文档**

- 什么是源站，请参见 [源站](https://help.aliyun.com/zh/cdn/product-overview/terms#section-fce-wpt-1bf "")。

- 当您使用多个源站进行加速时，可以通过设置不同的回源HOST来指定CDN节点回源到不同的源站，请参见 [配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host "")。

- 如果您需要自定义HTTP或HTTPS回源协议，请参见 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy "")。

- 如果您的源站使用的是阿里云对象存储OSS，并且OSS的Bucket被配置为私有模式，需要给加速域名开启OSS私有Bucket回源功能，请参见 [OSS私有Bucket回源](https://help.aliyun.com/zh/cdn/user-guide/grant-alibaba-cloud-cdn-access-permissions-on-private-oss-buckets "")。

- 如果您的源站IP绑定了多个域名，且CDN回源协议为HTTPS时，需配置回源SNI，请参见 [配置默认回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni "")。