### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Object操作](https://help.aliyun.com/zh/oss/developer-reference/object-operations/)[基础操作](https://help.aliyun.com/zh/oss/developer-reference/basic-operations-1/)Callback

# Callback

更新时间：2025-09-19 03:36:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PostObject](https://help.aliyun.com/zh/oss/developer-reference/postobject)[下一篇：RestoreObject](https://help.aliyun.com/zh/oss/developer-reference/restoreobject)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

回调流程概览

开发实现指南

客户端实现

服务端实现

建议配置

验证请求签名确保安全

callback参数详情

callbackBody支持的系统参数

SDK

错误排查

常见问题

OSS上传文件失败后是否会发送回调通知给应用服务器？

报错Response body is not valid json format.如何处理？

OSS支持在文件上传后自动触发回调，通知应用服务器执行后续操作。

## **使用限制**

- 地域限制

华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北 3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华南1（深圳）、华南2（河源）、华南3（广州）、西南1（成都）、中国香港、美国（硅谷）、美国（弗吉尼亚）、日本（东京）、新加坡、马来西亚（吉隆坡）、印度尼西亚（雅加达）、菲律宾（马尼拉）、德国（法兰克福）、英国（伦敦）、阿联酋（迪拜）地域支持设置Callback。

- 回调行为说明

  - 回调请求必须在5秒内响应，超时将视为失败。

  - 回调失败不影响文件上传成功。

  - 回调失败不会自动重试。
- 接口支持

[PutObject](https://help.aliyun.com/zh/oss/developer-reference/putobject#reference-l5p-ftw-tdb "")、 [PostObject](https://help.aliyun.com/zh/oss/developer-reference/postobject#reference-smp-nsw-wdb "")、 [CompleteMultipartUpload](https://help.aliyun.com/zh/oss/developer-reference/completemultipartupload#reference-lq1-dtx-wdb "") 接口支持设置 Callback。V2 SDK 基于以上基础接口封装的文件上传管理器、预签名 URL 也支持设置 Callback。


## **回调流程概览**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8637628571/CAEQVRiBgMCfpe6JshkiIDI5MjRmMzQ1MDg1ZjRlYmM4MzRjMjFjOTc3OTJmZjA33963382_20230830144006.372.svg)

OSS 回调具体步骤如下：

1. **客户端上传文件（附带回调参数）**

上传文件时，客户端需要携带 Callback 参数，指定回调服务器的地址和回调内容。若需要传递自定义变量，还可以选择附加callback-var参数。

2. **OSS 存储文件并发送回调请求**

文件上传成功后，OSS 以 POST 方式向回调 URL 发送请求，包含文件信息（如 bucket、object、size、ETag等）及自定义参数。

3. **服务器处理回调并返回响应**

服务器接收回调请求后，验证请求签名（可选）以确保安全，5 秒内完成处理并返回 JSON 响应。HTTP 状态码 200 表示成功，非 200 视为回调失败。

4. **OSS 返回上传结果**

在回调响应成功后，OSS会根据应用服务器的返回结果向客户端提供最终处理结果。


## **开发实现指南**

上传回调的调试包含两部分：客户端上传和服务端回调处理。建议先调试客户端上传部分，再调试应用服务器部分，两部分均调试完成后，再进行完整的联调验证。

### **客户端实现**

> 以下内容主要说明上传回调参数的构造逻辑与处理流程。如需快速实现上传回调功能，建议参考 [SDK](https://help.aliyun.com/zh/oss/developer-reference/callback#34a8c03254bun "") 提供的示例代码。

为了让 OSS 在文件上传完成后自动触发回调，您需要通过上传请求传入两个参数：callback和（可选的）callback-var。

1. **构造callback参数。**

该参数用于定义应用服务器地址、请求内容格式等信息，必须以 JSON 格式构造并进行 Base64 编码。

1. 最简配置示例：















      ```json
      {
      "callbackUrl":"http://oss-demo.aliyuncs.com:23450",
      "callbackBody":"bucket=${bucket}&object=${object}&my_var=${x:my_var}"
      }
      ```



      在该示例中：

      - callbackUrl：应用服务器地址，需根据实际地址修改。此处以`http://oss-demo.aliyuncs.com:23450`为例。

      - callbackBody：回调请求体的内容。您可以使用占位符动态传入上传信息，例如`${bucket}`表示Bucket名称、`${object}`表示文件完整路径，还可以使用`${x:xxx}`引用自定义变量。OSS 会在回调时将这些占位符替换为实际值。更多可传入的信息请参见 [callbackBody支持的系统参数](https://help.aliyun.com/zh/oss/developer-reference/callback#3efd8ac8c0l4f "")。
2. 进阶配置示例：















      ```json
      {
      "callbackUrl":"http://oss-demo.aliyuncs.com:23450",
      "callbackHost":"oss-cn-hangzhou.aliyuncs.com",
      "callbackBody":"bucket=${bucket}&object=${object}&my_var=${x:my_var}",
      "callbackBodyType":"application/x-www-form-urlencoded",
      "callbackSNI":false
      }
      ```



      详细字段说明请参见： [callback参数详情](https://help.aliyun.com/zh/oss/developer-reference/callback#19f2e6eb46b27 "")。
2. **构造callback-var参数（可选）**

该参数用于向应用服务器传递自定义业务信息，例如用户 ID、订单号等。必须符合 JSON 格式，且每个自定义参数的 key 必须以 x: 开头，并使用小写字母。例如：















```json
{
     "x:uid": "12345",
     "x:order_id": "67890"
}
```



callback-var必须与 callbackBody 配合使用。对于上述示例中的自定义参数用户id（uid）和订单号（order\_id），在callbackBody中需要通过占位符${x:xxx} 来引用。例如：















```json
{
     "callbackUrl": "http://oss-demo.aliyuncs.com:23450",
     "callbackBody": "uid=${x:uid}&order=${x:order_id}"
}
```



实际回调时，OSS会发送以下内容（假设callbackBodyType为 application/x-www-form-urlencoded）：















```plaintext
uid=12345&order=67890
```

3. **在构造好callback 和callback-var参数后，您需要将它们进行Base64编码。**

   - **示例：callback参数编码**

     原始callback参数















     ```json
     {
         "callbackUrl": "http://oss-demo.aliyuncs.com:23450",
         "callbackHost": "your.callback.com",
         "callbackBody": "bucket=${bucket}&object=${object}&uid=${x:uid}&order=${x:order_id}",
         "callbackBodyType": "application/x-www-form-urlencoded",
         "callbackSNI": false
     }
     ```



     Base64编码后的结果：















     ```json
     eyJjYWxsYmFja0hvc3QiOiAieW91ci5jYWxsYmFjay5jb20iLCAiY2FsbGJhY2tVcmwiOiAiaHR0cDovL29zcy1kZW1vLmFsaXl1bmNzLmNvbToyMzQ1MCIsICJjYWxsYmFja0JvZHkiOiAiYnVja2V0PSR7YnVja2V0fSZvYmplY3Q9JHtvYmplY3R9JnVpZD0ke3g6dWlkfSZvcmRlcj0ke3g6b3JkZXJfaWR9IiwgImNhbGxiYWNrQm9keVR5cGUiOiAiYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIiwgImNhbGxiYWNrU05JIjogZmFsc2V9
     ```

   - **示例：callback-var参数编码**

     原始callback-var参数：















     ```json
     {
       "x:uid": "12345",
       "x:order_id": "67890"
     }
     ```



     Base64编码后的结果：















     ```json
     eyJ4OnVpZCI6ICIxMjM0NSIsICJ4Om9yZGVyX2lkIjogIjY3ODkwIn0=
     ```
4. **将编码后的参数附加到请求中。**

完成编码后，您可以通过以下方式将编码后的参数传递给OSS。






在Header中携带参数（推荐）



在POST请求的Body中使用表单域来携带参数



在URL中携带参数



















适用于通过SDK或后端代码上传对象的场景，安全性高，推荐优先使用。您可通过设置HTTP头部字段x-oss-callback和x-oss-callback-var来传递回调参数：



   - x-oss-callback：Base64 编码后的 callback 参数

   - x-oss-callback-var（可选）：Base64 编码后的 callback-var 参数


> 注意：计算请求签名时，这两个参数必须包含在Canonical Headers中，以确保请求合法。

**示例：通过 Header 传递回调参数**

```json
PUT /your_object HTTP/1.1
Host: callback-test.oss-test.aliyun-inc.com
Accept-Encoding: identity
Content-Length: 5
x-oss-callback-var: eyJ4OnVpZCI6ICIxMjM0NSIsICJ4Om9yZGVyX2lkIjogIjY3ODkwIn0=
User-Agent: aliyun-sdk-python/0.4.0 (Linux/2.6.32-220.23.2.ali1089.el5.x86_64/x86_64;2.5.4)
x-oss-callback: eyJjYWxsYmFja0hvc3QiOiAieW91ci5jYWxsYmFjay5jb20iLCAiY2FsbGJhY2tVcmwiOiAiaHR0cDovL29zcy1kZW1vLmFsaXl1bmNzLmNvbToyMzQ1MCIsICJjYWxsYmFja0JvZHkiOiAiYnVja2V0PSR7YnVja2V0fSZvYmplY3Q9JHtvYmplY3R9JnVpZD0ke3g6dWlkfSZvcmRlcj0ke3g6b3JkZXJfaWR9IiwgImNhbGxiYWNrQm9keVR5cGUiOiAiYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIiwgImNhbGxiYWNrU05JIjogZmFsc2V9
Host: callback-test.oss-test.aliyun-inc.com
Expect: 100-Continue
Date: Wed, 26 Apr 2023 03:46:17 GMT
Content-Type: text/plain
Authorization: OSS qn6q**************:77Dv****************
Test
```

仅适用于 [PostObject](https://help.aliyun.com/zh/oss/developer-reference/postobject#reference-smp-nsw-wdb "") 接口上传，回调参数只能通过 POST 请求的 Body 中的表单域传递。

   - **callback参数：** 需作为独立表单项传入，值为Base64编码后的JSON配置。















     ```json
     --9431149156168
     Content-Disposition: form-data; name="callback"
     eyJjYWxsYmFja0hvc3QiOiAieW91ci5jYWxsYmFjay5jb20iLCAiY2FsbGJhY2tVcmwiOiAiaHR0cDovL29zcy1kZW1vLmFsaXl1bmNzLmNvbToyMzQ1MCIsICJjYWxsYmFja0JvZHkiOiAiYnVja2V0PSR7YnVja2V0fSZvYmplY3Q9JHtvYmplY3R9JnVpZD0ke3g6dWlkfSZvcmRlcj0ke3g6b3JkZXJfaWR9IiwgImNhbGxiYWNrQm9keVR5cGUiOiAiYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIiwgImNhbGxiYWNrU05JIjogZmFsc2V9
     ```

   - **callback-var参数（自定义参数）：** 每个自定义字段必须作为独立表单项传入，不能封装成一个整体的callback-var字段。

     例如，对于自定义参数uid和order\_id：















     ```json
     {
       "x:uid": "12345",
       "x:order_id": "67890"
     }
     ```



     应转换为表单中的两个独立字段。















     ```json
     --9431149156168
     Content-Disposition: form-data; name="x:uid"
     12345
     --9431149156168
     Content-Disposition: form-data; name="x:order_id"
     67890
     ```

   - **验证callback参数（可选）**：您可以在 policy 中指定 callback 参数的校验条件。如果未设置，则上传时不会校验该参数。例如：















     ```json
     { "expiration": "2021-12-01T12:00:00.000Z",
       "conditions": [\
         {"bucket": "examplebucket" },\
         {"callback": "eyJjYWxsYmFja0hvc3QiOiAieW91ci5jYWxsYmFjay5jb20iLCAiY2FsbGJhY2tVcmwiOiAiaHR0cDovL29zcy1kZW1vLmFsaXl1bmNzLmNvbToyMzQ1MCIsICJjYWxsYmFja0JvZHkiOiAiYnVja2V0PSR7YnVja2V0fSZvYmplY3Q9JHtvYmplY3R9JnVpZD0ke3g6dWlkfSZvcmRlcj0ke3g6b3JkZXJfaWR9IiwgImNhbGxiYWNrQm9keVR5cGUiOiAiYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIiwgImNhbGxiYWNrU05JIjogZmFsc2V9"},\
         ["starts-with", "$key", "user/eric/"]\
       ]
     }
     ```


   - 该方式常用于预签名URL上传文件的场景，通过将回调参数 Base64 编码后拼接在 URL 中实现自动回调。但由于回调信息暴露在 URL 中，存在一定的安全风险，仅建议用于临时访问或低敏感场景。

   - 如果您选择通过 URL 携带回调参数，则必须包含`callback`参数，`callback-var`参数为可选。签名计算时，这些参数需作为Canonical Query String的一部分参与计算。更多信息，请参见 [签名版本4](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls#d3a828057bem1 "")。

     示例：















     ```plaintext
     PUT /your_object?OSSAccessKeyId=LTAI******************&Signature=vjby*************************************&Expires=1682484377&callback-var=eyJ4OnVpZCI6ICIxMjM0NSIsICJ4Om9yZGVyX2lkIjogIjY3ODkwIn0=&callback=eyJjYWxsYmFja0hvc3QiOiAieW91ci5jYWxsYmFjay5jb20iLCAiY2FsbGJhY2tVcmwiOiAiaHR0cDovL29zcy1kZW1vLmFsaXl1bmNzLmNvbToyMzQ1MCIsICJjYWxsYmFja0JvZHkiOiAiYnVja2V0PSR7YnVja2V0fSZvYmplY3Q9JHtvYmplY3R9JnVpZD0ke3g6dWlkfSZvcmRlcj0ke3g6b3JkZXJfaWR9IiwgImNhbGxiYWNrQm9keVR5cGUiOiAiYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIiwgImNhbGxiYWNrU05JIjogZmFsc2V9 HTTP/1.1
     Host: callback-test.oss-cn-hangzhou.aliyuncs.com
     Date: Wed, 26 Apr 2023 03:46:17 GMT
     Content-Length: 5
     Content-Type: text/plain
     ```


### **服务端实现**

> 以下为服务端的处理流程。各语言的代码示例请参见 [服务端代码示例](https://help.aliyun.com/zh/oss/developer-reference/callback#10ba2ec05cm06 "")。

应用服务器需要具备以下能力：

1. **接收OSS发送的POST请求**

当文件上传成功后，OSS 会根据回调参数，自动向您配置的应用服务器发送一个POST请求。示例如下：















```json
POST /test HTTP/1.1
Host: your.callback.com
Connection: close
Authorization: GevnM3**********3j7AKluzWnubHSVWI4dY3VsIfUHYWnyw==
Content-MD5: iKU/O/JB***ZMd8Ftg==
Content-Type: application/x-www-form-urlencoded
Date: Tue, 07 May 2024 03:06:13 GMT
User-Agent: aliyun-oss-callback
x-oss-bucket: your_bucket
x-oss-pub-key-url: aHR0cHM6Ly9nb3NzcHVi**********vY2FsbGJeV92MS5wZW0=
x-oss-request-id: 66399AA50*****3334673EC2
x-oss-requester: 23313******948342006
x-oss-signature-version: 1.0
x-oss-tag: CALLBACK
bucket=your_bucket&object=your_object&uid=12345&order_id=67890
```

2. **验证请求签名确保安全（可选）**

为确保回调请求来自 OSS，建议在应用服务器中对请求签名进行验证。具体验证方法，请参见 [建议配置](https://help.aliyun.com/zh/oss/developer-reference/callback#256812b0e5wv1 "")。



**说明**





签名验证不是必选项，您可按需决定是否启用。

3. **返回回调响应**

应用服务器收到回调请求后，需要向OSS返回响应。回调响应必须符合以下要求：


   - 正常情况下，应用服务器应返回 HTTP/1.1 200 OK。

   - 响应头中必须包含Content-Length。

   - 响应体格式支持JSON或XML，此处以 JSON 为例。如果您希望使用XML作为响应体格式，在响应头中添加`Content-Type: application/xml`即可。


例如，此处应用服务器返回了{"Status": "OK"}

注意：本示例中的Python版本为2.7.6，实际开发建议使用Python 3。

```http
HTTP/1.0 200 OK
Server: BaseHTTP/0.3 Python/2.7.6
Date: Mon, 14 Sep 2015 12:37:27 GMT
Content-Type: application/json
Content-Length: 9
{"Status": "OK"}
```

之后OSS会将该响应内容透传给客户端。示例如下：

```http
HTTP/1.1 200 OK
Date: Mon, 14 Sep 2015 12:37:27 GMT
Content-Type: application/json
Content-Length: 9
Connection: keep-alive
ETag: "D8E8FCA2DC0F896FD7CB4CB0031BA249"
Server: AliyunOSS
x-oss-bucket-version: 1442231779
x-oss-request-id: 55F6BF87207FB30F2640C548
{"Status": "OK"}
```

**重要**

对于`CompleteMultipartUpload`请求，如果原本的响应body中存在内容（例如JSON格式的信息），启用上传回调后，该内容会被回调返回的覆盖，例如此处被`{"Status": "OK"}`覆盖。

## **建议配置**

### **验证请求签名确保安全**

在设置回调参数后，OSS会根据您配置的callbackUrl发送POST回调请求到应用服务器。为确保请求来自OSS，您可以对回调请求中的签名进行验证。以下是验证过程的详细步骤。

1. **客户端生成签名（由OSS完成）**

OSS 使用 RSA 非对称加密算法，结合 MD5 哈希，对请求内容生成签名，并将签名添加到请求头的 authorization 字段中。

   - 签名计算方式如下：















     ```shell
     authorization = base64_encode(rsa_sign(private_key, url_decode(path) + query_string + '\n' + body, md5))
     ```





     **说明**





     其中，private\_key为私钥，path为回调请求的资源路径，query\_string为查询字符串，body为回调的消息体。

   - 生成签名的步骤：

     1. 获取待签名字符串：资源路径经过URL解码后，会附加原始的查询字符串、一个回车符以及回调消息体。

     2. RSA签名：使用密钥对待签名字符串进行签名，签名的哈希函数为md5。

     3. 将签名后的结果做Base64编码，获取最终的签名，然后将签名放在回调请求的authorization头中。
   - 生成签名的示例：















     ```json
     POST /index.php?id=1&index=2 HTTP/1.0
     Host: 172.16.XX.XX
     Connection: close
     Content-Length: 18
     authorization: kKQeGTRccDKyHB3H9vF+xYMSrmhMZj****/kdD1ktNVgbWEfYTQG0G2SU/RaHBovRCE8OkQDjC3uG33esH2t****
     Content-Type: application/x-www-form-urlencoded
     User-Agent: http-client/0.0.1
     x-oss-pub-key-url: aHR0cDovL2dvc3NwdWJsaWMuYWxpY2RuLmNvbS9jYWxsYmFja19wdWJfa2V5X3YxLnsr****
     bucket=examplebucket
     ```



     path为`/index.php`，query\_string为`?id=1&index=2`，body为`bucket=examplebucket`，最终签名结果为`kKQeGTRccDKyHB3H9vF+xYMSrmhMZjzzl2/kdD1ktNVgbWEfYTQG0G2SU/RaHBovRCE8OkQDjC3uG33esH2t****`。
2. **回调服务器验证签名**

您的应用服务器需对OSS请求进行签名验证，以确认请求来源的合法性。验证步骤如下：

1. 获取公钥：

      从请求头的 x-oss-pub-key-url 字段获取 Base64 编码的公钥 URL，并进行解码。















      ```plaintext
      public_key = urlopen(base64_decode(x-oss-pub-key-url头的值))
      ```



      解码前的示例值：















      ```plaintext
      aHR0cDovL2dvc3NwdWJsaWMuYWxpY2RuLmNvbS9jYWxsYmFja19wdWJfa2V5X3YxLnBlbQ==
      ```



      解码后：















      ```plaintext
      http://gosspublic.alicdn.com/callback_pub_key_v1.pem
      ```





      **说明**





      公钥URL必须以`http://gosspublic.alicdn.com/`或者`https://gosspublic.alicdn.com/`开头。由于公钥地址的内容不变，建议缓存公钥以避免因网络波动影响服务。

2. 解码签名。

      从请求头的 authorization 字段获取签名，并进行 Base64 解码：















      ```shell
      signature = base64_decode(authorization头的值)
      ```

3. 构造待验证字符串。

      将资源路径、查询字符串、换行符和回调消息体按如下格式拼接：















      ```shell
      sign_str = url_decode(path) + query_string + ‘\n’ + body
      ```

4. 执行签名验证。

      使用 MD5 哈希加 RSA 公钥进行验证：















      ```shell
      result = rsa_verify(public_key, md5(sign_str), signature)
      ```
3. **验证签名示例**

以Python 3为例，演示应用服务器中验证签名的方法，此示例需要安装M2Crypto库。















```python
import http.client
import base64
import hashlib
import urllib.request
import urllib.parse
import socket
from http.server import BaseHTTPRequestHandler, HTTPServer
from M2Crypto import RSA
from M2Crypto import BIO

def get_local_ip():
       try:
           csock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
           csock.connect(('8.8.8.8', 80))
           (addr, port) = csock.getsockname()
           csock.close()
           return addr
       except socket.error:
           return ""

class MyHTTPRequestHandler(BaseHTTPRequestHandler):
       '''
       def log_message(self, format, *args):
           return
       '''
       def do_POST(self):
           #get public key
           pub_key_url = ''
           try:
               pub_key_url_base64 = self.headers['x-oss-pub-key-url']
               pub_key_url = base64.b64decode(pub_key_url_base64).decode()
               if not pub_key_url.startswith("http://gosspublic.alicdn.com/") and not pub_key_url.startswith("https://gosspublic.alicdn.com/"):
                   self.send_response(400)
                   self.end_headers()
                   return
               url_reader = urllib.request.urlopen(pub_key_url)
               #you can cache it,recommend caching public key content based on the public key address
               pub_key = url_reader.read()
           except Exception as e:
               print('pub_key_url : ' + pub_key_url)
               print('Get pub key failed! Error:', str(e))
               self.send_response(400)
               self.end_headers()
               return

           #get authorization
           authorization_base64 = self.headers['authorization']
           authorization = base64.b64decode(authorization_base64)
           #get callback body
           content_length = self.headers['content-length']
           callback_body = self.rfile.read(int(content_length))
           #compose authorization string
           auth_str = ''
           pos = self.path.find('?')
           if -1 == pos:
               auth_str = urllib.parse.unquote(self.path) + '\n' + callback_body.decode()
           else:
               auth_str = urllib.parse.unquote(self.path[0:pos]) + self.path[pos:] + '\n' + callback_body.decode()
           print(auth_str)
           #verify authorization
           auth_md5 = hashlib.md5(auth_str.encode()).digest()
           bio = BIO.MemoryBuffer(pub_key)
           rsa_pub = RSA.load_pub_key_bio(bio)
           try:
               result = rsa_pub.verify(auth_md5, authorization, 'md5')
           except:
               result = False
           if not result:
               print('Authorization verify failed!')
               print('Public key : %s' % (pub_key))
               print('Auth string : %s' % (auth_str))
               self.send_response(400)
               self.end_headers()
               return

           #do something according to callback_body
           #response to OSS
           resp_body = '{"Status":"OK"}'
           self.send_response(200)
           self.send_header('Content-Type', 'application/json')
           self.send_header('Content-Length', str(len(resp_body)))
           self.end_headers()
           self.wfile.write(resp_body.encode())

class MyHTTPServer(HTTPServer):
       def __init__(self, host, port):
           super().__init__((host, port), MyHTTPRequestHandler)

if __name__ == '__main__':
       server_ip = get_local_ip()
       server_port = 23451
       server = MyHTTPServer(server_ip, server_port)
       server.serve_forever()
```



其他语言的服务端代码请参见下表。




| **SDK语言** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **SDK语言** | **描述** |
| Java | - 下载地址： [Java](https://gosspublic.alicdn.com/images/AppCallbackServer.zip)<br>     <br>   - 运行方法：解压包运行`java -jar oss-callback-server-demo.jar 9000`（9000指运行的端口，可以自行指定）。 |
| Python | - 下载地址： [Python](https://gosspublic.alicdn.com/images/callback_app_server.py.zip)<br>     <br>   - 运行方法：解压包直接运行`python callback_app_server.py`，运行该程序需要安装RSA的依赖。 |
| PHP | - 下载地址： [PHP](https://gosspublic.alicdn.com/callback-php-demo.zip)<br>     <br>   - 运行方法：部署到Apache环境下，因为PHP本身语言的特点，取一些数据头部会依赖于环境。所以可以参考例子根据所在环境修改。 |
| .NET | - 下载地址： [.NET](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/131396/intl_en/1597211267799/callback-server-dotnet-20200810.zip)<br>     <br>   - 运行方法：解压后参看`README.md`。 |
| Node.js | - 下载地址： [Node.js](https://gosspublic.alicdn.com/doc/oss-doc/callback-nodejs-demo.zip)<br>     <br>   - 运行方法：解压包直接运行`node example.js`。 |
| Ruby | - 下载地址： [Ruby](https://github.com/rockuw/oss-callback-server)<br>     <br>   - 运行方法：ruby aliyun\_oss\_callback\_server.rb |


## **callback参数详情**

以下是callback参数的详细说明，用于配置OSS文件上传成功后的回调请求内容与行为。

| **字段** | **是否必选** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **是否必选** | **描述** |
| callbackUrl | 是 | 文件上传成功后，OSS向此URL发送POST回调请求。<br>- 支持同时配置最多5个URL，多个URL间以分号（;）分隔。OSS会依次发送请求，直到第一个回调请求成功返回。<br>  <br>- 支持HTTPS协议地址。<br>  <br>- 不支持填写IPV6地址，也不支持填写指向IPV6地址的域名。<br>  <br>- 为了保证正确处理中文等情况，callbackUrl需做URL编码处理，例如`https://example.com/中文.php?key=value&中文名称=中文值`需要编码为`https://example.com/%E4%B8%AD%E6%96%87.php?key=value&%E4%B8%AD%E6%96%87%E5%90%8D%E7%A7%B0=%E4%B8%AD%E6%96%87%E5%80%BC`。 |
| callbackBody | 是 | 发起回调时请求体的内容，格式需与 callbackType 参数保持一致：<br>- 当 callbackType 为默认值`application/x-www-form-urlencoded`时，callbackBody 应为键值对格式，例如：`bucket=${bucket}&object=${object}&my_var_1=${x:my_var1}&my_var_2=${x:my_var2}`<br>  <br>- 当 callbackType 为`application/json`时，callbackBody 应为 JSON格式，例如：`{\"bucket\":${bucket},\"object\":${object},\"mimeType\":${mimeType},\"size\":${size},\"my_var1\":${x:my_var1},\"my_var2\":${x:my_var2}}`<br>  <br>callbackBody 支持引用 OSS 系统参数、自定义变量和常量。系统参数说明请参见 [callbackBody支持的系统参数](https://help.aliyun.com/zh/oss/developer-reference/callback#3efd8ac8c0l4f "")。 |
| callbackHost | 否 | 发起回调请求时Host头的值，格式为域名或IP地址。<br>- 如果没有配置callbackHost，则解析callbackUrl中的URL，并将解析的Host填充到callbackHost中。 |
| callbackSNI | 否 | 是否在回调请求中携带 SNI（用 HTTPS请求中标识域名并返回正确证书）。<br>当 callbackUrl 使用 HTTPS 时，建议开启该参数，否则可能因证书不匹配导致回调失败（如 502 callback failed）。取值如下：<br>- true：发送SNI。<br>  <br>- false（默认值）：不发送SNI。<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  英国（伦敦）地域始终发送SNI，不受此参数控制。 |
| callbackBodyType | 否 | 发起回调请求的Content-Type，即`callbackBody`的数据格式。<br>支持以下两种类型：<br>- application/x-www-form-urlencoded（默认值）<br>  <br>  将经过URL编码的值替换callbackBody中的变量。<br>  <br>- application/json<br>  <br>  按照JSON格式替换callbackBody中的变量。 |

## **callbackBody支持的系统参数**

callback参数中callbackBody字段支持引用多个系统参数，用于在回调请求中传递上传文件的相关信息。支持的系统参数如下表所示：

| **系统参数** | **含义** |
| --- | --- |

|     |     |
| --- | --- |
| **系统参数** | **含义** |
| bucket | 存储空间名称。 |
| object | 对象（文件）的完整路径。 |
| etag | 文件的ETag，即返回给用户的ETag字段。 |
| size | Object大小。调用CompleteMultipartUpload时，size为整个Object的大小。 |
| mimeType | 资源类型，例如jpeg图片的资源类型为image/jpeg。 |
| imageInfo.height | 图片高度。该变量仅适用于图片格式，对于非图片格式，该变量的值为空。 |
| imageInfo.width | 图片宽度。该变量仅适用于图片格式，对于非图片格式，该变量的值为空。 |
| imageInfo.format | 图片格式，例如JPG、PNG等。该变量仅适用于图片格式，对于非图片格式，该变量的值为空。 |
| crc64 | 与上传文件后返回的x-oss-hash-crc64ecma头内容一致。 |
| contentMd5 | 与上传文件后返回的Content-MD5头内容一致。<br>**重要**<br>仅在调用PutObject和PostObject接口上传文件时，该变量的值不为空。 |
| vpcId | 发起请求的客户端所在的VpcId。如果不是通过VPC发起请求，则该变量的值为空。 |
| clientIp | 发起请求的客户端IP地址。 |
| reqId | 发起请求的RequestId。 |
| operation | 发起请求的接口名称，例如PutObject、PostObject等。 |

## SDK

以下为客户端实现的示例demo。

|     |     |     |     |
| --- | --- | --- | --- |
|  | 简单上传<br>（使用 [PutObject](https://help.aliyun.com/zh/oss/developer-reference/putobject#reference-l5p-ftw-tdb "") 接口） | 分片上传<br>（使用 [CompleteMultipartUpload](https://help.aliyun.com/zh/oss/developer-reference/completemultipartupload#reference-lq1-dtx-wdb "") 接口） | 使用预签名URL上传<br>（使用 [PutObject](https://help.aliyun.com/zh/oss/developer-reference/putobject#reference-l5p-ftw-tdb "") 接口） |
| Java | [demo](https://help.aliyun.com/zh/oss/developer-reference/upload-callbacks-11 "") | [demo](https://help.aliyun.com/zh/oss/developer-reference/upload-callbacks-11#bf40fed3a95o5 "") | [demo](https://help.aliyun.com/zh/oss/developer-reference/upload-an-object-using-a-signed-url-generated-with-oss-sdk-for-java#c70d9abfa09zs "") |
| Python V2 | [demo](https://help.aliyun.com/zh/oss/developer-reference/simple-upload-using-oss-sdk-for-python-v2#c5dae89e32xfo "") | - | [demo](https://help.aliyun.com/zh/oss/developer-reference/upload-an-object-using-a-signed-url-generated-with-oss-sdk-for-python-v2#655eb3b3a7elg "") |
| Go V2 | [demo](https://help.aliyun.com/zh/oss/developer-reference/v2-simple-upload#16bf5fcc0bh6p "") | [demo](https://help.aliyun.com/zh/oss/developer-reference/v2-multipart-upload#cad1c80985x85 "") | [demo](https://help.aliyun.com/zh/oss/developer-reference/v2-presign-upload#c70d9abfa09zs "") |

## **错误排查**

OSS返回的错误信息中包含EC错误码，使用Callback过程若出现错误，您可以使用EC码进行排查。EC码与错误原因一一对应。与Callback相关的EC错误码，请参见 [07-CALLBACK](https://help.aliyun.com/zh/oss/user-guide/07-callback/ "")。

## 常见问题

### OSS上传文件失败后是否会发送回调通知给应用服务器？

不会。OSS上传文件成功后会执行回调，如果上传失败，则不执行回调，直接返回错误信息。

### 报错Response body is not valid json format.如何处理？

- 应用服务器处理过程中抛出异常，导致返回给OSS的Body不是JSON格式，如下图所示：![callback](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6630541761/p536785.png)

解决方法：

  - 通过以下命令确认内容。















    ```shell
    curl -d "<Content>" <CallbackServerURL> -v
    ```

  - 通过抓包确认内容。

    Windows下推荐使用工具Wireshark抓包，Linux下使用命令tcpdump抓包。
- 应用服务器返回给OSS的Body中带有BOM头。

这类错误常见于使用PHP SDK编写的应用服务器中。由于PHP SDK返回了BOM头，导致OSS收到的Body中多了三个字节，出现不符合JSON格式的Body。如下图所示，ef bb bf这三个字节为BOM头。

![callback1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6630541761/p536787.png)

解决方法：删除应用服务器返回OSS Body中的BOM头。