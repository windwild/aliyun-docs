- v1.0.9.15-g3957085-aliyun

修复了偶发的升级失败的问题。

- v1.0.9.14-ga0346bb-aliyun
  - 修复Terway获取弹性网卡信息时偶发性失败的问题。
  - 修复创建容器时上报failed to move veth to host netns: file exists 的问题。

  - 新增对弹性网卡状态定期扫描，对于异常释放的弹性网卡会定期回收的功能。
  - 优化健康检查：Terway健康检查方式从HTTP路径检查优化成TCP端口检查。

请前往容器服务控制台升级最新的Terway系统组件，此次升级不会对业务造成影响。

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[动态与公告](https://help.aliyun.com/zh/ack/product-overview/announcements-and-updates/)[组件变更](https://help.aliyun.com/zh/ack/product-overview/components/)【组件升级】升级Terway组件的公告

# 【组件升级】升级Terway组件的公告

更新时间：2021-06-07 22:47:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：【组件升级】Helm V2 Tiller升级公告](https://help.aliyun.com/zh/ack/product-overview/component-updates-update-helm-v2-to-v3)[下一篇：【组件升级】升级Metrics Server组件公告](https://help.aliyun.com/zh/ack/product-overview/component-upgrades-upgrade-metrics-server)

该文章对您有帮助吗？

反馈