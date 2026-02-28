### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/)[回源HOST](https://help.aliyun.com/zh/cdn/user-guide/origin-host/)配置默认回源HOST

# 配置默认回源HOST

更新时间：2025-04-28 03:45:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OSS私有Bucket回源](https://help.aliyun.com/zh/cdn/user-guide/grant-alibaba-cloud-cdn-access-permissions-on-private-oss-buckets)[下一篇：指定源站回源HOST](https://help.aliyun.com/zh/cdn/user-guide/specify-an-origin-host-for-each-origin)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景介绍

虚拟站点技术

默认回源HOST

操作步骤

配置示例

CDN在发起回源请求时携带的HOST请求头默认为加速域名，您可使用本功能自定义回源HOST请求头。

## **背景介绍**

当您有多个加速域名，每个加速域名负责加速不同静态的资源，常见的做法是开发多个源站，以支持不同加速域名发起回源请求资源。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0336285471/CAEQShiBgMD5n.m52BgiIGFkN2ExN2QzOTliYTRhZjFiN2E5NGIxNmFiYmY3NDI24020287_20230925170844.702.svg)

如果加速域名比较多，回源流量很少时，重复建站会带来资源的极度浪费，您可通过虚拟站点技术解决该问题。

### **虚拟站点技术**

虚拟站点技术是一种在单个Web服务器上提供多个网站服务的技术。服务器通过使用不同的域名或主机名来区分和隔离不同的网站。当用户请求访问某个特定的域名或主机名时，服务器会根据请求的域名或主机名，将请求定向到相应的虚拟站点，从而提供相应的网站内容。示意图如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1336285471/CAEQShiBgICAqre62BgiIGM2NmRjMDM2ZmFkMjRkYTc5MTM5NTc5OTMzYTViMzA34020287_20230925170844.702.svg)

**Nginx相关实现**

Nginx支持通过`server`区块配置多个虚拟站点，示例如下：

```yaml
server {
    listen      80;
    server_name example.org www.example.org;
    ...
}

server {
    listen      80;
    server_name example.net www.example.net;
    ...
}

server {
    listen      80;
    server_name example.com www.example.com;
    ...
}
```

项目配置了3个虚拟站点，分别是`example.org`、`example.net`、`example.com`。Nginx通过`server_name`匹配HTTP请求头中的`Host`字段来选择虚拟站点，如果没有匹配到任何一个虚拟站点，Nginx会使用默认的虚拟站点提供服务（若未配置，默认为第一个`server`配置的默认站点）。

### **默认回源HOST**

当您访问一个URL链接时，不指定HOST字段，该请求的HOST字段默认为您访问URL链接的主机+端口部分。但是CDN默认将HOST字段设置为加速域名，您也可以根据您源站的虚拟站点配置，自定义HOST字段的默认值。

**重要**

您的源站服务器需支持通过HOST请求头匹配不同的虚拟站点，否则该功能配置无法达到预期的功能效果。

## **操作步骤**

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **默认回源HOST** 区域，单击 **修改配置**。

6. 打开 **回源HOST** 开关，选择 **域名类型**。



![回源配置](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0664788951/p64119.png)






| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **加速域名** | 以终端用户访问的加速域名作为回源HOST。 |
| **源站域名** | 以源站服务器的域名作为回源HOST。<br>**说明**<br>   - 源站信息为IP地址类型时， **源站域名** 选项置灰，不可选择。<br>     <br>   - 源站信息为OSS域名时，将会同步开启 **回源HOST** 功能，并且设置域名类型为 **源站域名**。 |
| **自定义域名** | 以用户指定的域名作为回源HOST。<br>**说明**<br>   - 自定义域名确保为您已经绑定的域名，否则回源失败。<br>     <br>   - 您的源站绑定了多个域名，您希望用户从指定域名获取资源。 |

7. 单击 **确定**。


## **配置示例**

**示例一：**当源站类型为域名。

| **域名** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **域名** | **说明** |
| 加速域名：<br>`image.example.com`<br>源站地址：<br>`source.example.com` | 功能默认关闭。您可主动开启默认回源HOST功能。<br>回源域名类型说明：<br>- **加速域名**：当CDN回源时，会到`source.example.com`源站上的`image.example.com`的虚拟站点获取资源。<br>  <br>- **源站域名**：当CDN回源时，会到源站`source.example.com`获取资源。<br>  <br>- **自定义域名**：回源HOST为用户输入的自定义域名。 |

**示例二：**当源站类型为IP地址。

| **域名** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **域名** | **说明** |
| 加速域名：<br>`example.com`<br>源站地址：<br>`10.10.10.10` | 功能默认关闭。您可主动开启默认回源HOST功能。<br>回源域名类型说明：<br>- **加速域名**：当CDN回源时，会到`10.10.10.10`这台主机上的`example.com`的虚拟站点获取资源。<br>  <br>- **源站域名**：源站信息为IP地址类型时， **源站域名** 选项置灰，不可选择。<br>  <br>- **自定义域名**：当CDN回源时，会到`10.10.10.10`这台主机上自定义域名的虚拟主机获取资源。 |

**示例三：**当源站类型为OSS域名。

| **域名** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **域名** | **说明** |
| 加速域名：<br>`example.com`<br>源站地址：<br>`example.oss-cn-hangzhou.aliyuncs.com` | 当源站信息为OSS域名时，CDN将会同步开启 **回源HOST** 功能，并且设置域名类型为 **源站域名**。<br>回源域名类型说明：<br>- **加速域名**：当CDN回源时，会到`example.oss-cn-hangzhou.aliyuncs.com`OSS域名上的`example.com`站点获取资源。<br>  <br>- **源站域名**：当CDN回源时，会到OSS域名`example.oss-cn-hangzhou.aliyuncs.com`获取资源。<br>  <br>- **自定义域名**：当CDN回源时，会到您的`example.oss-cn-hangzhou.aliyuncs.com`站点上自定义域名的虚拟站点获取资源。 |