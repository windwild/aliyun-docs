### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)worm（合规保留策略）

# worm（合规保留策略）

更新时间：2025-04-09 01:07:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：website（静态网站托管及回源配置）](https://help.aliyun.com/zh/oss/developer-reference/website)[下一篇：查看选项](https://help.aliyun.com/zh/oss/developer-reference/view-options)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

创建并锁定合规保留策略

延长保留周期

查询合规保留策略配置

删除合规保留策略

通用选项

OSS保留策略具有WORM（Write Once Read Many）特性，满足用户以不可删除、不可篡改的方式保存和使用数据。如果您希望指定时间内任何用户（包括资源拥有者）均不能修改和删除OSS某个Bucket中的Object，您需要通过`worm`命令为Bucket配置保留策略。在保留策略指定的Object保留时间到期之前，仅支持在Bucket中上传和读取Object。Object保留时间到期后，才可以修改或删除Object。

## **注意事项**

- 要创建合规保留策略，您必须具有`oss:InitiateBucketWorm`权限；要锁定合规保留策略，您必须具有`oss:CompleteBucketWorm`权限；要延长保留天数，您必须具有`oss:ExtendBucketWorm`权限；要获取合规保留策略，您必须具有`oss:GetBucketWorm`权限；要删除未锁定的合规保留策略，您必须具有`oss:AbortBucketWorm`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。

- 关于合规保留策略的更多信息，请参见 [合规保留策略](https://help.aliyun.com/zh/oss/user-guide/oss-retention-policies#concept-lnj-4rl-cfb "")。


## 创建并锁定合规保留策略

若您希望使用合规保留策略保护您Bucket中的文件，您需要为Bucket创建一条合规保留策略，然后锁定该策略。

1. 创建合规保留策略

   - 命令格式















     ```shell
     ossutil worm init oss://BucketName days
     ```



     参数说明：




     | **参数** | **说明** |
     | --- | --- |



     |     |     |
     | --- | --- |
     | **参数** | **说明** |
     | BucketName | 配置合规保留策略的目标Bucket名称。 |
     | days | 指定合规保留策略的保留周期。在保留周期内，您无法对目标Bucket中的Object进行任何修改和删除操作。<br>     - 单位：天<br>       <br>     - 取值范围：1~25550 |

   - 使用示例



     为examplebucket创建合规保留策略，并指定其保留周期为180天。

















     ```shell
     ossutil worm init oss://examplebucket 180
     ```





     以下输出结果表明已成功创建合规保留策略。

















     ```shell
     init success,worm id is 581D8A7FFA064C80827CAB4076A93A78
     ```
2. 锁定合规保留策略

   - 命令格式















     ```shell
     ossutil worm complete oss://BucketName WormId
     ```





     参数说明：






     | **参数** | **说明** |
     | --- | --- |



     |     |     |
     | --- | --- |
     | **参数** | **说明** |
     | BucketName | 指定要锁定合规保留策略的目标Bucket名称。 |
     | WormId | 填写创建合规保留策略时返回的策略ID。 |

   - 使用示例



     锁定examplebucket的合规保留策略。

















     ```shell
     ossutil worm complete oss://examplebucket 581D8A7FFA064C80827CAB4076A93A78
     ```





     以下输出结果表明已锁定合规保留策略。

















     ```shell
     0.073810(s) elapsed
     ```

## 延长保留周期

合规保留策略锁定后，在保留周期未到期之前，任何人都无法修改和删除Bucket中的Object。若当前的保留周期无法满足数据保护的需求，您可以通过以下命令延长保留周期。

- 命令格式















```shell
ossutil worm extend oss://BucketName days WormId
```

- 使用示例



将examplebucket的合规保留策略的保留周期延长到360天。

















```shell
ossutil worm extend oss://examplebucket 360 581D8A7FFA064C80827CAB4076A93A78
```





以下输出结果表明保留周期已延长到360天。

















```shell
0.067810(s) elapsed
```


## 查询合规保留策略配置

对于已创建的合规保留策略，您可以通过以下命令查询配置参数。

- 命令格式















```shell
ossutil worm get oss://BucketName
```

- 使用示例

查询examplebucket的合规保留策略。















```shell
ossutil worm get oss://examplebucket
```



以下输出结果表明已查询到合规保留策略的配置参数，结果中包含策略ID、状态、保留天数、策略创建时间。















```shell
<WormConfiguration>
        <WormId>581D8A7FFA064C80827CAB4076A93A78</WormId>
        <State>Locked</State>
        <RetentionPeriodInDays>360</RetentionPeriodInDays>
        <CreationDate>2021-01-19T03:36:53.000Z</CreationDate>
    </WormConfiguration>
```


## 删除合规保留策略

在合规保留策略未锁定前，您可以删除该策略。

- 命令格式















```shell
ossutil worm abort oss://BucketName
```

- 使用示例

删除为examplebucket配置的合规保留策略。















```shell
ossutil worm abort oss://examplebucket
```



以下输出结果表明策略已删除。















```shell
0.067810(s) elapsed
```


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如您需要为另一个阿里云账号下，华东1（杭州）名为test的Bucket创建合规保留策略，命令如下：

```shell
ossutil worm init oss://test -e oss-cn-hangzhou.aliyuncs.com -i yourAccessKeyID -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。