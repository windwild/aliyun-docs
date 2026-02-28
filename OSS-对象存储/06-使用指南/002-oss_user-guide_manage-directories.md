### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[对象/文件（Object）](https://help.aliyun.com/zh/oss/user-guide/object-file-object/)管理目录

# 管理OSS目录

更新时间：2025-10-18 22:49:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

创建目录

重命名目录

删除目录

查询目录的文件数量及大小

应用于生产

权限管理

性能优化

OSS中文件数量庞大时，所有文件平铺存储会导致查找困难、批量操作复杂。为了解决这些问题，OSS提供了目录功能，通过模拟文件夹的结构来组织和管理海量对象。

## **工作原理**

OSS本质上是扁平存储，没有真正的文件夹。控制台所显示的“目录”是OSS依据文件名中的`/`分隔符自动生成的。

当在控制台看到如下的层级结构时：

```plaintext
examplebucket
    └── log/
       ├── date1.txt
       ├── date2.txt
       ├── date3.txt
    └── destfolder/
       └── 2021/
          ├── photo.jpg
```

实际上OSS只是存储了这些文件：

```plaintext
log/date1.txt
log/date2.txt
destfolder/2021/photo.jpg
```

## 创建目录

目录生成有两种方式：

- **上传文件时自动生成：** 上传包含路径的文件时，相应的目录会自动出现。

- **主动创建空目录：** 此操作的本质是创建一个以`/`结尾的0字节文件，以此作为空目录的占位符。






控制台



ossutil



SDK



ossbrowser



















1. 在[OSS管理控制台](https://oss.console.aliyun.com/)，进入目标Bucket的 **文件管理** **\>** **文件列表** 页面。

2. 单击 **新建目录**。

3. 输入 **目录名**，然后单击 **确定**。



     目录命名规范如下：



     - 不允许使用表情符，请使用符合要求的UTF-8字符。
     - 正斜线`/`用于分割路径，可快速创建子目录，但不要以正斜线`/`或反斜线`\`开头，不要出现连续的正斜线`/`。
     - 不允许出现名为`..`的子目录。
     - 总长度控制在1~254个字符。

以下示例展示了如何在存储空间`examplebucket`中创建目录`dir/`。

```bash
ossutil mkdir oss://examplebucket/dir
```

更多用法见 [mkdir（创建目录）](https://help.aliyun.com/zh/oss/developer-reference/mkdir-create-directory#c557acd62dc2b "")。

以下仅列举常见SDK创建目录的代码示例。关于其他SDK的创建目录的代码示例，请参见 [SDK简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

Java

PHP

Node.js

Python

C#

C

Java

```java
import com.aliyun.oss.ClientException;
import com.aliyun.oss.OSS;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.OSSClientBuilder;
import com.aliyun.oss.OSSException;
import com.aliyun.oss.model.PutObjectRequest;
import java.io.ByteArrayInputStream;

public class Demo {

    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 强烈建议不要把访问凭证保存到工程代码里，否则可能导致访问凭证泄露，威胁您账号下所有资源的安全。本代码示例以从环境变量中获取访问凭证为例。运行本代码示例之前，请先配置环境变量。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写目录名称，目录需以正斜线结尾。
        String objectName = "exampledir/";

        // 创建OSSClient实例。
        OSS ossClient = new OSSClientBuilder().build(endpoint, credentialsProvider);

        try {
            String content = "";

            // 创建PutObjectRequest对象。
            PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, objectName, new ByteArrayInputStream(content.getBytes()));

            // 如果需要上传时设置存储类型和访问权限，请参考以下示例代码。
            // ObjectMetadata metadata = new ObjectMetadata();
            // metadata.setHeader(OSSHeaders.OSS_STORAGE_CLASS, StorageClass.Standard.toString());
            // metadata.setObjectAcl(CannedAccessControlList.Private);
            // putObjectRequest.setMetadata(metadata);

            // 上传字符串。
            ossClient.putObject(putObjectRequest);
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
// 填写Bucket名称，例如examplebucket。
$bucket= "examplebucket";
// 填写目录名称，目录需以正斜线结尾。
$object = "exampledir/";
$content = "";
try{
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
    );
    $ossClient = new OssClient($config);

    $ossClient->putObject($bucket, $object, $content);
} catch(OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . "OK" . "\n");

// 上传时可以设置相关的headers，例如设置访问权限为private、自定义元数据等。
$options = array(
    OssClient::OSS_HEADERS => array(
        'x-oss-object-acl' => 'private',
        'x-oss-meta-info' => 'your info'
    ),
);
try{
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
    );
    $ossClient = new OssClient($config);

    $ossClient->putObject($bucket, $object, $content, $options);
} catch(OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . "OK" . "\n");
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
  // 填写Bucket名称。
  bucket: 'examplebucket',
});

async function putBuffer () {
  try {
    // 填写目录名称，目录需以正斜线结尾。
    const result = await client.put('exampledir/', new Buffer(''));
    console.log(result);
  } catch (e) {
    console.log(e);
  }
}

putBuffer();
```

Python

```python
# -*- coding: utf-8 -*-

import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuth(EnvironmentVariableCredentialsProvider())
# yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
# 填写Bucket名称。
bucket = oss2.Bucket(auth, 'https://oss-cn-hangzhou.aliyuncs.com', 'examplebucket')

# 填写目录名称，目录需以正斜线结尾。
bucket.put_object('exampledir/', '')
```

C#

```csharp
using System.Text;
using Aliyun.OSS;

// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
var endpoint = "yourEndpoint";
// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
var accessKeyId = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_ID");
var accessKeySecret = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET");
// 填写Bucket名称，例如examplebucket。
var bucketName = "examplebucket";
// 填写目录名称，目录需以正斜线结尾。
var objectName = "exampledir/";
var objectContent = "";

// 创建OssClient实例。
var client = new OssClient(endpoint, accessKeyId, accessKeySecret);
try
{
    byte[] binaryData = Encoding.ASCII.GetBytes(objectContent);
    MemoryStream requestContent = new MemoryStream(binaryData);
    // 创建目录。
    client.PutObject(bucketName, objectName, requestContent);
    Console.WriteLine("Put object succeeded");
}
catch (Exception ex)
{
    Console.WriteLine("Put object failed, {0}", ex.Message);
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
/* 填写目录名称，目录需以正斜线结尾。*/
const char *object_name = "exampledir/";
const char *object_content = "";
void init_options(oss_request_options_t *options)
{
    options->config = oss_config_create(options->pool);
    /* 用char*类型的字符串初始化aos_string_t类型。*/
    aos_str_set(&options->config->endpoint, endpoint);
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    aos_str_set(&options->config->access_key_id, getenv("OSS_ACCESS_KEY_ID"));
    aos_str_set(&options->config->access_key_secret, getenv("OSS_ACCESS_KEY_SECRET"));
    /* 是否使用了CNAME。0表示不使用。*/
    options->config->is_cname = 0;
    /* 设置网络相关参数，比如超时时间等。*/
    options->ctl = aos_http_controller_create(options->pool, 0);
}
int main(int argc, char *argv[])
{
    /* 在程序入口调用aos_http_io_initialize方法来初始化网络、内存等全局资源。*/
    if (aos_http_io_initialize(NULL, 0) != AOSE_OK) {
        exit(1);
    }
    /* 用于内存管理的内存池（pool），等价于apr_pool_t。其实现代码在apr库中。*/
    aos_pool_t *pool;
    /* 重新创建一个内存池，第二个参数是NULL，表示没有继承其它内存池。*/
    aos_pool_create(&pool, NULL);
    /* 创建并初始化options，该参数包括endpoint、access_key_id、acces_key_secret、is_cname、curl等全局配置信息。*/
    oss_request_options_t *oss_client_options;
    /* 在内存池中分配内存给options。*/
    oss_client_options = oss_request_options_create(pool);
    /* 初始化Client的选项oss_client_options。*/
    init_options(oss_client_options);
    /* 初始化参数。*/
    aos_string_t bucket;
    aos_string_t object;
    aos_list_t buffer;
    aos_buf_t *content = NULL;
    aos_table_t *headers = NULL;
    aos_table_t *resp_headers = NULL;
    aos_status_t *resp_status = NULL;
    aos_str_set(&bucket, bucket_name);
    aos_str_set(&object, object_name);
    aos_list_init(&buffer);
    content = aos_buf_pack(oss_client_options->pool, object_content, strlen(object_content));
    aos_list_add_tail(&content->node, &buffer);
    /* 上传文件。*/
    resp_status = oss_put_object_from_buffer(oss_client_options, &bucket, &object, &buffer, headers, &resp_headers);
    /* 判断上传是否成功。*/
    if (aos_status_is_ok(resp_status)) {
        printf("put object from buffer succeeded\n");
    } else {
        printf("put object from buffer failed\n");
    }
    /* 释放内存池，相当于释放了请求过程中各资源分配的内存。*/
    aos_pool_destroy(pool);
    /* 释放之前分配的全局资源。*/
    aos_http_io_deinitialize();
    return 0;
}
```

1. [安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#2e1e5eee641da "") 并 [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")。

2. 进入目标Bucket，选择 **新建目录**。

3. 输入目录名并确认 **保存**。


## **重命名目录**

目录重命名并非单一的原子操作，无论使用何种工具，其底层原理都是一个复合工作流：

1. **复制**：将原目录下的所有文件递归地复制到一个新的目标目录下。

2. **删除**：确认复制成功后，将原目录及其下的所有文件彻底删除。


**重要**

由于重命名需要逐一复制和删除目录下的所有文件，该操作对大目录将非常耗时，并会产生大量的API调用和流量费用，请务必谨慎评估。

ossbrowser

ossutil

SDK

API

ossbrowser将上述复杂的“复制-删除”工作流自动化了，用户只需在界面上进行一次操作即可。对于大多数场景，推荐优先使用此方式。

1. [安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#2e1e5eee641da "") 并 [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")。

2. 选中目录，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6067946371/p902619.png)，选择 **重命名**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6067946371/p902616.png)

3. 设置新的目录名，然后单击 **确认修改**。


使用ossutil时，需要手动执行 **复制** 和 **删除** 两个核心步骤来完成重命名。

1. **复制文件**

使用 [cp（拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/cp-1 "") 命令并附带`--recursive (-r)` 选项，将存储空间`examplebucket`中`old-dir/`下的所有内容复制到`new-dir/`。















```bash
ossutil cp oss://examplebucket/old-dir/ oss://examplebucket/new-dir/ -r
```

2. **（可选）验证**

使用 [ls（列举账号级别下的资源）](https://help.aliyun.com/zh/oss/developer-reference/ls-list-resources-under-the-account-level "") 命令检查新目录，确保所有文件已成功复制。















```bash
ossutil ls oss://examplebucket/new-dir/
```

3. **删除原目录**

确认复制无误后，使用 [rm（删除）](https://help.aliyun.com/zh/oss/developer-reference/rm-deleted "") 命令并附带`--recursive (-r)`选项，删除原目录`old-dir/`。



**警告**





此操作将永久删除`old-dir/`目录及其下的所有文件，删除后无法恢复，请务必谨慎操作。



















```bash
ossutil rm oss://examplebucket/old-dir/ -r
```


如上所述，通过SDK重命名目录需要组合多个API完成。具体实现可分别参考以下核心操作的SDK文档：

- [列举文件](https://help.aliyun.com/zh/oss/user-guide/list-objects-18 "")

- [拷贝文件](https://help.aliyun.com/zh/oss/user-guide/copy-objects-16 "")

- [删除文件](https://help.aliyun.com/zh/oss/user-guide/delete-objects-18 "")


通过API重命名目录，需要组合以下API调用完成：

- 复制： [CopyObject](https://help.aliyun.com/zh/oss/developer-reference/copyobject "")

- 列举： [ListObjectsV2（GetBucketV2）](https://help.aliyun.com/zh/oss/developer-reference/listobjects-v2 "")

- 删除： [DeleteObject](https://help.aliyun.com/zh/oss/developer-reference/deleteobject "")


## 删除目录

**警告**

删除目录会同步删除目录下包含的子目录以及所有文件，请谨慎操作。

控制台

ossutil

SDK

ossbrowser

API

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 进入目标Bucket的**文件管理** > **文件列表**页面。

3. 选择要删除的目录，单击 **操作** 列的 **彻底删除**。

4. 在弹出的对话框中单击 **确定**。



**重要**





删除目录及文件期间，请勿刷新或关闭任务列表，否则会导致任务中断。


以下示例展示了如何删除存储空间`examplebucket`下的目录`test/`。

```bash
ossutil rm oss://examplebucket/test/ -r
```

更多用法见 [rm（删除）](https://help.aliyun.com/zh/oss/developer-reference/rm-deleted "")。

您可以通过指定`Prefix`的方式删除目录及目录下的所有文件。例如，您希望删除存储空间examplebucket下目录log及该目录下的所有文件，请将示例代码中的Prefix参数指定为`log/`。

Java

PHP

Node.js

Python

Go

C++

Java

```java
import com.aliyun.oss.ClientException;
import com.aliyun.oss.OSS;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.OSSClientBuilder;
import com.aliyun.oss.OSSException;
import com.aliyun.oss.model.*;
import java.io.UnsupportedEncodingException;
import java.net.URLDecoder;
import java.util.ArrayList;
import java.util.List;

public class Demo {

    public static void main(String[] args) throws Exception {
        // yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
        String endPoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 强烈建议不要把访问凭证保存到工程代码里，否则可能导致访问凭证泄露，威胁您账号下所有资源的安全。本代码示例以从环境变量中获取访问凭证为例。运行本代码示例之前，请先配置环境变量。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";

        // 填写待删除目录的完整路径，完整路径中不包含Bucket名称。
        final String prefix = "log/";

        // 创建OSSClient实例。
        OSS ossClient = new OSSClientBuilder().build(endPoint, credentialsProvider);

        try {
            // 删除目录及目录下的所有文件。
            String nextMarker = null;
            ObjectListing objectListing = null;
            do {
                ListObjectsRequest listObjectsRequest = new ListObjectsRequest(bucketName)
                        .withPrefix(prefix)
                        .withMarker(nextMarker);

                objectListing = ossClient.listObjects(listObjectsRequest);
                if (objectListing.getObjectSummaries().size() > 0) {
                    List<String> keys = new ArrayList<String>();
                    for (OSSObjectSummary s : objectListing.getObjectSummaries()) {
                        System.out.println("key name: " + s.getKey());
                        keys.add(s.getKey());
                    }
                    DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName).withKeys(keys).withEncodingType("url");
                    DeleteObjectsResult deleteObjectsResult = ossClient.deleteObjects(deleteObjectsRequest);
                    List<String> deletedObjects = deleteObjectsResult.getDeletedObjects();
                    try {
                        for(String obj : deletedObjects) {
                            String deleteObj =  URLDecoder.decode(obj, "UTF-8");
                            System.out.println(deleteObj);
                        }
                    } catch (UnsupportedEncodingException e) {
                        e.printStackTrace();
                    }
                }

                nextMarker = objectListing.getNextMarker();
            } while (objectListing.isTruncated());
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

use OSS\OssClient;
use OSS\Core\OssException;
// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$accessKeyId = getenv("OSS_ACCESS_KEY_ID");
$accessKeySecret = getenv("OSS_ACCESS_KEY_SECRET");
// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
$endpoint = "yourEndpoint";
// 填写Bucket名称。
$bucket = "examplebucket";

try {
   $ossClient = new OssClient($accessKeyId, $accessKeySecret, $endpoint, false);
   $option = array(
      OssClient::OSS_MARKER => null,
      // 填写待删除目录的完整路径，完整路径中不包含Bucket名称。
      OssClient::OSS_PREFIX => "log/",
      OssClient::OSS_DELIMITER=>'',
   );
   $bool = true;
   while ($bool){
      $result = $ossClient->listObjects($bucket,$option);
      $objects = array();
      if(count($result->getObjectList()) > 0){
         foreach ($result->getObjectList() as $key => $info){
            printf("key name:".$info->getKey().PHP_EOL);
            $objects[] = $info->getKey();
         }
         // 删除目录及目录下的所有文件。
         $delObjects = $ossClient->deleteObjects($bucket, $objects);
         foreach ($delObjects as $info){
            $obj = strval($info);
            printf("Delete ".$obj." : Success" . PHP_EOL);
         }
      }

      if($result->getIsTruncated() === 'true'){
         $option[OssClient::OSS_MARKER] = $result->getNextMarker();
      }else{
         $bool = false;
      }
   }
   printf("Delete Objects : OK" . PHP_EOL);
} catch (OssException $e) {
   printf("Delete Objects : Failed" . PHP_EOL);
   printf($e->getMessage() . PHP_EOL);
   return;
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
  // 填写存储空间名称。
  bucket: 'yourbucketname'
});

// 处理请求失败的情况，防止promise.all中断，并返回失败原因和失败文件名。
async function handleDel(name, options) {
  try {
    await client.delete(name);
  } catch (error) {
    error.failObjectName = name;
    return error;
  }
}

// 删除多个文件。
async function deletePrefix(prefix) {
  const list = await client.list({
    prefix: prefix,
  });

  list.objects = list.objects || [];
  const result = await Promise.all(list.objects.map((v) => handleDel(v.name)));
  console.log(result);
}
// 删除目录及目录下的所有文件。
deletePrefix('log/')
```

Python

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuth(EnvironmentVariableCredentialsProvider())
# yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
# 填写Bucket名称。
bucket = oss2.Bucket(auth, 'https://oss-cn-hangzhou.aliyuncs.com', 'examplebucket')
prefix = "exampledir/"

# 删除目录及目录下的所有文件。
for obj in oss2.ObjectIterator(bucket, prefix=prefix):
    bucket.delete_object(obj.key)
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
    client, err := oss.New("yourEndpoint", "", "", oss.SetCredentialsProvider(&provider))
    if err != nil {
        fmt.Println("Error:", err)
        os.Exit(-1)
    }

    // 填写Bucket名称。
    bucket, err := client.Bucket("examplebucket")
    if err != nil {
        fmt.Println("Error:", err)
        os.Exit(-1)
    }

    marker := oss.Marker("")
    // 填写待删除目录的完整路径，完整路径中不包含Bucket名称。
    prefix := oss.Prefix("log/")
    count := 0
    for {
        lor, err := bucket.ListObjects(marker, prefix)
        if err != nil {
            fmt.Println("Error:", err)
            os.Exit(-1)
        }

        objects := []string{}
        for _, object := range lor.Objects {
            objects = append(objects, object.Key)
        }
        // 删除目录及目录下的所有文件。
        // 将oss.DeleteObjectsQuiet设置为true，表示不返回删除结果。
        delRes, err := bucket.DeleteObjects(objects, oss.DeleteObjectsQuiet(true))
        if err != nil {
            fmt.Println("Error:", err)
            os.Exit(-1)
        }

        if len(delRes.DeletedObjects) > 0 {
            fmt.Println("these objects deleted failure,", delRes.DeletedObjects)
            os.Exit(-1)
        }

        count += len(objects)

        prefix = oss.Prefix(lor.Prefix)
        marker = oss.Marker(lor.NextMarker)
        if !lor.IsTruncated {
            break
        }
    }
    fmt.Printf("success,total delete object count:%d\n", count)
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
    /* 填写Bucket名称。*/
    std::string BucketName = "examplebucket";
    /* 填写待删除目录的完整路径，完整路径中不包含Bucket名称。*/
    std::string keyPrefix = "log/";

    /* 初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);

    std::string nextMarker = "";
    bool isTruncated = false;
    do {
            ListObjectsRequest request(BucketName);
            request.setPrefix(keyPrefix);
            request.setMarker(nextMarker);
            auto outcome = client.ListObjects(request);

            if (!outcome.isSuccess()) {
                /* 异常处理。*/
                std::cout << "ListObjects fail" <<
                ",code:" << outcome.error().Code() <<
                ",message:" << outcome.error().Message() <<
                ",requestId:" << outcome.error().RequestId() << std::endl;
                break;
            }
            for (const auto& object : outcome.result().ObjectSummarys()) {
                DeleteObjectRequest request(BucketName, object.Key());
                /* 删除目录及目录下的所有文件。*/
                auto delResult = client.DeleteObject(request);
            }
            nextMarker = outcome.result().NextMarker();
            isTruncated = outcome.result().IsTruncated();
    } while (isTruncated);

    /* 释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

1. [安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#2e1e5eee641da "") 并 [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")。

2. 选中目录，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6067946371/p902619.png)图标。

3. 选择 **删除**，然后单击 **确认删除**。


如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。更多信息，请参见 [DeleteObject](https://help.aliyun.com/zh/oss/developer-reference/deleteobject#reference-iqc-mqv-wdb "")。

## 查询目录的文件数量及大小

#### **方式一：通过列举文件的方式临时查询**

该方式适用于指定目录下文件数量较少（如一万以内），且以临时性查询为主的场景。

1. 在目标Bucket的左侧导航栏， 选择**文件管理** \> **文件列表**。

2. 单击目标目录右侧的 **统计**。

![filesize.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951261571/p694302.jpg)


#### **方式二：通过存储空间清单的方式定期查询**

该方式适用于指定目录的文件数量较大（百亿级）且需要定期查询的场景。

1. 在目标Bucket的左侧导航栏， 选择**数据管理** \> **Bucket 清单**。

2. 单击 **创建清单**，在 **设置清单报告规则** 面板，选择 **存储清单 Bucket**、清单内容选择 **Object大小**、按前缀匹配输入需要查询的目录名称（例如random\_files/），其他参数保留默认配置。

![screenshot_2025-07-04_18-14-09](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7809842571/p982552.png)

3. 查看清单结果。

1. 在 **文件列表** 页面的`/存储清单Bucket/清单id/data/`路径下找到生成的清单结果文件。

      ![screenshot_2025-07-04_18-22-28](<Base64-Image-Removed>)

2. 将清单结果文件下载到本地，查看该目录下的文件数量和大小。

      清单结果文件中A列数据代表Bucket名称，B列数据是该目录及目录下的所有文件列表，C列数据是目录和目录下的文件大小。

      ![screenshot_2025-07-04_18-28-44](<Base64-Image-Removed>)

更多存储空间清单信息，请参见 [存储空间清单](https://help.aliyun.com/zh/oss/user-guide/bucket-inventory "")。

#### **方式三：通过标量检索的方式结合多种条件查询**

该方式适用于需要对指定目录下的文件数量和大小进行准实时统计，并且支持灵活条件筛选（如按前缀、时间、文件类型等）的场景。

1. 在目标Bucket的左侧导航栏， 选择**文件管理** \> **数据索引**

2. 在 **数据索引** 页面，单击 **立即开启**，然后选择 **标量检索**，单击 **确认开启**。





**说明**





开启标量检索需要等待一定的时间，具体等待时长取决于Bucket中Object的数量。

3. 将 **文件名** 设置为前缀匹配，并输入前缀匹配：`random_files/`，其他参数保留默认设置。

![image](<Base64-Image-Removed>)

4. **设置输出方式**。

   - **对象排序方式** 选择按照 **默认排序** 排列。

   - **数据聚合** 选择按照 **文件大小** 的 **求和** 输出。

     ![image](<Base64-Image-Removed>)
5. 单击 **立即查询**，可以看到最终统计到的random\_files/目录下所有文件和总大小结果。



![image](<Base64-Image-Removed>)


更多标量检索信息，请参见 [标量检索](https://help.aliyun.com/zh/oss/user-guide/scalar-retrieval/ "")。

## **应用于生产**

### 权限管理

OSS的权限管理基于文件前缀匹配，而不是目录文件本身。

例如，要授予用户只读访问 `logs/` 目录下所有文件的权限。

- **错误做法**：尝试为 `logs/` 这个0字节对象设置权限。

- **正确做法**：创建RAM策略，将`Resource`字段设置为 `acs:oss:*:*:your-bucket-name/logs/*`。该策略会匹配所有以 `logs/` 为前缀的对象，无论 `logs/` 目录的0字节占位符对象是否存在。


### 性能优化

- **目录层级深度**：避免过深的嵌套结构（如 `a/b/c/d/.../file.log`），因为列举操作的过滤逻辑会影响性能。

- **大规模重命名**：重命名包含大量文件的目录会产生大量API调用和流量费用，设计系统时应尽量避免。