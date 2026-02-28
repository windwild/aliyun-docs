### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for ALB（原ALB日志中心）](https://help.aliyun.com/zh/sls/usage-notes-15/)日志字段详情

# 日志字段详情

更新时间：2024-01-23 02:53:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

本文介绍ALB负载均衡7层访问日志的字段详情。

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为alb\_layer7\_access\_log。 |
| body\_bytes\_sent | 发送给客户端的HTTP Body字节数。 |
| client\_ip | 请求客户端IP地址。 |
| host | 域名或IP地址。优先从请求参数中获取host，如果获取不到则从host header取值，如果还是获取不到则以处理请求的后端服务器IP地址作为host。 |
| http\_host | 请求报文host header的内容。 |
| http\_referer | URL跳转来源。 |
| http\_user\_agent | 客户端浏览器等信息。 |
| http\_x\_forwarded\_for | 经过HTTP代理后的客户端IP地址。 |
| http\_x\_real\_ip | 真实的客户端IP地址。 |
| read\_request\_time | Proxy读取请求的时间，单位：毫秒。 |
| request\_length | 请求的长度，包括请求行、请求头和请求正文。 |
| request\_method | 请求方法。 |
| request\_time | Proxy收到第一个请求报文的时间到Proxy返回应答之间的间隔时间，单位：秒。 |
| request\_uri | Proxy收到的请求报文的URI。 |
| scheme | 请求的schema，包括HTTP、HTTPS。 |
| server\_protocol | Proxy收到的HTTP协议的版本，例如HTTP/1.0或HTTP/1.1。 |
| slb\_vport | 负载均衡的监听端口。 |
| app\_lb\_id | ALB负载均衡实例ID。 |
| ssl\_cipher | 建立SSL连接使用的密码，例如ECDHE-RSA-AES128-GCM-SHA256等。 |
| ssl\_protocol | 建立SSL连接使用的协议，例如TLSv1.2。 |
| status | Proxy应答报文的状态。 |
| tcpinfo\_rtt | 客户端TCP连接时间，单位：微秒。 |
| time | 日志记录时间。 |
| upstream\_addr | 后端服务器的IP地址和端口。 |
| upstream\_response\_time | 从负载均衡向后端建立连接开始到接收完数据然后关闭连接为止的时间，单位：秒。 |
| upstream\_status | Proxy收到的后端服务器的响应状态码。 |
| vip\_addr | 虚拟IP地址。 |
| write\_response\_time | Proxy收到后端的请求后，把这个请求发送给客户端的时间。单位：毫秒。 |