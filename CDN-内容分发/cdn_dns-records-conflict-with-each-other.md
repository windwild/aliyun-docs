### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 如何解决DNS解析记录冲突

# 如何解决DNS解析记录冲突

更新时间：2025-11-27 02:47:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

场景一：已有网站（A记录）接入CDN（需CNAME）

操作步骤

场景二：根域名（@）同时用于网站和企业邮箱

操作步骤

配置生效验证

添加解析记录时，若提示“记录冲突”导致无法保存，通常是由于待添加的CNAME记录与同一主机记录下已存在的其他记录（如A、MX记录）发生冲突。

## **场景一：已有网站（A记录）接入CDN（需CNAME）**

建议在业务低峰期操作，以降低切换窗口影响。

### **操作步骤**

1. CDN控制台完成域名接入和CNAME配置，确保CNAME地址已生效。

2. 降低原A记录TTL。

1. 登录 [云解析DNS控制台](https://dns.console.aliyun.com/)，进入目标域名的 **解析设置** 页面。

2. 找到待修改的主机记录（如`www`）对应的A记录，将其TTL修改为当前版本支持的最小值：

      - 个人版用户：最小为10分钟。

      - 企业旗舰版用户：可设为60秒或更低（如10秒）。
3. 等待原TTL时长（例如原为10分钟，则等待≥10分钟），确保全球DNS缓存更新为新TTL。
3. 切换至CNAME记录（建议连续操作，间隔越短越好）。

1. 删除原A记录。

2. 添加CNAME记录。




      | **参数** | **值示例** | **说明** |
      | --- | --- | --- |



      |     |     |     |
      | --- | --- | --- |
      | **参数** | **值示例** | **说明** |
      | 记录类型 | `CNAME` | 必选 |
      | 主机记录 | `www` | 与原记录一致 |
      | 记录值 | `example.cdn.aliyun.com.` | 从CDN控制台复制，末尾的点`.`不可省略 |
      | TTL | 按CDN推荐值设置（通常10分钟） | 可保持默认 |

* * *

## **场景二：根域名（@）同时用于网站和企业邮箱**

通过URL转发将根域名的HTTP/HTTPS请求重定向至已配置CNAME的子域名（如 `www`），从而规避 CNAME与MX的冲突。

### **操作步骤**

1. 根域名（URL转发前域名）与`www`域名（URL转发后域名）均已完成 ICP 备案（中国境内服务强制要求）。

2. 为 `www` 添加CNAME记录，指向CDN提供的地址（如 `example.cdn.aliyun.com.`）。

3. 为根域名（`@`）添加显性URL转发记录，目标为 `https://www.example.com`。

4. 保留根域名（`@`）的MX记录用于邮件服务。


**说明**

此方案仅适用于 Web 访问场景，非HTTP 协议（如 API、邮件客户端）无法通过 URL 转发访问根域名

## 配置生效验证

DNS 修改后需等待全球缓存刷新。可通过以下命令验证：

```bash
# 验证 CNAME
dig www.example.com CNAME +short
# 预期输出：example.cdn.aliyun.com.

# 验证 MX
dig example.com MX +short
# 预期输出：10 your-mail-server.com.
```