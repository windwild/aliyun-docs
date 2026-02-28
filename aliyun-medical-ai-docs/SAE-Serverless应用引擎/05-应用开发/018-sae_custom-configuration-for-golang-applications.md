### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)[应用配置](https://help.aliyun.com/zh/sae/application-settings-new/)Golang应用自定义配置

# Golang应用自定义配置

更新时间：2025-05-18 23:19:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java应用自定义配置](https://help.aliyun.com/zh/sae/custom-configurations-for-java-applications)[下一篇：Python应用自定义配置](https://help.aliyun.com/zh/sae/custom-configurations-for-python-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能入口

采样设置

探针开关设置

Runtime开关设置

应用日志关联配置

URL收敛设置

持续性能剖析设置

接口调用配置

数据库调用配置

调用链透传协议设置

探针采集配置

高级设置

将配置复制到其他应用

将单个配置复制到其他应用

将所有配置复制到其他应用

全局默认配置

您可以在自定义配置页签上调整探针功能开关、采样策略等常用设置。

## **功能入口**

在 **应用监控** 页面，单击 **应用设置**，然后单击 **自定义配置**，即可配置以下功能。

## 采样设置

在 **采样设置** 区域，可以为调用链设置采样策略。Golang应用目前仅支持通过固定采样率采样，同时支持按接口名、接口前缀、接口后缀配置全采样。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6084370471/p917790.png)

## **探针开关设置**

在 **探针开关设置** 区域，可以控制应用监控的启停并调整各插件开关。

**重要**

应用监控的启停修改即时生效，无需重启应用。如果暂停应用监控，则系统将无法监控您的应用，请谨慎操作。

对各插件开关的修改，手动重启应用后生效。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1834790371/p866007.png)

## Runtime开关设置

在 **Runtime开关设置** 区域，可以打开或关闭Runtime监控功能。更多信息，请参见 [Runtime监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/golang-application-instance-monitoring#a34feddf1b9yc "")。

**重要**

修改动态生效，无需重启应用。若关闭Runtime监控功能，ARMS将不会采集Runtime指标，请谨慎操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2461749171/p813643.png)

## 应用日志关联配置

在 **应用日志关联配置** 区域，可以设置应用关联的日志源信息，将SpanId、TraceId打印到对应的日志中。更多信息，请参见 [Golang应用业务日志关联调用链TraceId](https://help.aliyun.com/zh/arms/application-monitoring/use-cases/associate-trace-ids-with-business-logs-for-a-go-application "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5664825371/p896078.png)

## URL收敛设置

在 **URL收敛设置** 区域，可以打开或关闭收敛功能的开关，并设置收敛阈值、收敛规则。URL收敛是指将具有相似性的一系列URL作为一个单独的个体展示，例如将前半部分都为/service/demo/的一系列URL集中展示。收敛阈值是指要进行URL收敛的最低数量条件，例如当阈值为100时，则符合规则正则表达式的URL数量达到100才会对它们进行收敛。更多信息，请参见 [ARMS收敛机制说明](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/arms-convergence-mechanism-description "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1834790371/p866010.png)

## **持续性能剖析设置**

在 **持续性能剖析设置** 区域，可以打开或关闭总开关、CPU热点、内存热点、代码热点、协程热点、阻塞分析和互斥锁分析功能。更多信息，请参见 [Golang应用持续剖析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/continuous-analysis-of-golang-applications "")。

![8NnQv5UKxP](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9874267471/p948969.png)

## 接口调用配置

在 **接口调用配置** 区域，可以设置慢调用阈值、HTTP状态码白名单、无效接口调用过滤等。

![2025-02-18_16-05-16](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6084370471/p917793.png)

- **慢调用阈值**：默认为500，当接口响应时间大于该阈值的时候，该接口会被标记为慢调用。

- **HTTP状态码白名单**：

默认情况下，HTTP 状态码大于 400 会被归类为错误调用。如果您不希望某类状态码被归类为错误，可以设置白名单来忽略这类错误。

仅对应用监控当前 [支持的 HTTP 框架](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/go-components-and-frameworks-supported-by-arms-application-monitoring "") 产生影响。

**影响数据**：HTTP 服务端/客户端的错误数指标（arms\_http\_requests\_error\_count、arms\_http\_client\_requests\_error\_count、arms\_app\_requests\_error\_count）、Span 状态。

**影响功能**： [应用概览](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/new-application-overview "")、 [提供服务](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/provision-of-services "")、 [依赖服务](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/dependent-services "") 页签中的错误数， [调用链分析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/trace-explorer "") 页面的 Span 状态、错误数告警。

**内容格式**：填写单一状态码，多个状态码用英文半角逗号（,）分隔，不支持模糊匹配。

**示例**：`403,502`

**默认值**：空

- **无效接口调用过滤**：

如果您不希望在 [提供服务](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/provision-of-services "") 页签看到这类调用，可以输入不需要查看调用情况的接口名，探针将不会上报相关接口产生的观测数据，从而将其从接口调用页面隐去。

**影响数据**：接口对应的所有指标、Span 都会被忽略。

**影响功能**： [应用概览](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/new-application-overview "")、 [提供服务](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/provision-of-services "")、 [依赖服务](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/dependent-services "") 页签对应接口的所有指标， [调用链分析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/trace-explorer "") 页面的 Span 数量、对应接口的调用量、错误数、慢调用告警。

**内容格式**：使用 **字符串** 或 **AntPath 表达式** 匹配无效接口全名，多个规则请使用英文半角逗号（,）分隔。（默认值的 AntPath 表达式写法是为了兼容存量数据，不建议删除，新增配置请拼接在原有规则之后）。

**示例**：`/api/test/*,/api/playground/create`

**默认值**：`/**/*.jpg,/**/*.png,/**/*.js,/**/*.jpeg,/**/*.pdf,/**/*.xlsx,/**/*.txt,/**/*.docs,/**/*.gif,/**/*.csv`

- **开启打印HTTP请求Body**：开启后会在HTTP Client的Span中增加http.request.body字段表示请求的Body，默认打印的长度是1024。

- **开启打印HTTP请求Header**：开启后会在HTTP Client的Span中增加http.request.header字段表示请求的Header。

- **HTTP Body长度**：HTTP请求Body的长度，默认打印的长度是1024。

- **HTTP返回结果中包含TraceId**：开启后会在返回的Header中添加TraceId，Key是Eagleeye-TraceId。

- **开启打印HTTP返回Body**：开启后会在HTTP Server的Span中增加http.response.body字段表示返回的Body。

- **开启打印HTTP返回Header**：开启后会在HTTP Server的Span中增加http.response.header字段表示返回的Header。

- **HTTP返回Body的长度**：HTTP返回Body的长度，默认打印的长度是1024。

- **HTTP请求Header Key写入Span**：填写Header中出现的Key，多个可以用英文半角逗号分隔，填写后会在HTTP Client的Span中增加http.request.header.key 字段。

- **HTTP返回Header Key写入Spa** n：填写Header中出现的Key，多个可以用英文半角逗号分隔，填写后会在HTTP Server的Span中增加http.response.header.key 字段。


## 数据库调用配置

在 **数据库调用配置** 区域，可以设置慢SQL阈值、采集SQL最大保留长度，并设置是否展示SQL中的变量绑定值以及常量值。

- **展示SQL中的变量绑定值**：捕获PreparedStatement参数绑定的变量值，无需重启应用即可生效。

- **展示SQL中的常量值**：仅对SQL截断，不做额外处理，无需重启应用即可生效。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1834790371/p866013.png)

## **调用链透传协议设置**

在 **调用链透传协议设置** 区域，您可以根据自己的需求选择使用的Trace协议。默认使用W3C协议，可以选择Zipkin、Jaeger、EagleEye。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5664825371/p896107.png)

## **探针采集配置**

在 **探针采集配置** 区域，可以设置探针每秒最大链路采集量和探针日志级别。

![image](<Base64-Image-Removed>)

## 高级设置

在 **高级设置** 区域，可以设置分位数统计、错慢采样、异常堆栈收集大长度等。

![image](<Base64-Image-Removed>)

## 将配置复制到其他应用

如果您需要为其他应用同步相同配置，可以将对应配置复制到其他应用上。

### **将单个配置复制到其他应用**

1. 在对应配置区域单击 **保存并批量复制到其他应用**。

2. 如果弹出 **当前设置未保存** 对话框，请单击 **确定** 保存本应用配置后，再单击 **保存并批量复制到其他应用**。

3. 在弹出的对话框中选择生效的应用，然后单击 **确定**。


### **将所有配置复制到其他应用**

1. 在页面底部单击 **保存并批量复制到其他应用**。

2. 如果弹出 **当前设置未保存** 对话框，请单击 **确定** 保存本应用配置后，再单击 **保存并批量复制到其他应用**。

3. 在弹出的对话框中选择生效的应用，然后单击 **确定**。


## 全局默认配置

您可以将当前配置保存为全局默认配置，在之后创建新应用时将会默认使用当前配置。

1. 在页面底部单击 **保存当前应用设置为全局默认配置**。

2. 如果弹出 **当前设置未保存** 对话框，请单击 **确定** 保存本应用配置后，再单击 **保存当前应用设置为全局默认配置**。

3. 在弹出的对话框中单击 **确认**。