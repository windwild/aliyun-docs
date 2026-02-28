### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用访问和流量管理](https://help.aliyun.com/zh/sae/sae-network-related-concepts-and-capabilities/)[配置网关路由（Ingress）访问](https://help.aliyun.com/zh/sae/configuring-gateway-routing-ingress-access/)[为应用设置路由规则（ALB）](https://help.aliyun.com/zh/sae/set-routing-rules-for-an-application-alb/)ALB使用约束

# ALB使用约束

更新时间：2025-05-14 04:05:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：为应用设置路由规则（ALB）](https://help.aliyun.com/zh/sae/set-routing-rules-for-an-application-alb/)[下一篇：ALB配额计算方式](https://help.aliyun.com/zh/sae/methods-to-calculate-alb-quotas)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

约束

重写配置说明

路径重写原理

注意事项

配置和替换示例

Serverless 应用引擎 SAE（Serverless App Engine）利用七层负载均衡能力，将请求流量按照转发规则分发到指定应用实例上。本文介绍在使用SAE网关路由功能前，需要了解的负载均衡ALB的相关约束以及转发动作中的重写配置。

## 约束

SAE的负载均衡实质是七层的负载均衡服务，通过为您配置ALB实例的监听来实现。

从ALB产品的角度而言，您在ALB配置行为和SAE侧的ALB配置行为不作区分，但是ALB侧对SAE侧的ALB配置起不到保护作用，允许在ALB侧篡改或破坏SAE所维护的配置，可能导致业务不符预期。

对于SAE配置的一条网关路由，SAE会自动创建相关的监听或服务器组，不建议您进行任何的修改或引用，否则对您的业务有一定的影响。如果您需要进行修改，请检查操作的合法性，合法性如下表所示。

**说明**

“Y”表示支持，“N”表示不支持，“-”表示有特殊要求。

| **类型** | **修改项** | **合法性** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **类型** | **修改项** | **合法性** | **说明** |
| 实例 | 实例名称 | Y | 无 |
| 实例标签 | - | 禁止以下操作： <br>- 更改SAE创建的标签。<br>  <br>- 删除SAE创建的标签。 |
| EIP绑定 | Y | 无 |
| 升降配 | Y | 无 |
| 监听 | 监听名称 | N | 无 |
| 虚拟服务器组ID | N | 无 |
| 规则 | N | - 禁止修改SAE侧维护的规则。<br>  <br>- 允许添加自定义规则（不能依赖规则之间的顺序），SAE的规则可能会出现在第一位或者最后一位。<br>  <br>- 不允许自定义规则指向SAE的服务器组，因为SAE的服务器组会重建。 |
| - 连接空闲超时时间<br>  <br>- 连接请求超时时间<br>  <br>- 数据压缩<br>  <br>- 附加HTTP头字段<br>  <br>- …… | N | 在ALB侧修改的配置，会被SAE侧覆盖为默认值。 |
| 证书配置 | N | 必须在SAE侧配置修改，如果在ALB侧修改，会被SAE的配置覆盖。 |
| 虚拟服务器组 | 名称 | N | 无 |
| 标签 | N | 修改标签会导致服务器组重建。 |
| 后端服务器（权重、实例、端口等） | N | - 禁止删除SAE的IP地址。<br>  <br>- 禁止修改SAE的IP对应的端口和权重。<br>  <br>- 无法添加ECS的IP，添加后会被SAE移除。 |
| 路由规则 | 所有配置修改 | N | 无 |

## 重写配置说明

### 路径重写原理

1. 路径匹配：客户端发送请求，并匹配到某一条路径转发规则的正则表达式。

2. 提取与替换：按照正则表达式的规范提取，将前三个半角圆括号`( )`提取出来的内容分别保存至`${1}`、`${2}`、`${3}`中，用于在转发动作的重写或重定向路径中替换。

3. 拼接：按照转发动作中重写或重定向路径的配置，对其中的`${1}`、`${2}`、`${3}`进行值的替换，最终拼接成重写或重定向的实际路径。


### 注意事项

- 转发条件中正则表达式中包含的半角圆括号`( )`需要与转发动作中重写或重定向路径中$变量的个数保持一致。

- 转发动作中重写的路径中需要包含`${1}`、`${2}`、`${3}`中的一个或多个，且这三个变量不支持使用其余字符代替。


### 配置和替换示例

| **编号** | **步骤** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **编号** | **步骤** | **示例** |
| 1 | 配置转发规则中的转发条件和转发动作。 | - 转发条件路径：`/sys/(.*)/(.*)/aaa`<br>  <br>- 转发动作重写或重定向路径：`/${1}/${2}` |
| 2 | 客户端发送请求，并匹配路径。 | - 客户端发送的请求路径：`/sys/ccc/bbb/aaa`<br>  <br>- 匹配到的转发条件路径：`/sys/(.*)/(.*)/aaa` |
| 3 | 提取与替换 | 按照正则表达式规范，转发条件路径中的两个`(.*)`分别提取到`ccc`和`bbb`，并分别保留至转发动作中重写或重定向路径中的`${1}`和`${2}`。<br>- `${1}`替换为`ccc`<br>  <br>- `${2}`替换为`bbb` |
| 4 | 拼接路径 | 后端服务器接收到的路径：`/ccc/bbb`![sc_splice_the_strings_that_overwrote_the_variables_to_form_the_new_url](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8942433861/p667783.png) |