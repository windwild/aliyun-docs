### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[基本配置](https://help.aliyun.com/zh/cdn/user-guide/basic-settings/)配置全球资源计划

# 配置全球资源计划

更新时间：2026-01-09 03:06:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：加速区域](https://help.aliyun.com/zh/cdn/user-guide/change-the-accelerated-region)[下一篇：配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

节点分布

注意事项

开启全球资源计划后支持的配置功能

配置入口

全球资源计划是一种资源服务计划，同时使用阿里云自建节点和全球合作伙伴节点为域名提供加速服务。开启后，您的域名可以享受更丰富的节点资源，更好地覆盖非中国内地区域，提升域名的访问体验。

## **节点分布**

全球资源计划在全球覆盖200+节点，具体节点分布如下表所示：

| **计费区域** | **节点分布** |
| --- | --- |

|     |     |
| --- | --- |
| **计费区域** | **节点分布** |
| 北美 | 美国、加拿大、墨西哥 |
| 南美 | 巴西、阿根廷、哥伦比亚、智利、秘鲁 |
| 欧洲 | 英国、德国、意大利、荷兰、法国、瑞典、奥地利、西班牙、波兰、比利时、瑞士、葡萄牙、保加利亚、克罗地亚、捷克、丹麦、芬兰、希腊、匈牙利、爱尔兰、挪威、罗马尼亚 |
| 亚太1区 | 中国香港、中国台湾、日本、新加坡、菲律宾、马来西亚、泰国 |
| 亚太2区 | 韩国、印度、越南、印度尼西亚 |
| 亚太3区 | 澳大利亚、新西兰 |
| 中东/非洲 | 以色列、阿拉伯联合酋长国、南非、阿曼、尼日利亚、巴林、肯尼亚 |

**说明**

全球资源计划开启前后 [计费规则](https://help.aliyun.com/zh/cdn/product-overview/billing-overview "") 不变。

## **注意事项**

- 该功能正在分阶段开放中，如果您暂时还未看到该功能，请耐心等待。

- 仅支持加速区域为 **全球（不包含中国内地）** 的域名。

- 全球资源计划开启后支持部分功能。具体范围请参考 [开启全球资源计划后支持的配置功能](https://help.aliyun.com/zh/cdn/user-guide/configure-global-resource-planning#3e09051014jbv "")。

- 全球资源计划开启后无法直接关闭。关闭该功能需要删除后重新添加域名至阿里云 CDN。


## **开启全球资源计划后支持的配置功能**

**说明**

暂不支持POST请求。

开启 **全球资源计划** 之后，您的域名可以享受更丰富的节点资源，但是支持的功能会受到限制，请谨慎评估之后使用。以下为 **全球资源计划** 支持的功能列表：

| **功能大类** | **功能集** | **功能介绍** | **全球资源计划支持情况** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能大类** | **功能集** | **功能介绍** | **全球资源计划支持情况** |
|  | 基本配置 | [加速区域修改](https://help.aliyun.com/zh/cdn/user-guide/change-the-accelerated-region "") | 不支持 |
| [源站配置](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server "") | 支持 |
| [配置条件源站](https://help.aliyun.com/zh/cdn/user-guide/configure-a-conditional-origin "") | 不支持 |
| [IPv6配置](https://help.aliyun.com/zh/cdn/user-guide/configure-ipv6 "") | 支持 |
| 回源配置<br>**说明**<br>默认支持Range回源功能，控制台暂不支持关闭。如果需要关闭，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。 | [配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host "") | 支持 |
| [指定源站回源HOST](https://help.aliyun.com/zh/cdn/user-guide/specify-an-origin-host-for-each-origin "") | 支持 |
| [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy "") | 支持 |
| [OSS私有Bucket回源](https://help.aliyun.com/zh/cdn/user-guide/grant-alibaba-cloud-cdn-access-permissions-on-private-oss-buckets "") | 支持 |
| [配置默认回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni "") | 不支持 |
| [指定回源SNI](https://help.aliyun.com/zh/cdn/user-guide/specify-origin-sni "") | 不支持 |
| [配置回源请求超时时间](https://help.aliyun.com/zh/cdn/user-guide/configure-a-timeout-period-for-back-to-origin-http-requests "") | 支持 |
| [修改出站请求头](https://help.aliyun.com/zh/cdn/user-guide/configure-custom-request-headers "") | 支持 |
| [修改入站响应头](https://help.aliyun.com/zh/cdn/user-guide/rewrite-http-response-headers "") | 支持 |
| [Common Name白名单](https://help.aliyun.com/zh/cdn/user-guide/common-name-whitelist "") | 不支持 |
| [高级回源](https://help.aliyun.com/zh/cdn/user-guide/configure-advanced-origin-settings "") | 不支持 |
| [配置回源301/302跟随](https://help.aliyun.com/zh/cdn/user-guide/configure-301-or-302-redirection "") | 不支持 |
| [重写回源路径](https://help.aliyun.com/zh/cdn/user-guide/rewrite-urls-in-back-to-origin-requests "") | 支持 |
| [重写回源参数](https://help.aliyun.com/zh/cdn/user-guide/rewrite-url-parameters-in-back-to-origin-requests "") | 支持 |
| 缓存配置 | [配置缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time "") | 支持 |
| [配置状态码过期时间](https://help.aliyun.com/zh/cdn/user-guide/create-a-cache-rule-for-http-status-codes "") | 不支持 |
| [修改出站响应头](https://help.aliyun.com/zh/cdn/user-guide/create-a-custom-http-response-header "") | 不支持 |
| [配置自定义页面](https://help.aliyun.com/zh/cdn/user-guide/create-a-custom-error-page "") | 不支持 |
| [配置访问URL改写规则](https://help.aliyun.com/zh/cdn/user-guide/create-an-access-url-rewrite-rule "") | 不支持 |
| [自定义Cachekey](https://help.aliyun.com/zh/cdn/user-guide/create-custom-cache-keys "") | 不支持 |
| [配置共享缓存](https://help.aliyun.com/zh/cdn/user-guide/configure-shared-cache "") | 不支持 |
| [响应过期缓存](https://help.aliyun.com/zh/cdn/user-guide/serve-stale-content "") | 不支持 |
| HTTPS配置<br>**说明**<br>默认支持TLS v1.2版本，暂不支持修改配置。如果需要兼容TLS v1.0和v1.1版本，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请。 | [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate "")<br>**说明**<br>仅支持2048和3072位的RSA密钥。 | 支持 |
| [配置HTTP/2](https://help.aliyun.com/zh/cdn/user-guide/enable-http-or-2 "") | 支持 |
| [配置协议重定向](https://help.aliyun.com/zh/cdn/user-guide/configure-url-redirection "")<br>**说明**<br>仅支持默认和HTTP跳转至HTTPS方式。 | 支持 |
| [配置TLS版本控制与加密套件](https://help.aliyun.com/zh/cdn/user-guide/configure-tls-version-control "") | 不支持 |
| [配置HSTS](https://help.aliyun.com/zh/cdn/user-guide/configure-hsts "") | 不支持 |
| [配置OCSP Stapling](https://help.aliyun.com/zh/cdn/user-guide/configure-ocsp-stapling "") | 不支持 |
| [客户端认证证书](https://help.aliyun.com/zh/cdn/user-guide/client-authentication-certificate "") | 不支持 |
| 访问控制 | [配置Referer防盗链](https://help.aliyun.com/zh/cdn/user-guide/configure-a-referer-whitelist-or-blacklist-to-enable-hotlink-protection "") | 不支持 |
| [URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/url-signing/ "") | 不支持 |
| [IP黑/白名单](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ip-blacklist-or-whitelist "") | 不支持 |
| [配置UA黑白名单](https://help.aliyun.com/zh/cdn/user-guide/configure-a-user-agent-blacklist-or-whitelist "") | 不支持 |
| [配置远程鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-remote-authentication "") | 不支持 |
| 性能优化 | [页面优化](https://help.aliyun.com/zh/cdn/user-guide/enable-html-optimization "") | 不支持 |
| [Gzip压缩](https://help.aliyun.com/zh/cdn/user-guide/use-the-gzip-compression-feature "") | 不支持 |
| [Brotli压缩](https://help.aliyun.com/zh/cdn/user-guide/configure-brotli-compression "") | 不支持 |
| [忽略参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters "") | 不支持 |
| [图像处理](https://help.aliyun.com/zh/cdn/user-guide/image-editing/ "") | 不支持 |
| 视频相关 | [配置Range回源](https://help.aliyun.com/zh/cdn/user-guide/object-chunking "") | 不支持 |
| [配置拖拽播放](https://help.aliyun.com/zh/cdn/user-guide/video-seeking "") | 不支持 |
| [配置听视频](https://help.aliyun.com/zh/cdn/user-guide/audio-extraction "") | 不支持 |
| [配置音视频试看](https://help.aliyun.com/zh/cdn/user-guide/audio-and-video-preview "") | 不支持 |
| [配置M3U8标准加密改写](https://help.aliyun.com/zh/cdn/user-guide/m3u8-encryption-and-rewrite "") | 不支持 |
| 流量限制 | [配置用量封顶](https://help.aliyun.com/zh/cdn/user-guide/configure-usage-cap "") | 不支持 |
| [配置单请求限速](https://help.aliyun.com/zh/cdn/user-guide/configuration-order-request-speed-limit "") | 不支持 |
| 边缘脚本 | [边缘脚本EdgeScript](https://help.aliyun.com/zh/cdn/user-guide/edgescript-overview "") | 不支持 |
| 规则引擎 | [规则引擎](https://help.aliyun.com/zh/cdn/user-guide/rules-engine "") | 不支持 |
| Quic协议 | [配置QUIC协议](https://help.aliyun.com/zh/cdn/user-guide/what-is-the-quic-protocol "") | 不支持 |
| 资源监控 | 资源监控 | [资源监控](https://help.aliyun.com/zh/cdn/user-guide/resource-monitoring "") | 不支持 |
| 实时监控 | [实时监控](https://help.aliyun.com/zh/cdn/user-guide/real-time-monitoring "") | 不支持 |
| 边缘脚本监控 | [边缘脚本监控](https://help.aliyun.com/zh/cdn/user-guide/es-monitoring "") | 不支持 |
| 刷新和预热 | 刷新资源 | [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "") | 支持 |
| 预热资源 | [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "") | 不支持 |
| 工具服务 | 检测IP地址 | [检测IP地址](https://help.aliyun.com/zh/cdn/user-guide/does-the-ip-belong-to-cdn-pops "") | 支持 |
| 自助诊断工具 | [自助诊断工具](https://help.aliyun.com/zh/cdn/user-guide/self-diagnostic-tools "") | 不支持 |
| 安全防护 | 证书服务 | [批量配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate-for-multiple-domain-names "") | 支持 |
| [查询域名证书](https://help.aliyun.com/zh/cdn/user-guide/query-ssl-certificates-of-domain-names "") | 支持 |
| 沙箱 | [沙箱说明](https://help.aliyun.com/zh/cdn/user-guide/introduction-to-sandboxes "") | 不支持 |
| 用量查询 | 用量查询 | [用量查询](https://help.aliyun.com/zh/cdn/user-guide/query-resource-usage-1 "") | 支持 |
| 资源包管理 | [资源包管理](https://help.aliyun.com/zh/cdn/user-guide/query-the-details-of-resource-plans "") | 支持 |

## **配置入口**

1. [CDN控制台](https://cdn.console.aliyun.com/)

2. 在左侧导航栏，单击 **域名管理**。

3. 单击 **添加域名**，在 **域名信息** 页面，配置 **加速区域**，选择 **全球（不包含中国内地）**。

4. 开启 **全球资源计划**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1577459471/p966100.png)