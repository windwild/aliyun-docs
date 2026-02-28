### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[工具服务](https://help.aliyun.com/zh/cdn/user-guide/tools/)自助诊断工具

# 自助诊断工具

更新时间：2023-10-24 03:28:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：检测IP地址是否属于阿里云CDN节点](https://help.aliyun.com/zh/cdn/user-guide/does-the-ip-belong-to-cdn-pops)[下一篇：批量配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate-for-multiple-domain-names)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用场景

操作步骤

如果在使用CDN过程中，遇到了网页打不开、页面报错等问题时，您可以通过自助诊断工具来进行诊断。诊断工具会告知本次诊断结果，您可以根据结果来调整CDN配置或提交工单进行咨询。

## 使用场景

主要支持以下情况：

- **域名访问异常**：当您成功添加CDN域名成功后，无法正常访问，您可以尝试使用自助诊断工具发现并解决问题。

- **域名访问慢**：当您的CDN域名出现偶发性或持续性的访问慢问题时，您可以尝试使用自助诊断工具发现并解决问题。

- **其他情况**：如果您想了解CDN加速的健康度和加速链路情况，您也可以使用自助诊断工具，了解加速链路的细节。


## **操作步骤**

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **工具服务**。
3. 在 **自助诊断工具** 区域单击 **去使用**。

4. 进入 **自助诊断工具** 页面后，单击 **创建诊断**。

5. 在 **创建诊断** 对话框中输入 **诊断URL**，单击 **验证**。
![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9106967961/p728811.png)


**说明**





   - 仅支持当前账号下的域名诊断。

   - 填入的格式必须是一个URL链接，不能是域名名称，否则会报错。

   - 若被诊断URL中的域名未添加到CDN，请先添加域名，具体请参见 [添加加速域名](https://help.aliyun.com/zh/cdn/add-a-domain-name "")。

   - 若您的域名为非 **正常运行** 状态，则加速不成功，诊断失败。

   - 若您的域名在沙箱或黑名单中，加速效果将受到影响。

   - 若您的域名CNAME未配置或者配置错误，则访问无法通过CDN加速，具体请参见 [配置CNAME](https://help.aliyun.com/zh/cdn/add-a-cname-record-for-a-domain-name "")。


6. 成功验证后会生成 **诊断链接**，链接有效时长2小时，您可以通过该链接查看客户端的诊断信息。访问一次诊断链接会生成一个诊断报告，最多可点击访问10次。完整的CDN链路诊断信息，请返回到 **自助诊断工具** 页面，单击 **操作** 列的 **查看报告**。
![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8106967961/p728842.png)


**说明**





诊断链接中包含请求耗时、缓存耗时、本地IP、运营商等客户端信息；诊断报告中包含诊断状态、调度状态、异常项、域名状态、响应时长、响应速度等更多信息。