## 问题现象

在轻量级配置及注册中心中，服务消费者调用服务提供者失败。

## 可能原因

- 服务在轻量级配置及注册中心注册失败。
- 服务的网络发生切换。
- 服务推送失败。

## 解决方案

1. 在轻量级配置及注册中心，查看服务是否注册成功。
   - 注册成功，执行 [步骤](https://help.aliyun.com/zh/sae/service-call-failed#step-yum-do3-diz "") [2](https://help.aliyun.com/zh/sae/service-call-failed#step-yum-do3-diz "")。

   - 注册失败，执行 [步骤](https://help.aliyun.com/zh/sae/service-call-failed#step-hhv-45r-uhd "") [5](https://help.aliyun.com/zh/sae/service-call-failed#step-hhv-45r-uhd "")。
2. 查看服务所在的实例是否发生网络切换，即服务提供方的IP地址变动。
   - 发生了网络切换，执行 [步骤](https://help.aliyun.com/zh/sae/service-call-failed#step-4v1-byy-zm8 "") [3](https://help.aliyun.com/zh/sae/service-call-failed#step-4v1-byy-zm8 "")。

   - 未发生网络切换，执行 [步骤](https://help.aliyun.com/zh/sae/service-call-failed#step-mdk-deg-uek "") [4](https://help.aliyun.com/zh/sae/service-call-failed#step-mdk-deg-uek "")。
3. 重新启动应用，使用最新的IP地址注册成功后，再次检查调用是否成功。
   - 调用成功，结束。
   - 仍然调用不通，执行 [步骤](https://help.aliyun.com/zh/sae/service-call-failed#step-mdk-deg-uek "") [4](https://help.aliyun.com/zh/sae/service-call-failed#step-mdk-deg-uek "")。
4. 查看轻量级注册及配置中心的推送日志（`${安装目录}/logs/config-server-push.log`），排查服务是否推送成功。
   - 如果服务端推送成功，则在消费端的机器或者容器的日志文件中，查看是否接收到最新的服务IP地址列表，或者观察是否有ERROR级别的日志。

     基于不同方式开发的应用，日志文件的路径不同。


     - 基于HSF和Dubbo开发的应用：${user.home}/logs/configclient/config-client.log
     - 基于ACM开发的应用：${user.home}/logs/vipsrv-logs/vipclient.log
     - 基于Nacos开发的应用：${user.home}/logs/nacos/naming.log

   - 如果服务端推送不成功，请联系产品技术专家获取技术支持。更多信息，请参见[联系我们](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/support/contact-us#concept-2361378 "")。
5. 在轻量版配置及注册中心，查看不到该服务的注册。此时，可以在应用所在的机器或者容器内查看日志文件${user.home}/logs/configclient/config-client.log，查看是否注册发生异常。

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 服务调用不通怎么办？

# 服务调用不通怎么办？

更新时间：2022-12-23 00:21:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

问题现象

可能原因

解决方案