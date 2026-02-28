### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)[OSS Browser.js SDK](https://help.aliyun.com/zh/oss/developer-reference/browser-js/)常见问题（Browser.js SDK）

# 常见问题（Browser.js SDK）

更新时间：2025-11-28 03:08:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：异常处理（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/error-handling)[下一篇：OSS Kotlin SDK V2（预览版）](https://help.aliyun.com/zh/oss/developer-reference/oss-kotlin-sdk-v2-preview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

如何调用STS

如何开启HTTPS访问

浏览器跨域问题如何解决

如何设置上传文件的用户自定义数据（meta）、文件类型（mime）和请求头（header）

关于浏览器端断点续传的说明

如何上传文件到指定目录

如何上传base64编码的图片

如何限制上传文件的大小

如何获取上传进度

如何获取下载进度

如何获取Object的签名URL

如何使用SDK生成的签名URL并进行资源上传

如何使用表单上传方式上传资源到OSS服务器

如何运行示例工程

如何添加上传回调

浏览器是否支持以chunck的方法浏览文件？

如何通过OSS js SDK进行日志收集？

常见错误参考

本文主要介绍Browser.js SDK中的常见问题与解决方法。

## 如何调用STS

浏览器是不受信任的环境，如果把AccessKey ID和AccessKey Secret直接保存在浏览器端，存在极高的风险。建议在浏览器环境下使用 [STS](https://help.aliyun.com/zh/ram/user-guide/what-is-sts#concept-ong-5nv-xdb "") 模式进行OSS接口调用。

获取STS token后，即可进行SDK初始化操作。

```javascript
<script type="text/javascript">
  $.ajax("http://your_sts_server/",{method: 'GET'},function (err, result) {
    let client = new OSS({
      authorizationV4: true,
      accessKeyId: result.AccessKeyId,
      accessKeySecret: result.AccessKeySecret,
      stsToken: result.SecurityToken,
      region: 'yourRegion',
      bucket: 'yourBucketName'
    });
  });
</script>

```

## 如何开启HTTPS访问

您可以在初始化SDK时，通过设置`secure:true`的方式开启HTTPS访问。更多信息，请参见 [初始化（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/initialization "")。

## 浏览器跨域问题如何解决

在浏览器中使用SDK前，需要对Bucket配置跨域规则。具体操作，请参见 [准备工作](https://help.aliyun.com/zh/oss/developer-reference/installation#section-lc9-9ju-8da "")。

## 如何设置上传文件的用户自定义数据（meta）、文件类型（mime）和请求头（header）

请参见 [简单上传（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/simple-upload-8 "")。

## 关于浏览器端断点续传的说明

将checkpoint保存到浏览器的localstorage，在下次调用时传入checkpoint参数，即可实现断点续传功能。更多信息，请参见 [断点续传上传（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/resumable-upload-9 "")。

## 如何上传文件到指定目录

通过在上传的Object名称前指定前缀的方式实现将文件上传到指定目录。

```javascript
let OSS = require('ali-oss')
let client = new OSS({
  authorizationV4: true,
  region: 'yourRegion',
  accessKeyId: 'yourAccessKeyId',
  accessKeySecret: 'yourAccessKeySecret',
  bucket: 'yourBucketName'
});

client.multipartUpload('base-dir/' +'object-key', 'local-file', {
    progress: async function (p) {
      console.log('Progress: ' + p);
    }
  });
  console.log(result);
}).catch((err) => {
  console.log(err);
});


```

## 如何上传base64编码的图片

base64先转码成指定格式图片，然后调用OSS上传接口进行上传。更多信息，请参见 [Github示例](https://github.com/ali-sdk/ali-oss/blob/master/example/src/main.js#L109)。

```javascript
/**
 * base64 to file
 * @param dataurl   base64 content
 * @param filename  set up a meaningful suffix, or you can set mime type in options
 * @returns {File|*}
 */
const dataURLtoFile = function dataURLtoFile(dataurl, filename) {
  const arr = dataurl.split(',');
  const mime = arr[0].match(/:(.*?);/)[1];
  const bstr = atob(arr[1]);
  let n = bstr.length;
  const u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new Blob([u8arr], { type: mime });// if env support File, also can use this: return new File([u8arr], filename, { type: mime });
};

// client表示OSS client实例
const uploadBase64Img = function uploadBase64Img(client) {
  // base64格式的内容
  const base64Content = 'data:image:****';
  const filename = 'img.png';
  const imgfile = dataURLtoFile(base64Content, filename);
 //key表示上传的object key，imgFile表示dataURLtoFile处理后返回的图片。
  client.multipartUpload(key, imgfile).then((res) => {
    console.log('upload success: %j', res);
  }).catch((err) => {
    console.error(err);
  });
};
```

## 如何限制上传文件的大小

在浏览器中可以根据document.getElementById(“file”).files\[0\].size获取上传文件的大小（字节数）。更多信息，请参见 [Web端直传实践](https://help.aliyun.com/zh/oss/use-postobject-to-upload-objects-by-using-web-clients#concept-iyn-vfy-5db "") 的post请求。

## 如何获取上传进度

您可以通过分片上传的方式获取上传进度。更多信息，请参见 [分片上传（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/multipart-upload-11 "")。

## 如何获取下载进度

浏览器中无法获取进度，可调用`signatureUrl`方法，获取下载地址。更多信息，请参见 [相关文档](https://help.aliyun.com/zh/oss/developer-reference/preview-or-download-an-object#concept-64052-zh "")。

## 如何获取Object的签名URL

可调用`signatureUrl`方法，获取下载地址。更多信息，请参见 [预览或下载文件（Browser.js SDK）](https://help.aliyun.com/zh/oss/developer-reference/preview-or-download-an-object "")。

## 如何使用SDK生成的签名URL并进行资源上传

签名URL常用于授权给第三方进行资源的下载和上传操作。下载请参见上一条。SDK中提供signatureUrl API，用于返回一个经过签名的URL，用户直接使用该URL上传或者下载资源即可。利用签名URL上传资源请参见SDK工程示例 [签名URL上传资源示例](https://github.com/ali-sdk/ali-oss/blob/master/example/src/main.js)。

## 如何使用表单上传方式上传资源到OSS服务器

请参见 [Web端直传实践](https://help.aliyun.com/zh/oss/use-postobject-to-upload-objects-by-using-web-clients#concept-iyn-vfy-5db "")。

## 如何运行示例工程

进入ali-oss/example执行` npm run start`。

## 如何添加上传回调

```javascript
const uploadFile = function uploadFile(client) {
if (!uploadFileClient || Object.keys(uploadFileClient).length === 0) {
uploadFileClient = client;
}

const file = document.getElementById('file').files[0];
const key = document.getElementById('object-key-file').value.trim() || 'object';

console.log(`${file.name} => ${key}`);
const options = {
progress,
partSize: 500 * 1024,
timeout:60000,
meta: {
year: 2017,
people: 'test',
},
callback: {

// 添加上传回调的位置。
url: 'https://example.aliyundoc.com/v2/sync',
/* host: 'oss-cn-shenzhen.aliyuncs.com', */
/* eslint no-template-curly-in-string: [0] */
body: 'bucket=${bucket}&object=${object}&var1=${x:var1}',
contentType: 'application/x-www-form-urlencoded',
customValue: {
var1: 'value1',
var2: 'value2',
},
},
```

关于上传回调的更多信息，请参见 [原理介绍](https://help.aliyun.com/zh/oss/overview-20/#concept-qp2-g4y-5db "")。

## 浏览器是否支持以chunck的方法浏览文件？

不支持。

## **如何通过OSS js SDK进行日志收集？**

具体操作，请参见 [GitHub](https://github.com/luozhang002/oss-js-sdk-log)。

## 常见错误参考

- [SDK开启异常日志](https://help.aliyun.com/zh/oss/developer-reference/error-handling#concept-64055-zh "")

- [OSS常见错误](https://help.aliyun.com/zh/oss/user-guide/overview-14#concept-dt2-hq3-wdb "")