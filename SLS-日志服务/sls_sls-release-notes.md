### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[LoongCollector数据采集器（原Logtail）](https://help.aliyun.com/zh/sls/loongcollector-management/)[Logtail（旧版采集器）](https://help.aliyun.com/zh/sls/use-logtail-to-collect-data/)Logtail发布历史

# Logtail发布历史

更新时间：2026-01-05 02:53:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Logtail网络类型，启动参数与配置文件](https://help.aliyun.com/zh/sls/select-a-network-type)[下一篇：Logtail限制说明](https://help.aliyun.com/zh/sls/logtail-limits)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

2.1.16

修复

2.1.15

修复

2.1.14

修复

2.1.13

修复

2.1.11

修复

2.1.10

修复

2.1.9

修复

2.1.8

修复

2.1.7

修复

2.1.6

优化

修复

2.1.5

新功能

修复

2.1.1

新功能

2.0.10

修复

2.0.8

修复

2.0.7

修复

2.0.6

新功能

2.0.5

优化

修复

1.8.11

优化

修复

1.8.10

优化

1.8.9

优化

修复

1.8.8

优化

修复

1.8.7

新功能

修复

1.8.6

优化

修复

1.8.5

修复

1.8.4

优化

修复

1.8.3

修复

1.8.0

1.7.1

1.6.0

1.5.1

1.4.0

1.3.2

1.3.1

1.2.1

1.1.1

1.1.0

1.0.34

1.0.32

1.0.31

1.0.30

1.0.29

1.0.28

1.0.27

1.0.26

1.0.25

1.0.24

1.0.22

1.0.21

0.16.68

0.16.64

0.16.62

0.16.60

0.16.56

0.16.54

0.16.52

0.16.50

0.16.48

0.16.46

0.16.44

0.16.42

0.16.40

0.16.38

0.16.36

0.16.34

0.16.32

0.16.30

0.16.28

0.16.26

0.16.24

0.16.32

0.16.21

0.16.18

0.16.16

0.16.15

0.16.14

0.16.13

0.16.11

0.16.10

0.16.9

0.16.8

0.16.6

0.16.5

0.16.4

0.16.2

0.16.0

本文介绍日志服务Logtail的发布历史。

**说明**

Logtail在3.X版本后升级为使用LoongCollector镜像，详情请参考 [LoongCollector发布历史](https://help.aliyun.com/zh/sls/loongcollector-release-history "")。

## 2.1.16

发布时间： 2025.09.09

### 修复

- 修复了从 checkpoint 恢复 reader 时的容器文件描述符释放问题。

- 修复反馈导致超时事件和日志截断。


## 2.1.15

发布时间：2025.08.15

### 修复

- 增强处理器的超时和零宽度正则表达式告警。


## 2.1.14

发布时间：2025.07.04

### 修复

- 修复了当容器停止时，rotator reader 不会关闭文件的问题，避免文件描述符泄露。


## 2.1.13

发布时间：2025.07.01

### 修复

- 修复了 Docker inspect 命令可能导致的超时问题。

- 修复容器停止时 rotator reader 未关闭文件的问题。

- 支持 ECS 加固元数据访问方式。


## 2.1.11

发布时间：2025.06.16

### 修复

- 修复了 Golang 中由于接口空值判断错误导致的崩溃问题。

- 修复了 JsonLogFileReader 在读取时可能因缓冲区溢出导致崩溃的问题。

- 修复文件读取时的无意义空字符。


## **2.1.10**

发布时间：2025-05-28

- ### **修复**


  - 修复磁盘满后恢复时，Logtail采集无法自动恢复的故障。

## **2.1.9**

发布时间：2025-05-23

- ### **修复**


  - 更新runc库版本，修复runc文件描述符泄漏漏洞。

  - 支持CRI V1接口，适配 containerd 2.0。

## **2.1.8**

发布时间：2025-05-14

- ### **修复**


  - 修复旧版标准输出采集插件在容器停止情况下最后部分日志未采集完整问题。

  - 时序数据写入 Metricstore 优化。

## **2.1.7**

发布时间：2025-04-01

- ### **修复**


  - 修复 Linux 场景采集配置中路径为根目录时目录拼接不正确的问题。

  - 修复容器场景因为并发写导致容器信息中挂载信息错误的问题。

  - 修复指标采集数据格式错误问题。

  - 修复容器采集场景部分容器元信息缺失问题。

## **2.1.6**

发布时间：2025-03-03

- ### 优化


  - 添加FORCE\_RELEASE\_STOP\_CONTAINER\_FILE环境变量，支持在业务容器停止的情况下强制释放文件句柄。
- ### **修复**


  - 修复容器文件采集场景，由于持久化卷挂载，导致容器状态识别异常问题。

  - 修复容器场景采集配置路径中多个斜杠导致的采集路径识别异常问题。

  - 修复 C++ 标准输出日志解析模块对最后一行日志解析的问题。

  - 修复 Containerd 运行时场景下，enable\_containerd\_upper\_dir\_detect 环境变量未生效的问题。

## **2.1.5**

发布时间：2025-01-02

- ### 新功能


  - 环境变量配置方式支持C++标准输出插件。

  - 支持OTLP trace数据发送到SLS。
- ### **修复**


  - 修复Docker Compose场景，重复执行up命令导致的容器信息获取缺失的问题。

  - 修复自监控CPU指标缺失问题。

  - 修复C++标准输出插件解析最后一行失败导致崩溃问题。

## **2.1.1**

发布时间：2024-11-01

- ### 新功能


  - 新增使用C++实现的容器标准输出采集。

  - 自监控能力升级，C++模块和 Golang 插件模块统一上报自监控数据。

## **2.0.10**

发布时间：2024.10.19

- ### **修复**


  - 修复了bin log插件在GTID超过1024字节时无法获取GTID的问题。

  - 修复了原生分隔符插件在处理包含双引号的字符串时解析失败的问题。

## **2.0.8**

发布时间：2024.08.13

- ### **修复**


  - 修复2.0.7版本引入的ENV管控方式token过期问题。

## **2.0.7**

发布时间：2024.07.31

- ### **修复**


  - 修复转义零字节导致JSON截断。

  - 修复使用非线程安全的gethostbyname方法导致的coredump问题 。

  - 修复opentelemetry解析gauge类型指标数据的时候缺失标签的问题 。

  - 修复从checkpoint恢复的时候，轮转文件过多可能导致超出reader队列长度的reader恢复失败，进一步引发在inode复用时，新的reader读到了错误的老reader的checkpoint，这会导致截断和重复采集 。

  - 修复`input_canel`插件GTID不准确的问题 。

  - 当资源使用超过硬限制的时候立刻自杀 。

## **2.0.6**

发布时间：2024.07.03

- ### **新功能**


  - 增加对容器计算服务（ACS）rund架构支持。

## **2.0.5**

发布时间：2024.06.25

- ### **优化**


  - containerd sock重试容错机制优化。
- ### **修复**


  - 修复2.0.4版本引入的k8s场景环境变量配置不生效的问题。

  - 修复标准输出场景`GetRealPath`函数导致的插件模块`panic`问题。

  - 修复包含拓展插件的时候，神农自监控日志缺失问题。

  - 修复超时读截断问题。

  - 系统时间去纳秒支持。

  - 多上切分插件指标缺失。

## **1.8.11**

发布时间：2024.09.04

- ### **优化**


  - 优化了容器运行时的探测重试机制，并修复了运行时识别不准确的问题。

  - 从`config server`拉取配置的时候支持`DNS cache`。

  - 多行分隔超时时间默认设置成60秒。

  - `processor_gotime`支持纳秒配置。
- ### **修复**


  - 修复`bin log`插件当GTID超过1024字节之后不能获取GTID的问题。

  - 修复原生分隔符插件包含双引号的时候解析失败的问题。

  - 修复内部`gethostbyname`函数线程不安全问题。

## **1.8.10**

发布时间：2024.07.12

- ### 优化


  - 支持使用环境变量`ALICLOUD_SLS_CLIENT_AUTH_VERSION`配置Logtail使用的SDK的V4鉴权。

## **1.8.9**

发布时间：2024.06.25

- ### 优化


  - 容器运行时探测重试机制优化。
- ### 修复


  - 修复`dockershim`文件存在的情况下，`containerd`运行时识别不准确的问题。

  - 修复文件路径中存在`*//`导致的`coredump`问题。

  - 修复采集容器标准输出场景获取文件路径异常问题。

  - 修复文件轮转的时候强制刷新数据不完全的问题。

## **1.8.8**

发布时间：2024.04.17

- ### 优化


优化发送模块`sender`的日志打印。

- ### 修复


  - 日志内容中重复key场景兼容并且保证key顺序正确。

  - 修复用户标识`aliuid`文件删除的情况下日志仍然采集的问题。

## **1.8.7**

发布时间：2024.03.05

- ### **新功能**


  - Logtail-ds组件在ACK场景下支持资源组配置。

  - 拓展插件新增`processor_rate_limit`插件。
- ### 修复


  - 修复Logtail使用历史数据采集之后进程无法优雅退出的问题。

## **1.8.6**

发布时间：2024.01.30

- ### **优化**


  - Golang插件指标数据和上报逻辑优化，指标统一通过C++指标模块上报
- ### 修复


  - 修复开启高精度时间戳开关后Golang模块误加载问题

## **1.8.5**

发布时间：2024.01.24

- ### 修复


  - 修复标签数据多线程处理导致Golang插件模块异常的问题

## **1.8.4**

发布时间：2024.01.04

- ### **优化**


  - goprofile插件上报数据中使用机器的IP地址
- ### 修复


  - 修复正则配置time\_key没有默认设置为time的兼容性问题

  - 修复使用libcurl因没有设置CURLOPT\_NOSIGNAL导致偶尔崩溃的问题

  - 修复原生分隔符解析插件解析行首有空格的日志时字段错乱的问题

  - 修复原生插件丢弃超时日志时区处理错误的问题

  - 修复解析任意含有content key的JSON后，原生JSON插件总是错误保留原始content字段的问题

  - 修复原生分隔符插件的内存泄露问题

  - 修复因检查点转储早于目录注册导致的日志重复问题

  - 修复飞天日志无法解析带逗号时间格式的兼容性问题

  - 原生解析失败并选择保留原始日志，原始日志将仅保留在\_\_raw\_log\_\_而不再保留在content字段以避免数据重复

  - 修复K8s集群Pod网络为HostNetwork时获取到的容器IP有时为空的问题

## **1.8.3**

- ### **修复**


  - 解决因容器内存修复引入的日志重复采集问题

  - 修复container info含nil字段导致的插件崩溃

  - 修复ProcessorParseDelimiterNative解析携带下一行数据的问题

  - 修复在反压情况下可能出现的文件无法读完的问题

  - 修复plugin\_export panic导致插件崩溃的问题

  - 修复解析Apsara格式日志导致的崩溃问题

  - 修复解析Apsara格式日志解析数据黏连问题

## **1.8.0**

- 新功能

  - 支持超时切分行。

  - 日志服务Flusher支持纳秒级日志时间。

  - 新增全局主机路径黑名单。

  - 新增Trace解析插件processor\_otel\_metric。

  - 以环境变量方式创建Logtail配置时支持添加资源标签。
- 优化

  - 缓存未构成完整行的日志，减少读文件系统调用。

  - 支持使用环境变量控制日志打印级别。

  - skywalking插件支持捕获db.connection\_string标签。

  - 校验网卡IP地址以获取更精确的主机IP地址。
- 修复

  - 解决采集有挂载卷的statefulset漂移到不同节点时数据重复采集的问题。

  - 修复空文件inode复用后导致采集到的日志文件名错误的问题。

  - 修复因Checkpoint重新打开文件导致容器无法退出的问题。

  - 修复飞天日志时间无法调整时区的问题。

  - 修复JSON模式日志解析时，最后没有回车可能解析不正确的问题。

  - 修复读取到的数据开头含有非法JSON时，JSON解析异常的问题。

## **1.7.1**

- 新功能

  - 新增采集插件input\_command，支持采集命令执行结果。

  - 新增处理插件processor\_log\_to\_sls\_metric，支持将Log解析为Metric。
- 优化

  - processor\_json插件支持解析JSON array格式数据。

  - containerd容器采集支持自定义rootfs路径和自动发现路径。

  - 优化容器元信息预览功能的上报逻辑。
- 修复

  - 修复stdout文件路径为软链接时无法采集容器stdout的问题。

  - 修复当只有容器删除事件时容器因FD锁住无法退出的问题。

  - 修复service\_go\_profile插件报nil panic问题。

  - 采集磁盘相关指标时增加超时配置，避免采集异常。

  - 修复容器场景下profile数据元信息不准确的问题。

## 1.6.0

- 新功能

全栈监控应用支持采集Kubernetes openkruise指标数据。

- 优化

Logtailprofile数据增加容器元信息数据。

- 问题修复

  - 修复容器退出导致的FD被释放问题。

  - 修复Kubernetes场景下Env配置缓存问题。

## 1.5.1

- 新功能

  - 新增启动参数data\_endpoint\_policy，支持设置Logtail对日志服务访问域名的切换策略。

  - Profiling功能支持goprofile拉取模式。

  - 新增字符串替换插件processor\_string\_replace。

  - Logtail支持通过HTTP\_PROXY配置网络代理。
- 优化

优化了processor\_split\_key\_value插件的性能，并增加多字符引用符。

- 问题修复

修复metric\_system\_v2插件磁盘用量指标统计问题。


## 1.4.0

- 新功能

  - HTTP输入服务新增Pyroscope协议。

  - 支持上报端上容器信息，增强容器采集配置可观测性。
- 优化

ENV自动采集方式支持更多LogStore相关的配置参数，例如冷存储配置。


## 1.3.2

- 优化

prometheus抓取插件支持Staleness数据。

- 问题修复

  - 修复时区相关问题，使用系统时间和解析日志时间失败时忽略时区调整选项的问题。

  - 修复因inode复用导致的日志重复采集问题。

  - 修复Grok插件在解析中文时可能会不工作的问题。

  - 修复1.2.1版本中引入的容器发现所占用的内存过高的问题。

## 1.3.1

- 新功能

  - 支持通过HTTP接入Open Telemetry协议日志。

  - 新增脱敏插件processor\_desensitize。更多信息，请参见 [脱敏插件](https://help.aliyun.com/zh/sls/desensitization-plug-in#db09c59087exo "")。
- 优化

  - 在容器环境下，使用环境变量方式创建SLS资源时支持使用HTTPS协议。

  - 在容器环境下，通过CRD方式创建LogStore时，支持选择LogStore规格。

  - 使用插件处理数据时也支持输出内容在文件内偏移量。

  - 默认支持采集容器标准输出时，保持连续的上下文。

  - Prometheus数据接入内存优化。
- 问题修复

  - 修复Docker环境下潜在的FD泄露和事件遗漏问题。

  - 修复Logtail采集配置更新时文件句柄泄露的问题。

  - 修复IP地址在特殊主机名下解析错误的问题。

  - 修复多个配置路径存在父子目录关系时文件重复采集的问题。

## 1.2.1

- 新功能

  - 支持采集SQL Server、PostgreSQL查询结果。更多信息，请参见 [采集SQL Server查询结果](https://help.aliyun.com/zh/sls/collect-sql-server-query-results#task-2260852 "")、 [采集PostgreSQL查询结果](https://help.aliyun.com/zh/sls/collect-postgresql-query-results#task-2261264 "")。

  - 支持采集JMX性能指标。

  - 新增日志上下文聚合插件（aggregator\_context插件）。更多信息，请参见 [aggregators配置](https://help.aliyun.com/zh/sls/overview-22#section-yfm-xyj-hit "")。

    使通过Logtail插件处理的日志的上下文查询、\_\_topic\_\_字段提取和LiveTail等功能可用。

  - 新增Grok插件，用于提取日志字段。更多信息，请参见 [表单配置方式](https://help.aliyun.com/zh/sls/extract-content-from-log-fields#section-ucx-pqc-4wh "")。

    支持设置多个Grok表达式匹配日志的多种格式。
- 优化

支持采集秒退容器的标准输出。

- 问题修复

修复飞天日志格式微秒时间戳解析问题。


## 1.1.1

- 新功能

  - 新增Logtail CSV处理插件。更多信息，请参见 [表单配置方式](https://help.aliyun.com/zh/sls/extract-content-from-log-fields#section-52b-6cx-jz8 "")。

  - 支持通过eBPF进行四层、七层网络流量分析，支持HTTP、MySQL、PgSQL、Redis、DNS协议。

## 1.1.0

- 新功能

netping插件支持httping和DNS解析耗时。


## 1.0.34

- 新功能

新增Skywalking Logging API。

- 优化

支持快速释放已停止的containerd容器文件句柄。

- 问题修复

修复containerd容器的Kubernetes Label无法匹配问题。


## 1.0.32

- 新功能

采集文本日志时，支持通过扩展配置（"enable\_precise\_timestamp": true）或processor\_strptime插件解析高精度时间。

- 优化

  - 优化Kubernetes场景下rootfs探测机制。

  - 优化Kubernetes场景下容器运行时的识别机制。
- 问题修复

修复netping插件在Windows系统中的异常问题。


## 1.0.31

- 新功能

  - Logtail采集配置支持环境变量替换。

  - 新增netping插件，用于采集指定的IP地址与目标IP地址之间的网络ping数据。

  - gotime插件支持将提取的日志时间转换为timestamp格式。

  - 采集syslog日志时，新增\_client\_ip\_字段，表示传输日志的客户端IP地址。
- 优化

优化容器标准输出流采集内存。


## 1.0.30

- 新功能

  - Prometheus插件支持通过多个Logtail采集配置采集同一台机器上的Prometheus数据。

  - 容器服务Kubernetes的Windows节点支持add-on token鉴权。
- 问题修复

  - 修复进程采集插件在Linux系统中发生threadNum与fdNum指标错误问题。

  - 修复SkyWalking插件出现ConfigurationDiscoveryService not implement错误问题。

## 1.0.29

- 问题修复

修复采集容器标准输出时，通过正则匹配Label失效的问题（该问题发生在Logtail 1.0.27、Logtail 1.0.28版本中）。


## 1.0.28

- 新功能

  - 支持采集SNMP协议数据。

  - SkyWalking V3版本插件支持过滤instance属性。

  - 支持配置分隔符模式的 **是否接受部分字段** 参数。
- 问题修复

修复SkyWalking V2版本插件的Span ID不正确问题。


## 1.0.27

- 新功能

  - 新增processor\_regex插件。

  - 支持多地域配置管控。
- 优化

优化主机指标的采集功能，支持采集IO Counter指标。

- 问题修复

  - 修复service\_http\_server插件不释放UNIX链接问题。

  - 修复Logtail同时运行多份metric\_meta\_kubernetes插件采集配置时冲突问题。

## 1.0.26

- 新功能

  - 支持采集进程指标。

  - 采集主机指标时，新增文件句柄以及TCP协议的采集。

  - 支持采集Kubernetes集群的Meta信息。

  - 支持采集主机的Meta信息。

  - 新增gRPC输出插件。

  - 采集容器日志时，支持Kubernetes集群语义识别。

  - 支持采集SkyWalking V2版本的Trace数据。

  - 支持在Windows i386平台运行input\_canal插件。
- 优化

优化容器环境下主机指标采集的准确性。


## 1.0.25

- 问题修复

修复导入历史数据时潜在的崩溃问题。

- 优化

加强在文件系统readdir API返回不精确元数据时的逻辑处理。


## 1.0.24

- 问题修复

修复Logtail刚启动时发送的数据未携带自定义标识符的问题。


## 1.0.22

- 问题修复

修复在全球加速模式下的网络中断时，Logtail可能停止上报状态数据（非用户数据）到日志服务的问题。


## 1.0.21

Logtail 1.0.21版本是首个全地域发布的Logtail 1.0版本，具备Logtail 0.16.64版本的所有功能，新增以下功能：

- 新功能

  - 新增配置项exactly\_once\_concurrency，实现了Logtail可以在本地磁盘记录细粒度的Checkpoint信息（文件级别）。更多信息，请参见 [Logtail配置（旧版）](https://help.aliyun.com/zh/sls/developer-reference/logtail-configurations#concept-f3n-s5q-12b "")。

  - 新增配置项enable\_log\_time\_auto\_adjust，实现了日志时间可自适应服务器本地时间。更多信息，请参见 [设置Logtail启动参数](https://help.aliyun.com/zh/sls/configure-the-startup-parameters-of-logtail#concept-sdg-czb-wdb "")。

  - 新增配置项enable\_log\_position\_meta，用于在日志中添加该日志所属原始文件的元数据信息。更多信息，请参见 [Logtail配置（旧版）](https://help.aliyun.com/zh/sls/developer-reference/logtail-configurations#concept-f3n-s5q-12b "")。

  - 新增配置项specified\_year，用于使用当前时间中的年份或指定年份补全日志时间。更多信息，请参见 [Logtail配置（旧版）](https://help.aliyun.com/zh/sls/developer-reference/logtail-configurations#concept-f3n-s5q-12b "")。

## 0.16.68

- 问题修复

  - 修复采集容器标准输出时，未正确处理P（partial）标签导致的解析失败问题。

  - 修复在service\_skywalking\_agent\_v3插件跨应用情况下，Links中的SpanID和ParentSpanID不正确的问题。

## 0.16.64

- 优化

上调请求容器引擎时的超时时间，将3秒调整为30秒。新增环境变量DOCKER\_CLIENT\_REQUEST\_TIMEOUT，用于设置请求容器引擎的超时时间。

- 问题修复

  - 修复service\_skywalking插件的父Span ID发生错误的缺陷。

  - 修复根据环境变量创建的采集配置的逻辑在容器引擎异常时可能退出的缺陷。

## 0.16.62

**说明**

如果您使用的是Logtail 0.16.58、0.16.60版本，建议您升级到Logtail 0.16.62版本。

- 问题修复

修复在数据乱序场景下小概率发生的数据发送失败问题。


## 0.16.60

- 新功能

支持采集containerd环境的容器数据。


## 0.16.56

- 优化

调整服务日志中net\_err\_stat指标的覆盖范围，仅覆盖网络引起的发送错误。


## 0.16.54

- 新功能

在服务日志中新增net\_err\_stat指标，记录最近1分钟、5分钟、15分钟内发生的发送错误的数量。


## 0.16.52

如果和容器（标准输出、容器文件）相关的采集配置较多，建议升级Logtail到0.16.52及以上版本，以有效地降低CPU开销。

- 优化

优化容器数据采集场景的CPU开销。


## 0.16.50

- 新功能

支持运行时按需安装service\_telegraf插件（仅限ECS用户）。


## 0.16.48

- 优化

优化service\_telegraf插件，支持单机多个配置。


## 0.16.46

**说明**

如果您在杭州、上海、北京地域，升级Logtail至0.16.46及以上版本，可避免Logtail在遇到网络抖动时切换Endpoint。

- 优化

严格限制允许Logtail使用的网络类型。


## 0.16.44

- 新功能

新增service\_telegraf插件，支持采集指标数据。更多信息，请参见 [接入Telegraf数据](https://help.aliyun.com/zh/sls/user-guide/overview-18#concept-1964724 "")。


## 0.16.42

- 新功能

黑名单过滤支持多级匹配，例如/path/\*\*/log。

- 优化

优化本地IP地址获取策略。在原先策略失效时，获取列表中的第一个IP地址。


## 0.16.40

- 新功能

  - 新增主机状态数据插件metric\_system\_v2。更多信息，请参见 [采集主机监控数据](https://help.aliyun.com/zh/sls/collect-metric-data-from-hosts#task-2538936 "")。

  - 新增环境变量ALIYUN\_LOGTAIL\_MAX\_DOCKER\_CONFIG\_UPDATE\_TIMES对应的参数max\_docker\_config\_update\_times，适用于在K8s环境中频繁创建Job短时任务的场景。
- 优化

优化容器采集场景中采集配置较多时的性能（CPU 开销）。

- 问题修复

修复processor\_split\_log\_string插件偶尔产生空行的问题。


## 0.16.38

- 新功能

  - 完整正则模式支持自定义时间字段名。

  - 在processor\_json、processor\_regex、processor\_split\_char插件中，新增KeepSourceIfParseError参数，支持解析失败时保留原始数据。更多信息，请参见 [使用Logtail插件处理数据](https://help.aliyun.com/zh/sls/overview-22#concept-hy3-nyc-wdb "")。

## 0.16.36

- 新功能

新增加密插件processor\_encrypt。


## 0.16.34

- 新功能

新增HTTP Probe，支持K8s健康检查。

- 问题修复

  - 修复某些环境中，由libcurl导致的core。

  - 修复在CentOS 8系统中安装Logtail，缺少libidn库的问题。

## 0.16.32

- 新功能

在processor\_json插件中，新增IgnoreFirstConnector参数。更多信息，请参见 [扩展插件：展开JSON字段](https://help.aliyun.com/zh/sls/expand-json-fields#concept-2010735 "")。


## 0.16.30

**重要**

此版本长时间运行时有潜在的打开文件失败风险，建议升级至最新版本。

- 新功能

在采集Docker标准输出及文件时，新增K8s级别的过滤功能。

- 优化

优化网络条件较差时同地域LogStore之间的并发竞争。

- 问题修复

修复由于文件打开逻辑错误小概率发生的checkpoint丢失问题。


## 0.16.28

- 新功能

新增参数，用于配置首次采集的Tail大小。

- 优化

优化容器元信息获取逻辑，降低异常容器对整体的影响。

- 问题修复

  - 修复docker\_stdout在复杂环境下的内存泄露问题。

  - 修复JSON模式下对毫秒时间戳不完整支持的问题。

## 0.16.26

- 新功能

支持采集containerd的日志。

- 问题修复

  - 修复极低概率下发生的轮转文件丢失checkpoint的问题。

  - 修复本地采集配置文件/etc/ilogtail/user\_config.d在/usr/local/ilogtail/user\_log\_config.json文件不存在时未被加载的问题。

## 0.16.24

- 新功能

  - 支持通过环境变量配置working\_ip和working\_hostname。

  - 新增force\_quit\_read\_timeout参数，支持设置强制退出的超时时间（持续阻塞无法读取事件）。

  - 支持向插件传递path、topic等tag。

  - 新增aggregator\_shardhash插件，支持在插件内设置shardhash。

  - 新增处理插件processor\_gotime、processor\_rename、processor\_add\_fields、processor\_json、processor\_packjson。更多信息，请参见 [使用Logtail插件处理数据](https://help.aliyun.com/zh/sls/overview-22#concept-hy3-nyc-wdb "")。

  - 更新LogtailInsight，新增进度查看功能（需要设置mark\_offset\_global\_flag或customized\_fields.mark\_offset）。
- 优化

  - 优化Journal长时间运行内存偏高的情况，尽可能及早释放。

  - 优化在本地无配置的情况下首次获取配置的时间间隔。
- 问题修复

  - 修复多个Logtail配置的情况下可能产生的重复采集问题。

  - 修复毫秒、微秒时间戳不支持JSON int64的问题。

## 0.16.32

- 新功能

  - 支持毫秒、微秒时间戳（%s）。

  - 支持加载多个本地Logtail配置（/etc/ilogtail/config.d/）。

  - 支持加载多个本地用户配置（/etc/ilogtail/user\_config.d/）。

  - 新增处理插件processor\_split\_key\_value、processor\_strptime。更多信息，请参见 [表单配置方式](https://help.aliyun.com/zh/sls/extract-content-from-log-fields#section-9jv-x7c-fbu "")、 [扩展插件：提取日志时间](https://help.aliyun.com/zh/sls/extract-log-time#concept-2010733 "")。

  - 新增oas\_connect\_timeout、oas\_request\_timeout参数，支持网络慢的场景。

  - 新增安装脚本支持通过金融云公网安装Logtail。更多信息，请参见 [安装Logtail（Linux系统）](https://help.aliyun.com/zh/sls/install-logtail-on-a-linux-server#section-xrx-wmv-vdb "")。
- 优化

取消混合配置（file+plugin）中对inputs的限制。


## 0.16.21

- 新功能

  - 支持自定义静态主题设置。

  - 支持黑名单过滤。

  - 在service\_canal插件中新增EnableEventMeta参数，支持采集MySQL Binlog对应的header信息。
- 优化

优化插件系统停止机制。

- 问题修复

修复GBK日志潜在的内存泄漏。


## 0.16.18

- 新功能

  - 支持采集Docker事件。更多信息，请参见 [采集Docker事件](https://help.aliyun.com/zh/sls/collect-docker-events#concept-lck-225-ngb "")。

  - 支持采集Systemd Journal日志。更多信息，请参见 [采集Systemd Journal日志](https://help.aliyun.com/zh/sls/collect-systemd-journal-logs#concept-oc3-pc5-ngb "")。

  - 新增处理插件processor\_pick\_key 、processor\_drop\_last\_key。
- 优化

  - 优化容器日志以及插件采集内存占用。

  - 优化采集容器标准输出（stdout）多行日志的性能。

## 0.16.16

- 新功能

  - 支持自动创建K8s审计日志相关的资源。

  - 支持通过环境变量配置启动参数，例如CPU、内存、发送并发等。

  - 支持通过环境变量配置自定义tag上传。

  - sidecar模式支持自动创建配置。更多信息，请参见 [通过Sidecar-CRD方式采集容器文本日志](https://help.aliyun.com/zh/sls/use-crds-to-collect-container-text-logs-in-sidecar-mode#task-1580748 "")。
- 优化

自动保存aliuid文件到本地文件。

- 问题修复

  - 修复采集容器文件出现极低概率的crash的问题。

  - 修复通过环境变量创建出的配置在K8s中存在的`IncludeLabel`不生效问题。

## 0.16.15

- 新功能

  - 采集MySQL Binlog时，支持GTID模式。在采集MySQL Binlog时自动开启该模式。

  - 历史数据导入文件名支持指定通配符。

  - K8s支持自动创建索引配置。
- 优化

  - 当分行失败时，支持检查`discardUnMatch`并上报分行失败的日志。

  - 遇到unknown send error时自动重试，防止极低情况下数据丢失（例如发送的数据包中途被篡改）。

## 0.16.14

- 新功能

  - 导入历史数据支持通配符模式。

  - 增加启动配置项`default_tail_limit_kb`，用于配置首次采集文件跳转大小（默认1024KB）。

  - 增加采集配置项`batch_send_seconds`，用于配置数据包发送的时间。

  - 增加采集配置项`batch_send_bytes`，用于配置数据包的大小。
- 优化

采集容器标准输出（stdout）时，支持自动合并被Docker Engine拆分的日志。


## 0.16.13

新功能

- 支持通过环境变量配置日志采集。

- 支持采集MySQL Binlog中的meta数据，即新增日志字段`_filename_`和`_offset_`。

- 安装脚本支持VPC下自动选择参数。

- 支持全球加速安装模式。更多信息，请参见 [步骤二：配置Logtail采集加速](https://help.aliyun.com/zh/sls/configure-log-collection-acceleration-for-logtail#concept-opz-gml-dgb "")。


## 0.16.11

- 优化

采集MySQL Binlog时，支持采集filename和offset信息。

- 问题修复

修复使用多行模式采集容器标准输出（stdout）时有一定概率出现异常的问题。


## 0.16.10

- 优化

升级容器标准输出（stdout）采集方式。


## 0.16.9

- 问题修复

  - 修复极低概率下出现的socket fd泄露问题。

  - 增加容器文件采集配置更新频率限制。

## 0.16.8

- 新功能

  - 新增Logtail Lumberjack插件，用于采集Logstash、Beats数据源。更多信息，请参见 [采集Beats和Logstash数据源](https://help.aliyun.com/zh/sls/collect-data-from-beats-and-logstash#concept-tk3-gtz-c2b "")。

  - 增加inotify黑名单功能。
- 问题修复

  - 修复旧安装包参数不统一的问题。

  - 修复在部分系统下安装Logtail时无法正确获取OS版本的问题。

## 0.16.6

- 新功能

  - 支持采集主机监控数据。

  - 支持采集Redis监控数据。

  - 支持采集MySQL Binlog中的DDL（data definition language）。

  - 支持采集容器标准输出（stdout）和容器文件时，通过docker ENV（environment）过滤。
- 问题修复

  - 兼容MySQL table无主键情况下的数据采集。

  - 兼容容器采集模式下因容器引擎订阅通道不稳定造成事件丢失的问题。

## 0.16.5

- 新功能

采集容器标准输出（stdout）时，新增多行采集模式。更多信息，请参见 [多行日志的Logtail配置示例](https://help.aliyun.com/zh/sls/collect-container-stdout-and-stderr-in-daemonset-mode#section-gf2-p8y-qsi "")。


## 0.16.4

- 新功能

  - 支持Docker&Kubernetes部署方案。

  - 支持采集容器标准输出（stdout）和容器文件。更多信息，请参见 [通过DaemonSet-控制台方式采集容器标准输出](https://help.aliyun.com/zh/sls/collect-container-stdout-and-stderr-in-daemonset-mode#task-1563727 "")、 [通过DaemonSet-控制台方式采集容器文本日志](https://help.aliyun.com/zh/sls/use-the-log-service-console-to-collect-container-text-logs-in-daemonset-mode#task-1563382 "")。

## 0.16.2

- 新功能

新增processor\_geoip插件。更多信息，请参见 [扩展插件：转换IP地址](https://help.aliyun.com/zh/sls/convert-ip-addresses#concept-2010729 "")。


## 0.16.0

- 新功能

  - 支持采集MySQL Binlog、MySQL查询结果、HTTP数据。更多信息，请参见 [使用Logtail插件采集数据](https://help.aliyun.com/zh/sls/overview-19#concept-apw-dvc-wdb "")。

  - 支持组合解析配置：正则模式、标定模式、分隔符模式、过滤器。