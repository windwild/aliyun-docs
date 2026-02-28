### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)[OSS C++ SDK](https://help.aliyun.com/zh/oss/developer-reference/cpp/)[数据安全（C++ SDK）](https://help.aliyun.com/zh/oss/developer-reference/data-security-5/)[版本控制（C++ SDK）](https://help.aliyun.com/zh/oss/developer-reference/versioning-2/)管理版本控制（C++ SDK）

# 管理版本控制（C++ SDK）

更新时间：2025-11-28 03:33:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

设置Bucket版本控制状态

获取Bucket版本控制状态信息

列举Bucket中所有Object的版本信息

相关文档

版本控制应用于存储空间（Bucket）内的所有文件（Object）。

## 注意事项

- 本文以华东1（杭州）外网Endpoint为例。如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint。关于OSS支持的Region与Endpoint的对应关系，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

- 本文以OSS域名新建OSSClient为例。如果您希望通过自定义域名、STS等方式新建OSSClient，请参见 [新建OssClient](https://help.aliyun.com/zh/oss/developer-reference/initialization-12#section-nqa-yww-gxo "")。

- 要设置Bucket版本控制状态，您必须具有`oss:PutBucketVersioning`权限；要获取Bucket版本控制状态信息，您必须具有`oss:GetBucketVersioning`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。


## 设置Bucket版本控制状态

以下代码用于设置Bucket为开启版本控制（Enabled）或暂停版本控制（Suspended）状态。

```c
#include <alibabacloud/oss/OssClient.h>
using namespace AlibabaCloud::OSS;

int main(void)
{
    /* 初始化OSS账号信息。*/

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /* 填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";

    /* 初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    /* 创建Bucket版本配置，状态设置为Enabled或Suspended。*/
    SetBucketVersioningRequest setrequest(BucketName, VersioningStatus::Enabled);
    auto outcome = client.SetBucketVersioning(setrequest);

    if (!outcome.isSuccess()) {
        /* 异常处理。*/
        std::cout << "SetBucketVersioning fail" <<
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

## 获取Bucket版本控制状态信息

以下代码用于获取Bucket的版本控制状态信息。

```c
#include <alibabacloud/oss/OssClient.h>
using namespace AlibabaCloud::OSS;

int main(void)
{
    /* 初始化OSS账号信息。*/

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /* 填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";

    /* 初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    /* 获取Bucket版本状态信息。*/
    auto outcome = client.GetBucketVersioning(GetBucketVersioningRequest(BucketName));

    if (!outcome.isSuccess()) {
        /* 异常处理。*/
        std::cout << "GetBucketVersioning fail" <<
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

## 列举Bucket中所有Object的版本信息

以下代码用于列举指定Bucket中包括删除标记（Delete Marker）在内的所有Object的版本信息。

```c
#include <alibabacloud/oss/OssClient.h>

using namespace AlibabaCloud::OSS;

int main(void)
{
    /* 初始化OSS账号信息。*/

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /* 填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";
    /* 填写Object完整路径，完整路径中不能包含Bucket名称，例如exampledir/exampleobject.txt。*/
    std::string ObjectName = "exampledir/exampleobject.txt";

    /* 初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    ListObjectVersionsRequest request(BucketName);
    bool IsTruncated = false;

    do {
            auto outcome = client.ListObjectVersions(request);

            if (outcome.isSuccess()) {
                /* 查看列出的Object删除标记的各版本信息。*/
                for (auto const &marker : outcome.result().DeleteMarkerSummarys()) {
                   std::cout << "marker key:" << marker.Key() << ",marker versionid:" << marker.VersionId() << std::endl;
                }

                /* 查看列出的Object各版本信息。*/
                for (auto const &obj : outcome.result().ObjectVersionSummarys()) {
                     std::cout << "object key:" << obj.Key() << ",object versionid:" << obj.VersionId() << std::endl;
                }
            }
            else {
                std::cout << "ListObjectVersions fail" <<
                ",code:" << outcome.error().Code() <<
                ",message:" << outcome.error().Message() <<
                ",requestId:" << outcome.error().RequestId() << std::endl;
                break;
            }
            request.setKeyMarker(outcome.result().NextKeyMarker());
            request.setVersionIdMarker(outcome.result().NextVersionIdMarker());
            IsTruncated = outcome.result().IsTruncated();
    } while (IsTruncated);

    /* 释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

## 相关文档

- 关于设置Bucket版本控制状态的API接口说明，请参见 [PutBucketVersioning](https://help.aliyun.com/zh/oss/developer-reference/putbucketversioning#reference-w2w-nm3-fhb "")。

- 关于获取Bucket版本控制状态的API接口说明，请参见 [GetBucketVersioning](https://help.aliyun.com/zh/oss/developer-reference/getbucketversioning#reference-fhn-kt3-fhb "")。