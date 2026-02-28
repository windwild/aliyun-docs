### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/)[Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/)[高级设置](https://help.aliyun.com/zh/sae/advanced-settings/)设置日志及监控metrics

# 设置日志及监控metrics

更新时间：2024-09-02 11:42:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置启动命令](https://help.aliyun.com/zh/sae/set-startup-command)[下一篇：设置环境变量](https://help.aliyun.com/zh/sae/setting-environment-variables)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

操作步骤

本文介绍如何Serverless 应用引擎 SAE（Serverless App Engine）提供基础实时日志功能，支持查看500行日志信息。同时，为满足更高的查阅需求，您可以将文件采集日志、标准输出日志收集并存储至日志服务 SLS（Simple Log Service），使用一站式数据功能，包括数据采集、加工、查询与分析、可视化和告警等，帮助您无限制行数查看日志、自行聚合分析日志，方便业务日志对接。本文介绍如何将日志、系统监控Metrics收集到SLS。

## **使用限制**

- 一个阿里云账号最多可创建200个Logstore资源、50个Project资源。


**警告**

日志服务基础资源的使用限制，会影响应用的日志收集结果，例如导致日志保存时间过短、日志收集失败等。更多使用限制，请参见 [基础资源](https://help.aliyun.com/zh/sls/basic-resources "")。

- 应用开始创建或更新后，系统会自动检查SLS服务是否开启、内置资源是否充足。

  - 如果SLS服务未开启，请按提示开通。

  - 如果内置资源不足，请申请提升额度。
- 使用SLS会产生额外费用，根据日志使用量计费。计费详情，请参见 [SLS计费概述](https://help.aliyun.com/zh/sls/billing-overview "")。

- 配置监控推送至SLS的规则仅适用于Web应用。

- SAE支持为用户自动创建SLS资源和使用已有的SLS资源。如果您选择使用已有的SLS资源，需要在创建SAE应用前创建相关资源。具体操作，请参见 [创建日志项目和日志库](https://help.aliyun.com/zh/sls/resource-management-overview "")。


## 操作步骤

在创建Web应用时设置

在部署新版本时设置

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击 **创建应用**。

4. 在 **基础信息设置** 页面，根据页面配置相关信息，然后单击 **下一步：高级设置**。

5. 在高级设置页面，展开 **日志 & 监控 metrics 设置** 区域，配置相关信息，然后单击 **创建应用**。


|     |     |
| --- | --- |
| **配置项** | **说明** |
| **日志收集到 SLS 日志服务** | 是否启用日志服务。启用后，应用的日志将被SLS存储，可以在SAE和SLS侧查看应用的日志。<br>   - **新建SLS资源**：SAE会自动帮您创建Project和Logstore。Project名称格式为`sae-proj-随机字符串`，日志库名称格式为`sae-store-随机字符串`。<br>     <br>   - **使用已有的 SLS 资源**：选择后，需要配置 **日志项目**。<br>     <br>**说明**<br>如果选择 **使用已有的 SLS 资源**，则 **日志项目** 不支持复用由SAE自动创建的Project。 |
| **收集规则配置** | 单击 **添加** 并填写以下信息。<br>   - **日志类型**：支持 **文件采集日志** 和 **标准输出日志**。 **文件日志采集** 支持同时配置多条， **标准输出日志** 仅支持配置1条规则。<br>     <br>   - **Logstore**：选择 **使用已有的 SLS 资源** 时需要配置。<br>     <br>   - **Logtail**：选择 **使用已有的 SLS 资源** 时需要配置。<br>     <br>   - **日志源**：输入日志源存放的文件路径，必须是绝对路径，例如`/tmp0/cjsc.log`。 **标准输出日志** 无需设置此选项。文件名与路径支持正则匹配，同一目录下，如果日志文件数量多，且文件格式相同，可以输入例如`/xxx/xxx/xxx/*.log`的格式。<br>     <br>**重要**<br>请勿在 **日志源** 的存放目录中存放其他重要文件，避免目录内的文件被覆盖。 |
| **推送规则配置** | 单击 **显示高级设置** 后配置。<br>是否将监控推送至SLS。打开 **监控推送至 SLS 日志服务** 开关并设置 **监控推送日志库**。开通后，可以查看已销毁实例的监控数据，查看请求级别的Tracing调用链，分析关键步骤（实例启动、请求的系统调用过程等）的耗时瓶颈。 |


应用创建成功后，页面会跳转至应用详情页面。您可以登录 [日志服务控制台](https://sls.console.aliyun.com/) 查看日志详情，更多信息，请参见 [查询和分析日志](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis "")。


**警告**

部署新版本后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击目标应用名称。

4. 在左侧导航栏，单击 **版本列表**，然后单击 **新建版本**。

5. 在 **日志 & 监控 metrics 设置** 区域，配置相关信息，然后单击 **确定**。


|     |     |
| --- | --- |
| **配置项** | **说明** |
| **日志收集到 SLS 日志服务** | 是否启用日志服务。启用后，应用的日志将被SLS存储，可以在SAE和SLS侧查看应用的日志。<br>   - **新建SLS资源**：SAE会自动帮您创建Project和Logstore。Project名称格式为`sae-proj-随机字符串`，日志库名称格式为`sae-store-随机字符串`。<br>     <br>   - **使用已有的 SLS 资源**：选择后，需要配置 **日志项目**。<br>     <br>**说明**<br>如果选择 **使用已有的 SLS 资源**，则 **日志项目** 不支持复用由SAE自动创建的Project。 |
| **收集规则配置** | 单击 **添加** 并填写以下信息。<br>   - **日志类型**：支持 **文件采集日志** 和 **标准输出日志**。 **文件日志采集** 支持同时配置多条， **标准输出日志** 仅支持配置1条规则。<br>     <br>   - **Logstore**：选择 **使用已有的 SLS 资源** 时需要配置。<br>     <br>   - **Logtail**：选择 **使用已有的 SLS 资源** 时需要配置。<br>     <br>   - **日志源**：输入日志源存放的文件路径，必须是绝对路径，例如`/tmp0/cjsc.log`。 **标准输出日志** 无需设置此选项。文件名与路径支持正则匹配，同一目录下，如果日志文件数量多，且文件格式相同，可以输入例如`/xxx/xxx/xxx/*.log`的格式的路径。<br>     <br>**重要**<br>请勿在 **日志源** 的存放目录中存放其他重要文件，避免目录内的文件被覆盖。 |
| **推送规则配置** | 单击 **显示高级设置** 后配置。<br>是否将监控推送至SLS。打开 **监控推送至 SLS 日志服务** 开关并设置 **监控推送日志库**。开通后，可以查看已销毁实例的监控数据，查看请求级别的Tracing调用链，分析关键步骤（实例启动、请求的系统调用过程等）的耗时瓶颈。 |


应用创建成功后，页面会跳转至应用详情页面。您可以登录 [日志服务控制台](https://sls.console.aliyun.com/) 查看日志详情，更多信息，请参见 [查询和分析日志](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis "")。