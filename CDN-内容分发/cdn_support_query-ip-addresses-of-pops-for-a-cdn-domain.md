### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[服务支持](https://help.aliyun.com/zh/cdn/support/)[回源/源站](https://help.aliyun.com/zh/cdn/support/51a989/)CDN回源节点IP地址有哪些？

# CDN回源节点IP地址有哪些？

更新时间：2025-09-03 22:27:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CDN如何在源站上获取客户端真实IP](https://help.aliyun.com/zh/cdn/support/how-to-obtain-the-real-client-ip-from-the-origin-server)[下一篇：如何处理源站的302跳转？](https://help.aliyun.com/zh/cdn/support/alibaba-cloud-cdn-process-302-redirects-from-an-origin-server)

该文章对您有帮助吗？

反馈

为了保护源站安全，一些用户希望获取阿里云CDN的回源节点IP，并在源站设置白名单，只允许阿里云CDN回源访问。

但需要注意的是，阿里云CDN回源时会动态分配节点IP，这些IP并不是固定的。因此， **不建议在源站设置固定的回源IP列表**，否则可能导致回源失败。

如果有特殊需求（例如源站安装了安全防护软件，如安全狗），确实需要配置白名单，请通过调用 [查询节点IP地址-L2](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-describel2vipsbydomain "") 获取最新的回源节点IP列表，并将其添加到源站白名单中，以确保正常访问。

**注意：** 该接口仅支持日峰值带宽为1Gbps以上的用户调用，如果符合该条件，请提交工单，申请该接口的调用权限。