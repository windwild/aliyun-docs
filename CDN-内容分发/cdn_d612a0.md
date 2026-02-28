本文为您介绍了阿里云实时日志计费调整详情。

## 调整内容

- 价格。

自2019年10月17日起，实时日志由原来0.06元/万次调整至0.01元/万次，调整原因如下所示。


  - 技术优化升级，让利客户。
  - 去除了SLS的费用，原来的0.06元包含了日志推送到SLS后产生的SLS费用，本次调整是让阿里云SLS和客户自行结算SLS的费用，不再由阿里云CDN承包成本。
  - 为后续更灵活的产品形态预留能力，目前由于包含了SLS的费用，所以只能强制日志推送到阿里云SLS。

变更前如下图所示。
![变更前](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9976148951/p59341.png)
变更后如下图所示。
![变更后](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9976148951/p59342.png)
- 账单。

变更前使用CDN实时日志功能只会产生一份账单，费用在CDN产品下，单价0.06元/万次。变更后使用CDN实时日志功能会产生两份账单，一份在CDN产品下，单价0.01元/万次。另一份在SLS产品下，SLS价格请参见[SLS定价](https://www.aliyun.com/price/product?spm=5176.10695662.1119587.3.3a376eee2mY3oJ#/sls/detail)。


- 用户操作。

在CDN控制台开启和使用实时日志的操作没有变化。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 实时日志计费调整

# 实时日志计费调整

更新时间：2022-03-03 01:00:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调整内容