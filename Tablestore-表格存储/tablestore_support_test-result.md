本章节为您介绍本次表格存储性能测试中容量型实例的测试结果。

测试解析

- 同分区情况下，若随着压力升高，随机写操作延时变化不明显，则说明后端该分区上的资源还比较空闲，随着压力增高，QPS会继续提高。

- 同分区情况下，若随着压力升高，随机写操作延时升高，则说明服务端该分区上的请求开始出现排队，随着压力增高，QPS不会再线性增加。

- 随机读和随机范围读两个测试用例的性能会很大程度上受到Cache命中率的影响，为了避免Cache命中率影响测试结果，我们将Cache命中率控制在了极低的水平，在实际使用容量型实例的过程中，用户能达到的性能极大概率会高于此次测试结果。

- 本次性能测试不是产品在各个分区情况下的极限测试，故测试并没有触发表格存储服务端的流控措施，表格存储的自动负载均衡机制也尽可能地保证用户单表提供的服务能力能够水平扩展。


随机写性能

![](http://help-static-aliyun-doc.aliyuncs.com/assets/img/20498/156386435212033_zh-CN.png)

随机读性能

![](http://help-static-aliyun-doc.aliyuncs.com/assets/img/20498/156386435212034_zh-CN.png)

批量随机写性能

![](http://help-static-aliyun-doc.aliyuncs.com/assets/img/20498/156386435212035_zh-CN.png)

随机范围读性能

![](http://help-static-aliyun-doc.aliyuncs.com/assets/img/20498/156386435312036_zh-CN.png)

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[服务支持](https://help.aliyun.com/zh/tablestore/support/)[性能白皮书](https://help.aliyun.com/zh/tablestore/support/performance-white-paper/)测试结果（容量型实例）

# 测试结果（容量型实例）

更新时间：2019-07-23 02:45:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：测试结果（高性能实例）](https://help.aliyun.com/zh/tablestore/support/test-result-1)[下一篇：联系我们](https://help.aliyun.com/zh/tablestore/support/contact-us)

该文章对您有帮助吗？

反馈