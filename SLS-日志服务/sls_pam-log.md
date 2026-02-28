### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[日志审计（旧版）](https://help.aliyun.com/zh/sls/log-audit-service/)[日志字段详情](https://help.aliyun.com/zh/sls/log-fields-34/)PAM日志

# PAM日志

更新时间：2023-08-25 04:10:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DNS](https://help.aliyun.com/zh/sls/dns)[下一篇：常见问题及错误排查](https://help.aliyun.com/zh/sls/faq-and-troubleshooting-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

运维审计日志

操作审计日志

本文介绍特权访问管理中心PAM的运维审计日志和操作审计日志字段详情。

## **运维审计日志**

| **字段名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段名称** | **说明** |
| user\_id | 用户ID |
| instance\_id | 实例ID |
| operator\_id | 运维员ID |
| user\_type | 用户类型，包括：<br>- RAM\_ROOT：阿里云账号<br>  <br>- RAM\_SUB\_USER：阿里云RAM用户<br>  <br>- BUILTIN：PAM本地账号 |
| system\_account | 系统账户名 |
| asset\_ip | 资产IP地址 |
| asset\_name | 资产名称 |
| asset\_port | 资产端口 |
| asset\_region\_id | 资产所在地域 |
| asset\_id | 资产ID |
| asset\_type | 资产类型，包括<br>- Ecs：云服务器ECS<br>  <br>- Ack：容器服务Kubernetes版ACK |
| content | 指令内容 |
| credential\_name | 凭据名称 |
| event\_time | 事件时间 |
| intercepted | 是否被拦截 |
| protocol\_type | 协议类型，包括：<br>- ssh：SSH协议<br>  <br>- rdp：RDP协议<br>  <br>- k8s：kubectl exec协议 |
| region\_id | 会话发生地域 |
| session\_id | 会话的唯一标识符ID |
| source\_ip | 源IP地址 |
| event\_type | 事件类型，包括：<br>- session：会话<br>  <br>- cmd：命令 |
| event\_sub\_type | 事件子类型<br>- close：会话关闭<br>  <br>- open：会话开始<br>  <br>- command：指令执行<br>  <br>- update\_asset\_fingerprint：更新指纹 |
| video\_size | 录像大小 |

## **操作审计日志**

| **字段名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段名称** | **说明** |
| user\_id | 用户ID |
| instance\_id | 实例ID |
| event\_sub\_type | 事件类型，包括：<br>- FILE\_Upload：文件上传<br>  <br>- FILE\_Download：文件下载 |
| event\_type | 事件大类，值为FILE，表示文件相关操作。 |
| event\_detail | 事件详情 |
| event\_content | 事件内容 |
| event\_id | 事件UUID |
| user\_name | 操作用户名 |
| user\_type | 操作用户类型，包括：<br>- RAM\_ROOT：阿里云账号<br>  <br>- RAM\_SUB\_USER：阿里云RAM用户<br>  <br>- BUILTIN：PAM本地账号 |
| operator\_id | 操作人ID |
| start\_time | 事件开始时间 |
| end\_time | 事件结束时间 |