### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[日志与监控](https://help.aliyun.com/zh/oss/user-guide/log-management-and-monitoring/)[监控服务](https://help.aliyun.com/zh/oss/user-guide/overview-72/)常见问题

# 常见问题

更新时间：2025-02-28 00:47:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OSS系统事件](https://help.aliyun.com/zh/oss/user-guide/oss-system-events)[下一篇：静态网站托管](https://help.aliyun.com/zh/oss/user-guide/hosting-static-websites)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

案例：报警规则的状态出现“数据不足”

案例：云监控上发现上传下载延迟

案例：某公司自己的监控系统发现OSS请求数据有延迟

案例：有效请求率降低

案例：云监控报警404

案例：云监控出现NoSuchWebSiteConfigration

案例：OSS控制台API统计图无数据

案例：通过OSS监控计费核对账单发现数据不准确

案例：云监控显示某个时间段的有效请求率下降为0，但是OSS的log以及控制台的监控数据都是正常

本文介绍在使用阿里云云监控产品监控OSS数据时遇到的一些常见问题及解决方案。

OSS将数据推送至云监控，云监控进行分析处理。OSS控制台上的存储容量和带宽流量监控数据来自云监控。

OSS数据推送到云监控会延迟2\\~3小时，且单次推送间隔不能超过5分钟，否则云监控会拒绝接收过期数据，也不支持补推。因此，不建议根据云监控的数据计算您的费用。如需核对费用，建议联系[技术支持](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 案例：报警规则的状态出现“数据不足”

问题分析：此问题可以查看 **用户概况** 的 **服务监控总览** 内的数据。如果无数据产生，则会出现数据不足的情况。

## 案例：云监控上发现上传下载延迟

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4947559951/p39974.png)

问题分析：云监控平台上查看到的数据是云监控产品节点发起探测请求获得的数据，并不代表真实用户环境。

解决方案：云监控平台监控到访问延迟较大的情况，可通过如下步骤排查：

1. 确认客户端访问是否真的有延迟。

2. 若用户访问对应的Bucket也出现延迟的情况，需通过抓包获取访问数据分析。

3. 您也可以通过日志分析对应时间内的访问数据，确认是否有访问延迟的情况。


## 案例：某公司自己的监控系统发现OSS请求数据有延迟

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4947559951/p39975.png)某公司监控系统发现OSS访问延迟较大，可按以下步骤排查：

1. 检查公司网络，通过ping其他网站测试延迟。

2. 在OSS同地域创建ECS服务器，测试访问延迟。

3. 将延迟的OSS requestID发送给[技术支持](https://selfservice.console.aliyun.com/ticket/createIndex)，查看问题。

4. 抓包分析上传数据，使用以下参数：















```plaintext
tcpdump -i <出口网卡> -s0 ( 本机出口IP and OSS域名 ) -w result.pcap
```


## 案例：有效请求率降低

问题现象：云监控出现“对象存储 OSS (<)Bucket=p2xxx，userId=135114002(>)，有效请求率（30.51<90% ），持续时间0分钟”的报错。

解决方案：异常请求率是通过`2xx+3xx`总体数量计算得出，您可以先查看云监控的 OSS 控制台统计的`2xx+3xx`及其他异常状态码的占比，确认是否因异常状态码增加导致有效请求率下降。您也可以开通OSS日志分析请求行为。

## 案例：云监控报警404

问题现象：云监控出现“对象存储OSS实例：Bucket=\*\*\*-ali，userId=197\*\*\*\*\*745，资源不存在错误请求数于11:45恢复正常，值为30次，持续时间5分钟”的报错。

问题分析：原因是Bucket资源不存在导致的报警，属于正常的响应，并非是异常状态。

## 案例：云监控出现NoSuchWebSiteConfigration

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4947559951/p39976.png)

问题分析：当客户端请求OSS数据时，因功能配置不存在，导致404错误。200状态码表示用户已在OSS上配置功能模块，不是异常现象。

## 案例：OSS控制台API统计图无数据

问题分析：API的监控数据都是隔天显示，例如10月13日才能查看10月12日产生的完整数据。

## 案例：通过OSS监控计费核对账单发现数据不准确

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2374202071/p745671.png)

OSS的数据推送到云监控会延迟1~2小时，且单次推送间隔不能超过5分钟，否则云监控会拒绝接收并且不支持补推。因此，不建议使用云监控数据对账，因为数据不准确。您可以通过以下方式对账：

- 提前开启OSS日志，然后将OSS日志统计情况与账单核对。

- 开启OSS日志分析功能，导入日志后直接查看分析结果。


## 案例：云监控显示某个时间段的有效请求率下降为0，但是OSS的log以及控制台的监控数据都是正常

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4947559951/p39979.png)

问题分析：云监控有效请求率的计算公式是：100%-（2xx+3xx)/总请求数量。发现类似情况可查看OSS控制台或OSS log有没有异常即可。

原因是OSS将整个集群日志推送到云监控时超过了云监控的接收窗口期，而云监控不支持补推，所以导致数据为0 。