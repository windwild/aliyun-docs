### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[日志审计（旧版）](https://help.aliyun.com/zh/sls/log-audit-service/)[日志字段详情](https://help.aliyun.com/zh/sls/log-fields-34/)云安全中心

# 云安全中心

更新时间：2024-11-27 04:11:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DDoS防护](https://help.aliyun.com/zh/sls/anti-ddos)[下一篇：API网关](https://help.aliyun.com/zh/sls/api-gateway)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

网络日志

安全日志

主机日志

本文介绍云安全中心网络日志、安全日志和主机日志的字段详情。

## 网络日志

- DNS日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-log-dns。 |
| owner\_id | 阿里云账号ID。 |
| additional | additional字段，各个值之间以竖线（\|）分隔。 |
| additional\_num | additional字段数量。 |
| answer | DNS回答信息，各个值之间以竖线（\|）分隔。 |
| answer\_num | DNS回答信息数量。 |
| authority | authority字段。 |
| authority\_num | authority字段数量。 |
| client\_subnet | 客户端子网。 |
| dst\_ip | 目标IP地址。 |
| dst\_port | 目标端口。 |
| net\_connect\_dir | 数据的传输方向，包括：<br>  - in：入方式<br>    <br>  - out：出方向 |
| qid | 查询ID。 |
| query\_name | 查询域名。 |
| query\_type | 查询类型。 |
| query\_datetime | 查询时间戳，单位：毫秒。 |
| rcode | 返回代码。 |
| region | 来源地域ID，包括：<br>  - 1：北京<br>    <br>  - 2：青岛<br>    <br>  - 3：杭州<br>    <br>  - 4：上海<br>    <br>  - 5：深圳<br>    <br>  - 6：其它 |
| response\_datetime | 返回时间。 |
| src\_ip | 源IP地址。 |
| threat\_src\_ip | 源IP地址的威胁情报。更多信息，请参见 [威胁情报字段](https://help.aliyun.com/zh/sls/generate-threat-intelligence#section-ghm-rcz-m63 "")。 |
| src\_port | 源端口。 |
| start\_time | 开始时间戳，单位秒。 |

- 本地DNS日志




| **字段名** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **字段名** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为local-dns。 |
| owner\_id | 阿里云账号ID。 |
| answer\_rdata | DNS回答信息，各个值之间以竖线（\|）分隔。 |
| answer\_ttl | DNS回答的时间周期，各个值之间以竖线（\|）分隔。 |
| answer\_type | DNS回答的类型，各个值之间以竖线（\|）分隔。以下是常见的DNS响应类型取值：<br>  - **1**：A记录。<br>    <br>  - **2**：NS记录。<br>    <br>  - **5**：CNAME记录。<br>    <br>  - **6**：SOA记录。<br>    <br>  - **10**：NULL记录。<br>    <br>  - **12**：PTR记录。<br>    <br>  - **15**：MX记录。<br>    <br>  - **16**：TXT记录。<br>    <br>  - **25**：KEY记录。<br>    <br>  - **28**：AAAA记录。<br>    <br>  - **33**：SRV记录。<br>    <br>  - **41**：OPT记录。<br>    <br>  - **43**：DS记录。<br>    <br>  - **44**：SSHFP记录。<br>    <br>  - **45**：IPSECKEY记录。<br>    <br>  - **46**：RRSIG记录。<br>    <br>  - **47**：NSEC记录。 |
| answer\_name | DNS回答的名称，各个值之间以竖线（\|）分隔。 |
| dst\_ip | 目标IP地址。 |
| dst\_port | 目标端口。 |
| group\_id | 分组ID。 |
| host | 主机名。 |
| id | 查询ID。 |
| instance\_id | 实例ID。 |
| internet\_ip | 互联网IP地址。 |
| ip\_ttl | IP地址的周期。 |
| query\_name | 查询域名。 |
| query\_type | 查询类型。 |
| src\_ip | 源IP地址。 |
| src\_port | 源端口。 |
| start\_time | 查询时间戳，单位：秒。 |
| time\_usecond | 响应耗时，单位：微秒。 |
| tunnel\_id | 通道ID。 |

- 网络会话日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-log-session。 |
| owner\_id | 阿里云账号ID。 |
| asset\_type | 关联的资产类型，例如ECS、SLB、RDS等。 |
| net\_connect\_dir | 网络连接方向。 |
| dst\_ip | 目标IP地址。 |
| dst\_port | 目标端口。 |
| l4\_proto | 协议类型，例如TCP、UDP。 |
| session\_time | Session时间。 |
| src\_ip | 源IP地址。 |
| src\_port | 源端口。 |
| start\_time | 开始时间戳，单位秒。 |

- Web日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-log-http。 |
| owner\_id | 阿里云账号ID。 |
| response\_content\_length | 内容长度。 |
| dst\_ip | 目标IP地址。 |
| dst\_port | 目标端口。 |
| host | 访问主机名。 |
| jump\_location | 重定向地址。 |
| request\_method | HTTP访问。 |
| request\_datetime | 请求时间。 |
| status | 返回状态值。 |
| content\_type | 请求内容类型。 |
| response\_content\_type | 响应内容类型。 |
| src\_ip | 源IP地址。 |
| src\_port | 源端口。 |
| request\_uri | 请求URI。 |
| http\_user\_agent | 向客户端发起的请求。 |
| http\_x\_forward\_for | 路由跳转信息。 |


## 安全日志

- 漏洞日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-vul-log。 |
| owner\_id | 阿里云账号ID。 |
| vul\_name | 漏洞名称。 |
| vul\_alias\_name | 漏洞别名。 |
| risk\_level | 风险等级。 |
| vul\_primary\_id | 漏洞标识符。 |
| instance\_name | 机器名称。 |
| operation | 操作信息，包括： <br>  - new：新增<br>    <br>  - verify：验证<br>    <br>  - fix：修复 |
| status | 状态。更多信息，请参见 [安全日志状态码](https://help.aliyun.com/zh/sls/security-center#table-zcd-26q-vi1 "")。 |
| tag | 漏洞标签，例如oval、system、cms，主要用于区分EMG紧急漏洞。 |
| type | 漏洞类型，包括：<br>  - sys：windows漏洞<br>    <br>  - cve：Linux漏洞<br>    <br>  - cms：Web CMS漏洞<br>    <br>  - emg：紧急漏洞 |
| uuid | 客户端号。 |
| extend\_content | 漏洞扩展信息。 |
| instance\_id | 实例ID。 |
| internet\_ip | 资产的公网IP。 |
| intranet\_ip | 资产的私网IP。 |
| start\_time | 开始时间戳，单位秒。 |

- 基线日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-hc-log。 |
| owner\_id | 阿里云账号ID。 |
| risk\_level | 风险级别。 |
| operation | 操作信息，包括：<br>  - new：新增<br>    <br>  - verify：验证 |
| risk\_name | 风险名称。 |
| status | 状态。更多信息，请参见 [安全日志状态码](https://help.aliyun.com/zh/sls/security-center#table-zcd-26q-vi1 "")。 |
| sub\_type\_alias\_name | 子类型别名，中文。 |
| sub\_type\_name | 子类型名称。 |
| type\_name | 类型名称。更多信息，请参见 [基线type-sub-type列表](https://help.aliyun.com/zh/sls/security-center#table-pd5-rqj-a8d "")。 |
| type\_alias\_name | 类型别名，中文。 |
| uuid | 客户端号。 |
| check\_item\_name | 检查项名称。 |
| check\_item\_level | 检查项级别。 |
| check\_type | 检查项类型。 |
| instance\_id | 示例ID。 |
| start\_time | 开始时间戳，单位秒。 |




表 1\. 基线type-sub-type列表



|     |     |
| --- | --- |
| **type\_name** | **sub\_type\_name** |
| system | baseline |
| weak\_password | postsql\_weak\_password |
| database | redis\_check |
| account | system\_account\_security |
| account | system\_account\_security |
| weak\_password | mysq\_weak\_password |
| weak\_password | ftp\_anonymous |
| weak\_password | rdp\_weak\_password |
| system | group\_policy |
| system | register |
| account | system\_account\_security |
| weak\_password | sqlserver\_weak\_password |
| system | register |
| weak\_password | ssh\_weak\_password |
| weak\_password | ftp\_weak\_password |
| cis | centos7 |
| cis | tomcat7 |
| cis | memcached-check |
| cis | mongodb-check |
| cis | ubuntu14 |
| cis | win2008\_r2 |
| system | file\_integrity\_mon |
| cis | linux-httpd-2.2-cis |
| cis | linux-docker-1.6-cis |
| cis | SUSE11 |
| cis | redhat6 |
| cis | bind9.9 |
| cis | centos6 |
| cis | debain8 |
| cis | redhat7 |
| cis | SUSE12 |
| cis | ubuntu16 |



表 2\. 安全日志状态码



|     |     |
| --- | --- |
| **状态值** | **说明** |
| 1 | 未修复 |
| 2 | 修复失败 |
| 3 | 回滚失败 |
| 4 | 修复中 |
| 5 | 回滚中 |
| 6 | 验证中 |
| 7 | 修复成功 |
| 8 | 修复成功待重启 |
| 9 | 回滚成功 |
| 10 | 忽略 |
| 11 | 回滚成功待重启 |
| 12 | 已不存在 |
| 20 | 已失效 |

- 安全告警日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为sas-security-log。 |
| data\_source | 数据源。更多信息，请参见 [安全告警data\_source列表](https://help.aliyun.com/zh/sls/security-center#table-iwf-4vy-jpn "")。 |
| level | 告警级别。 |
| name | 名称。 |
| operation | 操作信息，包括：<br>  - new：新增<br>    <br>  - dealing：处理 |
| status | 状态。更多信息，请参见 [安全日志状态码](https://help.aliyun.com/zh/sls/security-center#table-zcd-26q-vi1 "")。 |
| uuid | 客户端号。 |
| detail | 告警详情。 |
| unique\_info | 告警的唯一标识。 |
| instance\_id | 示例ID。 |
| internet\_ip | 资产的公网IP。 |
| intranet\_ip | 资产的私网IP。 |
| start\_time | 开始时间戳，单位秒。 |




表 3\. 安全告警data\_source列表



|     |     |
| --- | --- |
| **值** | **描述** |
| aegis\_suspicious\_event | 主机异常。 |
| aegis\_suspicious\_file\_v2 | Webshell。 |
| aegis\_login\_log | 异常登录。 |
| security\_event | 安全中心异常事件。 |

- 云平台配置检查日志




| 日志字段 | 说明 |
| --- | --- |



|     |     |
| --- | --- |
| 日志字段 | 说明 |
| \_\_topic\_\_ | 日志主题，固定为sas-cspm-log。 |
| check\_id | 检查项ID。您可以调用 [ListCheckResult - 查看云产品中云平台配置检查风险项结果详情](https://help.aliyun.com/zh/security-center/developer-reference/api-sas-2018-12-03-listcheckresult#main-107864 "") 接口获取ID值。 |
| check\_item\_name | 检查项名称。 |
| instance\_id | 实例ID。 |
| instance\_name | 实例名称。 |
| instance\_result | 风险产生的影响。格式为JSON字符串。 |
| instance\_sub\_type | 实例的子类型。取值：<br>  - 当实例类型为ECS时，子类型的取值：<br>    <br>    - INSTANCE。<br>      <br>    - DISK。<br>      <br>    - SECURITY\_GROUP。<br>  - 当实例类型为ACR时，子类型的取值：<br>    <br>    - REPOSITORY\_ENTERPRISE。<br>      <br>    - REPOSITORY\_PERSON。<br>  - 当实例类型为RAM时，子类型的取值：<br>    <br>    - ALIAS。<br>      <br>    - USER。<br>      <br>    - POLICY。<br>      <br>    - GROUP。<br>  - 当实例类型为WAF时，子类型的取值为DOMAIN。<br>    <br>  - 当实例类型为其他值时，子类型的取值为INSTANCE。 |
| instance\_type | 实例类型。取值：<br>  - ECS：云服务器。<br>    <br>  - SLB：负载均衡。<br>    <br>  - RDS：RDS数据库。<br>    <br>  - MONGODB：MongoDB数据库。<br>    <br>  - KVSTORE：Redis数据库。<br>    <br>  - ACR：容器镜像服务。<br>    <br>  - CSK：CSK。<br>    <br>  - VPC：专有网络。<br>    <br>  - ACTIONTRAIL：操作审计。<br>    <br>  - CDN：内容分发网络。<br>    <br>  - CAS：数字证书管理服务（原SSL证书）。<br>    <br>  - RDC：云效。<br>    <br>  - RAM：访问控制。<br>    <br>  - DDoS：DDoS防护。<br>    <br>  - WAF：Web应用防火墙。<br>    <br>  - OSS：对象存储。<br>    <br>  - POLARDB：PolarDB数据库。<br>    <br>  - POSTGRESQL：PostgreSQL数据库。<br>    <br>  - MSE：微服务引擎。<br>    <br>  - NAS：文件存储。<br>    <br>  - SDDP：敏感数据保护。<br>    <br>  - EIP：弹性公网IP。 |
| region\_id | 实例所在地域ID。 |
| requirement\_id | 条例ID。您可以通过 [ListCheckStandard - 云平台配置检查获取标准列表](https://help.aliyun.com/zh/security-center/developer-reference/api-sas-2018-12-03-listcheckstandard#main-107864 "") 接口获取该ID。 |
| risk\_level | 风险级别。取值：<br>  - LOW。<br>    <br>  - MEDIUM。<br>    <br>  - HIGH。 |
| section\_id | 章节ID。您可以通过 [ListCheckResult - 查看云产品中云平台配置检查风险项结果详情](https://help.aliyun.com/zh/security-center/developer-reference/api-sas-2018-12-03-listcheckresult#main-107864 "") 接口获取ID值。 |
| standard\_id | 标准ID。您可以通过 [ListCheckStandard - 云平台配置检查获取标准列表](https://help.aliyun.com/zh/security-center/developer-reference/api-sas-2018-12-03-listcheckstandard#main-107864 "") 接口获取该ID。 |
| status | 检查项的状态。取值：<br>  - NOT\_CHECK：未检查。<br>    <br>  - CHECKING：检查中。<br>    <br>  - PASS：检查通过。<br>    <br>  - NOT\_PASS：检查未通过。<br>    <br>  - WHITELIST：已加入白名单。 |
| vendor | 所属云厂商。固定取值：ALIYUN。 |
| start\_time | 开始时间戳，单位秒。 |

- 网络防御日志




| 日志字段 | 说明 |
| --- | --- |



|     |     |
| --- | --- |
| 日志字段 | 说明 |
| \_\_topic\_\_ | 日志主题，固定为sas-net-block。 |
| cmd | 被攻击的进程命令行。 |
| cur\_time | 攻击事件的发生时间。 |
| decode\_payload | HEX格式转换为字符的payload。 |
| dst\_ip | 被攻击资产的IP地址。 |
| dst\_port | 被攻击资产的端口。 |
| func | 拦截事件的类型。取值：<br>  - payload：恶意负载类型，表示由于检测到恶意数据或指令而触发的攻击事件拦截。<br>    <br>  - tuple：恶意IP类型，表示由于检测到恶意IP访问而触发的攻击事件拦截。 |
| rule\_type | 拦截事件下的具体规则类型。取值：<br>  - alinet\_payload：云安全中心指定的payload事件防御规则。<br>    <br>  - alinet\_tuple：云安全中心指定的tuple事件防御规则。 |
| instance\_id | 被攻击资产的实例ID。 |
| internet\_ip | 被攻击资产的公网IP。 |
| intranet\_ip | 被攻击资产的私网IP。 |
| final\_action | 防御动作模式。取值：block（已拦截）。 |
| payload | HEX格式的payload。 |
| pid | 被攻击的进程ID。 |
| platform | 被攻击资产的系统类型。取值：<br>  - win。<br>    <br>  - linux。 |
| proc\_path | 被攻击的进程路径。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |
| src\_ip | 发起攻击的源IP地址。 |
| src\_port | 发起攻击的源端口。 |
| uuid | 服务器的UUID。 |
| owner\_id | 阿里云账号ID。 |
| start\_time | 开始时间戳，单位秒。 |

- 应用防护日志




| 日志字段 | 说明 |
| --- | --- |



|     |     |
| --- | --- |
| 日志字段 | 说明 |
| \_\_topic\_\_ | 日志主题，固定为sas-rasp-log。 |
| app\_dir | 应用所在目录。 |
| app\_id | 应用ID。 |
| app\_name | 应用名称。 |
| confidence\_level | 检测算法的置信度。取值：<br>  - high。<br>    <br>  - medium。<br>    <br>  - low。 |
| request\_body | 请求体信息。 |
| request\_content\_length | 请求体长度。 |
| data | hook点参数。 |
| headers | 请求头信息。 |
| hostname | 主机或网络设备的名称。 |
| host\_ip | 主机私网IP地址。 |
| is\_clipped | 该条日志是否因为超长被裁剪过。取值：<br>  - true：裁剪过。<br>    <br>  - false：未裁剪过。 |
| jdk\_version | JDK版本。 |
| message | 告警描述信息。 |
| request\_method | 请求方法。 |
| platform | 操作系统类型。 |
| arch | 操作系统架构。 |
| kernel\_version | 操作系统内核版本。 |
| param | 请求参数，常见格式包括：<br>  - GET参数。<br>    <br>  - application/x-www-form-urlencoded。 |
| payload | 有效攻击载荷。 |
| payload\_length | 有效攻击载荷长度。 |
| rasp\_id | 应用防护探针唯一ID。 |
| rasp\_version | 应用防护探针版本。 |
| src\_ip | 请求者IP地址。 |
| final\_action | 告警处理结果。取值：<br>  - block：防护，即阻断。<br>    <br>  - monitor：监控。 |
| rule\_action | 规则指定的告警处理方式。取值：<br>  - block。<br>    <br>  - monitor。 |
| risk\_level | 风险级别。取值：<br>  - high。<br>    <br>  - medium。<br>    <br>  - low。 |
| stacktrace | 堆栈信息。 |
| time | 触发告警的时间。 |
| timestamp | 触发告警的时间戳，单位为毫秒。 |
| type | 漏洞类型。取值：<br>  - attach：恶意Attach。<br>    <br>  - beans：恶意beans绑定。<br>    <br>  - classloader：恶意类加载。<br>    <br>  - dangerous\_protocol：危险协议使用。<br>    <br>  - dns：恶意DNS查询。<br>    <br>  - engine：引擎注入。<br>    <br>  - expression：表达式注入。<br>    <br>  - file：恶意文件读写。<br>    <br>  - file\_delete：任意文件删除。<br>    <br>  - file\_list：目录遍历。<br>    <br>  - file\_read：任意文件读取。<br>    <br>  - file\_upload：恶意文件上传。<br>    <br>  - jndi：JNDI注入。<br>    <br>  - jni：JNI注入。<br>    <br>  - jstl：JSTL任意文件包含。<br>    <br>  - memory\_shell：内存马注入。<br>    <br>  - rce：命令执行。<br>    <br>  - read\_object：反序列化攻击。<br>    <br>  - reflect：恶意反射调用。<br>    <br>  - sql：SQL注入。<br>    <br>  - ssrf：恶意外连。<br>    <br>  - thread\_inject：线程注入。<br>    <br>  - xxe：XXE攻击。 |
| url | 请求URL。 |
| rasp\_attack\_uuid | 漏洞UUID。 |
| uuid | 主机UUID。 |
| internet\_ip | 主机公网IP地址。 |
| intranet\_ip | 主机私网IP地址。 |
| sas\_group\_name | 云安全中心服务器分组名称。 |
| instance\_id | 主机实例ID。 |
| owner\_id | 阿里云账号ID。 |
| start\_time | 开始时间戳，单位秒。 |

- 文件检测日志




| 字段名 | 说明 |
| --- | --- |



|     |     |
| --- | --- |
| 字段名 | 说明 |
| \_\_topic\_\_ | 日志主题，固定为sas-filedetect-log。 |
| bucket\_name | Bucket名称。 |
| event\_id | 告警ID。 |
| event\_name | 告警名称。 |
| md5 | 文件的MD5值。 |
| sha256 | 文件的SHA256值。 |
| result | 检测结果。<br>  - 0：文件安全。<br>    <br>  - 1：存在恶意文件。 |
| file\_path | 文件路径。 |
| etag | OSS文件标识。 |
| risk\_level | 风险等级。<br>  - serious：紧急。<br>    <br>  - suspicions：可疑。<br>    <br>  - remind：提醒。 |
| source | 检测场景。<br>  - OSS：在云安全中心控制台执行对阿里云对象存储Bucket内文件的检测。<br>    <br>  - API：通过SDK接入的方式检测恶意文件，支持通过Java或Python接入。 |
| parent\_md5 | 父类文件或压缩包文件的MD5值。 |
| parent\_sha256 | 父类文件或压缩包文件的SHA256值。 |
| parent\_file\_path | 父类文件或压缩包文件的名称。 |
| owner\_id | 阿里云账号ID。 |
| start\_time | 开始检测时间的时间戳。单位为秒。 |


## 主机日志

- 进程启动日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-process。 |
| uuid | 客户端号。 |
| host\_ip | 客户端主机的IP地址。 |
| cmdline | 用户启动完整命令行。 |
| username | 用户名。 |
| uid | 用户ID。 |
| pid | 进程ID。 |
| proc\_name | 进程文件名。 |
| proc\_path | 进程文件完整路径。 |
| proc\_start\_time | 进程的启动时间。 |
| parent\_proc\_start\_time | 父进程的启动时间。 |
| groupname | 用户组。 |
| ppid | 父进程ID。 |
| parent\_proc\_name | 父进程文件名。 |
| parent\_proc\_path | 父进程文件完整路径。 |
| cmd\_chain | 进程链。 |
| container\_hostname | 容器主机名。 |
| container\_pid | 容器PID。 |
| container\_image\_id | 镜像ID。 |
| container\_image\_name | 镜像名称。 |
| container\_name | 容器名称。 |
| container\_id | 容器ID。 |
| cwd | 进程运行目录。 |
| owner\_id | 阿里云账号ID。 |
| start\_time | 开始时间戳，单位秒。 |
| cmd\_chain\_index | 进程链索引，可以通过相同索引查找进程链。 |
| cmd\_index | 命令行每个参数的索引，每两个为一组，标识一个参数的起止索引。 |
| comm | 进程关联的命令名。 |
| gid | 进程组的ID。 |
| instance\_id | 实例ID。 |
| parent\_cmd\_line | 父进程的命令行。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |
| srv\_cmd | 祖进程的命令行。 |
| tty | 登录的终端。 **N/A** 表示账号从未登录过终端。 |
| uid | 用户ID。 |
| start\_time | 开始时间戳，单位秒。 |

- 进程快照日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-snapshot-process。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端主机的IP地址。 |
| cmdline | 用户启动完整命令行。 |
| pid | 进程ID。 |
| proc\_name | 进程文件名。 |
| proc\_path | 进程文件完整路径。 |
| md5 | 进程文件进行MD5计算，超过1 MB的进程文件不进行计算。 |
| parent\_proc\_name | 父进程文件名。 |
| proc\_start\_time | 进程启动时间，内置字段。 |
| user | 用户名。 |
| uid | 用户ID。 |
| start\_time | 开始时间戳，单位秒。 |
| instance\_id | 实例ID。 |
| pname | 父进程文件名。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |

- 登录日志



1分钟内重复登录会被合并为1条日志。






| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-login。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端主机的IP地址。 |
| src\_ip | 登录来源IP地址。 |
| dst\_port | 登录端口。 |
| login\_type | 登录类型，例如SSHLOGIN、RDPLOGIN、IPCLOGIN。 |
| username | 登录用户名。 |
| login\_count | 登录次数，例如3次表示这次登录前1分钟内还发送了2次。 |
| instance\_id | 实例ID。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |
| start\_time | 开始时间戳戳，单位秒。 |

- 暴力破解日志




| **字段名** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **字段名** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-crack。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端主机的IP地址。 |
| src\_ip | 登录来源IP地址。 |
| dst\_port | 登录端口。 |
| login\_type | 登录类型，例如SSHLOGIN、RDPLOGIN、IPCLOGIN。 |
| username | 登录用户名。 |
| login\_count | 失败登录次数。 |
| instance\_id | 实例ID。 |
| sas\_group\_name | 服务器在云安全中心的资产分组 。 |
| start\_time | 开始时间戳，单位秒。 |

- 主机网络连接日志



主机上每隔10秒到1分钟会收集变化的网络连接。






| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-network。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端主机的IP地址。 |
| src\_ip | 源IP地址。 |
| src\_port | 源端口。 |
| dst\_ip | 目标IP地址。 |
| threat\_dst\_ip | 目标IP地址的威胁情报。更多信息，请参见 [威胁情报字段](https://help.aliyun.com/zh/sls/generate-threat-intelligence#section-ghm-rcz-m63 "")。 |
| dst\_port | 目标端口。 |
| proc\_name | 进程名。 |
| proc\_path | 进程路径。 |
| connection\_type | 连接协议。 |
| status | 连接状态。更多信息，请参见 [网络连接状态描述列表](https://help.aliyun.com/zh/sls/security-center#table-e3e-l2j-flw "")。 |
| net\_connect\_dir | 网络连接方向。 |
| parent\_proc\_name | 父进程可执行文件名。 |
| cmd\_chain | 进程链。 |
| cmd\_chain\_index | 进程链索引，可以通过相同索引查找进程链。 |
| container\_hostname | 容器内服务器名称。 |
| container\_id | 容器ID。 |
| container\_image\_id | 镜像ID。 |
| container\_image\_name | 镜像名称。 |
| container\_name | 容器名称。 |
| container\_pid | 容器内进程ID。 |
| instance\_id | 实例ID。 |
| pid | 进程ID。 |
| ppid | 父进程ID。 |
| proc\_start\_time | 进程的启动时间。 |
| src\_ip | 源IP地址。 |
| src\_port | 源端口。 |
| srv\_comm | 父进程的父进程关联的命令名。 |
| type | 实时网络连接的类型。取值如下：<br>  - **connect**：主动发起TCP connect连接。<br>    <br>  - **accept**：收到TCP连接。<br>    <br>  - **listen**：端口监听。 |
| uid | 进程用户的ID。 |
| username | 进程的用户名。 |
| start\_time | 开始时间戳，单位秒。 |





表 4\. 网络连接状态描述列表



|     |     |
| --- | --- |
| **状态值** | **描述** |
| 1 | closed |
| 2 | listen |
| 3 | syn send |
| 4 | syn recv |
| 5 | establisted |
| 6 | close wait |
| 7 | closing |
| 8 | fin\_wait1 |
| 9 | fin\_wait2 |
| 10 | time\_wait |
| 11 | delete\_tcb |

- 端口监听快照




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-snapshot-port。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端IP地址。 |
| connection\_type | 监听协议。 |
| src\_ip | 监听IP地址。 |
| src\_port | 监听端口。 |
| pid | 进程ID。 |
| proc\_name | 进程名。 |
| net\_connect\_dir | 网络连接方向。 |
| dst\_ip | 网络连接接收者的IP。<br>  - **dir** 为 **out** 时，表示对端主机。<br>    <br>  - **dir** 为 **in** 时，表示本机。 |
| dst\_port | 网络连接接收者的端口。 |
| instance\_id | 实例ID。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |
| status | 网络连接状态。取值：<br>  - **1**：连接已关闭（closed）。<br>    <br>  - **2**：正在等待连接请求（listen）。<br>    <br>  - **3**：已发送SYN请求（syn send）。<br>    <br>  - **4**：已接收SYN请求（syn recv）。<br>    <br>  - **5**：连接已建立（established）。<br>    <br>  - **6**：等待关闭连接（close wait）。<br>    <br>  - **7**：正在关闭连接（closing）。<br>    <br>  - **8**：等待对方发送关闭请求（fin\_wait1）。<br>    <br>  - **9**：等待对方发送关闭请求并确认（fin\_wait2）。<br>    <br>  - **10**：等待足够的时间以确保对方收到关闭请求的确认（time\_wait）。<br>    <br>  - **11**：已删除传输控制块（delete\_tcb）。 |
| start\_time | 开始时间戳，单位秒。 |

- 账户快照




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-snapshot-host。 |
| owner\_id | 阿里云账号ID。 |
| name | 漏洞名称。 |
| alias\_name | 漏洞别名。 |
| op | 操作信息，包括：<br>  - new：新增<br>    <br>  - verify：验证<br>    <br>  - fix：修复 |
| status | 连接状态。更多信息，请参见 [网络连接状态描述列表](https://help.aliyun.com/zh/sls/security-center#table-e3e-l2j-flw "")。 |
| tag | 漏洞标签，例如oval、system、cms等，主要用于区分EMG紧急漏洞。 |
| type | 漏洞类型，包括：<br>  - sys：windows漏洞<br>    <br>  - cve：Linux漏洞<br>    <br>  - cms：Web CMS漏洞<br>    <br>  - EMG：紧急漏洞 |
| uuid | 客户端号。 |
| username | 登录用户名。 |
| host\_ip | 服务器IP地址。 |
| account\_expire | 账号的过期时间。 **never** 表示永不过期。 |
| domain | 账号所在的域或目录服务。 **N/A** 表示不属于任何域。 |
| groups | 账号所在的分组。 **N/A** 表示不属于任何组。 |
| home\_dir | 主目录，是系统中存储和管理文件的默认位置。 |
| instance\_id | 实例ID。 |
| last\_chg | 最后一次修改密码的日期。 |
| last\_logon | 最后一次登录账号的日期和时间。 **N/A** 表示从未登录过。 |
| login\_ip | 最后一次登录账号的远程IP地址。 **N/A** 表示从未登录过。 |
| passwd\_expire | 密码的过期日期。 **never** 表示永不过期。 |
| perm | 是否拥有root权限。取值：<br>  - **0**：没有root权限。<br>    <br>  - **1**：有root权限。 |
| sas\_group\_name | 服务器在云安全中心的资产分组。 |
| shell | Linux的Shell命令。 |
| tty | 登录的终端。 **N/A** 表示从未登录过终端。 |
| warn\_time | 密码到期提醒日期。 **never** 表示永不提醒。 |
| start\_time | 开始时间戳，单位秒。 |

- DNS请求日志




| **日志字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-dns-query。 |
| owner\_id | 阿里云账号ID。 |
| uuid | 客户端号。 |
| host\_ip | 客户端机器IP地址。 |
| pid | DNS请求发起者进程ID。 |
| ppid | DNS请求发起者的父进程ID。 |
| time | DNS请求发生时间。 |
| domain | DNS请求对应域名。 |
| proc\_path | DNS请求发起进程路径。 |
| cmdline | DNS请求发起进程命令行。 |
| cmd\_chain | DNS请求发起者进程链。 |
| sas\_group\_name | 云安全中心分组名称。 |
| instance\_id | 实例ID。 |
| start\_time | 开始时间戳，单位秒。 |

- 客户端事件日志




| 字段名 | 说明 |
| --- | --- |



|     |     |
| --- | --- |
| 字段名 | 说明 |
| \_\_topic\_\_ | 日志主题，固定为aegis-log-client。 |
| uuid | 服务器的UUID。 |
| host\_ip | 服务器IP地址。 |
| agent\_version | 客户端版本。 |
| last\_login | 上次登录的时间戳。单位：毫秒。 |
| platform | 操作系统类型。取值：<br>  - windows<br>    <br>  - linux |
| region\_id | 服务器所在地域ID。 |
| status | 客户端状态。取值：<br>  - online<br>    <br>  - offline |
| owner\_id | 阿里云账号ID。 |
| start\_time | 开始时间戳，单位秒。 |