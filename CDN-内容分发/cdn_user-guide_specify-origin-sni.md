### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/)[回源SNI](https://help.aliyun.com/zh/cdn/user-guide/origin-sni/)指定回源SNI

# 指定回源SNI

更新时间：2025-09-09 02:38:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

指定回源SNI和默认回源SNI的区别

操作步骤

当您的加速域名配置了多个源站地址，且回源协议为HTTPS，同时每个源站对外提供Web服务的域名地址存在差异的情况下，您可以设置使用不同的SNI值回源到不同的源站地址，这样不同的源站将会根据不同的SNI值来响应不同的HTTPS证书给阿里云CDN回源节点，以便于阿里云CDN回源节点能够与不同的源站地址之间成功建立SSL连接。

## **指定回源SNI和默认回源SNI的区别**

- 指定回源SNI可以实现在多源站的情况下，不同的源站设置不同的回源SNI。

- 默认回源SNI是指，无论是单个还是多个源站，使用同一个回源SNI。默认回源SNI请参见 [配置默认回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni "")。

- 当指定回源SNI与默认回源SNI同时设置时，优先使用指定回源SNI的域名配置。


## **操作步骤**

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在 **回源配置** 页签下找到 **指定回源SNI**，单击 **添加**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2097937571/p1004853.png)




| **配置项** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **配置项** | **说明** |
| **源站地址** | 需要指定SNI的源站地址。 |
| **SNI HOST** | - **跟随源站地址**：<br>     <br>     - 效果：SNI值等于源站地址。<br>       <br>     - 使用场景：源站地址为域名地址，并且源站SNI校验要求匹配为源站域名。<br>   - **跟随回源HOST**：<br>     <br>     - 效果：SNI值等于回源HOST。<br>       <br>     - 使用场景：源站SNI校验要求匹配为回源HOST。<br>   - **自定义**：<br>     <br>     - 效果：用户可以设定任意的SNI值。<br>       <br>     - 使用场景：源站SNI校验要求匹配的值既不是源站域名，也不是回源HOST。 |
| **长连接SNI** | - 开启：CDN节点将请求发送给源站时，SNI不同的请求将使用不同的长连接，避免出现同一个长连接上SNI冲突的情况。<br>     <br>   - 关闭：CDN节点与源站的同一个长连接上面只能使用同一个SNI。 |

5. 单击 **确定**，完成配置。