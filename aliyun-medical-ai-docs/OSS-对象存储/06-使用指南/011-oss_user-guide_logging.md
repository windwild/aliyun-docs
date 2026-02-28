### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[日志与监控](https://help.aliyun.com/zh/oss/user-guide/log-management-and-monitoring/)[日志管理](https://help.aliyun.com/zh/oss/user-guide/manage-logs/)日志转存

# 日志转存

更新时间：2025-12-02 01:41:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用CloudLens for OSS](https://help.aliyun.com/zh/oss/user-guide/use-cloudlens-for-oss)[下一篇：设置日志记录请求头或查询参数](https://help.aliyun.com/zh/oss/user-guide/set-logging-request-headers-or-url-parameters/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

配置日志转存

为Bucket配置日志转存

为向量Bucket配置日志转存

日志文件命名规则

日志的格式和示例

常见问题

中断的请求能否在OSS访问日志中查询？

访问OSS的过程中会产生大量的访问日志。您可以通过日志转存功能将这些日志按照固定命名规则，以小时为单位生成日志文件写入您指定的存储空间（Bucket）。对于已存储的日志，您可以通过阿里云日志服务或搭建Spark集群等方式进行分析。

## 注意事项

- 如果生成日志的源Bucket有地域属性，则存储日志的目标Bucket与源Bucket可以相同也可以不同，但是必须属于同一账号下的相同地域。

为源Bucket配置日志转存时，日志推送操作本身也会生成新的日志。如果源Bucket和目标Bucket是同一个，这些新生成的日志还会被日志功能再次记录并推送，导致日志不断循环产生。建议将日志转存的源Bucket和存储日志的目标Bucket配置为不同的Bucket。

- 如果生成日志的源Bucket无地域属性，则存储日志的目标Bucket必须与源Bucket为同一个Bucket。

- 日志文件预计会在48小时内生成。某个时段的日志文件可能不会记录该时段的所有请求，部分请求可能会出现在上一时段或下一时段的日志文件中。因此，某个时段的日志文件不能确保该时段日志记录的完整性和即时性。

- 在您关闭日志转存功能前，OSS的日志文件会每隔1小时生成一次。请及时清理不再需要的日志文件，以减少您的存储费用。

您可以通过生命周期规则定期删除日志文件。更多信息，请参见 [基于最后一次修改时间的生命周期规则](https://help.aliyun.com/zh/oss/user-guide/lifecycle-rules-based-on-the-last-modified-time#concept-y2g-szy-5db "")。

- 为避免影响OSS-HDFS服务的正常使用或者引发数据污染的风险，在开通了OSS-HDFS服务的Bucket中设置日志转存规则时，禁止将 **日志前缀** 填写为`.dlsdata/`。

- OSS会根据需求在日志的尾部添加一些字段，请您在开发日志处理工具时考虑兼容性的问题。从 2025 年 9 月 17 日起，日志内容新增 Bucket ARN 字段。


## **配置日志转存**

### **为Bucket配置日志转存**

控制台

ossutil

SDK

API

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 单击 **Bucket 列表**，然后单击目标Bucket名称。

3. 在左侧导航栏，选择**日志管理** \> **日志转存**。

4. 在 **日志转存** 页面， **开启日志存储**，按以下说明完成各配置项。


|     |     |
| --- | --- |
| **配置项** | **说明** |
| 日志存储位置 | 默认存储在当前Bucket。如果您希望存储至其他Bucket，需要下拉选择存储日志记录的Bucket名称，只能选择同一账号下相同地域的Bucket。 |
| 日志前缀 | 日志文件存储的目录。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。例如，日志前缀指定为 `log/`，则日志文件将被记录在log/目录下。 |
| 授权角色 | 授权OSS通过扮演默认角色或者自定义角色完成日志转存操作。<br>   - 默认日志转存授权（建议使用）<br>     <br>     选择默认日志转存授权后，会自动生成默认角色`AliyunOSSLoggingDefaultRole`，并完成角色授权。该角色支持本账号下所有Bucket日志转存的授权。首次使用日志转存功能时，需要单击 **一键授权** 自动完成默认角色创建和授权操作。<br>     <br>   - 自定义授权<br>     <br>     如果您只需要授权对指定Bucket完成日志转存，可以使用自定义角色授权的方式。使用自定义授权时，您需要完成以下步骤。<br>     <br>     1. [创建普通服务角色](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-role-for-a-trusted-alibaba-cloud-service#section-0xg-2ri-2sr "")。创建角色过程中，信任主体类型选择 **云服务**，信任主体名称选择 **对象存储**。<br>        <br>     2. [通过脚本编辑模式创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy#section-kwn-gu8-48m "")。<br>        <br>        <br>        <br>        <br>        <br>        <br>        使用KMS加密方式的Bucket<br>        <br>        <br>        <br>        未使用KMS加密方式的Bucket<br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        ```json<br>        {<br>          "Version": "1",<br>          "Statement": [<br>            {<br>              "Effect": "Allow",<br>              "Action": [<br>                "kms:List*",<br>                "kms:Describe*",<br>                "kms:GenerateDataKey",<br>                "kms:Decrypt"<br>              ],<br>              "Resource": "*"<br>            },<br>            {<br>              "Effect": "Allow",<br>              "Action": [<br>                "oss:PutObject",<br>                "oss:AbortMultipartUpload"<br>              ],<br>              "Resource": "acs:oss:*:*:examplebucket/*"<br>            }<br>          ]<br>        }<br>        ```<br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        未使用KMS加密方式包括两种，即Bucket未开启服务端加密或者使用了OSS完全托管的加密方式。以上两种情况需按以下示例配置自定义权限策略。<br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        <br>        ```json<br>        {<br>          "Version": "1",<br>          "Statement": [  <br>            {<br>              "Effect": "Allow",<br>              "Action": [<br>                "oss:PutObject",<br>                "oss:AbortMultipartUpload"<br>              ],<br>              "Resource": "acs:oss:*:*:examplebucket/*"<br>            }<br>          ]<br>        }<br>        ```<br>        <br>     3. [为RAM角色授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-role "")。 |

5. 单击 **保存**。


您可以使用命令行工具ossutil来开启日志转存功能，ossutil的安装请参见 [安装ossutil](https://help.aliyun.com/zh/oss/install-ossutil2#DAS "")。

以下命令用于为存储空间`examplebucket`开启日志转存功能，日志文件前缀为`MyLog-`，存储访问日志的Bucket为`dest-bucket`。

```bash
ossutil api put-bucket-logging --bucket examplebucket --bucket-logging-status "{\"LoggingEnabled\":{\"TargetBucket\":\"destBucket\",\"TargetPrefix\":\"MyLog-\"}}"
```

关于该命令的更多信息，请参见 [put-bucket-logging](https://help.aliyun.com/zh/oss/developer-reference/put-bucket-logging "")。

以下仅列举常见SDK的设置日志转存的代码示例。关于其他SDK的设置日志转存的代码示例，请参见 [SDK简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

Java

PHP

Node.js

Python

C#

Android-Java

Go

C++

C

Ruby

Java

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.SetBucketLoggingRequest;

public class Demo {

    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写待开启日志转存功能的Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写存放日志文件的目标Bucket。targetBucketName与bucketName可以为相同或不同的Bucket。
        String targetBucketName = "yourTargetBucketName";
        // 设置日志文件存储的目录为log/。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。
        String targetPrefix = "log/";
        // 填写Bucket所在地域。以华东1（杭州）为例，Region填写为cn-hangzhou。
        String region = "cn-hangzhou";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
        .endpoint(endpoint)
        .credentialsProvider(credentialsProvider)
        .clientConfiguration(clientBuilderConfiguration)
        .region(region)
        .build();

        try {
            SetBucketLoggingRequest request = new SetBucketLoggingRequest(bucketName);
            request.setTargetBucket(targetBucketName);
            request.setTargetPrefix(targetPrefix);
            ossClient.setBucketLogging(request);
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

PHP

```php
<?php
if (is_file(__DIR__ . '/../autoload.php')) {
    require_once __DIR__ . '/../autoload.php';
}
if (is_file(__DIR__ . '/../vendor/autoload.php')) {
    require_once __DIR__ . '/../vendor/autoload.php';
}

use OSS\Credentials\EnvironmentVariableCredentialsProvider;
use OSS\OssClient;
use OSS\CoreOssException;

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
$endpoint = "yourEndpoint";
// 填写待开启日志转存功能的Bucket名称，例如examplebucket。
$bucket= "examplebucket";

$option = array();
// 设置存放日志文件的目标Bucket。
$targetBucket = "destbucket";
// 设置日志文件存储的目录。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。
$targetPrefix = "log/";

try {
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

    // 开启日志转存。
    $ossClient->putBucketLogging($bucket, $targetBucket, $targetPrefix, $option);
} catch (OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . ": OK" . "\n");
```

Node.js

```nodejs
const OSS = require('ali-oss')
const client = new OSS({
  // yourregion填写Bucket所在地域。以华东1（杭州）为例，Region填写为oss-cn-hangzhou。
  region: 'yourregion',
  // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  accessKeyId: process.env.OSS_ACCESS_KEY_ID,
  accessKeySecret: process.env.OSS_ACCESS_KEY_SECRET,
  authorizationV4: true,
  // yourbucketname填写存储空间名称。
  bucket: 'yourbucketname'
});
async function putBucketLogging () {
  try {
     const result = await client.putBucketLogging('bucket-name', 'logs/');
     console.log(result)
  } catch (e) {
    console.log(e)
  }
}
putBucketLogging();
```

Python

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider
from oss2.models import BucketLogging

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuthV4(EnvironmentVariableCredentialsProvider())

# 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
endpoint = "https://oss-cn-hangzhou.aliyuncs.com"
# 填写Endpoint对应的Region信息，例如cn-hangzhou。注意，v4签名下，必须填写该参数
region = "cn-hangzhou"

# examplebucket填写存储空间名称。
bucket = oss2.Bucket(auth, endpoint, "examplebucket", region=region)

# 将日志文件保存在当前Bucket。
# 设置日志文件存储的目录为log/。如果指定此项，则日志文件将保存在Bucket的指定目录下。如果不指定此项，则日志文件将保存在Bucket的根目录下。
# 开启日志转存功能。
logging = bucket.put_bucket_logging(BucketLogging(bucket.bucket_name, 'log/'))
if logging.status == 200:
    print("Enable access logging")
else:
    print("request_id ：", logging.request_id)
    print("resp : ", logging.resp.response)
```

C#

```csharp
using Aliyun.OSS;
using Aliyun.OSS.Common;

// 填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
var endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
var accessKeyId = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_ID");
var accessKeySecret = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET");
// 填写待开启日志转存功能的Bucket名称，例如examplebucket。
var bucketName = "examplebucket";
// 填写存放日志文件的目标Bucket。targetBucketName与bucketName可以为相同或不同的Bucket。
var targetBucketName = "destbucket";
// 填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。
const string region = "cn-hangzhou";

// 创建ClientConfiguration实例，按照您的需要修改默认参数。
var conf = new ClientConfiguration();

// 设置v4签名。
conf.SignatureVersion = SignatureVersion.V4;

// 创建OssClient实例。
var client = new OssClient(endpoint, accessKeyId, accessKeySecret, conf);
client.SetRegion(region);
try
{
    // 设置日志文件存储的目录为log/。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。
    var request = new SetBucketLoggingRequest(bucketName, targetBucketName, "log/");
    // 开启日志转存功能。
    client.SetBucketLogging(request);
    Console.WriteLine("Set bucket:{0} Logging succeeded ", bucketName);
}
catch (OssException ex)
{
    Console.WriteLine("Failed with error info: {0}; Error info: {1}. \nRequestID:{2}\tHostID:{3}",
        ex.ErrorCode, ex.Message, ex.RequestId, ex.HostId);
}
catch (Exception ex)
{
    Console.WriteLine("Failed with error info: {0}", ex.Message);
}
```

Android-Java

```androidjava
PutBucketLoggingRequest request = new PutBucketLoggingRequest();
// 指定要开启访问日志记录的源Bucket。
request.setBucketName("yourSourceBucketName");
// 指定存储访问日志的目标Bucket。
// 目标Bucket和源Bucket必须属于同一地域。源Bucket和目标Bucket可以是同一个Bucket，也可以是不同的Bucket。
request.setTargetBucketName("yourTargetBucketName");
// 设置日志文件存放的目录。
request.setTargetPrefix("<yourTargetPrefix>");

OSSAsyncTask task = oss.asyncPutBucketLogging(request, new OSSCompletedCallback<PutBucketLoggingRequest, PutBucketLoggingResult>() {
    @Override
    public void onSuccess(PutBucketLoggingRequest request, PutBucketLoggingResult result) {
        OSSLog.logInfo("code::"+result.getStatusCode());
    }

    @Override
    public void onFailure(PutBucketLoggingRequest request, ClientException clientException, ServiceException serviceException) {
         OSSLog.logError("error: "+serviceException.getRawMessage());
    }
});
task.waitUntilFinished();
```

Go

```go
package main

import (
	"fmt"
	"os"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func main() {
	// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}

	// 创建OSSClient实例。
	// yourEndpoint填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
	// yourRegion填写Bucket所在地域，以华东1（杭州）为例，填写为cn-hangzhou。其它Region请按实际情况填写。
	clientOptions := []oss.ClientOption{oss.SetCredentialsProvider(&provider)}
	clientOptions = append(clientOptions, oss.Region("yourRegion"))
	// 设置签名版本
	clientOptions = append(clientOptions, oss.AuthVersion(oss.AuthV4))
	client, err := oss.New("yourEndpoint", "", "", clientOptions...)
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}
	// 填写待开启日志转存功能的Bucket名称，例如examplebucket。
	bucketName := "examplebucket"
	// 填写存放日志文件的目标Bucket。targetBucketName与bucketName必须处于相同地域，可以是相同或不同的Bucket。
	targetBucketName := "destbucket"
	// 设置日志文件存储的目录为log/。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。
	targetPrefix := "log/"

	// 开启日志转存功能。
	err = client.SetBucketLogging(bucketName, targetBucketName, targetPrefix, true)
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}
}
```

C++

```cpp
#include <alibabacloud/oss/OssClient.h>
using namespace AlibabaCloud::OSS;

int main(void)
{
    /* 初始化OSS账号信息。*/

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /* 填写待开启日志转存功能的Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";
    /* 填写存放日志文件的目标Bucket。targetBucketName与bucketName可以为相同或不同的Bucket。*/
    std::string TargetBucketName = "destbucket";
    /* 设置日志文件存储的目录为log/。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。*/
    std::string TargetPrefix  ="log/";

    /* 初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    /* 开启日志转存功能。*/
    SetBucketLoggingRequest request(BucketName, TargetBucketName, TargetPrefix);
    auto outcome = client.SetBucketLogging(request);

    if (!outcome.isSuccess()) {
        /* 异常处理。*/
        std::cout << "SetBucketLogging fail" <<
        ",code:" << outcome.error().Code() <<
        ",message:" << outcome.error().Message() <<
        ",requestId:" << outcome.error().RequestId() << std::endl;
        return -1;
    }

    /* 释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

C

```c
#include "oss_api.h"
#include "aos_http_io.h"
/* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
const char *endpoint = "yourEndpoint";
/* 填写Bucket名称，例如examplebucket。*/
const char *bucket_name = "examplebucket";
/* 填写存放日志文件的目标Bucket。targetBucketName与bucketName可以为相同或不同的Bucket。*/
const char *target_bucket_name = "yourTargetBucketName";
/* 设置日志文件存储的目录。如果指定此项，则日志文件将保存在目标Bucket的指定目录下。如果不指定此项，则日志文件将保存在目标Bucket的根目录下。*/
const char *target_logging_prefix = "yourTargetPrefix";
/* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
const char *region = "yourRegion";
void init_options(oss_request_options_t *options)
{
    options->config = oss_config_create(options->pool);
    /* 用char*类型的字符串初始化aos_string_t类型。*/
    aos_str_set(&options->config->endpoint, endpoint);
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    aos_str_set(&options->config->access_key_id, getenv("OSS_ACCESS_KEY_ID"));
    aos_str_set(&options->config->access_key_secret, getenv("OSS_ACCESS_KEY_SECRET"));
    //需要额外配置以下两个参数
    aos_str_set(&options->config->region, region);
    options->config->signature_version = 4;
    /* 是否使用了CNAME。0表示不使用。*/
    options->config->is_cname = 0;
    /* 用于设置网络相关参数，比如超时时间等。*/
    options->ctl = aos_http_controller_create(options->pool, 0);
}
int main(int argc, char *argv[])
{
    /* 在程序入口调用aos_http_io_initialize方法来初始化网络、内存等全局资源。*/
    if (aos_http_io_initialize(NULL, 0) != AOSE_OK) {
        exit(1);
    }
    /* 用于内存管理的内存池（pool）， 等价于apr_pool_t。其实现代码在apr库中。*/
    aos_pool_t *pool;
    /* 重新创建一个内存池，第二个参数是NULL，表示没有继承其它内存池。*/
    aos_pool_create(&pool, NULL);
    /* 创建并初始化options，该参数包括endpoint、access_key_id、acces_key_secret、is_cname、curl等全局配置信息。*/
    oss_request_options_t *oss_client_options;
    /* 在内存池中分配内存给options。*/
    oss_client_options = oss_request_options_create(pool);
    /* 初始化Client的选项oss_client_options。*/
    init_options(oss_client_options);
    /* 初始化参数 */
    aos_string_t bucket;
    oss_logging_config_content_t *content;
    aos_table_t *resp_headers = NULL;
    aos_status_t *resp_status = NULL;
    aos_str_set(&bucket, bucket_name);
    content = oss_create_logging_rule_content(pool);
    aos_str_set(&content->target_bucket, target_bucket_name);
    aos_str_set(&content->prefix, target_logging_prefix);
    /* 开启存储空间的访问日志记录。*/
    resp_status = oss_put_bucket_logging(oss_client_options, &bucket, content, &resp_headers);
    if (aos_status_is_ok(resp_status)) {
        printf("put bucket logging succeeded\n");
    } else {
        printf("put bucket logging failed, code:%d, error_code:%s, error_msg:%s, request_id:%s\n",
            resp_status->code, resp_status->error_code, resp_status->error_msg, resp_status->req_id);
    }
    /* 释放内存池，相当于释放了请求过程中各资源分配的内存。*/
    aos_pool_destroy(pool);
    /* 释放之前分配的全局资源。*/
    aos_http_io_deinitialize();
    return 0;
}
```

Ruby

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

调用 [PutBucketLogging](https://help.aliyun.com/zh/oss/developer-reference/putbucketlogging "") 接口为Bucket开启日志转存功能。

### **为向量Bucket配置日志转存**

控制台

ossutil

SDK

API

1. 在 [向量Bucket](https://oss.console.aliyun.com/vector-bucket-list) 页面，单击目标Bucket，在左侧导航栏选择 **日志管理** > **日志转存**。

2. 开启 **日志转存** 开关，并配置以下参数：

   - **目标存储位置**：选择用于存放日志文件的Bucket（必须与向量Bucket在同一地域）。

   - **日志前缀**：设置日志文件的目录和前缀，如 `MyLog-`。

   - **授权角色**：使用默认的日志服务角色AliyunOSSLoggingDefaultRole或选择一个自定义角色。

以下示例展示了如何为名为`examplebucket`的存储空间开启日志转存功能，日志文件前缀为`MyLog-`，存储访问日志的Bucket为`examplebucket`。

- 使用JSON配置文件，bucket-logging-status.json内容如下：















```json
{
    "BucketLoggingStatus": {
      "LoggingEnabled": {
        "TargetBucket": "examplebucket",
        "TargetPrefix": "MyLog-",
        "LoggingRole": "AliyunOSSLoggingDefaultRole"
      }
    }
}
```



命令示例如下：















```bash
ossutil vectors-api put-bucket-logging --bucket examplebucket --bucket-logging-status file://bucket-logging-status.json
```

- 使用JSON配置参数，命令示例如下：















```bash
ossutil vectors-api put-bucket-logging --bucket examplebucket --bucket-logging-status "{\"BucketLoggingStatus\":{\"LoggingEnabled\":{\"TargetBucket\":\"examplebucket\",\"TargetPrefix\":\"MyLog-\",\"LoggingRole\":\"AliyunOSSLoggingDefaultRole\"}}}"
```


Python

Go

```pgsql
import argparse
import alibabacloud_oss_v2 as oss
import alibabacloud_oss_v2.vectors as oss_vectors

parser = argparse.ArgumentParser(description="vector put bucket logging sample")
parser.add_argument('--region', help='The region in which the bucket is located.', required=True)
parser.add_argument('--bucket', help='The name of the bucket.', required=True)
parser.add_argument('--endpoint', help='The domain names that other services can use to access OSS')
parser.add_argument('--account_id', help='The account id.', required=True)
parser.add_argument('--target_bucket', help='The name of the target bucket.', required=True)

def main():
    args = parser.parse_args()

    # Loading credentials values from the environment variables
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # Using the SDK's default configuration
    cfg = oss.config.load_default()
    cfg.credentials_provider = credentials_provider
    cfg.region = args.region
    cfg.account_id = args.account_id
    if args.endpoint is not None:
        cfg.endpoint = args.endpoint

    vector_client = oss_vectors.Client(cfg)

    result = vector_client.put_bucket_logging(oss_vectors.models.PutBucketLoggingRequest(
        bucket=args.bucket,
        bucket_logging_status=oss_vectors.models.BucketLoggingStatus(
            logging_enabled=oss_vectors.models.LoggingEnabled(
                target_bucket=args.target_bucket,
                target_prefix='log-prefix',
                logging_role='AliyunOSSLoggingDefaultRole'
            )
        )
    ))

    print(f'status code: {result.status_code},'
          f' request id: {result.request_id},'
    )

if __name__ == "__main__":
    main()
```

```stylus
package main

import (
	"context"
	"flag"
	"github.com/aliyun/alibabacloud-oss-go-sdk-v2/oss/vectors"
	"log"

	"github.com/aliyun/alibabacloud-oss-go-sdk-v2/oss"
	"github.com/aliyun/alibabacloud-oss-go-sdk-v2/oss/credentials"
)

var (
	region     string
	bucketName string
	accountId  string
)

func init() {
	flag.StringVar(&region, "region", "", "The region in which the vector bucket is located.")
	flag.StringVar(&bucketName, "bucket", "", "The name of the vector bucket.")
	flag.StringVar(&accountId, "account-id", "", "The id of vector account.")
}

func main() {
	flag.Parse()
	if len(bucketName) == 0 {
		flag.PrintDefaults()
		log.Fatalf("invalid parameters, bucket name required")
	}

	if len(region) == 0 {
		flag.PrintDefaults()
		log.Fatalf("invalid parameters, region required")
	}

	if len(accountId) == 0 {
		flag.PrintDefaults()
		log.Fatalf("invalid parameters, accounId required")
	}

	cfg := oss.LoadDefaultConfig().
		WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()).
		WithRegion(region).WithAccountId(accountId)

	client := vectors.NewVectorsClient(cfg)

	request := &vectors.PutBucketLoggingRequest{
		Bucket: oss.Ptr(bucketName),
		BucketLoggingStatus: &vectors.BucketLoggingStatus{
			&vectors.LoggingEnabled{
				TargetBucket: oss.Ptr("TargetBucket"),
				TargetPrefix: oss.Ptr("TargetPrefix"),
				LoggingRole:  oss.Ptr("AliyunOSSLoggingDefaultRole"),
			},
		},
	}
	result, err := client.PutBucketLogging(context.TODO(), request)
	if err != nil {
		log.Fatalf("failed to put vector bucket logging %v", err)
	}

	log.Printf("put vector bucket logging result:%#v\n", result)
}
```

调用 [PutBucketLogging](https://help.aliyun.com/zh/oss/developer-reference/putbucketlogging "") 接口为向量Bucket开启日志转存功能。

## 日志文件命名规则

转存后的日志文件命名规则如下：

```plaintext
<TargetPrefix><SourceBucket>YYYY-mm-DD-HH-MM-SS-UniqueString
```

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| TargetPrefix | 日志文件的文件名前缀。 |
| SourceBucket | 产生访问日志的源Bucket名称。 |
| YYYY-mm-DD-HH-MM-SS | 日志的时间分区。从左到右分别表示：年、月、日、小时、分钟和秒。当前转存的日志是以小时粒度存放，例如：HH 为 01 时，代表为 01 点 00 分 00 秒 - 01 点 59 分 59 秒之间的日志信息，同时 MM、SS 均会推送 00。 |
| UniqueString | 系统生成的字符串，是日志文件的唯一标识。 |

## 日志的格式和示例

- 日志格式

OSS的访问日志包含请求者和被访问资源的相关信息，格式如下：















```plaintext
RemoteIP Reserved Reserved Time "RequestURL" HTTPStatus SentBytes RequestTime "Referer" "UserAgent" "HostName" "RequestID" "LoggingFlag" "RequesterAliyunID" "Operation" "BucketName" "ObjectName" ObjectSize ServerCostTime "ErrorCode" RequestLength "UserID" DeltaDataSize "SyncRequest" "StorageClass" "TargetStorageClass" "TransmissionAccelerationAccessPoint" "AccessKeyID" "BucketARN"
```






| **字段** | **示例值** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **字段** | **示例值** | **说明** |
| RemoteIP | 192.168.0.1 | 请求者的IP地址。 |
| Reserved | - | 保留字段，固定值为-。 |
| Reserved | - | 保留字段，固定值为-。 |
| Time | 03/Jan/2021:14:59:49 +0800 | OSS收到请求的时间。 |
| RequestURL | GET /example.jpg HTTP/1.0 | 包含query string的请求URL。<br>OSS会忽略以`x-`开头的query string参数，但这个参数会被记录在访问日志中。所以您可以使用`x-`开头query string参数标记一个请求，然后使用这个标记快速查找该请求对应的日志。 |
| HTTPStatus | 200 | OSS返回的HTTP状态码。 |
| SentBytes | 999131 | 请求产生的下行流量。单位：Byte。 |
| RequestTime | 127 | 完成本次请求耗费的时间。单位：ms。 |
| Referer | http://www.aliyun.com/product/oss | 请求的HTTP Referer。 |
| UserAgent | curl/7.15.5 | HTTP的User-Agent头。 |
| HostName | examplebucket.oss-cn-hangzhou.aliyuncs.com | 请求访问的目标域名。 |
| RequestID | 5FF16B65F05BC932307A3C3C | 请求的Request ID。 |
| LoggingFlag | true | 是否已开启日志转存。取值如下：<br>  - true表示已开启日志转存。<br>    <br>  - false表示未开启日志转存。 |
| RequesterAliyunID | 16571836914537\*\*\*\* | 请求者的用户ID。取值-表示匿名访问。 |
| Operation | GetObject | 请求类型。 |
| BucketName | examplebucket | 请求的目标Bucket名称。 |
| ObjectName | example.jpg | 请求的目标Object名称。 |
| ObjectSize | 999131 | 目标Object大小。单位：Byte。 |
| ServerCostTime | 88 | OSS处理本次请求所花的时间。单位：毫秒。 |
| ErrorCode | - | OSS返回的错误码。取值-表示未返回错误码。 |
| RequestLength | 302 | 请求的长度。单位：Byte。 |
| UserID | 16571836914537\*\*\*\* | Bucket拥有者ID。 |
| DeltaDataSize | - | Object大小的变化量。取值-表示此次请求不涉及Object的写入操作。 |
| SyncRequest | - | 请求类型。取值如下：<br>  - -：一般请求。<br>    <br>  - cdn：CDN回源请求。<br>    <br>  - lifecycle：通过生命周期规则转储或者删除数据的请求。 |
| StorageClass | Standard | 目标Object的存储类型。取值如下：<br>  - Standard：标准存储。<br>    <br>  - IA：低频访问存储。<br>    <br>  - Archive：归档存储。<br>    <br>  - Cold Archive：冷归档存储。<br>    <br>  - DeepCold Archive：深度冷归档存储。<br>    <br>  - -：未获取到Object存储类型。 |
| TargetStorageClass | - | 是否通过生命周期规则或CopyObject转换了Object的存储类型。取值如下：<br>  - Standard：转换为标准存储。<br>    <br>  - IA：转换为低频访问存储。<br>    <br>  - Archive：转换为归档存储。<br>    <br>  - Cold Archive：转换为冷归档存储。<br>    <br>  - DeepCold Archive：转换为深度冷归档存储。<br>    <br>  - -：不涉及Object存储类型转换操作。 |
| TransmissionAccelerationAccessPoint | - | 通过传输加速域名访问目标Bucket时使用的传输加速接入点。例如请求者通过华东1（杭州）的接入点访问目标Bucket时，值为cn-hangzhou。<br>取值-表示未使用传输加速域名或传输加速接入点与目标Bucket所在地域相同。 |
| AccessKeyID | LTAI\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* | 请求者的AccessKey ID。<br>  - 通过控制台的方式发起请求时，日志字段中会显示为以TMP开头的临时AccessKey ID。<br>    <br>  - 通过工具、SDK以长期密钥的方式发起请求时，日志字段中显示为常见的AccessKey ID，示例值为`LTAI****************`。<br>    <br>  - 通过STS临时访问凭证发起请求时，显示为以STS开头的临时AccessKey ID。<br>    <br>**说明**<br>AccessKey ID字段显示为-，表示匿名请求。 |
| BucketArn | acs:oss\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* | Bucket的全局唯一资源描述符。 |

- 日志示例















```plaintext
192.168.0.1 - - [03/Jan/2021:14:59:49 +0800] "GET /example.jpg HTTP/1.0" 200 999131 127 "http://www.aliyun.com/product/oss" "curl/7.15.5" "examplebucket.oss-cn-hangzhou.aliyuncs.com" "5FF16B65F05BC932307A3C3C" "true" "16571836914537****" "GetObject" "examplebucket" "example.jpg" 999131 88 "-" 302 "16571836914537****" - "cdn" "standard" "-" "-" "LTAI****************" "acs:oss***************"
```



日志文件转存到OSS指定Bucket后，您可以通过日志服务对日志文件进行分析。对日志文件进行分析前，您需要通过数据导入方式将OSS日志文件导入到日志服务。有关数据导入的具体操作，请参见 [导入OSS数据](https://help.aliyun.com/zh/sls/import-data-from-oss-to-log-service#task-2372154 "")。有关日志服务分析功能的更多信息，请参见 [查询与分析概述](https://help.aliyun.com/zh/sls/log-analysis-overview#concept-nyf-cjq-zdb "")。


## 常见问题

### **中断的请求能否在OSS访问日志中查询？**

OSS访问日志目前不会记录中断的请求。如果您是通过SDK发起的请求，可以根据SDK的返回值判断请求中断的原因。