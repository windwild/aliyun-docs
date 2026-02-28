### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)[OSS Go SDK V1](https://help.aliyun.com/zh/oss/developer-reference/go-sdk-v1/)[数据安全（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/data-security/)数据校验（Go SDK V1）

# 数据校验（Go SDK V1）

更新时间：2025-11-26 20:44:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：客户端加密（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/client-side-encryption-2)[下一篇：数据复制（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/data-replication)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

MD5校验

CRC64校验

OSS提供基于MD5和CRC64的数据校验，确保上传、下载和拷贝文件（Object）过程中的数据完整性。

## 注意事项

- 本文以华东1（杭州）外网Endpoint为例。如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint。关于OSS支持的Region与Endpoint的对应关系，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

- 本文以从环境变量读取访问凭证为例。如何配置访问凭证，请参见 [配置访问凭证（Go SDK V1）](https://help.aliyun.com/zh/oss/go-configure-access-credentials "")。

- 本文以OSS域名新建OSSClient为例。如果您希望通过自定义域名、STS等方式新建OSSClient，请参见 [配置客户端（Go SDK V1）](https://help.aliyun.com/zh/oss/initialization-9#concept-52931-zh "")。


## MD5校验

当上传文件时，如果指定了`Content-MD5`，OSS将根据接收到的数据重新计算MD5值。若OSS计算出的MD5值与上传时提供的值不符，将返回 `InvalidDigest`异常，以此确保数据的完整性和准确性。遇到`InvalidDigest`异常时，建议检查文件是否在传输过程中发生改变或损坏，并重新上传文件。

**说明**

putObject、getObject、appendObject、postObject、uploadPart支持MD5校验。

以下代码用于上传文件时进行MD5校验：

```go
package main

import (
	"crypto/md5"
	"encoding/base64"
	"log"
	"strings"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

// 计算给定内容的MD5校验码
func calculateMD5(content string) string {
	h := md5.New()
	h.Write([]byte(content))
	return base64.StdEncoding.EncodeToString(h.Sum(nil))
}

func main() {
	// 从环境变量中加载OSS访问凭证
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		log.Fatalf("Failed to create credentials provider: %v", err)
	}

	// 替换为实际的Bucket名称
	bucketName := "yourBucketName"

	// 创建OSS客户端
	// yourEndpoint填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
	// yourRegion填写Bucket所在地域，以华东1（杭州）为例，填写为cn-hangzhou。其它Region请按实际情况填写。
	clientOptions := []oss.ClientOption{oss.SetCredentialsProvider(&provider)}
	clientOptions = append(clientOptions, oss.Region("yourRegion"))
	// 设置签名版本
	clientOptions = append(clientOptions, oss.AuthVersion(oss.AuthV4))
	client, err := oss.New("yourEndpoint", "", "", clientOptions...)
	if err != nil {
		log.Fatalf("Failed to create OSS client: %v", err)
	}

	// 获取指定的Bucket
	bucket, err := client.Bucket(bucketName)
	if err != nil {
		log.Fatalf("Failed to get bucket %s: %v", bucketName, err)
	}

	// 要上传的内容
	content := "yourObjectValue"   // 替换为实际要上传的内容
	objectName := "yourObjectName" // 替换为实际的对象名称

	// 计算内容的MD5校验码
	contentMD5 := calculateMD5(content)

	// 上传文件到OSS
	err = bucket.PutObject(objectName, strings.NewReader(content), oss.ContentMD5(contentMD5))
	if err != nil {
		log.Fatalf("Failed to upload object %s: %v", objectName, err)
	}

	log.Printf("Object '%s' uploaded successfully.", objectName)
}
```

## CRC64校验

**说明**

**CRC64 校验注意事项：**

- putObject、getObject、appendObject、uploadPart支持CRC64校验。

- 上传、下载和拷贝文件时，默认启用 CRC 数据校验。如果客户端计算的 CRC 值与服务端返回的 CRC 值不一致，将返回错误。

- 范围下载不支持 CRC64 校验。

- 启用 CRC64 校验会占用一定的 CPU 资源，对上传、下载速度均会有影响。


以下代码用于追加上传文件时进行CRC64数据完整性校验：

```go
package main

import (
	"log"
	"strings"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func main() {
	// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		log.Fatalf("Failed to create credentials provider: %v", err)
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
		log.Fatalf("Failed to create OSS client: %v", err)
	}

	// yourBucketName填写存储空间名称。
	bucketName := "yourBucketName" // 替换为实际的Bucket名称
	bucket, err := client.Bucket(bucketName)
	if err != nil {
		log.Fatalf("Failed to get bucket %s: %v", bucketName, err)
	}

	// 定义要追加的Object名称
	objectName := "yourObjectName" // 替换为实际的Object名称

	// 第一次追加的位置是0，返回值为下一次追加的位置。后续追加的位置是追加前文件的长度。
	request := &oss.AppendObjectRequest{
		ObjectKey: objectName,
		Reader:    strings.NewReader("YourObjectAppendValue1"),
		Position:  0,
	}

	// 第一次追加时，初始化crc的值为0。
	options := []oss.Option{oss.InitCRC(0)}
	result, err := bucket.DoAppendObject(request, options)
	if err != nil {
		log.Fatalf("Failed to append object %s for the first time: %v", objectName, err)
	}
	log.Printf("First append successful. Next position: %d", result.NextPosition)

	// 第二次追加的位置从第一次的返回长度开始。
	request = &oss.AppendObjectRequest{
		ObjectKey: objectName,
		Reader:    strings.NewReader("YourObjectAppendValue2"),
		Position:  result.NextPosition,
	}

	// 第二次追加的初始化crc值为第一次返回值。
	options = []oss.Option{oss.InitCRC(result.CRC)}
	result, err = bucket.DoAppendObject(request, options)
	if err != nil {
		log.Fatalf("Failed to append object %s for the second time: %v", objectName, err)
	}
	log.Printf("Second append successful. Next position: %d", result.NextPosition)

	// 您可以进行多次AppendObject操作。
	log.Printf("All appends completed successfully.")
}
```