### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-languages/)[Node.js](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/node-js/)事件请求处理程序（Event Handler）

# 事件请求处理程序（Event Handler）

更新时间：2025-08-04 01:21:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Event Handler签名

Node.js 18及以上版本

ES模块

CommonJS模块

Node.js 16及以下版本

Async/Await

示例一：解析JSON格式参数

示例代码

ES模块

CommonJS模块

前提条件

操作步骤

示例二：通过临时密钥安全读写OSS的资源

示例代码

ES模块

CommonJS模块

前提条件

操作步骤

示例三：调用外部命令

ES模块

CommonJS模块

本文介绍Node.js事件请求处理程序的结构特点和示例。

## Event Handler签名

**说明**

函数计算从Node.js 18运行时开始支持ECMAScript（ES）模块。在此之前（Node.js 16及以前的版本），函数计算仅支持使用CommonJS 模块。详情请参见 [将请求处理程序指定为ES模块](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/overview-37#792ea514078gw "")。

一个简单的Event Handler签名定义如下。

## **Node.js 18及以上版本**

### **ES** 模块

```nodejs
// index.mjs
export const handler = async (event, context) => {
  console.log("event: \n" + event);
  return "Hello World!";
};
```

### **CommonJS模块**

```nodejs
// index.js
exports.handler = async function(event, context) {
  console.log("event: \n" + event);
  return "Hello World!";
};
```

## **Node.js 16及以下版本**

```nodejs
// index.js
exports.handler = async function(event, context, callback) {
  console.log("event: \n" + event);
  callback(null, 'hello world');
};
```

Event Handler的示例解析如下：

`handler`是方法名称，与[函数计算控制台](https://fcnext.console.aliyun.com/)配置的 **请求处理程序** 相对应。例如，创建函数时指定的 **请求处理程序** 为`index.handler`，那么函数计算会去加载`index.js`中定义的`handler`函数，并从这里开始执行。

函数计算运行时会将请求参数传递到请求处理程序中，第一个参数是`event`对象，包含请求的有效负载信息，`event`对象是Buffer类型，您可以将其转换成所需要的对象类型。第二个参数是 `context`对象，提供在调用时的运行上下文信息。更多信息，请参见 [上下文](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/context-3 "")。

**说明**

- 使用Node.js 18及以上版本的运行时环境时，建议您使用 [Async/Await](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/event-handler#0fadb42637ooo "") 功能，而不是使用回调函数`callback`。

- 函数计算会根据返回值的类型对返回结果做相应转换。


  - Buffer类型：不转换，原样返回。

  - Object类型：转换为JSON格式后返回。

  - 其他类型：转换为字符串后返回。


### Async/Await

使用Node.js 18及以上版本的运行时环境时，建议您使用Async/Await方式来实现。Async/Await是一种简洁、易读的Node.js异步代码编写方式，无需嵌套回调或链式调用。

**重要**

如果您使用的Node.js 16及以下版本的运行时环境，则必须显式使用回调方法 `callback`发送响应，否则会出现请求超时错误。

Async/Await方式与回调函数`callback`相比，有以下优点：

- **可读性更好：** Async/Await方式的代码更加线性和同步，更易于理解和维护。它避免了回调函数嵌套过深的情况，使代码结构更清晰。

- **调试和错误处理更简单：** 可以使用try-catch块更方便地捕获和处理异步操作中的错误，错误堆栈更加清晰，可以更准确地追踪错误发生的位置。

- **效率更高：** 回调函数通常需要在代码的不同部分之间切换。Async/Await方式可以减少上下文切换的数量，从而提高代码效率。


## 示例一：解析JSON格式参数

### **示例代码**

当您传入JSON格式参数时，函数计算会透传参数内容，需要您在代码中自行解析。下面是解析JSON格式事件的代码示例。

## ES模块

**说明**

此示例仅支持运行在Node.js 18及以上版本的运行时环境。

```nodejs
export const handler = async (event, context) => {
  var eventObj = JSON.parse(event.toString());
  return eventObj['key'];
};
```

## CommonJS模块

```nodejs
exports.handler = function(event, context, callback) {
  var eventObj = JSON.parse(event.toString());
  callback(null, eventObj['key']);
};
```

### **前提条件**

已创建Node.js函数，具体操作，请参见 [创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#section-b9y-zn1-5wr "")。如果您需要将代码指定为ES模块，创建函数时，运行环境需选择Node.js 18或Node.js 20。

### **操作步骤**

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称，然后在函数详情页面，单击 **函数代码** 页签。
4. 在 **函数代码** 页签，在代码编辑器中输入上述示例代码，然后单击 **部署代码**。





**说明**





上述示例代码中函数的请求处理程序是`index.js`或`index.mjs`中的`handler`方法。如果您的函数的请求处理程序配置不同，请获取对应的文件和方法进行更新。

5. 在 **函数代码** 页签，单击 **测试函数** 右侧的![down](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3854548461/p423464.png)图标，从下拉列表中选择 **配置测试参数**，输入如下示例测试参数，然后单击 **确定**。

















```json
{
     "key": "value"
}
```

6. 单击 **测试函数**。



函数执行成功后，查看返回结果，您可以看到返回结果为`value`。


## 示例二：通过临时密钥安全读写OSS的资源

### **示例代码**

您可以使用函数计算为您提供的临时密钥访问对象存储OSS，代码示例如下所示。

## ES模块

**说明**

此示例仅支持运行在Node.js 18及以上版本的运行时环境。

```nodejs
// index.mjs
import OSSClient from 'ali-oss';

export const handler = async (event, context) => {
    console.log(event.toString());

    var ossClient = new OSSClient({
        accessKeyId: context.credentials.accessKeyId,
        accessKeySecret: context.credentials.accessKeySecret,
        stsToken: context.credentials.securityToken,
        region: 'oss-cn-shenzhen',
        bucket: 'my-bucket',
    });

    try {
      // 上传文件到OSS，'object'是OSS中的文件名，'localfile'是本地文件的路径。
      const uploadResult = await ossClient.put('myObj', Buffer.from('hello, fc', "utf-8"));
      console.log('upload success, ', uploadResult);
      return "succ"
    } catch (error) {
      throw error
    }
};
```

代码示例解析：

- `context.credentials`：从 context 参数中获取临时密钥，避免在代码中硬编码密码等敏感信息。

- `myObj`：OSS对象名。

- `Buffer.from('hello, fc', "utf-8")`： 上传的对象内容。

- `return "succ"`：上传成功正常返回 "succ"。

- `throw err`：上传失败时抛出异常。


## CommonJS模块

```nodejs
var OSSClient = require('ali-oss');

exports.handler = function (event, context, callback) {
    console.log(event.toString());

    var ossClient = new OSSClient({
        accessKeyId: context.credentials.accessKeyId,
        accessKeySecret: context.credentials.accessKeySecret,
        stsToken: context.credentials.securityToken,
        region: 'oss-cn-shenzhen',
        bucket: 'my-bucket',
    });

    ossClient.put('myObj', Buffer.from('hello, fc', "utf-8")).then(function (res) {
        callback(null, 'succ');
    }).catch(function (err) {
        callback(err);
    });
};
```

代码示例解析：

- `context.credentials`：从context参数中获取临时密钥，避免在代码中硬编码密码等敏感信息。

- `myObj`：OSS对象名。

- `Buffer.from('hello, fc', "utf-8")`：上传的对象内容。

- `callback(null, 'put object')`：上传成功正常返回"succ"。

- callback(err)：上传失败时异常返回err。


### **前提条件**

- 为服务配置具有访问对象存储OSS的权限的角色。具体操作，请参见 [授予函数计算访问其他云服务的权限](https://help.aliyun.com/zh/functioncompute/fc-2-0/security-and-compliance/grant-function-compute-permissions-to-access-other-alibaba-cloud-services#task-2077619 "")。

- 创建运行环境为Node.js的函数。具体操作，请参见 [创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#section-b9y-zn1-5wr "")。如果您需要将代码指定为ES模块，创建函数时，运行环境需选择Node.js 18或Node.js 20。


### **操作步骤**

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称，然后在函数详情页面，单击 **函数代码** 页签。
4. （可选）在 **函数代码** 页签，在下方的WebIDE界面，依次选择**Terminal** \> **New Terminal**打开终端，执行以下命令安装ali-oss依赖。















```shell
npm install ali-oss --save
```



安装完成后，在WebIDE界面左侧代码目录可以看到生成了`node_modules`文件夹，文件夹内包含`ali-oss`目录以及其他依赖库。

5. 在 **函数代码** 页签，在下面代码编辑器中，输入上述 [示例代码](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/event-handler#p-pkj-kzr-lu4 "")，保存并单击 **部署代码**。





**说明**





   - 上述示例代码中函数的请求处理程序是`index.js`或`index.mjs`中的handler方法。如果您的函数的请求处理程序配置不同，请获取对应的文件和方法进行更新。

   - 上述示例代码中`region`和`bucket`需按照实际情况填写。


6. 单击 **测试函数**。



函数执行成功后，查看返回结果，您可以看到返回结果为`succ`。


## 示例三：调用外部命令

您的Node.js程序也可以创建`fork`进程，调用外部命令。例如，您可以使用`child_process`模块调用Linux的`ls -l`命令，输出当前目录下的文件列表。代码示例如下：

## ES模块

**说明**

此示例仅支持运行在Node.js 18及以上版本的运行时环境。

```nodejs
import { exec } from 'child_process';
import { promisify } from 'util';

const execPromisify = promisify(exec);
export const handler = async (event, context) => {
  try {
    const { stdout, stderr } = await execPromisify("ls -l");
    console.log(`stdout: ${stdout}`);
    if (stderr !== "") {
      console.error(`stderr: ${stderr}`);
    }
    return stdout;
  } catch (error) {
    console.error(`exec error: ${error}`);
    return error;
  }
}
```

## CommonJS模块

```nodejs
'use strict';

var exec = require('child_process').exec;
exports.handler = (event, context, callback) => {
  console.log('start to execute a command');
  exec("ls -l", function(error, stdout, stderr){
    callback(null, stdout);
});
}
```