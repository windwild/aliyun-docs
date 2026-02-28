### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) waitUntil类FAQ

# waitUntil类FAQ

更新时间：2024-11-01 01:36:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么Fetch请求有时能完成，有时不能完成？

waitUntil可以调用多次吗？

本文为您列出了边缘程序ER（EdgeRoutine）的waitUntil相关的常见问题。

## 为什么Fetch请求有时能完成，有时不能完成？

Fetch请求有时能完成，有时不能完成的原因如下：

- 受生命周期限制

当您调用`addEventListener`注册事件回调函数时，会自动创建上下文。当您的主回复结束，即调用`event.respondWith`返回的Response对象被读取完毕（包括header、body）后会结束上下文。

所有异步函数的生命周期都在上下文生命周期之内，您在回调函数中await的Promise会阻塞当前的回调函数，直到该Promise被resolve。如果您不想await，则可以使用event.waitUntil函数，该函数会延长上下文的生命周期，直到所有被waitUntil的Promise执行完毕。

- 受共享状态影响



多个上下文之间不能共享状态，任何非JS标准的数据结构都不支持跨上下文共享，例如Service Worker API的数据结构、Stream对象。当上下文A使用非上下文A的对象时，会被ER检测出来并抛出异常。





**说明**





您可以使用JS的原生对象共享状态，例如String、Array、Object和数字等，您自己编写的Class也可以用于共享状态。

- 受并发影响

所有没有被await的Promise都是并发的，如果您希望ER程序能立即回复浏览器，可以不await子请求，直接使用waitUntil保证程序正常执行。

- 受异步错误影响

如果waitUntil中的子请求有一个出错，整个上下文会被立刻退出。


## waitUntil可以调用多次吗？

waitUntil可以调用多次，也可以嵌套waitUntil，即一个waitUntil的Promise被resolve，其回调函数中继续调用waitUntil。

**说明**

上下文有时间限制，超过时间的上下文会被强制退出。