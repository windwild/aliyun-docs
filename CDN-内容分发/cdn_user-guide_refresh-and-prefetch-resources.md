### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[刷新和预热](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch/)刷新和预热资源

# 刷新和预热资源

更新时间：2025-12-03 22:45:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：边缘脚本监控](https://help.aliyun.com/zh/cdn/user-guide/es-monitoring)[下一篇：正则刷新说明](https://help.aliyun.com/zh/cdn/user-guide/configure-url-refresh-rules-that-contain-regular-expressions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

资源刷新

资源预热

前提条件

注意事项

费用说明

操作指南

验证结果

使用限制

拓展阅读：CDN的缓存刷新机制

常见问题

相关API

通过刷新功能，您可以删除CDN边缘节点上已经缓存的资源，并强制CDN边缘节点回源站获取最新资源，适用于源站资源更新和发布、违规资源清理、域名配置变更等；通过预热功能，您可以在业务高峰前预先将热门资源缓存到CDN边缘节点，降低源站压力。

## 功能介绍

### **资源刷新**

刷新操作的本质是向CDN边缘节点下发缓存失效指令，而非直接删除文件。边缘节点收到指令后，会将匹配的缓存资源标记为“失效”或“过期”。当用户再次请求该资源时，边缘节点发现缓存已失效，便会回源获取最新资源，并在返回给用户的同时重新缓存。

**适用场景**

1. **资源更新和发布：** 源站的旧资源更新或升级后，为避免用户仍访问到旧的缓存资源，可通过提交对应资源的URL或目录进行刷新，确保用户访问到最新的资源并缓存至CDN边缘节点。

2. **违规资源清理：** 如果您的源站存在不合规内容（如使用限制中提及的内容），删除源站资源后，由于CDN边缘节点仍可能存在缓存，资源仍可能被访问到。此时可通过URL刷新功能更新缓存资源，确保违规内容及时清除。


### **资源预热**

预热操作是由CDN边缘节点根据您提交的URL列表，主动向源站发起请求，将资源缓存到CDN边缘节点上，而非由源站主动推送。预热可提升新资源或活动页面的首次访问速度，同时减少活动上线时的回源压力，保护源站。

**适用场景**

1. **首次接入阿里云CDN：** 当您首次接入CDN后，可选择将热点静态资源提前预热至CDN边缘节点。用户访问时可直接由CDN边缘节点响应，避免初次访问速度慢的问题，提升用户体验。

2. **运营活动：** 在运营大型活动时，提前将活动页涉及的静态资源预热至CDN边缘节点。活动开始后，用户访问的所有静态资源均已缓存至CDN边缘节点，由边缘节点直接响应，确保活动页面快速加载。

3. **安装包或其他大文件发布：** 新版本安装包或升级包发布前，提前将资源预热至CDN边缘节点。产品正式上线后，用户的下载请求将直接由CDN边缘节点响应，提升下载速度，降低源站压力。


## **前提条件**

- **权限要求：** 使用 RAM 用户操作时，必须先授予 `cdn:PushObjectCache`（预热） 和 `cdn:RefreshObjectCaches`（刷新） 权限。详情请参见 [授予RAM用户刷新预热权限](https://help.aliyun.com/zh/cdn/user-guide/authorize-a-ram-user-to-prefetch-and-refresh-resources#task-2087340 "")。

- **URL 格式：** 提交的 URL 中若包含非 ASCII 字符（如中文、空格），必须先进行`UTF-8`百分号编码（Percent-encoding）。


## **注意事项**

- **操作时机：** 刷新预热任务会产生回源流量，建议在业务 **流量低峰期** 执行大规模的刷新或预热任务。

- **共享缓存：** 若域名配置了 [共享缓存](https://help.aliyun.com/zh/cdn/user-guide/configure-shared-cache "")，使用主域名或任意关联域名提交刷新任务，均可使所有关联域名的缓存失效。

- **重写访问URL：** 如果域名配置了 [重写访问URL](https://help.aliyun.com/zh/cdn/user-guide/create-an-access-url-rewrite-rule "")，CDN节点将会使用重写以后的URL来生成Cachekey，因此需要提交重写后的URL来进行刷新预热操作。


## **费用说明**

刷新和预热功能 **本身不收取任何操作费用**。

但是，这两种操作都会触发CDN边缘节点回源拉取资源，由此产生的回源流量和回源请求次数将会产生费用。计费标准遵循您所使用的源站类型：

- 如果源站是阿里云 OSS，将按 OSS 的计费规则收取 [流量费用](https://help.aliyun.com/zh/oss/traffic-fees "") 和 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees "")。

- 如果源站是 ECS 或其他服务器，将按其网络带宽或流量计费。


**重要**

大规模的刷新或预热操作，尤其是在短时间内，可能会导致回源成本增加。请在操作前评估潜在的成本影响。

## **操作指南**

刷新资源

预热资源

自动化刷新或预热

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **刷新预热**。

3. 在 **刷新缓存/预热缓存** 页签，选择操作类型为 **刷新**。

4. 根据您的需求，选择刷新方式并提交任务。


|     |     |
| --- | --- |
| **刷新方式** | **操作说明** |
| URL刷新 | **目的：** 精确失效一个或多个具体文件的缓存。<br>**操作：** 在 刷新内容 输入框中，输入完整的 URL（包含 `http://` 或 `https://`），每行一个。例如：`https://www.example.com/static/image.jpg`。 |
| 目录刷新 | **目的：** 失效指定 URL 目录下所有文件和子目录的缓存。<br>**操作：** 输入完整的目录 URL，且必须以 `/` 结尾。例如：`https://www.example.com/static/`。<br>**说明：** 此方式为 [标记刷新](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#8b45c38be284o "")。若需强制刷新整个目录，请使用 [刷新缓存API](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-refreshobjectcaches "") 并设置 `Force=true`。 |
| 正则刷新 | **目的：** 按正则表达式匹配 URL 路径，批量失效符合规则的资源缓存。<br>**操作：** 输入带有正则表达式的 URL。例如：`https://www.example.com/static/[0-9][a-z].*.jpg`。<br>**说明：** 此方式为 [标记刷新](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#8b45c38be284o "")。若需强制刷新整个目录，请使用 [刷新缓存API](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-refreshobjectcaches "") 并设置 `Force=true`。<br>**注意：** 尽量使用更精确的匹配规则，避免非预期的、大范围的缓存失效。 |

5. 单击 **提交**，系统将开始执行刷新任务。



**说明**





   - 刷新任务一旦提交成功，将无法中止。

   - 刷新任务通常需要 5-6 分钟 在全网生效。如果您的缓存过期时间本身就小于此值，则无需手动刷新。

   - 如果您在OSS控制台开启了 [CDN缓存自动刷新](https://help.aliyun.com/zh/oss/user-guide/cdn-acceleration#3056dca9044fm "")，则无法通过CDN控制台查看OSS的缓存自动刷新任务。


1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **刷新预热**。

3. 在 **刷新缓存/预热缓存** 页签，选择操作类型为 **预热**。

4. 在 预热内容 输入框中，输入需要预热的完整文件 URL，每行一个。不支持预热目录。例如：`https://www.example.com/install/package.zip`。

5. 单击 **提交**，系统将开始执行预热任务。



**说明**





   - 刷预热任务一旦提交成功，将无法中止。

   - 预热任务的完成时间取决于文件大小、数量和源站性能，通常需要 5-30 分钟。


如果您有以下情况，建议您使用 [自动化脚本刷新和预热](https://help.aliyun.com/zh/cdn/user-guide/run-scripts-to-refresh-and-prefetch-content#topic-2404622 "")：

- 无开发人员，需手动提交刷新预热任务，运维成本高。

- 刷新或预热URL过多，分批提交导致刷新或预热效率低。

- 需要人工或程序判断刷新预热任务是否正常进行，费时费力。


## **验证结果**

- **手动查询**

在 [操作记录](https://cdn.console.aliyun.com/refresh/record) 页签中查看资源刷新或预热的详细记录和进度。进度为100%，表示任务执行完成。刷新或预热的数量过多，会影响任务的完成进度，请您耐心等待。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3520213371/p880358.png)

- **接口查询**

调用 [DescribeRefreshTaskById](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-describerefreshtaskbyid "") 接口，查询刷新或预热任务是否完成。

- **命令行验证**

执行命令`curl -I <资源链接>`，系统显示结果如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9096630471/p919897.png)

存在`X-Cache`的情况：


  - `X-Cache`是`HIT`，说明此次请求命中缓存，预热成功。

  - `X-Cache`是`MISS`，说明此次请求未命中缓存，预热任务未完成或预热失败，请重新预热。


不存在`X-Cache`的情况：

如果不存在`X-Cache`，说明该资源未接入CDN，请参照 [快速接入阿里云CDN](https://help.aliyun.com/zh/cdn/getting-started/quick-access-to-alibaba-cloud-cdn "")，先将该URL的域名接入阿里云CDN，再进行资源的预热。

## 使用限制

| **操作类型** | **方式** | **配额限制** | **管理额度** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **操作类型** | **方式** | **配额限制** | **管理额度** |
| 刷新 | URL刷新 | 每个账号每日最多10000条 | [配额管理](https://help.aliyun.com/zh/cdn/user-guide/quota-management#concept-2086246 "") |
| 目录刷新 | 每次最多提交100条；每个域名每分钟最多100条 |
| 正则刷新 | 每个账号每日最多20条 |
| 预热 | URL预热 | 每次最多提交100条；每个账号每日最多1000条 |

## **拓展阅读：CDN的缓存刷新机制**

CDN 针对目录刷新和正则刷新提供两种缓存刷新机制：标记刷新和强制刷新，适用于不同场景，帮助您灵活高效的管理缓存内容。

**标记刷新（CDN默认策略）**

- **适用场景：** 常规内容更新，如发布新版静态文件。

- **机制：** 这是目录刷新和正则刷新在控制台上的默认行为。CDN 边缘节点在回源时，会携带 `If-Modified-Since` 或 `If-None-Match` 请求头。源站会根据这些头信息判断资源是否已更新。

- **效果：** 如果源站资源未变更，源站将返回 `304 Not Modified` 状态码，CDN 边缘节点会继续使用旧的缓存副本，不会消耗回源流量。这是一种节省成本和源站资源的优化方式。


**强制刷新**

- **适用场景：** 紧急清理违规或错误资源、修复错误的 `Cache-Control` 响应头配置后，需要强制全网更新的场景。

- **机制：** 通过 [刷新缓存API](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-refreshobjectcaches "") 提交刷新任务时，将参数 `Force` 设置为 `true` 来触发。此模式下，CDN 边缘节点会无条件地将缓存资源标记为失效。

- **效果：** 下次访问该资源时，CDN 边缘节点将必须回源获取新版本，即使源站上的文件并未改变。


## **常见问题**

- [预热失败了怎么办？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#4c57c3db57g4h "")

- [页面无法访问/访问异常问题排查。](https://help.aliyun.com/zh/cdn/support/faq#section-8ru-2us-33z "")

- [为什么使用CDN刷新预热功能后访问的资源没有更新？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#4566e64996ci4 "")

- [使用阿里云CDN加速后网站访问速度较慢排查。](https://help.aliyun.com/zh/cdn/user-guide/website-access-speed-is-slow-after-using-alibaba-cloud-cdn "")

- [配置CDN后如何对文件进行同名更新？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#e1c2548dbejfv "")

- [如何查看CDN的预热任务是否执行完成？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#6237a4ce5ei5l "")


## 相关API

您可以调用API接口，实现资源的刷新和预热，敬请参考 [刷新和预热API](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-dir-refresh-and-prefetch/ "")。