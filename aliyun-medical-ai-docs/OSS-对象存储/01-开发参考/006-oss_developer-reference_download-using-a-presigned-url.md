### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)[OSS Java SDK V1](https://help.aliyun.com/zh/oss/developer-reference/oss-java-sdk/)[对象/文件（Java SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/objects-8/)[下载文件（Java SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/overview-10/)使用预签名URL下载（Java SDK V1）

# 使用预签名URL下载（Java SDK V1）

更新时间：2025-11-25 03:29:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：限定条件下载（Java SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/conditional-download-2)[下一篇：进度条（Java SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/progress-bar)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

使用过程

代码示例

其他场景

生成指定版本的文件的GET方法的预签名URL

使用自定义域名生成用于下载文件的预签名URL

生成强制下载的预签名URL

相关文档

默认情况下，OSS Bucket中的文件是私有的，仅文件拥有者可访问。您可以使用OSS Java SDK生成带有过期时间的GET方法预签名URL，以允许他人临时下载文件。在有效期内可多次访问，超期后需重新生成。

## 注意事项

- 本文以华东1（杭州）外网Endpoint为例。如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint。关于OSS支持的Region与Endpoint的对应关系，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

- 本文以从环境变量读取访问凭证为例。如何配置访问凭证，请参见 [Java配置访问凭证](https://help.aliyun.com/zh/oss/developer-reference/oss-java-configure-access-credentials#main-2350752 "")。

- 本文以OSS域名新建OSSClient为例。如果您希望通过自定义域名、STS等方式新建OSSClient，请参见 [常见场景配置示例](https://help.aliyun.com/zh/oss/developer-reference/initialization-3#section-ngr-tjb-kfb "")。

- 预签名URL无需权限即可生成，但仅当您拥有`oss:GetObject`权限时，第三方才能通过该预签名URL成功下载文件。具体授权操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-flo-x8e-e94 "")。

- 本文以V4预签名URL为例，有效期最大为7天。更多信息，请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls "")。


## **使用过程**

使用预签名URL下载文件的过程如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4539504671/CAEQURiBgMC39Z3hqBkiIGMwZTFjM2JlMjk3ZDQ2OTdhOTg3MWM1MzZlY2YwOWY34751395_20241112152822.507.svg)

## **代码示例**

1. 文件拥有者生成GET方法的预签名URL。















```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;

import java.net.URL;
import java.util.Date;

public class Demo {
       public static void main(String[] args) throws Throwable {
           // 以华东1（杭州）的外网Endpoint为例，其它Region请按实际情况填写。
           String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
           // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
           EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
           // 填写Bucket名称，例如examplebucket。
           String bucketName = "examplebucket";
           // 填写Object完整路径，例如exampleobject.txt。Object完整路径中不能包含Bucket名称。
           String objectName = "exampleobject.txt";
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
               // 设置预签名URL过期时间，单位为毫秒。本示例以设置过期时间为1小时为例。
               Date expiration = new Date(new Date().getTime() + 3600 * 1000L);
               // 生成以GET方法访问的预签名URL。本示例没有额外请求头，其他人可以直接通过浏览器访问相关内容。
               URL url = ossClient.generatePresignedUrl(bucketName, objectName, expiration);
               System.out.println(url);
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

2. 其他人使用GET方法的预签名URL下载文件。






curl



Java



Node.js



Python



Go



JavaScript



Android-Java



Objective-C

































```curl
curl -SO "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************"
```



















```java
import java.io.BufferedInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Demo {
       public static void main(String[] args) {
           // 替换为生成的GET方法的预签名URL。
           String fileURL = "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************";
           // 填写文件保存的目标路径，包括文件名和扩展名。
           String savePath = "C:/downloads/myfile.txt";

           try {
               downloadFile(fileURL, savePath);
               System.out.println("Download completed!");
           } catch (IOException e) {
               System.err.println("Error during download: " + e.getMessage());
           }
       }

       private static void downloadFile(String fileURL, String savePath) throws IOException {
           URL url = new URL(fileURL);
           HttpURLConnection httpConn = (HttpURLConnection) url.openConnection();
           httpConn.setRequestMethod("GET");

           // 检查响应代码
           int responseCode = httpConn.getResponseCode();
           if (responseCode == HttpURLConnection.HTTP_OK) {
               // 输入流
               InputStream inputStream = new BufferedInputStream(httpConn.getInputStream());
               // 输出流
               FileOutputStream outputStream = new FileOutputStream(savePath);

               byte[] buffer = new byte[4096]; // 缓冲区
               int bytesRead;
               while ((bytesRead = inputStream.read(buffer)) != -1) {
                   outputStream.write(buffer, 0, bytesRead);
               }

               outputStream.close();
               inputStream.close();
           } else {
               System.out.println("No file to download. Server replied HTTP code: " + responseCode);
           }
           httpConn.disconnect();
       }
}
```



















```nodejs
const https = require('https');
const fs = require('fs');

const fileURL = "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************";
const savePath = "C:/downloads/myfile.txt";

https.get(fileURL, (response) => {
       if (response.statusCode === 200) {
           const fileStream = fs.createWriteStream(savePath);
           response.pipe(fileStream);

           fileStream.on('finish', () => {
               fileStream.close();
               console.log("Download completed!");
           });
       } else {
           console.error(`Download failed. Server responded with code: ${response.statusCode}`);
       }
}).on('error', (err) => {
       console.error("Error during download:", err.message);
});
```



















```python
import requests

file_url = "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************"
save_path = "C:/downloads/myfile.txt"

try:
       response = requests.get(file_url, stream=True)
       if response.status_code == 200:
           with open(save_path, 'wb') as f:
               for chunk in response.iter_content(4096):
                   f.write(chunk)
           print("Download completed!")
       else:
           print(f"No file to download. Server replied HTTP code: {response.status_code}")
except Exception as e:
       print("Error during download:", e)
```



















```go
package main

import (
       "io"
       "net/http"
       "os"
)

func main() {
       fileURL := "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************"
       savePath := "C:/downloads/myfile.txt"

       response, err := http.Get(fileURL)
       if err != nil {
           panic(err)
       }
       defer response.Body.Close()

       if response.StatusCode == http.StatusOK {
           outFile, err := os.Create(savePath)
           if err != nil {
               panic(err)
           }
           defer outFile.Close()

           _, err = io.Copy(outFile, response.Body)
           if err != nil {
               panic(err)
           }
           println("Download completed!")
       } else {
           println("No file to download. Server replied HTTP code:", response.StatusCode)
       }
}
```



















```javascript
const fileURL = "https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************";
const savePath = "C:/downloads/myfile.txt"; // 文件将在下载时使用的文件名

fetch(fileURL)
       .then(response => {
           if (!response.ok) {
               throw new Error(`Server replied HTTP code: ${response.status}`);
           }
           return response.blob(); // 将响应转换为 blob
       })
       .then(blob => {
           const link = document.createElement('a');
           link.href = window.URL.createObjectURL(blob);
           link.download = savePath; // 设置下载文件的名字
           document.body.appendChild(link); // 此步骤确保链接存在于文档中
           link.click(); // 模拟点击下载链接
           link.remove(); // 完成后移除链接
           console.log("Download completed!");
       })
       .catch(error => {
           console.error("Error during download:", error);
       });
```



















```androidjava
import android.os.AsyncTask;
import android.os.Environment;
import java.io.BufferedInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class DownloadTask extends AsyncTask<String, String, String> {
       @Override
       protected String doInBackground(String... params) {
           String fileURL = params[0];
           String savePath = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS) + "/myfile.txt"; // 修改后的保存路径
           try {
               URL url = new URL(fileURL);
               HttpURLConnection httpConn = (HttpURLConnection) url.openConnection();
               httpConn.setRequestMethod("GET");
               int responseCode = httpConn.getResponseCode();
               if (responseCode == HttpURLConnection.HTTP_OK) {
                   InputStream inputStream = new BufferedInputStream(httpConn.getInputStream());
                   FileOutputStream outputStream = new FileOutputStream(savePath);
                   byte[] buffer = new byte[4096];
                   int bytesRead;
                   while ((bytesRead = inputStream.read(buffer)) != -1) {
                       outputStream.write(buffer, 0, bytesRead);
                   }
                   outputStream.close();
                   inputStream.close();
                   return "Download completed!";
               } else {
                   return "No file to download. Server replied HTTP code: " + responseCode;
               }
           } catch (Exception e) {
               return "Error during download: " + e.getMessage();
           }
       }
}
```



















```objectc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
       @autoreleasepool {
           // 定义文件 URL 和保存路径（修改为有效的路径）
           NSString *fileURL = @"https://examplebucket.oss-cn-hangzhou.aliyuncs.com/exampleobject.txt?x-oss-date=20241112T092756Z&x-oss-expires=3599&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-credential=LTAI****************/20241112/cn-hangzhou/oss/aliyun_v4_request&x-oss-signature=ed5a******************************************************";
           NSString *savePath = @"/Users/your_username/Desktop/myfile.txt"; // 请替换为您的用户名

           // 创建 URL 对象
           NSURL *url = [NSURL URLWithString:fileURL];

           // 创建下载任务
           NSURLSessionDataTask *task = [[NSURLSession sharedSession] dataTaskWithURL:url completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {\
               // 错误处理\
               if (error) {\
                   NSLog(@"Error during download: %@", error.localizedDescription);\
                   return;\
               }\
\
               // 检查数据\
               if (!data) {\
                   NSLog(@"No data received.");\
                   return;\
               }\
\
               // 保存文件\
               NSError *writeError = nil;\
               BOOL success = [data writeToURL:[NSURL fileURLWithPath:savePath] options:NSDataWritingAtomic error:&writeError];\
               if (success) {\
                   NSLog(@"Download completed!");\
               } else {\
                   NSLog(@"Error saving file: %@", writeError.localizedDescription);\
               }\
           }];

           // 启动任务
           [task resume];

           // 让主线程继续运行以便异步请求能够完成
           [[NSRunLoop currentRunLoop] run];
       }
       return 0;
}
```


## **其他场景**

### 生成指定版本的文件的GET方法的预签名URL

以下代码示例在生成GET方法的预签名URL时，指定了文件的版本，以允许他人下载指定版本的文件。

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.GeneratePresignedUrlRequest;
import java.net.URL;
import java.util.*;
import java.util.Date;

public class Demo {
    public static void main(String[] args) throws Throwable {
        // 以华东1（杭州）的外网Endpoint为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
	// 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径，例如exampleobject.txt。Object完整路径中不能包含Bucket名称。
        String objectName = "exampleobject.txt";
        // 填写Object的versionId。
        String versionId = "CAEQARiBgID8rumR2hYiIGUyOTAyZGY2MzU5MjQ5ZjlhYzQzZjNlYTAyZDE3****";
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
            // 创建请求。
            GeneratePresignedUrlRequest generatePresignedUrlRequest = new GeneratePresignedUrlRequest(bucketName, objectName);
            // 设置HttpMethod为GET。
            generatePresignedUrlRequest.setMethod(HttpMethod.GET);
            // 设置预签名URL过期时间，单位为毫秒。本示例以设置过期时间为1小时为例。
            Date expiration = new Date(new Date().getTime() + 3600 * 1000L);
            generatePresignedUrlRequest.setExpiration(expiration);
            // Object的versionId。
            Map<String, String> queryParam = new HashMap<String, String>();
            queryParam.put("versionId", versionId);
            generatePresignedUrlRequest.setQueryParameter(queryParam);
            // 生成预签名URL。
            URL url = ossClient.generatePresignedUrl(generatePresignedUrlRequest);
            System.out.println(url);
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

### **使用自定义域名生成用于下载文件的** 预 **签名URL**

以下代码示例在生成GET方法的预签名URL时，使用了自定义域名。

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.GeneratePresignedUrlRequest;

import java.net.URL;
import java.util.Date;

public class Demo {
    public static void main(String[] args) throws Throwable {
        // yourCustomEndpoint请填写您的自定义域名。例如http://static.example.com。
        String endpoint = "yourCustomEndpoint";
        // 请填写您存储空间所在的Region信息，例如cn-hangzhou
        String region = "cn-hangzhou";
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径，例如exampleobject.txt。Object完整路径中不能包含Bucket名称。
        String objectName = "exampleobject.txt";

        // 从环境变量中获取访问凭证。运行本代码示例之前，请先配置环境变量
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        // 请注意，设置true开启CNAME选项
        clientBuilderConfiguration.setSupportCname(true);
        // 显式声明使用 V4 签名算法
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
                .endpoint(endpoint)
                .credentialsProvider(credentialsProvider)
                .clientConfiguration(clientBuilderConfiguration)
                .region(region)
                .build();

        try {
            // 指定生成的预签名URL过期时间，单位为毫秒。本示例以设置过期时间为1小时为例。
            Date expiration = new Date(new Date().getTime() + 3600 * 1000L);

            // 生成预签名URL。
            GeneratePresignedUrlRequest request = new GeneratePresignedUrlRequest(bucketName, objectName, HttpMethod.GET);

            // 设置过期时间。
            request.setExpiration(expiration);

            // 通过HTTP GET请求生成预签名URL。
            URL signedUrl = ossClient.generatePresignedUrl(request);
            // 打印预签名URL。
            System.out.println("signed url for getObject: " + signedUrl);
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

### **生成强制下载的预签名URL**

如果您使用自定义域名访问OSS，或开通OSS的时间早于2022年10月9日00:00，URL访问默认会以预览方式呈现。若需强制下载效果，可在响应头中添加 Content-Disposition: attachment。

以下示例展示了使用自定义域名时的设置强制下载，OSS默认域名同样适用。

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.CredentialsProviderFactory;
import com.aliyun.oss.common.auth.EnvironmentVariableCredentialsProvider;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.GeneratePresignedUrlRequest;

import java.net.URL;
import java.net.URLEncoder;
import java.util.Date;

public class Demo {
    public static void main(String[] args) throws Throwable {
        // 请填写您的自定义域名。例如http://static.example.com。
        String endpoint = "http://static.example.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();

        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径，例如exampleobject.txt。Object完整路径中不能包含Bucket名称。
        String objectName = "exampleobject.txt";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        String region = "cn-hangzhou";
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        // 请注意，若您使用自定义域名，需设置CNAME为true。
        clientBuilderConfiguration.setSupportCname(true);

        //设置V4签名算法
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
                .endpoint(endpoint)
                .credentialsProvider(credentialsProvider)
                .clientConfiguration(clientBuilderConfiguration)
                .region(region)
                .build();

        URL signedUrl = null;
        try {
            // 指定生成的预签名URL过期时间，单位为毫秒。本示例以设置过期时间为1小时为例。
            Date expiration = new Date(new Date().getTime() + 3600 * 1000L);

            // 定义客户端下载时显示的文件名，此处以"homework.txt"为例。
            String filename = "homework.txt";

            // 生成预签名URL。
            GeneratePresignedUrlRequest request = new GeneratePresignedUrlRequest(bucketName, objectName, HttpMethod.GET);

            // 设置下载行为（强制下载而非预览）及文件名
            request.getResponseHeaders().setContentDisposition("attachment;filename=" + URLEncoder.encode(filename,"UTF-8"));

            // 设置过期时间。
            request.setExpiration(expiration);

            // 通过HTTP GET请求生成预签名URL。
            signedUrl = ossClient.generatePresignedUrl(request);
            // 打印预签名URL。
            System.out.println("signed url for getObject: " + signedUrl);
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
        }
    }

}
```

## 相关文档

- 关于使用预签名URL下载文件的完整示例代码，请参见 [GitHub示例](https://github.com/aliyun/aliyun-oss-java-sdk/blob/master/src/samples/SignV4Sample.java)。

- 关于使用预签名URL下载文件的API接口说明，请参见 [GeneratePresignedUrlRequest](https://javadoc.io/doc/com.aliyun.oss/aliyun-sdk-oss/3.14.0/com/aliyun/oss/model/GeneratePresignedUrlRequest.html)。