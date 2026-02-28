### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[常见问题](https://help.aliyun.com/zh/sae/faq-1/)[应用托管FAQ](https://help.aliyun.com/zh/sae/faq-about-application-hosting/)[应用设置FAQ](https://help.aliyun.com/zh/sae/faq-about-applcation-configurations/)UseWisp2失败怎么办？

# UseWisp2失败怎么办？

更新时间：2024-09-02 14:33:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SAE应用如何设置时区？](https://help.aliyun.com/zh/sae/how-to-specify-a-time-zone-for-an-sae-application)[下一篇：SAE是否支持定时部署？](https://help.aliyun.com/zh/sae/does-sae-support-scheduled-application-deployment)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

问题现象

可能原因

解决方案

本文介绍使用SAE时，如何处理UseWisp2失败的问题。

## 问题现象

配置参数UseWisp2后，报错信息如下图所示。![sc_error_message_of_UseWisp2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9433621861/p628394.png)

## 可能原因

在非Dragonwell运行环境的JVM里添加了参数UseWisp2。

## 解决方案

参数UseWisp2表示Dragonwell的Wisp2协程，用于提升多线程调度切换的性能。如果在非Dragonwell运行环境的JVM里添加了该参数，遇到报错，删除该参数即可。