### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/) [命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/) [常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/) sign（生成签名URL）

# sign（生成签名URL）

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：set-meta（管理文件元数据）](https://help.aliyun.com/zh/oss/developer-reference/set-meta)[下一篇：stat（查看Bucket和Object信息）](https://help.aliyun.com/zh/oss/developer-reference/stat)

该文章对您有帮助吗？

反馈

默认情况下，OSS存储空间中文件的读写权限是私有，仅文件拥有者具有访问文件的权限。但是，文件拥有者可以通过sign命令创建签名URL的方式与第三方用户分享文件，签名URL使用安全凭证的方式授权第三方用户在指定时间内下载或者预览文件。

**重要**

- 第三方用户通过签名URL可以访问签名URL中指向的Object，与该Object的ACL是公共读或者私有，是否通过Bucket Policy或者RAM Policy授权第三方用户拥有访问指定Object的权限无关。

- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。


## 命令格式

```bash
ossutil sign cloud_url
[--timeout <value>]
[--version-id <value>]
[--trafic-limit <value>]
[--disable-encode-slash]
[--payer <value>]
[--query-param <value>]
```

参数及选项说明如下：

|     |     |
| --- | --- |
| **配置项** | **说明** |
| cloud\_url | 文件所在Bucket的完整路径。 |
| --timeout | 签名URL过期时间，单位为秒。默认值为60。<br>**重要** <br>当前时间戳与签名URL的过期时间之和不能超过9223372036854775807，否则会溢出报错。例如，当前时间戳为1643341269，则签名URL过期时间最大不能超过9223372035211434538。 |
| --version-id | Object的指定版本ID。仅适用于已开启或暂停版本控制状态Bucket下的Object。 |
| --trafic-limit | 限定HTTP的访问速度，单位为bit/s。缺省值为0，表示不受限制。取值范围为819200~838860800，即100 KB/s~100 MB/s。 |
| --disable-encode-slash | 不对cloud\_url中携带的正斜线（/）进行编码。 |
| --payer | 请求的支付方式。如果希望访问指定路径下的资源产生的流量、请求次数等费用由请求者支付，请将此选项的值设置为 `requester`。 |
| --query-param | 设置请求中的查询参数。该参数可以出现多次。例如，您可以将该参数设置为图片处理参数。<br>--query-param支持的参数为：x-oss-process、x-oss-traffic-limit、response-content-language、response-expires、response-cache-control、response-content-disposition、response-content-encoding、x-oss-ac-source-ip、x-oss-ac-subnet-mask、x-oss-ac-vpc-id、x-oss-ac-forward-allow。关于参数含义的更多信息，请参见 [签名版本1](https://help.aliyun.com/zh/oss/developer-reference/ddd-signatures-to-urls#concept-xqh-2df-xdb "") 和 [GetObject](https://help.aliyun.com/zh/oss/developer-reference/getobject#reference-ccf-rgd-5db "")。<br>**说明** <br>仅1.7.15及以上版本支持设置--query-param参数。 |

## 使用示例

- 为目标存储空间examplebucket下的文件exampleobject.png生成文件URL，其默认超时时间为60秒。


```bash
ossutil sign oss://examplebucket/exampleobject.png
```

- 为目标存储空间examplebucket下的文件exampleobject.png生成文件URL，并指定超时时间为3600秒。


```bash
ossutil sign oss://examplebucket/exampleobject.png --timeout 3600
```

- 为目标存储空间examplebucket下的文件exampleobject.png生成文件URL，指定其超时时间为7200秒，并限定其访问速度为100MB/s。


```bash
ossutil sign oss://examplebucket/exampleobject.png --timeout 7200 --trafic-limit 838860800
```

- 为已开启版本控制的存储空间examplebucket下的exampleobject.jpg的指定版本文件生成文件URL，并指定超时时间为1800秒。


```bash
ossutil sign oss://examplebucket/exampleobject.jpg --timeout 1800 --version-id  CAEQARiBgID8rumR2hYiIGUyOTAyZGY2MzU5MjQ5ZjlhYzQzZjNlYTAyZDE3****
```

- 为目标存储空间examplebucket下的文件exampleobject.jpg生成处理后的图片URL，将图片宽高设置为100px，并旋转90度。


```bash
ossutil sign oss://examplebucket/exampleobject.jpg  --query-param x-oss-process:image/resize,m_fixed,w_100,h_100/rotate,90
```

- 为目标存储空间examplebucket下的文件exampleobject.jpg生成处理后的图片URL，将图片宽高设置为100px，并旋转90度，然后限速100 KB/s，即819200 bit/s。


```bash
ossutil sign oss://examplebucket/exampleobject.jpg  --query-param x-oss-process:image/resize,m_fixed,w_100,h_100/rotate,90 --query-param x-oss-traffic-limit:819200
```

- 以上示例操作成功后，返回结果中将包含生成文件URL所用时长、文件URL过期时间以及签名等信息，示例如下：


```bash
https://examplebucket.ss-cn-hangzhou.aliyuncs.com/exampleobject.png?Expires=1608282224&OSSAccessKeyId=LTAI****************&Signature=jo4%****************************
0.368676(s) elapsed
```


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如您需要为另一个阿里云账号下，华东2（上海）地域下存储空间testbucket下的exampletest.jpg文件生成超时时间为3600秒的文件URL，命令如下：

```bash
ossutil sign oss://testbucket/exampletest.jpg --timeout 3600 -e oss-cn-shanghai.aliyuncs.com -i yourAccessKeyID  -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。