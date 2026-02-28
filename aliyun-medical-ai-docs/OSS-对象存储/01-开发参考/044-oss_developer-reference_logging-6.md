### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/) [OSS Ruby SDK](https://help.aliyun.com/zh/oss/developer-reference/ruby/) [存储空间（Ruby SDK）](https://help.aliyun.com/zh/oss/developer-reference/buckets-8/) 日志转存（Ruby SDK）

# 日志转存（Ruby SDK）

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：防盗链（Ruby SDK）](https://help.aliyun.com/zh/oss/developer-reference/ruby-hotlink-protection)[下一篇：跨域资源共享（Ruby SDK）](https://help.aliyun.com/zh/oss/developer-reference/cors-6)

该文章对您有帮助吗？

反馈

访问OSS的过程中会产生大量的访问日志。您可以通过日志转存功能将这些日志按照固定命名规则，以小时为单位生成日志文件写入您指定的存储空间（Bucket）。

## 开启日志转存

以下代码用于开启日志转存功能。

```ruby
require 'aliyun/oss'

client = Aliyun::OSS::Client.new(
  # Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
  endpoint: 'https://oss-cn-hangzhou.aliyuncs.com',
  # 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  access_key_id: ENV['OSS_ACCESS_KEY_ID'],
  access_key_secret: ENV['OSS_ACCESS_KEY_SECRET']
)

# 填写Bucket名称，例如examplebucket。
bucket = client.get_bucket('examplebucket')
# logging_bucket填写存放日志文件的目标Bucket。
# my-log填写日志文件存储的目录，如果指定此项，则日志文件将保存在指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。
bucket.logging = Aliyun::OSS::BucketLogging.new(
  enable: true, target_bucket: 'logging_bucket', target_prefix: 'my-log')
```

## 查看日志转存配置

以下代码用于查看日志转存配置。

```ruby
require 'aliyun/oss'

client = Aliyun::OSS::Client.new(
  # Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
  endpoint: 'https://oss-cn-hangzhou.aliyuncs.com',
  # 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  access_key_id: ENV['OSS_ACCESS_KEY_ID'],
  access_key_secret: ENV['OSS_ACCESS_KEY_SECRET']
)

# 填写Bucket名称，例如examplebucket。
bucket = client.get_bucket('examplebucket')
log = bucket.logging
puts log.to_s
```

## 关闭日志转存

以下代码用于关闭日志转存功能。

```ruby
require 'aliyun/oss'

client = Aliyun::OSS::Client.new(
  # Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
  endpoint: 'https://oss-cn-hangzhou.aliyuncs.com',
  # 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  access_key_id: ENV['OSS_ACCESS_KEY_ID'],
  access_key_secret: ENV['OSS_ACCESS_KEY_SECRET']
)

# 填写Bucket名称，例如examplebucket。
bucket = client.get_bucket('examplebucket')
bucket.logging = Aliyun::OSS::BucketLogging.new(enable: false)
```

## 相关文档

- 关于开启日志转存功能的API接口说明，请参见 [PutBucketLogging](https://help.aliyun.com/zh/oss/developer-reference/putbucketlogging#reference-t1g-zj5-tdb "")。

- 关于查看日志转存配置的API接口说明，请参见 [GetBucketLogging](https://help.aliyun.com/zh/oss/developer-reference/getbucketlogging#reference-mm3-zwv-tdb "")。

- 关于关闭日志转存功能的API接口说明，请参见 [DeleteBucketLogging](https://help.aliyun.com/zh/oss/developer-reference/deletebucketlogging#reference-jrn-gsw-tdb "")。