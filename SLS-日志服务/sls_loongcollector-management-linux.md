### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[LoongCollector数据采集器（原Logtail）](https://help.aliyun.com/zh/sls/loongcollector-management/)[Linux 安装与管理](https://help.aliyun.com/zh/sls/loongcollector-installation-and-management-linux/)配置管理

# 配置管理

更新时间：2026-02-05 22:13:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：安装采集器](https://help.aliyun.com/zh/sls/loongcollector-installation-linux)[下一篇：LoongCollector安装（Windows）](https://help.aliyun.com/zh/sls/loongcollector-installation-windows)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

LoongCollector常用命令

启动与停止LoongCollector

查看LoongCollector状态

查看LoongCollector版本

启动参数配置文件（ilogtail\_config.json）

采集性能配置规划

其他常用配置文件

LoongCollector采集配置文件（user\_log\_config.json）

AppInfo记录文件（app\_info.json）

LoongCollector运行日志（loongcollector.LOG）

用户ID文件

用户自定义标识文件

CheckPoint文件

安装LoongCollector后，您还需要了解如何管理LoongCollector的生命周期，运行配置等内容。

## **LoongCollector常用命令**

### **启动与停止LoongCollector**

> 对采集性能有要求时，可修改 [启动参数配置文件（ilogtail\_config.json）](https://help.aliyun.com/zh/sls/loongcollector-management-linux#5d5e0ea642guf "") 后再启动LoongCollector。

```shell
sudo /etc/init.d/loongcollectord start #启动
sudo /etc/init.d/loongcollectord stop #停止
sudo /etc/init.d/loongcollectord restart #重启
```

### **查看LoongCollector状态**

```shell
sudo /etc/init.d/loongcollectord status #返回loongcollector is running表示启动成功。
```

### **查看LoongCollector版本**

```shell
cat /usr/local/ilogtail/app_info.json #版本信息存储在loongcollector_version字段中。
```

## **启动参数配置文件（ilogtail\_config.json）**

- 文件描述：配置LoongCollector的启动参数，启动参数配置不合理会影响采集性能，配置错误可能导致采集异常问题发生。

- 文件路径：/usr/local/ilogtail/ilogtail\_config.json。

- 使用场景：日志服务限制了LoongCollector的采集性能，以防消耗过多服务器资源，影响其他服务运行。当LoongCollector采集性能不满足要求时，可通过修改启动参数进行尝试。具体使用场景可参考 [通过修改配置解决常见采集问题](https://help.aliyun.com/zh/sls/resolve-common-collection-issues-through-configuration-changes "")。

- 文件示例 ：















```shell
{
      "primary_region" : "cn-beijing", // 默认地域，可忽略
      "config_servers" : //获取采集配置时的地址
      [\
          "http://logtail.cn-beijing.log.aliyuncs.com"\
      ],
      "data_servers" : //与日志服务进行数据传输的地址
      [\
          {\
              "region" : "cn-beijing",\
              "endpoint_list": [\
                  "cn-beijing.log.aliyuncs.com"\
              ]\
          }\
      ],
      "cpu_usage_limit" : 0.4,
      "mem_usage_limit" : 384,
      "max_bytes_per_sec" : 20971520,
      "bytes_per_sec" : 1048576,
      "buffer_file_num" : 25,
      "buffer_file_size" : 20971520,
      "buffer_map_num" : 5
}
```

- 参数表：下表仅列出需要关注的常用启动参数，请根据需要新增或修改。未列出的参数请保持默认配置。



**ilogtail\_config.json启动参数表**






|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **说明** | **示例** |
| cpu\_usage\_limit | double | CPU使用阈值，以单核计算。取值如下：<br>  - 取值范围：0.1~当前机器的CPU核心数<br>    <br>  - 默认值：0.4<br>    <br>**警告**<br>cpu\_usage\_limit为软限制，实际占用的CPU可能超过限制值，超限5分钟后将触发熔断保护自动重启。<br>例如设置为0.4，表示日志服务将尽可能限制采集器的CPU使用为CPU单核的40%，超出后自动重启。<br>一般情况下，通过极简模式采集日志时，单核处理能力约100 MB/s；通过完整正则模式采集日志时，单核处理能力约20 MB/s 。 | "cpu\_usage\_limit" : 0.4 |
| mem\_usage\_limit | int | 内存使用阈值。取值如下：<br>  - 取值范围：128 MB ~ 8192 MB<br>    <br>  - 默认值：384 MB（主机），2048 MB（ACK组件）<br>    <br>**警告**<br>mem\_usage\_limit为软限制，实际占用的内存可能超过限制值，超限5分钟后将触发熔断保护自动重启。<br>采集速率、监控目录和文件数量、发送阻塞程度与mem\_usage\_limit参数有关。更多请参见 [限制说明](https://help.aliyun.com/zh/sls/logtail-limits "")。 | "mem\_usage\_limit" : 384 |
| max\_bytes\_per\_sec | int | 每秒钟发送原始数据的流量限制。取值如下：<br>  - 取值范围：1024 Byte/s ~ 52428800 Byte/s<br>    <br>  - 默认值：20971520 Byte/s<br>    <br>    <br>    <br>    **重要**<br>    <br>    <br>    <br>    <br>    <br>    设置的值超过20971520 Byte/s（20MB/s），表示不限速。 <br>    <br>例如设置为2097152，表示发送数据的速率为2 MB/s。 | "max\_bytes\_per\_sec" : 2097152 |
| process\_thread\_count | int | 处理数据的线程数。 取值如下：<br>  - 取值范围：1~64<br>    <br>  - 默认值：1<br>    <br>一般情况下，可以处理极简模式下24 MB/s的数据写入或完整正则模式12 MB/s的数据写入。默认情况下无需调整该参数取值。 | "process\_thread\_count" : 1 |
| send\_request\_concurrency | int | 异步并发的个数。取值如下：<br>  - 取值范围：1~50<br>    <br>  - 默认值：20<br>    <br>如果写入TPS很高，可以设置更高的异步并发个数。可以按照一个并发支持0.5 MB/s~1 MB/s网络吞吐来计算，实际根据网络延时而定。 <br>**说明**<br>设置异步并发个数过高容易导致网络端口占用过多，需调整TCP相关参数。更多信息，请参见 [调整TCP相关参数](https://yq.aliyun.com/articles/52884)。 | "send\_request\_concurrency" : 4 |
| buffer\_file\_num | int | 限制缓存文件的最大数目。取值如下：<br>  - 取值范围：1~100<br>    <br>  - 默认值：25<br>    <br>遇到网络异常、写入配额超限等情况时，采集器将实时解析后的日志写入本地文件（安装目录下）缓存起来，等待恢复后尝试重新发送。 | "buffer\_file\_num" : 25 |
| buffer\_file\_size | int | 单个缓存文件允许的最大字节数。取值如下：<br>  - 取值范围：1048576 Byte ~ 104857600 Byte<br>    <br>  - 默认值：20971520 Byte<br>    <br>buffer\_file\_size\*buffer\_file\_num是缓存文件可以实际使用的最大磁盘空间。 | "buffer\_file\_size" : 20971520 |
| buffer\_file\_path | String | 缓存文件存放目录。 默认值为空，即缓存文件存放于安装目录/usr/local/ilogtail下。 <br>当您设置此参数后，需手动将原目录下名为logtail\\\_buffer\\\_file\_\*的文件移动到此目录，以保证采集器可以读取到该缓存文件并在发送后进行删除。 | "buffer\_file\_path" : "" |
| bind\_interface | String | 本机绑定的网卡名。默认值为空，自动绑定可用的网卡。 <br>如果设置为指定的网卡（例如eth1），则表示将强制使用该网卡上传日志。 | "bind\_interface" : "" |
| check\_point\_filename | String | checkpoint文件的保存路径， 默认值：/tmp/logtail\_check\_point。 | "check\_point\_filename" : /tmp/logtail\_check\_point |
| check\_point\_dump\_interval | int | 更新Checkpoint文件的周期，默认值：900，单位：秒。即默认情况下每15分钟更新一次Checkpoint文件。 | "check\_point\_dump\_interval" : 900 |
| user\_config\_file\_path | String | 配置文件的保存路径，默认为进程binary所在目录，文件名为user\_log\_config.json。 | "user\_config\_file\_path" : user\_log\_config.json |
| discard\_old\_data | Boolean | 是否丢弃历史日志。默认值：true，表示丢弃距离当前时间超过12小时的日志。 | "discard\_old\_data" : true |
| ilogtail\_discard\_interval | int | 丢弃历史日志距离当前时间的阈值。默认值：43200（12小时），单位：秒。 | "ilogtail\_discard\_interval": 43200 |
| working\_ip | String | 默认值为空，表示自动从本服务器获取IP地址。修改后将以该值作为服务器的IP地址上报。 | "working\_ip" : "" |
| working\_hostname | String | 上报的本服务器的主机名。默认值为空，表示自动从本服务器获取主机名。 | "working\_hostname" : "" |
| max\_read\_buffer\_size | long | 每条日志读取的最大值。默认值：524288（512 KB），最大值：8388608（8 MB）。单位：Byte。<br>如果您的单条日志超过524288 Byte，可修改此参数。 | "max\_read\_buffer\_size" : 524288 |
| oas\_connect\_timeout | long | 发起获取采集配置、访问密钥等请求时，连接阶段的超时时间。默认值：5，单位：秒。 <br>网络条件较差，建立连接时间过长时可修改此参数。 | "oas\_connect\_timeout" : 5 |
| oas\_request\_timeout | long | 发起获取采集配置、访问密钥等请求时，整个请求阶段的超时时间。默认值：10，单位：秒。 <br>网络条件较差，建立连接时间过长时可修改此参数。 | "" : 10 |
| data\_server\_port | long | 设置data\_server\_port为443后，将通过HTTPS协议传输数据到日志服务。 | "data\_server\_port": 443 |
| enable\_log\_time\_auto\_adjust | Boolean | 设置enable\_log\_time\_auto\_adjust为true后，日志时间可自适应服务器本地时间。<br>出于数据安全考虑，日志服务会对请求（包括Logtail发起的请求）所携带的时间进行校验，拒绝与日志服务端时间相差超过15分钟的请求。采集器发起请求时所携带的时间为服务器本地时间，当服务器本地时间被修改后（例如某些测试场景下需要调整本地时间为未来时间），请求将被拒绝，导致写入数据失败。您可以使用该参数实现日志时间自适应服务器本地时间。<br>**重要**<br>  - 开启该功能后，日志时间将被加上日志服务端的时间与服务器本地时间的偏移量。由于偏移量只在请求被日志服务端拒绝时更新，因此可能出现日志服务端所查询到的日志的时间和日志实际的写入时间不一致的情况。<br>    <br>  - LoongCollector的部分逻辑依赖于系统时间的递增，建议在每次机器时间调整后重启采集器。 | "enable\_log\_time\_auto\_adjust": true |
| accept\_multi\_config | Boolean | 是否允许多个采集配置采集同一个文件。默认值：false，表示不允许。<br>默认情况下，一个文件只能被一个采集配置采集，您可以通过该参数消除限制。每个采集配置的处理过程是独立的，当允许多个采集配置采集同一个文件时，需要消耗多倍的CPU、内存开销。 | "accept\_multi\_config": true |
| enable\_checkpoint\_sync\_write | Boolean | 是否开启sync写功能。默认值：false，表示不开启。<br>sync写功能主要用于搭配ExactlyOnce写入功能。开启ExactlyOnce写入功能后，采集器会在本地磁盘记录细粒度的Checkpoint信息（文件级别）。但出于性能考虑，默认写入Checkpoint时不会调用sync落盘，所以如果机器重启导致buffer数据来不及写入磁盘时，可能导致Checkpoint丢失。此时，您可以设置enable\_checkpoint\_sync\_write为true，开启sync写功能。更多信息，请参见 [Logtail配置（旧版）](https://help.aliyun.com/zh/sls/developer-reference/logtail-configurations#section-okt-nus-mpa "")。 | "enable\_checkpoint\_sync\_write": false |
| enable\_env\_ref\_in\_config | Boolean | 是否启用采集配置环境变量替换功能。默认值：false。<br>开启该功能后，您可以在控制台的采集配置中使用`${xxx}`作为环境变量`xxx`的占位符。例如设置采集路径为`/${xxx}/logs`，环境变量为`xxx=user`，则生效的采集路径为`/user/logs`。<br>如果配置中需要使用`${`、`}`，则您可以使用`$${`、`$}`进行转义。 | "enable\_env\_ref\_in\_config": false |
| logreader\_max\_rotate\_queue\_size | Int | 轮转队列最大长度。默认值：20。当日志采集发生阻塞或延时，待采集的文件会持有文件句柄在队列中等待。<br>当采集延时，如果需要控制磁盘最大用量，可考虑减小该值。<br>**警告**<br>当延时的文件数超过该值时，将直接跳过新文件的采集。 | "logreader\_max\_rotate\_queue\_size" : 10 |
| data\_endpoint\_policy | string | 对日志服务访问域名的切换策略。可选值如下：<br>**说明**<br>您可以在ilogtail\_config.json文件的data\_server参数中，查看是否已配置默认域名。<br>  - designated\_first（默认）<br>    <br>    - 如果已指定某个地域的默认域名且默认域名可用，则系统优先使用默认域名。<br>      <br>    - 如果已指定某个地域的默认域名但默认域名不可用，则系统会自动选择一个可用域名。<br>      <br>    - 如果未指定某个地域的默认域名，则系统会自动选择一个可用域名。<br>  - designated\_locked<br>    <br>    - 如果已指定某个地域的默认域名，不管其是否可用，系统都将只使用默认域名。<br>      <br>    - 如果未指定某个地域的默认域名，系统会自动选择一个可用域名。 | "data\_endpoint\_policy" : "designated\_first" |
| inotify\_black\_list | Array<String> | inotify监听黑名单，黑名单为完全匹配，此列表中的目录不会启用inotify监听。 | "inotify\_black\_list": \["/tmp"\] |
| host\_path\_blacklist | String | 全局主机路径黑名单，黑名单为子串匹配。Linux系统下多个子串以半角冒号（:）分隔。<br>例如`"host_path_blacklist" : "/volumes/kubernetes.io~csi/nas-"`表示禁止采集NAS挂载数据。 | "host\_path\_blacklist" : "/volumes/kubernetes.io~csi/nas-" |
| LOGTAIL\_LOG\_LEVEL | String | 日志打印级别，需通过环境变量进行配置。默认值：空，表示info，可选值trace、debug、info、warning、error和fatal。 | LOGTAIL\_LOG\_LEVEL=info |
| FORCE\_RELEASE\_STOP\_CONTAINER\_FILE | Boolean | - 配置方式：仅支持通过环境变量方式进行配置。<br>    <br>  - 功能描述：当该参数设置为 `true` 时，采集器会在业务容器退出时立即释放容器文件句柄。此操作可防止因文件句柄未释放而导致容器无法正常退出。<br>    <br>  - 注意事项：<br>    <br>    - 此时无法保证容器内数据采集的完整性。<br>      <br>    - 建议在业务退出前增加几秒的延迟，以确保日志能够完整采集。 | **"** FORCE\_RELEASE\_STOP\_CONTAINER\_FILE **"** : "true" |


### **采集性能配置规划**

为防止采集器消耗过多服务器资源，影响其他服务运行，日志服务对采集性能做了限制。当需要提升采集性能时，可修改启动参数。

#### **推荐参数值示例**

根据实际经验推荐如下参数配置，适用于普通JSON文件的采集场景。完整正则模式和分隔符模式的性能与JSON模式相近，极简模式性能为JSON模式的5倍。由于数据、规则的复杂度、采集目录和文件的数量都会对CPU和内存消耗带来影响，请参照下述表格并结合实际情况按需调整。

添加或修改`/usr/local/ilogtail/ilogtail_config.json`中参数取值，并重启LoongCollector使修改生效。不同采集速率下的建议值参考如下：

**说明**

按表格中的**采集速率大于40 MB/s**列配置启动参数时，采集性能已接近极限。

| **参数** | **描述** | **采集速率大于10 MB/s** | **采集速率大于20 MB/s** | **采集速率大于40 MB/s** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **描述** | **采集速率大于10 MB/s** | **采集速率大于20 MB/s** | **采集速率大于40 MB/s** |
| **cpu\_usage\_limit** | CPU使用阈值，以单核计算。<br>- 取值范围：0.1~当前机器CPU核心数<br>  <br>- 默认值：0.4<br>  <br>**0.4**表示日志服务将尽可能限制采集器对CPU单核使用不超过40%，超出后LoongCollector自动重启。<br>> 该项为软限制，实际占用的CPU可能超过限制值，超限5分钟后将触发熔断保护自动重启。 | 1 | 2 | 4 |
| **mem\_usage\_limit** | 内存使用阈值。<br>- 取值范围：128 MB ~ 8192 MB<br>  <br>- 默认值：384 MB<br>  <br>采集速率、监控目录和文件数量、发送阻塞程度与该参数有关。更多请参见 [限制说明](https://help.aliyun.com/zh/sls/logtail-limits "")<br>> 该项为软限制，实际占用的内存可能超过限制值，超限5分钟后将触发熔断保护自动重启。 | 1024 | 2048 | 4096 |
| **process\_thread\_count** | 采集器处理数据的线程数。 <br>- 取值范围：1~64<br>  <br>- 默认值：1<br>  <br>单线程可以处理极简模式下24 MB/s的数据写入或完整正则模式12 MB/s的数据写入。默认情况下无需调整该参数取值。 | 2 | 4 | 8 |
| **max\_bytes\_per\_sec** | 每秒发送原始数据的流量限制。取值如下：<br>- 取值范围：1024 Byte/s ~ 52428800 Byte/s<br>  <br>- 默认值：20971520 Byte/s<br>  <br>**重要**<br>设置的值超过20971520 Byte/s（20MB/s），表示不限速。 | 209715200 | 209715200 | 209715200 |
| **send\_request\_concurrency** | 异步并发的个数。<br>- 取值范围：1~50<br>  <br>- 默认值：20<br>  <br>如果写入TPS很高，可以设置更高的异步并发个数。可以按照一个并发支持0.5 MB/s~1 MB/s网络吞吐来计算，实际根据网络延时而定。 | 20 | 40 | 80 |

## **其他常用配置文件**

LoongCollector运行时一系列配置文件与信息记录文件如下：

### **LoongCollector采集配置文件（user\_log\_config.json）**

- 描述：文件记录LoongCollector从日志服务获取的采集配置信息，每次采集配置更新时会同步更新该文件。除手动配置AccessKey信息、数据库密码等敏感信息外，不建议修改该文件。

- 路径：/usr/local/ilogtail/user\_log\_config.json。

- 使用场景：可通过查看该文件确认采集配置是否已经下发到服务器。若该文件存在，且内容与日志服务上的采集配置一致，表示采集配置已下发。


### **AppInfo记录文件（app\_info.json）**

- 描述：app\_info.json文件记录LoongCollector的启动时间、获取到的IP地址、主机名等信息。该文件仅作记录，任何修改操作均不会生效。

- 路径：/usr/local/ilogtail/app\_info.json。

- 使用场景：可查看日志服务采集时识别到的服务器ip信息，判断与日志服务控制台中IP型机器组内IP信息是否一致，一般用于解决IP型机器组心跳失败问题。


> 如果已在服务器的/etc/hosts文件中设置了主机名与IP地址绑定，则自动获取绑定的IP地址。如果没有设置主机名绑定，会自动获取本机的第一块网卡的IP地址。若设置了ilogtail\_config.json中的working\_ip参数，则以working\_ip值作为服务器的IP地址。


### **LoongCollector运行日志（loongcollector.LOG）**

- 描述：loongcollector.LOG文件记录了LoongCollector的运行日志，日志级别从低到高分别为INFO、WARN和ERROR。

- 路径：/usr/local/ilogtail/loongcollector.LOG。

- 使用场景：如果采集异常，请先使用 [运行情况诊断与监控](https://help.aliyun.com/zh/sls/automatic-diagnosis-and-monitoring-of-loongcollector-operation "") 排查错误，根据 [日志采集错误类型](https://help.aliyun.com/zh/sls/log-collection-error-type#undefined "") 排查具体的错误类型和LoongCollector运行日志排查问题。


### **用户ID文件**

- 描述：包含日志采集到的Project所属的阿里云主账号ID信息，文件名即账号ID，无需后缀，用于标识该账号有权限访问、采集这台服务器的日志。

- 路径：/etc/ilogtail/users/{阿里云账号ID}。

- 使用场景：只有在采集非本账号ECS、自建服务器、其他云厂商服务器日志时需要配置用户ID。多个账号对同一台服务器进行日志采集时，支持在同一台服务器上创建多个用户ID文件。


### **用户自定义标识文件**

- 描述：用于配置用户自定义标识，作为用户自定义标识机器组的内容，协助日志服务发现服务器上的LoongCollector并建立心跳。

- 路径：/etc/ilogtail/user\_defined\_id。

- 使用场景：使用用户自定义机器组时需要配置，了解更多信息请参考 [机器组与采集配置关联指南](https://help.aliyun.com/zh/sls/machine-group-and-collection-configuration-association-guide "")。


### **CheckPoint文件**

- 描述：checkpoint机制用于记录日志服务当前采集位置以确保日志完整性。

- 路径：默认为`/tmp/logtail_checkpoint`。

- 使用场景：可参考 [限制说明](https://help.aliyun.com/zh/sls/logtail-limits "") 修改启动参数文件进行管理。