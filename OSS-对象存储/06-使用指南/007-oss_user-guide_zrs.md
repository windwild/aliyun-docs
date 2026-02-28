### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据保护](https://help.aliyun.com/zh/oss/user-guide/data-protect/)[存储冗余](https://help.aliyun.com/zh/oss/user-guide/overview-of-storage-redundancy-types/)创建同城冗余存储Bucket

# 创建同城冗余存储Bucket

更新时间：2026-02-09 05:05:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

操作步骤

使用OSS控制台

使用阿里云SDK

使用命令行工具ossutil

使用REST API

OSS同城冗余存储提供99.9999999999%（12个9）的数据设计持久性。在支持多可用区的地域，OSS采用多可用区的数据冗余存储机制，将数据冗余存储在同一地域的多个可用区，通过跨可用区的数据分布确保当某个可用区发生故障时，仍能正常访问数据，实现机房级容灾保护。

## 注意事项

- 支持同城冗余的地域以及同城冗余的数据持久性和服务可用性，请参见 [存储冗余](https://help.aliyun.com/zh/oss/user-guide/overview-of-storage-redundancy-types/ "")。

- 相对于本地冗余存储，同城冗余存储会产生更高的存储费用。更多信息，请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

- 开启同城冗余存储后，不支持关闭。


## **操作步骤**

### **使用OSS控制台**

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 在左侧导航栏，单击 **Bucket列表** **，** 然后单击 **创建Bucket**。

3. 在 **创建Bucket** 面板，设置 **存储冗余类型** 为 **同城冗余存储（推荐）**，然后配置各项参数。

关于参数说明的更多信息，请参见 [创建存储空间](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4 "")。


### **使用阿里云SDK**

以下仅列举常见SDK在创建Bucket时开启同城冗余存储的代码示例。关于其他SDK在创建Bucket时开启同城冗余存储的代码示例，请参见 [SDK简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

Java

Node.js

Python

C#

C++

Go

Java

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.CannedAccessControlList;
import com.aliyun.oss.model.CreateBucketRequest;
import com.aliyun.oss.model.DataRedundancyType;
import com.aliyun.oss.model.StorageClass;

public class CreateBucket {

    public static void main(String[] args) throws Exception {
        // yourEndpoint填写Bucket所在地域对应的Endpoint。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称。
        String bucketName = "examplebucket";
        // 填写资源组ID。如果不填写资源组ID，则创建的Bucket属于默认资源组。
        //String rsId = "rg-aek27tc****";
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
            // 创建CreateBucketRequest对象。
            CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucketName);

            // 如果创建存储空间的同时需要指定存储类型、存储空间的读写权限、数据容灾类型, 请参考如下代码。
            // 此处以设置存储空间的存储类型为标准存储为例介绍。
            //createBucketRequest.setStorageClass(StorageClass.Standard);
            // 数据容灾类型默认为本地冗余存储，即DataRedundancyType.LRS。如果需要设置数据容灾类型为同城冗余存储，请设置为DataRedundancyType.ZRS。
            //createBucketRequest.setDataRedundancyType(DataRedundancyType.ZRS);
            // 设置存储空间读写权限为公共读，默认为私有。
            //createBucketRequest.setCannedACL(CannedAccessControlList.PublicRead);

            // 在支持资源组的地域创建Bucket时，您可以为Bucket配置资源组。
            //createBucketRequest.setResourceGroupId(rsId);

            // 创建存储空间。
            ossClient.createBucket(createBucketRequest);
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

Node.js

```nodejs
const OSS = require('ali-oss');

const client = new OSS({
  // yourregion填写Bucket所在地域。以华东1（杭州）为例，Region填写为oss-cn-hangzhou。
  region: 'yourregion',
  // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  accessKeyId: process.env.OSS_ACCESS_KEY_ID,
  accessKeySecret: process.env.OSS_ACCESS_KEY_SECRET,
  authorizationV4: true,
  // yourBucketName填写Bucket名称。
  bucket: 'yourBucketName',
});

// 创建存储空间。
async function putBucket() {
  try {
    const options = {
      storageClass: 'Standard', // 存储空间的默认存储类型为标准存储，即Standard。如果需要设置存储空间的存储类型为归档存储，请替换为Archive。
      acl: 'private', // 存储空间的默认读写权限为私有，即private。如果需要设置存储空间的读写权限为公共读，请替换为public-read。
      dataRedundancyType: 'LRS' // 存储空间的默认数据容灾类型为本地冗余存储，即LRS。如果需要设置数据容灾类型为同城冗余存储，请替换为ZRS。
    }
    // 填写Bucket名称。
    const result = await client.putBucket('examplebucket', options);
    console.log(result);
  } catch (err) {
    console.log(err);
  }
}

putBucket();
```

Python

```python
import argparse
import alibabacloud_oss_v2 as oss

# 创建命令行参数解析器
parser = argparse.ArgumentParser(description="put bucket sample")
# 添加命令行参数 --region，表示存储空间所在的区域，必需参数
parser.add_argument('--region', help='The region in which the bucket is located.', required=True)
# 添加命令行参数 --bucket，表示存储空间的名称，必需参数
parser.add_argument('--bucket', help='The name of the bucket.', required=True)
# 添加命令行参数 --endpoint，表示其他服务可用来访问OSS的域名，非必需参数
parser.add_argument('--endpoint', help='The domain names that other services can use to access OSS')

def main():
    args = parser.parse_args()  # 解析命令行参数

    # 从环境变量中加载凭证信息，用于身份验证
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # 加载SDK的默认配置，并设置凭证提供者
    cfg = oss.config.load_default()
    cfg.credentials_provider = credentials_provider
    # 设置配置中的区域信息
    cfg.region = args.region
    # 如果提供了endpoint参数，则设置配置中的endpoint
    if args.endpoint is not None:
        cfg.endpoint = args.endpoint

    # 使用配置好的信息创建OSS客户端
    client = oss.Client(cfg)

    # 执行创建存储空间的请求，存储类型为标准存储
    result = client.put_bucket(oss.PutBucketRequest(
        bucket=args.bucket,
        create_bucket_configuration=oss.CreateBucketConfiguration(
            storage_class='Standard',
           data_redundancy_type='ZRS'
        )
    ))
    # 输出请求的结果状态码和请求ID，用于检查请求是否成功
    print(f'status code: {result.status_code},'
          f' request id: {result.request_id}'
    )

if __name__ == "__main__":
    main()  # 脚本入口，当文件被直接运行时调用main函数
```

C#

```csharp
using Aliyun.OSS;
using Aliyun.OSS.Common;

// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
var endpoint = "yourEndpoint";
// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
var accessKeyId = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_ID");
var accessKeySecret = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET");
// 填写Bucket名称。
var bucketName = "examplebucket";
// 填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。
const string region = "cn-hangzhou";

// 创建ClientConfiguration实例，按照您的需要修改默认参数。
var conf = new ClientConfiguration();

// 设置v4签名。
conf.SignatureVersion = SignatureVersion.V4;

// 创建OssClient实例。
var client = new OssClient(endpoint, accessKeyId, accessKeySecret, conf);
client.SetRegion(region);
// 创建存储空间。
try
    {
        var request = new CreateBucketRequest(bucketName);
        //设置读写权限ACL为公共读PublicRead，默认为私有权限。
        request.ACL = CannedAccessControlList.PublicRead;
        //设置数据容灾类型为同城冗余存储。
        request.DataRedundancyType = DataRedundancyType.ZRS;
        client.CreateBucket(request);
        Console.WriteLine("Create bucket succeeded");
    }
    catch (Exception ex)
    {
        Console.WriteLine("Create bucket failed. {0}", ex.Message);
    }
```

C++

```cpp
#include <alibabacloud/oss/OssClient.h>
using namespace AlibabaCloud::OSS;

int main(void)
{
    /*初始化OSS账号信息。*/

    /*yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";

    / *yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn - hangzhou。 * /
    std::string Region = "yourRegion";

    /*填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";

    /*初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    /*指定新创建bucket的名称、存储类型和ACL。*/
    CreateBucketRequest request(BucketName, StorageClass::IA, CannedAccessControlList::PublicReadWrite);
    /*设置数据容灾类型为同城冗余存储。*/
    request.setDataRedundancyType(DataRedundancyType::ZRS);

    /*创建Bucket。*/
    auto outcome = client.CreateBucket(request);

    if (!outcome.isSuccess()) {
        /*异常处理。*/
        std::cout << "CreateBucket fail" <<
        ",code:" << outcome.error().Code() <<
        ",message:" << outcome.error().Message() <<
        ",requestId:" << outcome.error().RequestId() << std::endl;
        return -1;
    }

    /*释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

Go

```go
package main

import (
	"context"
	"flag"
	"log"

	"github.com/aliyun/alibabacloud-oss-go-sdk-v2/oss"
	"github.com/aliyun/alibabacloud-oss-go-sdk-v2/oss/credentials"
)

// 定义命令行参数
var (
	region     string // 存储空间所在区域
	bucketName string // 存储空间名称
)

// 初始化命令行参数解析
func init() {
	flag.StringVar(&region, "region", "", "The region in which the bucket is located.")
	flag.StringVar(&bucketName, "bucket", "", "The name of the bucket.")
}

func main() {
	// 解析命令行参数
	flag.Parse()

	// 检查存储空间名称是否为空
	if len(bucketName) == 0 {
		flag.PrintDefaults()
		log.Fatalf("invalid parameters, bucket name required")
	}

	// 检查区域是否为空
	if len(region) == 0 {
		flag.PrintDefaults()
		log.Fatalf("invalid parameters, region required")
	}

	// 配置OSS客户端
	cfg := oss.LoadDefaultConfig().
		WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()). // 使用环境变量提供访问凭证
		WithRegion(region)                                                                // 设置区域

	// 创建OSS客户端实例
	client := oss.NewClient(cfg)

	// 构建创建存储空间的请求
	request := &oss.PutBucketRequest{
		Bucket: oss.Ptr(bucketName), // 设置存储空间名称
		CreateBucketConfiguration: &oss.CreateBucketConfiguration{
			DataRedundancyType: oss.DataRedundancyZRS, // 设置数据冗余类型为ZRS（跨区域冗余存储）
		},
	}

	// 发送创建存储空间的请求
	result, err := client.PutBucket(context.TODO(), request)
	if err != nil {
		log.Fatalf("failed to put bucket: %v", err) // 处理错误并终止程序
	}

	// 输出创建存储空间的结果
	log.Printf("put bucket result: %#v\n", result)
}
```

### **使用命令行工具ossutil**

关于使用ossutil在创建Bucket时开启同城冗余存储的具体操作， 请参见 [put-bucket](https://help.aliyun.com/zh/oss/developer-reference/put-bucket#595bc9a51bbhb "")。

### **使用REST API**

如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。更多信息，请参见 [PutBucket](https://help.aliyun.com/zh/oss/developer-reference/putbucket#doc-api-Oss-PutBucket "")。