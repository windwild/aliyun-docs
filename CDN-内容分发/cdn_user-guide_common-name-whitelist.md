### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/) [回源SNI](https://help.aliyun.com/zh/cdn/user-guide/origin-sni/) Common Name白名单

# Common Name白名单

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：指定回源SNI](https://help.aliyun.com/zh/cdn/user-guide/specify-origin-sni)[下一篇：重写回源请求](https://help.aliyun.com/zh/cdn/user-guide/rewrite-origin-requests/)

该文章对您有帮助吗？

反馈

CDN节点以HTTPS协议回源时，会对回源请求的SNI和源站返回证书的CommonName进行校验，不一致时无法成功回源。将证书的Common Name加入白名单后，即使SNI和CommonName不一致也可成功回源。

## 功能示例

当CDN节点回源时，如果SNI和CommonName不一致时（如下图），无法建连。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7826519371/CAEQOhiBgMDx6K2K6xgiIDY1N2I1ZDYzZTg1YzQxYTdhZDM3NzZmZGJjY2ZmNjUw4020376_20230925174415.774.svg)

此时如果将domain2添加至CommonName白名单中，即可成功建连。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8826519371/CAEQORiBgMCdqs.W6hgiIDcxZTc2NTZlNzZkNDQ3ZWU5N2JmZmQwOTYyYzAxNjZi4020376_20230925174415.774.svg)

## 操作步骤

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **Common Name白名单** 区域，打开 **Common Name白名单** 状态开关。

6. 填写需要加入的域名。 ![ Common Name白名单](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3489975961/p90992.png)

7. 单击 **确定**。