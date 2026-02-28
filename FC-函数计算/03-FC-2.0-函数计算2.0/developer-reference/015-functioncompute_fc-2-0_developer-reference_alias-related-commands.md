### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[开发者工具](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/developer-tools/)[Serverless Devs](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/serverless-devs/)[使用Serverless Devs创建函数相关资源](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/fc-api/)别名相关命令

# 别名相关命令

更新时间：2025-08-04 04:54:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：版本相关命令](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/version-related-commands)[下一篇：自定义域名相关命令](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/custom-domain-name-related-commands)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

创建别名

删除别名

更新别名

获取别名配置信息

获取别名列表

FC组件是一款基于Serverless Devs的阿里云函数计算操作工具，通过该工具，您可以直接通过交互式命令使用函数计算服务别名相关的API。

## 前提条件

您已完成以下操作：

- [安装Serverless Devs工具及依赖](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/install-serverless-devs-and-docker#task-2093092 "")

- [配置Serverless Devs](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/configure-serverless-devs#task-2093369 "")

- [创建服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/service-related-commands#section-fz6-8jk-90k "")

- [创建版本](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/version-related-commands#section-3u1-sxu-jbc "")


## 创建别名

命令格式：

```plaintext
sudo s cli fc api CreateAlias --region <regionid> --access <accessname> --apiVersion <20210406 or 20160815> --path '{"serviceName": "serviceName"}' --body '{"additionalVersionWeight": "additionalVersionWeight","aliasName": "aliasname","description": "description","versionId": "versionid"}'
```

参数说明：

- （必选）--region string：指定部署资源的地域。

- （可选）--access string或-a string：指定使用的密钥别名。

- （可选）--apiVersion：指定API版本。取值包括20210406和20160815。

- path


  - （必选）--serviceName string：指定服务名称。


- body


    - --aliasName string：指定别名名称。

  - （可选）--versionId string：指定别名指向的版本。

  - （可选）--additionalVersionWeight string：设置别名指向的灰度版本和灰度权重。

  - （可选）--description string：指定别名的描述信息。


执行示例：

```plaintext
sudo s cli fc api CreateAlias --region cn-hangzhou --access default --path '{"serviceName": "mytest"}' --body '{"aliasName": "aliastest","versionId": "1"}'
```

关于创建别名的API接口的详细信息，请参见 [CreateAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createalias#doc-api-FC-CreateAlias "")。

## 删除别名

命令格式：

```plaintext
sudo s cli fc api DeleteAlias --region <regionid> --access <accessname> --apiVersion <20210406 or 20160815> --path '{"serviceName": "serviceName","aliasName": "ailasName"}'
```

参数说明：

- （必选）--region string：指定部署资源的地域。

- （可选）--access string或-a string：指定使用的密钥别名。

- （可选）--apiVersion：指定API版本。取值包括20210406和20160815。

- path


  - （必选）--serviceName string：指定服务名称。

  - （必选）--aliasName string：指定别名名称。


执行示例：

```plaintext
sudo s cli fc api DeleteAlias --region cn-hangzhou --access default --path '{"serviceName": "mytest","aliasName": "aliastest"}'
```

关于删除别名的API接口的详细信息，请参见 [DeleteAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-deletealias#doc-api-FC-DeleteAlias "")。

## 更新别名

命令格式：

```plaintext
sudo s cli fc api UpdateAlias --region <regionid> --access <accessname> --apiVersion <20210406 or 20160815> --path '{"serviceName": "serviceName","aliasName": "ailasName"}' --body '{"additionalVersionWeight": "additionalVersionWeight","description": "description","versionId": "versionid"}'
```

参数说明：

- （必选）--region string：指定部署资源的地域。

- （可选）--access string或-a string：指定使用的密钥别名。

- （可选）--apiVersion：指定API版本。取值包括20210406和20160815。

- path

- - （必选）--serviceName string：指定服务名称。

  - （必选）--aliasName string：指定别名名称。


- body


  - （可选）--versionId string：指定别名指向的版本。

  - （可选）--additionalVersionWeight string：设置别名指向的灰度版本和灰度权重。

  - （可选）--description string：指定别名的描述信息。


执行示例：

```plaintext
sudo s cli fc api UpdateAlias --region cn-hangzhou --access default --path '{"serviceName": "mytest","aliasName": "aliastest"}' --body '{"additionalVersionWeight": {"2":0.05}}'
```

关于更新别名的API接口的详细信息，请参见 [UpdateAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatealias#doc-api-FC-UpdateAlias "")。

## 获取别名配置信息

命令格式：

```plaintext
sudo s cli fc api GetAlias --region <regionid> --access <accessname> --apiVersion <20210406 or 20160815> --path '{"serviceName": "serviceName","aliasName": "ailasName"}'
```

参数说明：

- （必选）--region string：指定部署资源的地域。

- （可选）--access string或-a string：指定使用的密钥别名。

- （可选）--apiVersion：指定API版本。取值包括20210406和20160815。

- path


  - （必选）--serviceName string：指定服务名称。

  - （必选）--aliasName string：指定别名名称。


执行示例：

```plaintext
sudo s cli fc api GetAlias --region cn-hangzhou --access default --path '{"serviceName": "mytest","aliasName": "aliastest"}'
```

关于获取别名配置信息的API接口的详细信息，请参见 [GetAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getalias#doc-api-FC-GetAlias "")。

## 获取别名列表

命令格式：

```plaintext
sudo s cli fc api ListAliases --region <regionid> --access <accessname> --apiVersion <20210406 or 20160815> --path '{"serviceName": "serviceName"}' --query '{"limit": "limit","nextToken": "nextToken","prefix": "prefix","startKey": "startKey"}'
```

参数说明：

- （必选）--region string：指定部署资源的地域。

- （可选）--access string或-a string：指定使用的密钥别名。

- （可选）--apiVersion：指定API版本。取值包括20210406和20160815。

- path


  - （必选）--serviceName string：指定服务名称。


- query


  - （可选）--limit string：设置限定此次返回资源的数量。

  - （可选）--nextToken string：设置用来返回更多结果的令牌。第一次查询时不需要提供这个参数，后续查询的Token从返回结果中获取。

  - （可选）--prefix string：设置返回资源的名称前缀。

  - （可选）--startKey string：设定结果从startKey之后（包括startKey）按字母排序的第一个开始返回。


执行示例：

```plaintext
sudo s cli fc api ListAliases --region cn-hangzhou --access default --path '{"serviceName": "mytest"}' --query '{"limit": "3"}'
```

关于获取别名列表的API接口的详细信息，请参见 [ListAliases](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-listaliases#doc-api-FC-ListAliases "")。