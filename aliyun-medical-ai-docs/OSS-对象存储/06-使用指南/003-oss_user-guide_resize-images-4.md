### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/)[图片处理参数](https://help.aliyun.com/zh/oss/user-guide/img-parameters/)图片缩放

# 图片缩放

更新时间：2026-02-05 06:43:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图片处理操作方式](https://help.aliyun.com/zh/oss/user-guide/img-implementation-modes)[下一篇：图片水印](https://help.aliyun.com/zh/oss/user-guide/add-watermarks)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用场景

使用限制

操作方式

参数说明

等比例缩放

指定宽高缩放

缩放计算方式

使用示例

等比例缩小

等比例放大

宽度固定，高度自适应缩小

宽度固定，高度自适应放大

高度固定，宽度自适应缩小

高度固定，宽度自适应放大

长边固定，短边自适应缩放

短边固定，长边自适应缩放

固定宽高，缩略填充

固定宽高，居中裁剪

强制宽高缩放

计费说明

相关API

常见问题

图片缩放的参数不生效怎么办？

按宽高放大图片不生效怎么办？

如何持久化存储处理后的图片？

缩放后的图片读写权限为私有，如何正常访问？

图片缩放是否产生图片数据处理费用？

请求缩放后的图片产生的下行流量是按原图还是缩放后的图片计算？

原图WebP解码异常怎么办？

您可以在`GetObject`请求中添加图片缩放参数，以缩小或放大图片。

## **使用场景**

- 网页设计： 在网页设计和移动应用开发中，图片需要根据不同的屏幕尺寸和分辨率自适应显示。

- 社交媒体：用户上传的图片尺寸各异，平台需要统一处理为适合预览的尺寸。

- 图像识别和分析：在计算机视觉和机器学习领域，为了提高处理效率，对图像进行缩放。


## 使用限制

| **限制** | **项目** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **限制** | **项目** | **说明** |
| 原图限制 | 图片格式 | 原图只支持JPG、PNG、BMP、GIF、WebP、TIFF、HEIC。 |
| 图片大小 | 原图大小不能超过20 MB。如果您需要调整原图大小限制，请在 [配额中心](https://oss.console.aliyun.com/more-tool/quota-setting?spm=0.0.0.i2) 申请。 |
| 图片宽高 | 原图高或者宽不能超过30,000 px，且总像素不能超过2.5亿 px。<br>**说明**<br>动态图片（例如GIF图片）的总像素计算方式为`宽*高*图片帧数`；非动态图片（例如PNG图片）的总像素计算方式为`宽*高`。 |
| 缩放后限制 | 图片缩放 | 缩放后图片宽或高不能超过16,384 px，且总像素不能超过16,777,216 px。 |

## 操作方式

在OSS中，当您携带`?x-oss-process=image/resize,parame_value`参数时，OSS会实时处理该图片，返回处理后的结果。`image/resize`表示进行缩放处理；`parame`为图片缩放支持的参数，`value`为参数取值。对于参数的详细说明在下文 [参数说明](https://help.aliyun.com/zh/oss/user-guide/resize-images-4#section-vyx-j4n-vdb "") 中给出，且支持多个参数间的组合使用。

对于公共读的图片，您可以直接在图片URL后添加处理参数，以允许任何人永久匿名访问处理后的图片URL。如果您的图片为私有类型，您需要调用SDK携带签名信息或调用API处理图片。

公共读图片

私有图片

以下是公共读图片URL添加`?x-oss-process=image/resize,parame_value`参数的操作说明，您只需要根据您的业务需求将`parame_value`替换为具体的参数和值。

|     |     |
| --- | --- |
| **原始图片URL** | **添加处理参数后的图片URL** |
| [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p\_50](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p_50) |

您可以使用OSS SDK生成带有图片缩放参数的签名URL，以便允许获取该签名URL的用户临时访问处理后的图片，使用SDK为私有图片生成带`?x-oss-process=image/parame_value`参数的签名URL的示例如下：

Java

Python

PHP

Go

```java
package com.aliyun.oss.demo;
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.GeneratePresignedUrlRequest;
import java.net.URL;
import java.util.Date;

public class Demo {
    public static void main(String[] args) throws Throwable {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径。如果图片不在Bucket根目录，需携带图片完整路径，例如exampledir/exampleobject.jpg
        String objectName = "exampledir/exampleobject.png";
        // 填写Bucket所在地域。以华东1（杭州）为例，Region填写为cn-hangzhou。
        String region = "cn-hangzhou";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
                .endpoint(endpoint)
                .credentialsProvider(credentialsProvider)
                .clientConfiguration(clientBuilderConfiguration)
                .region(region)
                .build();

        try {
            // 图片缩放，parame_value需要替换为具体的参数和值，如“p_50”表示图片等比例缩小为之前的50%
            String style = "image/resize,parame_value";
            // 指定签名URL过期时间为3600秒)
            Date expiration = new Date(new Date().getTime() + 3600 );
            GeneratePresignedUrlRequest req = new GeneratePresignedUrlRequest(bucketName, objectName, HttpMethod.GET);
            req.setExpiration(expiration);
            req.setProcess(style);
            URL signedUrl = ossClient.generatePresignedUrl(req);
            System.out.println(signedUrl);
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

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuthV4(EnvironmentVariableCredentialsProvider())

# 填写Bucket名称
bucket = 'examplebucket'

# 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例
endpoint = 'https://oss-cn-hangzhou.aliyuncs.com'

# 填写阿里云通用Region ID
region = 'cn-hangzhou'
bucket = oss2.Bucket(auth, endpoint, bucket, region=region)

# 指定原图名称。如果图片不在Bucket根目录，需携带图片完整路径，例如exampledir/exampleobject.jpg
key = 'exampledir/exampleobject.png'

# 指定过期时间，单位秒
expire_time = 3600

# 图片缩放，parame_value需要替换为具体的参数和值，如“p_50”表示图片等比例缩小为之前的50%
image_process = 'image/resize,parame_value'

# 生成签名URL，带上图片处理参数
url = bucket.sign_url('GET', key, expire_time, params={'x-oss-process': image_process}, slash_safe=True)

# 打印签名URL
print(url)
```

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

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
$endpoint = "yourEndpoint";
// 填写Bucket名称，例如examplebucket。
$bucket= "examplebucket";
// 填写Object完整路径，例如exampledir/exampleobject.jpg。Object完整路径中不能包含Bucket名称。
$object = "exampledir/exampleobject.jpg";

$config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

// 生成一个带图片处理参数的签名的URL，有效期是3600秒，可以直接使用浏览器访问。
$timeout = 3600;

$options = array(
    // 图片缩放，parame_value需要替换为具体的参数和值，如“p_50”表示图片等比例缩小为之前的50%
    OssClient::OSS_PROCESS => "image/resize,parame_value");

$signedUrl = $ossClient->signUrl($bucket, $object, $timeout, "GET", $options);
print("rtmp url: \n" . $signedUrl);
```

```go
package main

import (
	"fmt"
	"os"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func HandleError(err error) {
	fmt.Println("Error:", err)
	os.Exit(-1)
}

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
		HandleError(err)
	}

	// 指定图片所在Bucket的名称，例如examplebucket。
	bucketName := "examplebucket"
	bucket, err := client.Bucket(bucketName)
	if err != nil {
		HandleError(err)
	}
	// 指定图片名称。如果图片不在Bucket根目录，需携带文件完整路径，例如exampledir/exampleobject.jpg。
	ossImageName := "exampledir/exampleobject.png"
	// 生成带签名的URL，并指定过期时间为3600s。（最长有效时间为32400秒）
	// 图片缩放，parame_value需要替换为具体的参数和值，如“p_50”表示图片等比例缩小为之前的50%
	signedURL, err := bucket.SignURL(ossImageName, oss.HTTPGet, 3600, oss.Process("image/resize,parame_value"))
	if err != nil {
		HandleError(err)
	} else {
		fmt.Println(signedURL)
	}
}
```

生成的签名URL示例如下：

```plaintext
https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampledir/exampleobject.png?x-oss-process=image%2Fresize%2Cp_50&x-oss-date=20241111T113707Z&x-oss-expires=3600&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI********************%2F20241111%2Fcn-hangzhou%2Foss%2Faliyun_v4_request&x-oss-signature=6fd07a2ba50bf6891474dc56aed976b556b6fbcd901cfd01bcde5399bf4802cb
```

如需使用其他SDK缩放图片的代码示例，请参见 [SDK简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

## 参数说明

操作名称：**resize**

### **等比例缩放**

您可以使用 `p` 参数指定图片等比例缩放的百分比。

| **参数** | **描述** | **取值** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **描述** | **取值** |
| p | 按百分比缩放图片。 | \[1,1000\]<br>小于100为缩小，大于100为放大。 |

**说明**

动图不支持此等比例缩放。

### 指定宽高缩放

您可以通过 `w` 和 `h` 参数指定宽度和高度，结合 `m` 参数来控制缩放模式，满足不同布局需求。如需控制缩放后的长边或短边，可使用 `l` 或 `s` 参数。当您想放大图片时，您需要增加`limit_0`参数。

| **参数** | **描述** | **取值** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **描述** | **取值** |
| w | 指定目标缩放图的宽度。 | \[1,16384\] |
| h | 指定目标缩放图的高度。 | \[1,16384\] |
| m | 指定缩放的模式。 | - **lfit（默认值）**：等比缩放至指定宽高区域内最大图形。<br>  <br>- mfit：等比缩放至覆盖指定宽高区域。<br>  <br>- fill：等比缩放至覆盖指定宽高区域并居中裁剪。<br>  <br>- pad：等比缩放至指定宽高内最大图形并填充颜色至指定尺寸。<br>  <br>- fixed：固定宽高，强制缩放。<br>  <br>关于按不同模式进行缩放后得到的图片说明，请参见 [缩放计算方式](https://help.aliyun.com/zh/oss/user-guide/resize-images-4#b3399c1514fei "")。<br>**说明**<br>当缩放模式设置为`m`模式下的任意值，并且指定了目标缩放图的`w`或`h`，则目标缩放图的`l`或`s`的设定将不会生效。 |
| l | 指定目标缩放图的最长边。<br>**说明**<br>长边即宽度或高度中较大的那一边。例如原图为100 px\*200 px，200那条是长边，100那条是短边。 | \[1,16384\] |
| s | 指定目标缩放图的最短边。 | \[1,16384\] |
| limit | 当目标图片分辨率大于原图分辨率时，设置是否进行缩放。<br>**重要**<br>目标缩放图比原图尺寸大时，默认返回原图。如果您想放大图片，您需要增加`limit_0`参数。 | - **1（默认值）**：返回按照原图分辨率转换的图片（可能和原图的体积不一样）。<br>  <br>- 0：按指定参数进行缩放。<br>  <br>**说明**<br>动图格式的图片只支持指定宽高缩小，不支持按等比例缩小，不支持放大。 |
| color | 当缩放模式选择为pad（缩放填充）时，可以设置填充的颜色。 | RGB颜色值，例如：000000表示黑色，FFFFFF表示白色。 <br>**默认值**：FFFFFF（白色） |

**说明**

- 若缩放时只指定宽度或者高度：

  - 缩放模式为lfit，mfit，fixed时，会按比例缩放图片。例如原图为256px\*144 px，将高缩放为100 px，则宽缩放为178px。

  - 缩放模式为pad，fill时，会将原图宽高按照指定值进行缩放。例如原图为256px\*144px，将高缩放为100 px，则宽也缩放为100 px。
- 当仅选择`l`或`s`进行指定时，图片将按指定的边进行缩放，而另一边则根据原图的比例自动调整，此时`m`参数的设置不起作用。

- 当同时设置了`l`和`s`参数时，图片的缩放会基于保持长宽比的原则进行，此时`m`参数将发挥作用。若未明确指定缩放模式，系统将采用默认的`lfit`方式处理。


## **缩放计算方式**

| **原图大小** | **指定缩放参数** | **缩放模式** | **缩放后大小** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **原图大小** | **指定缩放参数** | **缩放模式** | **缩放后大小** |
| 200 px\*100 px | 150 px\*80 px | **lfit（默认值）**<br>等比缩放，缩略图限制在指定w与h的矩形内的最大图片。 | 150 px\*75 px<br>![lfit](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4822359951/p137017.png) |
| **mfit**<br>等比缩放，缩略图为延伸出指定w与h的矩形框外的最小图片。 | 160 px\*80 px<br>![mfit](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4822359951/p137027.png) |
| **fill**<br>等比缩放，缩略图为延伸出指定w与h的矩形框外的最小图片，之后按照固定宽高进行裁剪。 | 150 px\*80 px<br>![fill](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4822359951/p137049.png) |
| **pad**<br>等比缩放，缩略图限制在指定w与h的矩形内的最大图片再按照固定宽高进行颜色填充。 | 150 px\*80 px<br>![pad](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4822359951/p137053.png) |
| **fixed**<br>按照固定宽高强制缩放，若宽高与原图宽高比例不同，则会导致图片变形。 | 150 px\*80 px<br>![fixed](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4822359951/p137056.png) |

**说明**

当缩放模式指定为lfit或mfit时，如果等比为小数，则四舍五入保留整数。

## 使用示例

### 等比例缩小

在图片URL末尾添加`?x-oss-process=image/resize,p_{percentage}`时，OSS会实时处理该图片，并按指定的百分比进行等比例缩小，返回处理后的结果。`image/resize`表示进行缩放处理，`p`表示按百分比缩放。`p`的取值范围为`[1, 100]`时表示按百分比缩小，`p`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,p_50`将图片缩小至原尺寸的50%的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p\_50](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p_50) |
| 图片尺寸 | 2500 x 1875 px | 1250 x 938 px |

### 等比例放大

在图片URL末尾添加`?x-oss-process=image/resize,p_{percentage}`时，OSS会实时处理该图片，并按指定的百分比进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`p`表示按百分比缩放。`p`的取值范围为`[100, 1000]`时，表示按百分比放大。`p`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,p_120`将图片放大至原尺寸的120%的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p\_120](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,p_120) |
| 图片尺寸 | 2500 x 1875 px | 3000 x 2250 px |

### 宽度固定，高度自适应缩小

在图片URL末尾添加`?x-oss-process=image/resize,w_{width}`时，OSS实时处理该图片，并根据指定的宽度进行等比例缩小，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`w`表示期望的图片宽度。`w`的取值范围为`[1,16384]`。`w`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,w_200`将图片宽度固定为200像素，高度自适应进行缩小的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,w\_200](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,w_200) |
| 图片尺寸 | 2500 x 1875 px | 200 x 150 px |

### 宽度固定，高度自适应放大

在图片URL末尾添加`?x-oss-process=image/resize,w_{width}`时，OSS实时处理该图片，并根据指定的宽度进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`w`表示期望的图片宽度。`w`的取值范围为`[1,16384]`。`w`的取值必须为正整数。

**重要**

由于当目标缩放图比原图尺寸大时，默认返回原图。如果您想放大图片，您需要增加`limit_0`参数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,w_3000,limit_0`将图片宽度固定3000像素，高度自适应进行放大的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,w\_3000,limit\_0](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,w_3000,limit_0) |
| 图片尺寸 | 2500 x 1875 px | 3000 x 2250 px |

### 高度固定，宽度自适应缩小

在图片URL末尾添加`?x-oss-process=image/resize,h_{height}`时，OSS实时处理该图片，并根据指定的高度进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`h`表示期望的图片高度。`h`的取值范围为`[1,16384]`。`h`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,h_100`将图片高度固定为100像素，宽度自适应进行缩小的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h\_100](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h_100) |
| 图片尺寸 | 2500 x 1875 px | 133 x 100 px |

### 高度固定，宽度自适应放大

在图片URL末尾添加`?x-oss-process=image/resize,h_{height}`时，OSS将实时处理该图片，并根据指定的高度进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`h`表示期望的图片高度。`h`的取值范围为`[1,16384]`。`h`的取值必须为正整数。

**重要**

由于当目标缩放图比原图尺寸大时，默认返回原图。如果您想放大图片，您需要增加`limit_0`参数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,h_2000,limit_0`将图片高度固定为2000像素，宽度自适应进行缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h\_2000,limit\_0](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h_2000,limit_0) |
| 图片尺寸 | 2500 x 1875 px | 2667 x 2000 px |

### 长边固定，短边自适应缩放

按长边缩放，图片将按指定的长边进行缩放，而短边则根据原图的比例自动调整，此时缩放模式`m`参数的设置不起作用。

在图片URL末尾添加`image/resize,l_{length}`时，OSS将实时处理该图片，并根据长边进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`l`表示长边，`l`的取值范围为`[1,16384]`,`l`的取值必须为正整数。

**重要**

由于当目标缩放图比原图尺寸大时，默认返回原图。如果您想放大图片，您需要增加`limit_0`参数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,l_200`将长边固定为200，短边自适应进行缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,l\_200](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,l_200) |
| 图片尺寸 | 2500 x 1875 px | 200 x 150 px |

### 短边固定，长边自适应缩放

图片将按指定的短边进行缩放，而另一边则根据原图的比例自动调整，此时缩放模式`m`参数的设置不起作用。

在图片URL末尾添加`image/resize,s_{length}`时，OSS将实时处理该图片，并根据短边进行等比例缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`s`表示短边，`s`的取值范围为`[1,16384]`,`s`的取值必须为正整数。

**重要**

由于当目标缩放图比原图尺寸大时，默认返回原图。如果您想放大图片，您需要增加`limit_0`参数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,s_200,limit_0`将短边固定为200，长边自适应进行缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | 图片处理URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,s\_200](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,s_200) |
| 图片尺寸 | 2500 x 1875 px | 267 x 200 px |

### 固定宽高，缩略填充

固定宽高，缩略填充在保持图像比例的同时将图像调整到指定的宽度和高度。

在图片URL末尾添加`image/resize,m_pad,w_{width},h_{height},color_{RGB}`时，OSS将实时处理该图片，并返回处理后的结果。其中，`image/resize`表示进行缩放处理，`m_pad`表示图片缩放为指定w与h的矩形内的最大图片，`color`表示指定居中填充空白部分的颜色，若不设置该参数，默认用白色填充。`w`表示期望的图片宽度，`h`表示期望的图片高度。`w`和`h`的取值范围都为`[1,16384]`。`w`和`h`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,m_pad,w_100,h_100`将图片宽度和高度都固定为100像素进行缩略填充缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m\_pad,w\_100,h\_100](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m_pad,w_100,h_100) |
| 图片尺寸 | 2500 x 1875 px | 100 x 100 px |

以下是使用`?x-oss-process=image/resize,m_pad,w_100,h_100,color_FF0000`将图片宽度和高度都固定为100像素，设置填充颜色为红色进行缩略填充缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m\_pad,w\_100,h\_100,color\_FF0000](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m_pad,w_100,h_100,color_FF0000) |
| 图片尺寸 | 2500 x 1875 px | 100 x 100 px |

### 固定宽高，居中裁剪

固定宽高，居中裁剪在原始图像的宽高比与目标尺寸的宽高比不一致时会根据目标尺寸的宽度或高度进行等比例缩放，并在缩放后将图像居中裁剪以达到固定的宽高比。

在图片URL末尾添加`image/resize,m_fill,w_{width},h_{height}`时，OSS将实时处理该图片，并根据指定的宽度和高度进行缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`m_fill`表示图片等比缩放为延伸出指定w与h的矩形框外的最小图片，超出的部分进行居中裁剪。`w`表示期望的图片宽度，`h`表示期望的图片高度。`w`和`h`的取值范围都为`[1,16384]`。`w`和`h`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,m_fill,w_100,h_100`将图片宽度和高度都固定为100像素进行居中裁剪缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m\_fill,w\_100,h\_100](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m_fill,w_100,h_100) |
| 图片尺寸 | 2500 x 1875 px | 100 x 100 px |

### 强制宽高缩放

固定宽高，强制缩放用于将图像调整为指定的宽度和高度，而不考虑原始图像的宽高比。这种处理方式可能会导致图像变形，因为图像会被拉伸或缩放以适应新的尺寸。

在图片URL末尾添加`image/resize,m_fixed,w_{width},h_{height}`时，OSS将实时处理该图片，并根据指定的宽度和高度进行强制缩放，返回处理后的结果。其中，`image/resize`表示进行缩放处理，`m_fixed`表示图片。`w`表示期望的图片宽度，`h`表示期望的图片高度。`w`和`h`的取值范围都为`[1,16384]`。`w`和`h`的取值必须为正整数。

#### 效果示例

以下是使用`?x-oss-process=image/resize,m_fixed,w_100,h_100`将图片宽度和高度都固定为100像素进行强制宽高缩放的示例：

|     |     |     |
| --- | --- | --- |
| **对比项目** | **原图** | **处理后的图片** |
| 图片预览 | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |
| URL | 原图URL: [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg) | [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m\_fixed,w\_100,h\_100](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,m_fixed,w_100,h_100) |
| 图片尺寸 | 2500 x 1875 px | 100 x 100 px |

## 计费说明

使用图片缩放时，会产生如下费用。有关计费项的定价详情，请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

- 图片处理费用：未超出免费额度时，不产生费用；超出免费额度后，按处理的原图实际大小计费。计费详情，请参见 [数据处理费用](https://help.aliyun.com/zh/oss/data-processing-fees#concept-2558464 "")。

- | **API** | **计费项** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **API** | **计费项** | **说明** |
| GetObject | GET 类型请求 | 根据成功的请求次数计算请求费用。 |
| 外网流出流量费用 | 如果是通过外网Endpoint（示例值oss-cn-hangzhou.aliyuncs.com）或者传输加速Endpoint（示例值oss-accelerate.aliyuncs.com）调用GetObject接口时，会产生外网流出流量费用，根据数据容量大小计费。 |
| 低频访问数据取回容量 | 如果取回的数据是低频访问数据，会产生低频访问数据取回容量的费用，按数据取回量计费。 |
| 归档直读数据取回容量 | 如果读取的是归档的Object且Bucket开启了归档直读，会产生归档直读数据取回容量费用，根据取回的数据容量大小计费。 |
| 传输加速 | 如果开启了传输加速功能且使用传输加速域名访问您的Bucket会产生传输加速费用，根据数据容量大小计费。 |


## **相关API**

如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。关于公共请求头Authorization的计算方法，请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/recommend-to-use-signature-version-4 "")。

您可以通过在GetObject接口中添加图片缩放参数的方式来处理图片。更多信息，请参见 [GetObject](https://help.aliyun.com/zh/oss/developer-reference/getobject#reference-ccf-rgd-5db "")。

```xml
GET /oss.jpg?x-oss-process=image/resize,p_50 HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Fri, 28 Oct 2022 06:40:10 GMT
Authorization: SignatureValue
```

## 常见问题

### 图片缩放的参数不生效怎么办？

请检查是否正在使用CDN域名，并确认是否关闭忽略参数缓存功能。若通过CDN启用了过滤参数选项，则文件URL请求中的所有查询参数（位于问号“?”之后）将被移除，导致直接访问到未带参数的原始文件，如example.jpg。为确保正确缓存与访问请关闭CDN的忽略参数缓存功能，具体操作可参考 [忽略参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters#task-187634 "")。然而，关闭此功能意味着带有不同参数的URL将被视为独立的请求，可能导致回源至OSS的频率上升，影响缓存效率。

### 按宽高放大图片不生效怎么办？

按宽高放大图片时，需要设置limit参数为0，否则放大不生效。

例如：在以下图片中，将图片高度由原来的1875 px放大为2000 px。

[https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h\_2000,limit\_0](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example1.jpg?x-oss-process=image/resize,h_2000,limit_0)

### **如何持久化存储处理后的图片？**

OSS会根据请求的参数实时生成图片，默认不保存处理后的图片。对于经常需要展示相同处理结果（例如缩略图、裁剪图或格式转换后的图片）的应用场景，您可以使用OSS图片处理持久化功能在图片处理的请求中添加转存参数，并将处理后的图片保存至指定的Bucket。具体操作，请参见 [图片处理持久化](https://help.aliyun.com/zh/oss/user-guide/save-processed-images#concept-bf1-ssc-wdb "")。

### 缩放后的图片读写权限为私有，如何正常访问？

必须对图片文件URL完成签名操作后才能正常访问。具体操作请参见 [上传Object后如何获取访问URL](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects#concept-39607-zh "")。

### 图片缩放是否产生图片数据处理费用？

图片缩放会产生图片数据处理费用，按处理的原图实际大小计费。图片缩放每月提供10TB的免费额度，超出部分按照0.025元/GB进行计费。

### 请求缩放后的图片产生的下行流量是按原图还是缩放后的图片计算？

请求缩放后的图片产生的下行流量费用按照缩放后的流量计算。例如原图为20 MB，缩放后大小为2 MB，图片产生的流量按照2 MB计算。

### 原图WebP解码异常怎么办？

WebP解码异常，可能是因为图片为动图，可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)开通WebP动图解码功能。