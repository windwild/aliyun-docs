### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [基本配置](https://help.aliyun.com/zh/cdn/user-guide/basic-settings/) 加速区域

# 加速区域

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：概述](https://help.aliyun.com/zh/cdn/user-guide/overview-5)[下一篇：配置全球资源计划](https://help.aliyun.com/zh/cdn/user-guide/configure-global-resource-planning)

该文章对您有帮助吗？

反馈

介绍三种加速区域的区别以及如何选择适合自己的加速区域，当您需要变更加速域名的CDN服务范围时，您可以通过切换加速区域功能实现。

## **加速区域**

|     |     |
| --- | --- |
| **参数** | **说明** |
| **仅中国内地** | 如果选择 **仅中国内地**，代表全球用户访问均会调度至中国内地加速节点进行服务（海外用户的访问流量将会被调度至华东电信的CDN节点）。同时需要工信部备案。域名备案方法，请参见 [使用限制](https://help.aliyun.com/zh/cdn/product-overview/limits#concept-um5-wdx-wdb "")。 |
| **全球** | 如果选择 **全球**，全球用户访问将会择优调度至最近的加速节点进行服务。同时需要工信部备案。域名备案方法，请参见 [使用限制](https://help.aliyun.com/zh/cdn/product-overview/limits#concept-um5-wdx-wdb "")。 |
| **全球（不包含中国内地）** | 如果选择 **全球（不包含中国内地）**，全球用户访问均会调度至中国香港、中国澳门、中国台湾以及其他国家和地区的加速节点进行服务（中国内地用户将会被调度至日本、新加坡和中国香港的CDN节点）。该选项无需工信部备案。<br>**说明** <br>加速区域选择 **全球（不包含中国内地）** 的情况下，客户端将无法访问中国内地的CDN节点，因此在将其他加速区域切换到“全球（不包含中国内地）”，需要确保已经没有中国内地的流量（尤其需要注意本地DNS缓存的影响）。 |

## 切换加速区域

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在 **基础信息** 区域，单击 **修改**。

5. 在 **加速区域** 对话框，选择您需要切换的加速区域。

![加速区域](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5564788951/p94752.png)

6. 单击 **确定**。