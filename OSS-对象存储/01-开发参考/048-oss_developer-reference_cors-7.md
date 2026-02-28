### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)[OSS PHP SDK V1](https://help.aliyun.com/zh/oss/developer-reference/preface-3/)[数据安全（PHP SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/data-security-10/)跨域资源共享（PHP SDK V1）

# 跨域资源共享（PHP SDK V1）

更新时间：2025-11-28 03:44:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

设置跨域资源共享规则

获取跨域资源共享规则

删除跨域资源共享规则

相关文档

跨域资源共享（Cross-origin resource sharing，简称CORS）允许Web端的应用程序访问不属于本域的资源。OSS提供跨域资源共享接口，方便您控制跨域访问的权限。

## 注意事项

- 本文以华东1（杭州）外网Endpoint为例。如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint。关于OSS支持的Region与Endpoint的对应关系，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

- 本文以OSS域名新建OSSClient为例。如果您希望通过自定义域名、STS等方式新建OSSClient，请参见 [新建OssClient](https://help.aliyun.com/zh/oss/developer-reference/initialization-6#section-wsn-wq4-kfb "")。

- 要设置跨域资源共享规则，您必须有`oss:PutBucketCors`权限；要获取跨域资源共享规则，您必须有`oss:GetBucketCors`权限；要删除跨域资源共享规则，您必须有`oss:DeleteBucketCors`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。


## 设置跨域资源共享规则

以下代码用于设置目标存储空间examplebucket的跨域资源共享规则。

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
use OSS\Model\CorsConfig;
use OSS\Model\CorsRule;

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
$endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 填写Bucket名称，例如examplebucket。
$bucket= "examplebucket";

$corsConfig = new CorsConfig();
$rule = new CorsRule();
// 设置允许跨域请求的响应头。AllowedHeader可以设置多个，每个AllowedHeader中最多只能使用一个通配符星号（*）。
// 建议无特殊需求时设置AllowedHeader为星号（*）。
$rule->addAllowedHeader("*");
// 设置允许用户从应用程序中访问的响应头。ExposeHeader可以设置多个，ExposeHeader中不支持使用通配符星号（*）。
$rule->addExposeHeader("x-oss-header");
// 设置允许的跨域请求的来源。AllowedOrigin可以设置多个，每个AllowedOrigin中最多只能使用一个通配符星号（*）。
$rule->addAllowedOrigin("https://example.com:8080");
$rule->addAllowedOrigin("https://*.aliyun.com");
// 设置AllowedOrigin为星号（*）时，表示允许所有域的来源。
//$rule->addAllowedOrigin("*");
// 设置允许的跨域请求方法。
$rule->addAllowedMethod("POST");
// 设置浏览器对特定资源的预取（OPTIONS）请求返回结果的缓存时间，单位为秒。
$rule->setMaxAgeSeconds(10);
// 每个Bucket最多支持添加10条规则。
$corsConfig->addRule($rule);
// 设置是否返回Vary: Origin头，取值为false表示任意情况下均不返回Vary: Origin头
$corsConfig->setResponseVary(false);

try{
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

    // 已存在的规则将被覆盖。
    $ossClient->putBucketCors($bucket, $corsConfig);
} catch(OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . ": OK" . "\n");
```

## 获取跨域资源共享规则

以下代码用于获取目标存储空间examplebucket的跨域资源共享规则。

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
use OSS\Core\OssException;

try {
    // 从环境变量中获取访问凭证,并保存在provider中。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
    $provider = new EnvironmentVariableCredentialsProvider();
    // 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
    $endpoint = "http://oss-cn-hangzhou.aliyuncs.com";
    // 填写Bucket名称，例如examplebucket。
    $bucket= "examplebucket";
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);
    $corsConfig = $ossClient->getBucketCors($bucket);

    if ($corsConfig->getResponseVary()){
        printf("Response Vary : true" .PHP_EOL);
    }else{
        printf("Response Vary : false" .PHP_EOL);
    }

    foreach ($corsConfig->getRules() as $key => $rule){
        if($rule->getAllowedHeaders()){
            foreach($rule->getAllowedHeaders() as $header){
                printf("Allowed Headers :" .$header .PHP_EOL);
            }
        }
        if ($rule->getAllowedMethods()){
            foreach($rule->getAllowedMethods() as $method){
                printf("Allowed Methods :" .$method . PHP_EOL);
            }

        }
        if($rule->getAllowedOrigins()){
            foreach($rule->getAllowedOrigins() as $origin){
                printf("Allowed Origins :" .$origin , PHP_EOL);
            }

        }
        if($rule->getExposeHeaders()){
            foreach($rule->getExposeHeaders() as $exposeHeader){
                printf("Expose Headers :" .$exposeHeader . PHP_EOL);
            }
        }
        printf("Max Age Seconds :" .$rule->getMaxAgeSeconds() .PHP_EOL);

    }
} catch (OssException $e) {
    printf($e->getMessage() . "\n");
    return;
}
```

## 删除跨域资源共享规则

以下代码用于删除目标存储空间examplebucket的所有跨域资源共享规则。

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
$endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 填写Bucket名称，例如examplebucket。
$bucket= "examplebucket";

try{
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

    $ossClient->deleteBucketCors($bucket);
} catch(OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . ": OK" . "\n");
```

## 相关文档

- 关于跨域资源共享的完整示例代码，请参见 [GitHub](https://github.com/aliyun/aliyun-oss-php-sdk/blob/master/samples/BucketCors.php)。

- 关于设置跨域规则的API接口说明，请参见 [PutBucketCors](https://help.aliyun.com/zh/oss/developer-reference/putbucketcors#reference-wtg-ttc-xdb "")。

- 关于获取跨域规则的API接口说明，请参见 [GetBucketCors](https://help.aliyun.com/zh/oss/developer-reference/getbucketcors#reference-m2w-ywc-xdb "")。

- 关于删除跨域规则的API接口说明，请参见 [DeleteBucketCors](https://help.aliyun.com/zh/oss/developer-reference/deletebucketcors#reference-fjn-szc-xdb "")。