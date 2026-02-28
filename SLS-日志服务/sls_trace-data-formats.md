### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Trace数据格式

# Trace数据格式

更新时间：2026-01-05 03:30:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是日志服务](https://help.aliyun.com/zh/sls/what-is-log-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

原始Trace数据

维度调用关系数据

聚合指标中间结果数据

本文介绍日志服务Trace数据的格式。

日志服务Trace数据格式完全兼容 [OpenTelemetry Trace 1.0](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md#span) 格式，通过OpenTelemetry、Jaeger、Zipkin、OpenCensus、SkyWalking等协议写入的Trace数据可自动映射成OpenTelemetry的Trace数据格式。其他类型的Trace数据可通过数据加工转换为日志服务Trace格式。

## 原始Trace数据

原始Trace数据会被采集到名为{instance}-traces的LogStore中，采集时所定义的字段如下所示。

| **字段** | **类型** | **是否必选** | **说明** | **示例** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **是否必选** | **说明** | **示例** |
| host | String | 否 | 资源所在主机的主机名。提取自resource字段中的host.name字段。 | test-host |
| service | String | 是 | 资源的服务名。提取自resource字段中的service.name字段。 | test-service |
| resource | JSON Object | 否 | 除host、service之外的其他资源字段，例如进程ID、进程名、Pod名等。更多信息，请参见 [Resource Semantic Conventions](https://github.com/open-telemetry/opentelemetry-specification/tree/main/specification/resource/semantic_conventions)。 | {"k8s.pod.name":"xxxx", "k8s.pod.namespace":"kube-system"} |
| otlp.name | String | 否 | Trace SDK名称。 | go-sdk |
| otlp.version | String | 否 | Trace SDK版本号。 | v1.0.0 |
| name | String | 是 | Span名称。 | /get/314159 |
| kind | String | 否 | Span类型，例如CLIENT、SERVER等。更多信息，请参见 [SpanKind](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md#spankind)。 | SERVER |
| traceID | String | 是 | Trace ID。使用十六进制表示。 | 0123456789abcde0123456789abcde |
| spanID | String | 是 | Span ID。使用十六进制表示。 | 0123456789abcde |
| parentSpanID | String | 是 | ParentSpan ID。使用十六进制表示。 | 0123456789abcde |
| links | JSON Array | 否 | 相关联的其他的Span。更多信息，请参见 [Specifying links](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md#specifying-links)。 | \[{"TraceID" : "abc", "SpanId" : "abc", "TraceState" : "", "Attributes" : { "k" : "v" } }\] |
| logs | JSON Array | 否 | 相关联的日志、事件信息。更多信息，请参见 [Add Events](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md#add-events)。 | 无 |
| traceState | String | 否 | W3C定义的Trace State信息。更多信息，请参见 [W3C Trace Context Specification](https://www.w3.org/TR/trace-context/#tracestate-header)。 | 无 |
| start | INT | 是 | 开始时间。Unix时间戳类型，单位：纳秒。 | 1686294916826000000 |
| end | INT | 否 | 结束时间。Unix时间戳类型，单位：纳秒。 | 1686294924827000000 |
| duration | INT | 是 | 延迟时间，start参数与end参数之间的差值。单位：纳秒。 | 8001000 |
| attribute | JSON Object | 是 | Span相关的属性信息，例如HTTP请求的URL、状态码等。更多信息，请参见 [Attribute Naming](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/common/attribute-naming.md)。 | {"custom":"custom","host.hostname":"myhost","my-label":"myapp-type","null-value":"","service.name":"myapp"} |
| statusCode | String | 是 | 状态码。取值为OK、ERROR、UNSET。其中，UNSET与OK同义。 | ERROR |
| statusMessage | String | 否 | 状态信息。 | stack overflow |

## 维度调用关系数据

Trace数据经计算生成的维度调用关系数据将被存储在名为{instance}-traces-deps的LogStore中，对应的字段说明如下所示。

| **字段** | **数据类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **数据类型** | **说明** |
| version | String | 不同维度下的调用关系，目前共有四个维度。<br>- service：服务维度，展示服务间调用关系。<br>  <br>- service\_name：服务方法维度。<br>  <br>- service\_name\_host：服务方法、主机维度。<br>  <br>- service\_name\_host\_resource：服务方法、主机、资源维度。 |
| child\_host | String | 被调用方的主机信息。<br>仅在version为service\_name\_host或service\_name\_host\_resource时出现。 |
| child\_name | String | 被调用方的方法。<br>仅在version为service\_name、service\_name\_host或service\_name\_host\_resource时出现。 |
| child\_resource | JSON Object | 被调用方的资源信息。<br>仅在version为service\_name\_host\_resource时出现。 |
| child\_service | String | 被调用方的服务名。 |
| child\_type | JSON Object | 被调用方的补充信息。 |
| inner\_percentile | String | 百分位，系统通过inner\_percentile函数解析百分位。 |
| max\_latency | Double | 调用服务方法的最大延迟值。 |
| min\_latency | Double | 调用服务方法的最小延迟值。 |
| n\_status\_fail | Double | 调用服务方法失败的次数。 |
| n\_status\_succ | Double | 调用服务方法成功的次数。 |
| parent\_host | JSON Array | 调用方的主机信息。<br>仅在version为service\_name\_host或service\_name\_host\_resource时出现。 |
| parent\_name | JSON Array | 调用方的方法。<br>仅在version为service\_name、service\_name\_host或service\_name\_host\_resource时出现。 |
| parent\_resource | JSON Object | 调用方的资源信息。<br>仅在version为service\_name\_host\_resource时出现。 |
| parent\_service | INT | 调用方服务名。<br>仅在version为service、service\_name或service\_name\_host\_resource时出现。 |
| parent\_type | INT | 调用方的补充信息。 |
| sum\_latency | INT | 调用服务方法的延迟累加值。 |

## 聚合指标中间结果数据

Trace数据经计算生成的聚合指标中间结果将被存储在名为{instance}-traces-metrics的LogStore中，对应的字段说明如下所示。

| **字段** | **数据类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **数据类型** | **说明** |
| host | STRING | Span的Host值。 |
| inner\_percentile | STRING | 百分位，系统通过inner\_percentile函数解析百分位。 |
| max\_latency | Double | 调用服务方法的最大延迟值。 |
| min\_latency | Double | 调用服务方法的最小延迟值。 |
| n\_status\_fail | INT | 服务方法执行失败的次数。 |
| name | STRING | Span名称。 |
| resource | JSON Object | Span资源信息。 |
| service | STRING | Span服务名称。 |
| sum\_latency | Double | 调用服务方法的延迟总和，通常和total一起使用，计算平均延迟。 |
| total | INT | 调用服务方法的次数。 |
| type | JSON Object | Span的补充信息，通常包含以下信息。<br>- parent：根节点信息。<br>  <br>- mq：MQ调用相关信息。如果为空，则不是MQ调用。<br>  <br>- kind：Span类型。<br>  <br>- env：Span环境信息，从resource.deployment.environment字段中提取。<br>  <br>- version：Span版本，从resource.service.version字段中提取。<br>  <br>- db：Database调用信息。如果为空，则不是Database调用。 |
| version | String | 指标类型，目前固定为metric\_info。 |