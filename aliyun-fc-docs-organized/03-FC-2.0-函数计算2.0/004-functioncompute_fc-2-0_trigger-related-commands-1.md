### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 触发器相关命令

# 触发器相关命令

更新时间：2024-10-17 04:48:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

创建触发器（mkt）

命令

示例

更新触发器（upt）

更多信息

本文介绍fcli中触发器相关的命令。

## 前提条件

在可执行文件所在文件夹下执行`fcli shell`，进入交互模式。

## 创建触发器（mkt）

### **命令**

- `-r string`或`--invocation-role string`：设置触发角色。

- `-s string`或`--source-arn string`：事件源的资源符号，例如acs:oss:cn-shanghai:12345678:myBucketName。

- `-c string`或`--trigger-config string`：设置触发器配置文件。

- `-t string`或`--type string`：触发器类型，默认值为oss。


### **示例**

- 创建OSS触发器















```plaintext
>>> mkt myFunction/myFunctionTrigger -t oss -r acs:ram::12345678:role/AliyunOSSEventNotificationRole -s acs:oss:cn-shanghai:12345678:myOssBucket -c code/ossTrigger.yaml
//其中yaml的文件内容如下triggerConfig。
      events:
        - oss:ObjectCreated:PutObject
        - oss:ObjectRemoved:DeleteObject
    filter:
        key:
            prefix: myPrefix
            suffix: mySuffix
```

- 创建HTTP触发器















```plaintext
>>> mkt myFunction/myFunctionTrigger -t http  -c code/httpTrigger.yaml
//其中yaml的文件内容如下triggerConfig:
    authType: anonymous
    methods:
    - GET
```

## 更新触发器（upt）

- `-r string`或`--invocation-role string`：设置触发角色。

- `-s string`或`--source-arn string`：事件源的资源符号，例如acs:oss:cn-shanghai:12345678:myBucketName。

- `-c string`或`--trigger-config string`：设置触发器配置文件。

- `-t string`或`--type string`：触发器类型，默认值为oss。


```plaintext
>>> upt myFunction/myFunctionTrigger -t oss -r acs:ram::account_id:role/AliyunOSSEventNotificationRole -s acs:oss:cn-region:account_id:bucketName -c code/trigger.yaml
```

## 更多信息

- [列出当前目录下的文件（ls）](https://help.aliyun.com/zh/functioncompute/fc-2-0/common-commands#section-m2t-xkm-gyc "")

- [查看资源的详细信息（info）](https://help.aliyun.com/zh/functioncompute/fc-2-0/common-commands#section-9tp-yjp-gmy "")

- [删除资源（rm）](https://help.aliyun.com/zh/functioncompute/fc-2-0/common-commands#section-bh0-a3h-cc1 "")