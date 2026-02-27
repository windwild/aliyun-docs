### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[常见问题](https://help.aliyun.com/zh/functioncompute/fc/faq-3-0/)[代码开发FAQ](https://help.aliyun.com/zh/functioncompute/fc/faq-about-code-development-1/)[咨询类FAQ](https://help.aliyun.com/zh/functioncompute/fc/general-faq-1/)函数计算是否支持SSE流式响应？

# 函数计算是否支持SSE流式响应？

更新时间：2024-07-03 01:44:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用go build编译的速度较慢怎么办？](https://help.aliyun.com/zh/functioncompute/fc/what-to-do-if-go-build-compilation-takes-a-long-time)[下一篇：函数计算是否支持部署静态资源？](https://help.aliyun.com/zh/functioncompute/fc/function-compute-support-deploying-static-resources-1)

该文章对您有帮助吗？

反馈

SSE是Server-Sent Events的简称，即流式响应。目前在函数计算中，使用创建 **Web函数** 方式部署的函数支持流式响应，使用创建 **事件函数或任务函数** 方式部署的函数暂不支持流式响应。

使用创建 **Web函数** 方式部署函数时，函数计算会根据响应头中是否带有`Transfer-Encoding:chunked`来判断是否为流式响应。为了方便您的使用，使用 **Web函数** 方式部署函数时，在运行时中可以选择流式响应的示例代码。