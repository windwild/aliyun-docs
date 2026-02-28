### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[性能优化](https://help.aliyun.com/zh/cdn/user-guide/performance-optimization/)忽略参数

# 忽略参数

更新时间：2025-07-09 03:05:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：获取信息](https://help.aliyun.com/zh/cdn/user-guide/query-image-information)[下一篇：使用阿里云CDN加速后网站访问速度较慢](https://help.aliyun.com/zh/cdn/user-guide/website-access-speed-is-slow-after-using-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

操作步骤

开启忽略参数功能后，CDN节点在处理用户请求时，会去除请求URL中携带在`?`之后的参数（例如：用户身份信息、访问渠道信息），以原始URL来生成缓存hashkey。本文为您详细介绍配置忽略参数的方法。

**说明**

由于功能特性，自定义CacheKey和忽略参数配置功能存在冲突。开启参数配置功能后，CDN节点在处理用户请求时，会去除请求URL中携带在`?`之后的参数，这将导致CacheKey中配置的请求参数失效。开启参数配置功能前，请确保您的K没有配置。

## 功能介绍

**说明**

URL鉴权功能的优先级高于忽略参数。由于鉴权方式A中的鉴权信息包含HTTP请求的参数部分，所以CDN优先进行鉴权判断，鉴权通过后在CDN节点缓存一份副本。配置URL鉴权的操作方法，请参见 [配置URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-url-signing#task-2106935 "")。

- 忽略参数




| **作用** | **适用场景** |
| --- | --- |



|     |     |
| --- | --- |
| **作用** | **适用场景** |
| 去除请求URL中`?`之后的参数，不同用户访问同一个文件时，即使携带不同的URL参数，也能够命中同一个缓存文件，这样可以提高缓存命中率，减少回源次数，提升文件分发效率。 | 很多用户会通过在请求URL的`?`后面携带参数的方式来传递访问信息给源站（例如：用户账号UID、用户渠道来源、推荐码等），URL携带参数以后，不同的客户端访问CDN上同一个资源文件会携带不同的参数。<br>如果您的请求URL中`?`后面携带参数，但参数差异与资源内容无关，建议您开启忽略参数。例如：<br>  - A用户：`http://example.com/1.jpg?uid=123***`<br>    <br>  - B用户：`http://example.com/1.jpg?uid=654***`<br>    <br>如果CDN节点直接使用A、B用户的原始URL来处理缓存文件访问请求，将无法命中同一个缓存文件，用户的每次请求都需要回源站获取资源。<br>开启忽略参数后，CDN节点在查找和匹配缓存文件时，会去除URL中`?`后面UID参数，使用URL：`http://example.com/1.jpg`来匹配。 |

- 保留回源参数




| **作用** | **适用场景** |
| --- | --- |



|     |     |
| --- | --- |
| **作用** | **适用场景** |
| 使用原始URL回源，将用户的关键信息传递给源站。 | 开启忽略参数功能后，CDN节点默认使用经过忽略参数处理后的URL回源。上面的例子中，A、B用户的回源请求都会使用URL：`http://example.com/1.jpg`，在回源的时候就会丢失关键信息UID。<br>通过开启保留回源参数功能，CDN节点将会使用原始URL回源，这样就可以把A、B用户的关键信息UID传递给源站。 |


忽略参数包含两种模式（保留指定参数、删除指定参数），开启忽略参数处理流程图如下所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7174402571/CAEQWhiBgIDVituG2hgiIGI4ZWQ5NjMzOTg1YjRmZWE4NGM0NmI3ZWQ0MGRkNGQ14037267_20231018151816.403.svg)

## 操作步骤

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **性能优化**。

5. 单击忽略参数区域的 **修改配置**，请根据您的实际需求选择 **模式**，完成相关配置。





**重要**





切换模式，原有配置会被删除。







   - **模式：保留指定参数**




     | **参数** | **说明** | **示例** |
     | --- | --- | --- |



     |     |     |     |
     | --- | --- | --- |
     | **参数** | **说明** | **示例** |
     | **忽略参数** | - **是**：开启忽略参数功能，用户请求回源时会去除URL中`？`之后的参数。<br>       <br>       <br>       <br>       **说明**<br>       <br>       <br>       <br>       <br>       <br>       如果仅开启过忽略参数开关，不设置具体的保留指定参数时，表示去除`?`之后的所有参数。<br>       <br>     - 否：关闭忽略参数功能。 | 假设原始URL为`http://example.com/1.jpg?key1=1&key2=2&key3=3`，实现特定的功能场景，设置参数后，原始URL经CDN处理后结果如下：<br>     - 示例一，过滤所有参数+使用忽略参数处理后的URL回源：<br>       <br>       - 配置：忽略参数设置为是，保留指定参数为空，保留回源参数设置为否。<br>         <br>       - 缓存key：`http://example.com/1.jpg`<br>         <br>       - 回源URL：`http://example.com/1.jpg`<br>     - 示例二，保留指定参数+使用忽略参数处理后的URL回源：<br>       <br>       - 配置：忽略参数设置为是，保留指定参数设置为`key1`，保留回源参数设置为否。<br>         <br>       - 缓存key：`http://example.com/1.jpg?key1=1`<br>         <br>       - 回源URL：`http://example.com/1.jpg?key1=1`<br>     - 示例三，过滤所有参数+使用原始URL回源：<br>       <br>       - 配置：忽略参数设置为是，保留指定参数为空，保留回源参数设置为是。<br>         <br>       - 缓存key：`http://example.com/1.jpg`<br>         <br>       - 回源URL：`http://example.com/1.jpg?key1=1&key2=2&key3=3`<br>     - 示例四，保留指定参数+使用原始URL回源：<br>       <br>       - 配置：忽略参数设置为是，保留指定参数设置为`key1`，保留回源参数设置为是。<br>         <br>       - 缓存key：`http://example.com/1.jpg?key1=1`<br>         <br>       - 回源URL：`http://example.com/1.jpg?key1=1&key2=2&key3=3` |
     | **保留指定参数** | 配置需要保留的参数，最多可以配置10个保留参数，多个参数用英文逗号（,）分隔 。 |
     | **保留回源参数** | - 是：在回源请求中保留原始请求URL中的所有参数。<br>       <br>     - 否：在回源请求中携带的参数与缓存hashkey的参数一致（即，保留了指定的参数）。 |
     | **规则条件** | 规则条件能够对用户请求中携带的各种参数信息进行识别，以此来决定某个配置是否对该请求生效。<br>     - **不使用**：不使用规则条件。<br>       <br>     - 若需新增或编辑规则条件，请在[规则引擎](https://help.aliyun.com/zh/cdn/user-guide/rules-engine "")中进行管理。 |

   - **模式：删除指定参数**




     | **参数** | **说明** | **示例** |
     | --- | --- | --- |



     |     |     |     |
     | --- | --- | --- |
     | **参数** | **说明** | **示例** |
     | **删除指定参数** | 配置需要删除的参数，最多可以配置10个参数，多个参数用空格作分隔符。 | 假设原始URL为`http://example.com/1.jpg?key1=1&key2=2&key3=3`，实现特定的功能场景，设置参数后，原始URL经CDN处理后结果如下：<br>     - 示例一，删除指定参数+使用忽略参数处理后的URL回源：<br>       <br>       - 配置：删除指定参数设置为`key1`，保留回源参数设置为否。<br>         <br>       - 缓存key：`http://example.com/1.jpg?key2=2&key3=3`<br>         <br>       - 回源URL：`http://example.com/1.jpg?key2=2&key3=3`<br>     - 示例二，删除指定参数+使用原始URL回源：<br>       <br>       - 配置：删除指定参数设置为`key1`，保留回源参数设置为是。<br>         <br>       - 缓存key：`http://example.com/1.jpg?key2=2&key3=3`<br>         <br>       - 回源URL：`http://example.com/1.jpg?key1=1&key2=2&key3=3` |
     | **保留回源参数** | - 是：在回源请求中保留原始请求URL中的所有参数。<br>       <br>     - 否：在回源请求中携带的参数与缓存hashkey的参数一致（即，删除了指定的参数）。 |
     | **规则条件** | 规则条件能够对用户请求中携带的各种参数信息进行识别，以此来决定某个配置是否对该请求生效。<br>     - **不使用**：不使用规则条件。<br>       <br>     - 若需新增或编辑规则条件，请在[规则引擎](https://help.aliyun.com/zh/cdn/user-guide/rules-engine "")中进行管理。 |


6. 单击 **确定**，完成配置。