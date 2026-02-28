### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[快速入门](https://help.aliyun.com/zh/ocr/getting-started/)快速使用文字识别

# 快速使用文字识别

更新时间：2025-01-24 03:21:36

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：文件格式说明](https://help.aliyun.com/zh/ocr/product-overview/supported-file-types)[下一篇：使用RAM进行访问控制](https://help.aliyun.com/zh/ocr/security-and-compliance/use-ram-for-access-control/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用流程

免登录体验服务

注册阿里云账号并完成实名认证

开通服务

在线调用测试

调用SDK

获取访问密钥

将AccessKey配置到环境变量

选择开发语言

后续步骤

OCR识别清单

本文介绍文字识别OCR产品的使用流程。

## **使用流程**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4986077371/CAEQURiBgMD6ye_ZnxkiIDlhN2Y5NGJjNDc0ZjQ5ODE5MDcwOWQ2MTYwN2U0Y2Y24821552_20241218095758.133.svg)

**重要**

通过体验馆和SDK调用文字识别OCR服务时，文字识别OCR仅做图片识别并返回结果，不会存储图片和识别结果。

## **免登录体验服务**

如果您是新用户（未注册过阿里云账号、未开通文字识别OCR服务），建议先通过 [阿里云文字识别体验馆](https://duguang.aliyun.com/experience?type=universal) > **体验中心** 的可视化界面上传单张图片体验OCR效果。体验馆无需注册和登录账号，免费体验所有文字识别服务，不限次数，但无法通过SDK批量测试，也无法将OCR识别服务对接到业务系统。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4870455371/p890239.png)

当您判断文字识别OCR产品能够满足业务需求时，可前往 [文字识别OCR控制台](https://ocr.console.aliyun.com/) 按需 [开通服务](https://help.aliyun.com/zh/ocr/getting-started/use-process#4e7db41c583z8 "")。

## **注册阿里云账号并完成实名认证**

1. 在 [阿里云官网](https://www.aliyun.com/) 右上角，单击 **立即注册**。

2. 在 **注册账号** 页面，按照操作提示完成账号注册。



**重要**





创建成功的阿里云账号，会作为阿里云系统识别的资源消费账户，阿里云账号拥有该账户的所有权限。



为保证账号和密码的安全性，请勿借给他人使用，并定期更新密码。

3. 阿里云账号实名认证。

为保证后续操作顺利进行，请务必完成实名认证操作。阿里云账号需要进行实名制认证后，才可以购买和使用阿里云的产品。

1. 进入 [账号管理](https://account.console.aliyun.com/#/secure) 页面。

2. 在左侧导航栏，单击 **实名认证**，按照操作提示完成账号 [实名认证](https://help.aliyun.com/zh/account/account-verification-overview#DAS "")。

## **开通服务**

使用 [阿里云账号（主账号）](https://help.aliyun.com/zh/ocr/getting-started/use-process#e3e13dcd71y8x "") 或者RAM账号（ [子账号](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "")）登录 [文字识别OCR控制台](https://ocr.console.aliyun.com/) 按需开通服务。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4870455371/p890449.png)

文字识别OCR产品提供10类OCR服务，每类服务需单独开通，开通服务不产生费用。根据开通的服务不同，产品按月赠送200次或者一次性赠送50次 [免费额度](https://help.aliyun.com/zh/ocr/product-overview/free-quota "")，每调用成功一次，统一从阿里云账户中扣除一次免费额度。免费额度用完后，阿里云账单系统将根据调用量开始计费。

[RAM账号](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "") 是由阿里云账号创建并授权，需要确保RAM账号拥有 [AliyunOCRFullAccess](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "") 和 [AliyunBSSContractFullAccess](https://help.aliyun.com/zh/ram/developer-reference/aliyunbsscontractfullaccess "") 权限，否则无法通过该账号开通服务。

**说明**

前往 [RAM权限列表](https://help.aliyun.com/zh/ram/user-guide/view-the-permissions-of-a-ram-user#undefined "") 查看RAM账号拥有的权限。

接下来，您可以将SDK集成到业务系统中，使用免费额度进行OCR效果批量评测。

## **在线调用测试**

正式集成SDK前，建议您通过 [OpenAPI开发者门户](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeAllText?sdkStyle=dara&RegionId=cn-hangzhou) 在线调用文字识别API服务，此门户提供多语言SDK示例代码以及SDK依赖信息，帮助您了解代码调用逻辑，降低后续使用API的难度。

## 调用 **SDK**

以OCR统一识别服务进行身份证识别为例，介绍SDK集成和调用流程。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4870455371/p891556.png)

### **获取访问密钥**

集成SDK前，请确保您已获取访问密钥（ [AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")，简称AK）。通过SDK调用阿里云服务时，发起的请求会携带AccessKey ID和AccessKey Secret加密请求内容生成的签名，进行身份验证及请求合法性校验。

1. 将鼠标悬浮在控制台右上方的账号图标上，单击 **AccessKey管理**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4870455371/p890291.png)

2. 在 **AccessKey** 页面，查看AccessKey信息。

![image](<Base64-Image-Removed>)

如果AccessKey列表为空或者没有已启用的AccessKey，前往 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")。


### **将** AccessKey **配置到环境变量**

建议您将AccessKey写入环境变量，避免在代码里显式地配置AccessKey，降低AccessKey泄漏风险。

Windows系统

macOS系统

Linux系统

在Windows系统中，您可以使用CMD、PowerShell配置环境变量，或者通过系统属性编辑环境变量。

CMD

PowerShell

通过系统属性编辑环境变量

添加永久性环境变量

添加临时性环境变量

如果您希望环境变量在当前用户的所有新会话中生效，可以按如下操作。

1. 在CMD中运行以下命令。















```bash
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
setx ALIBABA_CLOUD_ACCESS_KEY_ID <access_key_id>
setx ALIBABA_CLOUD_ACCESS_KEY_SECRET <access_key_secret>
```

2. 打开一个新的CMD窗口。

3. 在新的CMD窗口运行以下命令，检查环境变量是否生效。















```bash
echo %ALIBABA_CLOUD_ACCESS_KEY_ID%
echo %ALIBABA_CLOUD_ACCESS_KEY_SECRET%
```


如果您仅希望在当前会话中使用该环境变量，可以在CMD中运行以下命令。

```bash
# <access_key_id>需替换为您的AccessKey ID，<ACCESS_KEY_SECRET>替换为您的AccessKey Secret。
set ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
set ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```

您可以在当前会话运行以下命令检查环境变量是否生效。

```bash
echo %ALIBABA_CLOUD_ACCESS_KEY_ID%
echo %ALIBABA_CLOUD_ACCESS_KEY_SECRET%
```

添加永久性环境变量

添加临时性环境变量

如果您希望环境变量在当前用户的所有新会话中生效，可以按如下操作。

1. 在PowerShell中运行以下命令。















```powershell
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
[Environment]::SetEnvironmentVariable("ALIBABA_CLOUD_ACCESS_KEY_ID", "<access_key_id>", [EnvironmentVariableTarget]::User)
[Environment]::SetEnvironmentVariable("ALIBABA_CLOUD_ACCESS_KEY_SECRET", "<access_key_secret>", [EnvironmentVariableTarget]::User)
```

2. 打开一个新的PowerShell窗口。

3. 在新的PowerShell窗口运行以下命令，检查环境变量是否生效。















```powershell
echo $env:ALIBABA_CLOUD_ACCESS_KEY_ID
echo $env:ALIBABA_CLOUD_ACCESS_KEY_SECRET
```


如果您仅希望在当前会话中使用该环境变量，可以在PowerShell中运行以下命令。

```powershell
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
$env:ALIBABA_CLOUD_ACCESS_KEY_ID = "<access_key_id>"
$env:ALIBABA_CLOUD_ACCESS_KEY_SECRET = "<access_key_secret>"
```

您可以在当前会话运行以下命令检查环境变量是否生效。

```powershell
echo $env:ALIBABA_CLOUD_ACCESS_KEY_ID
echo $env:ALIBABA_CLOUD_ACCESS_KEY_SECRET
```

- **我的电脑** 右键，单击 **属性；** 打开 **设置** 界面，单击 **高级系统设置**，打开 **系统属性** 界面。

![image](<Base64-Image-Removed>)

- 在 **系统属性** 界面，单击 **环境变量**，打开 **环境变量** 界面。

![image](<Base64-Image-Removed>)

- 在界面下方 **系统变量** 中，单击 **新建**，打开 **新建系统变量**。

![image](<Base64-Image-Removed>)

- **变量名** 填入：分别新建您的ALIBABA\_CLOUD\_ACCESS\_KEY\_ID、ALIBABA\_CLOUD\_ACCESS\_KEY\_SECRET **，** 变量值填入您的`<access_key_id>`与`<access_key_secret>`。

![image](<Base64-Image-Removed>)![image](<Base64-Image-Removed>)


填入后，分别点击三个界面的确定后关闭。至此，环境变量已配置成功。

您可以在终端运行以下命令检查环境变量是否生效。

```bash
echo %ALIBABA_CLOUD_ACCESS_KEY_ID%
echo %ALIBABA_CLOUD_ACCESS_KEY_SECRET%
```

添加永久性环境变量

添加临时性环境变量

如果您希望环境变量在当前用户的所有新会话中生效，可以添加永久性环境变量。

1. 在终端中执行以下命令，查看默认Shell类型。















```bash
echo $SHELL
```

2. 根据默认Shell类型进行操作。






Zsh



Bash



















1. 执行以下命令来将环境变量设置追加到 `~/.zshrc` 文件中。















      ```zsh
      # <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
      echo "export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>" >> ~/.zshrc
      echo "export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>" >> ~/.zshrc
      ```



      也可以手动修改`~/.zshrc` 文件。



      **手动修改**






      执行以下命令，打开Shell配置文件。

















      ```zsh
      nano ~/.zshrc
      ```





      在配置文件中添加以下内容。

















      ```zsh
      # <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
      export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
      export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
      ```





      在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















      ```zsh
      source ~/.zshrc
      ```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















      ```zsh
      echo $ALIBABA_CLOUD_ACCESS_KEY_ID
      echo $ALIBABA_CLOUD_ACCESS_KEY_SECRET
      ```


1. 执行以下命令来将环境变量设置追加到 `~/.bash_profile` 文件中。















      ```bash
      # <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
      echo "export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>" >> ~/.bash_profile
      echo "export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>" >> ~/.bash_profile
      ```



      也可以手动修改`~/.bash_profile` 文件。



      **手动修改**






      执行以下命令，打开Shell配置文件。

















      ```bash
      nano ~/.bash_profile
      ```





      在配置文件中添加以下内容。

















      ```bash
      # <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
      export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
      export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
      ```





      在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















      ```zsh
      source ~/.bash_profile
      ```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















      ```zsh
      echo $ALIBABA_CLOUD_ACCESS_KEY_ID
      echo $ALIBABA_CLOUD_ACCESS_KEY_SECRET
      ```


如果您仅希望在当前会话中使用该环境变量，可以添加临时性环境变量。

1. 执行以下命令。















```bash
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```

2. 执行以下命令，验证该环境变量是否生效。















```bash
echo $ALIBABA_CLOUD_ACCESS_KEY_ID
echo $ALIBABA_CLOUD_ACCESS_KEY_SECRET
```


添加永久性环境变量

添加临时性环境变量

如果您希望环境变量在当前用户的所有新会话中生效，可以添加永久性环境变量。

1. 执行以下命令来将环境变量设置追加到`~/.bashrc`文件中。















```bash
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
echo "export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>" >> ~/.bashrc
echo "export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>" >> ~/.bashrc
```



也可以手动修改`~/.bashrc`文件。



**手动修改**






执行以下命令，打开`~/.bashrc`文件。

















```zsh
nano ~/.bashrc
```





在配置文件中添加以下内容。

















```bash
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```





在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















```bash
source ~/.bashrc
```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















```bash
echo $ALIBABA_CLOUD_ACCESS_KEY_ID
echo $ALIBABA_CLOUD_ACCESS_KEY_SECRET
```


如果您仅希望在当前会话中使用该环境变量，可以添加临时性环境变量。

1. 执行以下命令。















```bash
# <access_key_id>需替换为您的AccessKey ID，<access_key_secret>替换为您的AccessKey Secret。
export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```

2. 执行以下命令，验证该环境变量是否生效。















```bash
echo $ALIBABA_CLOUD_ACCESS_KEY_ID
echo $ALIBABA_CLOUD_ACCESS_KEY_SECRET
```


### **选择开发语言**

选择您需要的语言调用文字识别API服务。

Java

Python

Go

#### **步骤 1：配置Java环境**

##### **检查Java环境**

在终端中运行以下命令查看当前环境是否安装了Java：

```bash
java -version
```

要求Java 8或以上版本，通过打印信息的第一行确认Java版本，例如打印信息：`openjdk version "16.0.1" 2021-04-20`表明当前Java版本为Java 16。如果当前环境没有Java，或版本低于Java 8，前往 [Java](https://www.oracle.com/cn/java/technologies/downloads/) 下载与安装。

##### **安装SDK**

在Maven工程中使用OCR Java SDK，只需在`pom.xml`中加入相应依赖即可。以在<dependencies>中加入3.1.2版本的依赖为例：

```xml
<dependency>
  <groupId>com.aliyun</groupId>
  <artifactId>ocr_api20210707</artifactId>
  <version>3.1.2</version>
</dependency>
```

#### **步骤 2：调用文字识别OCR接口**

运行以下代码调用文字识别API：

```java
import com.aliyun.ocr_api20210707.models.RecognizeAllTextResponse;
import com.aliyun.tea.*;

public class Sample {

    public static com.aliyun.ocr_api20210707.Client createClient() throws Exception {
        com.aliyun.teaopenapi.models.Config config = new com.aliyun.teaopenapi.models.Config()
                // 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_ID。
                .setAccessKeyId(System.getenv("ALIBABA_CLOUD_ACCESS_KEY_ID"))
                // 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_SECRET。
                .setAccessKeySecret(System.getenv("ALIBABA_CLOUD_ACCESS_KEY_SECRET"));
        // 默认公网接入地址为"ocr-api.cn-hangzhou.aliyuncs.com"，若您需要使用vpc域名访问，请确保您的ecs建立在杭州region，vpc接入地址为"ocr-api-vpc.cn-hangzhou.aliyuncs.com"
        config.endpoint = "ocr-api.cn-hangzhou.aliyuncs.com";
        return new com.aliyun.ocr_api20210707.Client(config);
    }

    public static void main(String[] args_) throws Exception {
        java.util.List<String> args = java.util.Arrays.asList(args_);
        com.aliyun.ocr_api20210707.Client client = Sample.createClient();
        com.aliyun.ocr_api20210707.models.RecognizeAllTextRequest recognizeAllTextRequest = new com.aliyun.ocr_api20210707.models.RecognizeAllTextRequest()
                .setUrl("https://img.alicdn.com/tfs/TB1q5IeXAvoK1RjSZFNXXcxMVXa-483-307.jpg")
                .setType("IdCard");
        com.aliyun.teautil.models.RuntimeOptions runtime = new com.aliyun.teautil.models.RuntimeOptions();
        try {
            RecognizeAllTextResponse resp = client.recognizeAllTextWithOptions(recognizeAllTextRequest, runtime);
            System.out.println(com.aliyun.teautil.Common.toJSONString(resp.body.data));
        } catch (TeaException error) {
            // 此处仅做打印展示，请谨慎对待异常处理，在工程项目中切勿直接忽略异常。
            // 错误 message
            System.out.println(error.getMessage());
            // 诊断地址
            System.out.println(error.getData().get("Recommend"));
            com.aliyun.teautil.Common.assertAsString(error.message);
        } catch (Exception _error) {
            TeaException error = new TeaException(_error.getMessage(), _error);
            // 此处仅做打印展示，请谨慎对待异常处理，在工程项目中切勿直接忽略异常。
            // 错误 message
            System.out.println(error.getMessage());
            // 诊断地址
            System.out.println(error.getData().get("Recommend"));
            com.aliyun.teautil.Common.assertAsString(error.message);
        }
    }
}
```

**单击查看运行结果**

```json
{
	"height": 307,
	"subImageCount": 1,
	"subImages": [{\
		"angle": 0,\
		"kvInfo": {\
			"data": {\
				"address": "上海市西藏南路-瞿溪路弘辉名苑",\
				"ethnicity": "汉",\
				"sex": "女",\
				"name": "方大呆",\
				"idNumber": "371002200610020000",\
				"birthDate": "2006年10月2日"\
			},\
			"kvCount": 6,\
			"kvDetails": {\
				"address": {\
					"keyName": "address",\
					"keyConfidence": 100,\
					"value": "上海市西藏南路-瞿溪路弘辉名苑",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				},\
				"ethnicity": {\
					"keyName": "ethnicity",\
					"keyConfidence": 100,\
					"value": "汉",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				},\
				"sex": {\
					"keyName": "sex",\
					"keyConfidence": 100,\
					"value": "女",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				},\
				"name": {\
					"keyName": "name",\
					"keyConfidence": 100,\
					"value": "方大呆",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				},\
				"idNumber": {\
					"keyName": "idNumber",\
					"keyConfidence": 100,\
					"value": "371002200610020000",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				},\
				"birthDate": {\
					"keyName": "birthDate",\
					"keyConfidence": 100,\
					"value": "2006年10月2日",\
					"valueConfidence": 100,\
					"valueAngle": 0\
				}\
			}\
		},\
		"qualityInfo": {\
			"isCopy": false\
		},\
		"subImageId": 0,\
		"type": "身份证正面"\
	}],
	"width": 483
}
```

##### **步骤 1：配置 Python 环境**

##### **检查Python环境**

在终端中输入以下命令，查看当前计算环境是否安装了Python：

```bash
# 如果运行失败，您可以将python替换成python3再运行
python -V
```

要求Python 3.0及以上版本。如果您没有安装Python，或版本不符合要求，请参考 [Python](https://help.aliyun.com/zh/sdk/developer-reference/installing-python "") 进行安装。

##### **配置虚拟环境（可选）**

如果您的Python已安装完成，可以创建一个虚拟环境来安装文字识别OCR Python SDK，避免与其它项目发生依赖冲突。

1. **创建虚拟环境**

运行以下命令，创建一个命名为 **.venv** 的虚拟环境：















```shell
# 如果运行失败，您可以将python替换成python3再运行
python -m venv .venv
```

2. **激活虚拟环境**

如果是windows系统，运行以下命令激活虚拟环境：















```shell
.venv\Scripts\activate
```



如果是macOS或者Linux系统，运行以下命令激活虚拟环境：















```shell
source .venv/bin/activate
```


##### **安装SDK**

执行以下命令安装Python SDK：

```shell
pip install alibabacloud_ocr_api20210707==3.1.2
```

### **步骤 2：调用文字识别OCR接口**

您可以新建一个Python文件，命名为`hello_ocr.py`，将以下代码复制到`hello_ocr.py`中并保存。

```python
# -*- coding: utf-8 -*-
import os
import sys

from typing import List

from alibabacloud_ocr_api20210707.client import Client as ocr_api20210707Client
from alibabacloud_tea_openapi import models as open_api_models
from alibabacloud_ocr_api20210707 import models as ocr_api_20210707_models
from alibabacloud_tea_util import models as util_models
from alibabacloud_tea_util.client import Client as UtilClient

class Sample:
    def __init__(self):
        pass

    @staticmethod
    def create_client() -> ocr_api20210707Client:
        config = open_api_models.Config(
            # 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_ID。,
            access_key_id=os.environ['ALIBABA_CLOUD_ACCESS_KEY_ID'],
            # 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_SECRET。,
            access_key_secret=os.environ['ALIBABA_CLOUD_ACCESS_KEY_SECRET']
        )
        # 默认公网接入地址为"ocr-api.cn-hangzhou.aliyuncs.com"，若您需要使用vpc域名访问，请确保您的ecs建立在杭州region，vpc接入地址为"ocr-api-vpc.cn-hangzhou.aliyuncs.com"
        config.endpoint = f'ocr-api.cn-hangzhou.aliyuncs.com'
        return ocr_api20210707Client(config)

    @staticmethod
    def main(
        args: List[str],
    ) -> None:
        client = Sample.create_client()
        recognize_all_text_request = ocr_api_20210707_models.RecognizeAllTextRequest(
            url='https://img.alicdn.com/tfs/TB1q5IeXAvoK1RjSZFNXXcxMVXa-483-307.jpg',
            type='IdCard'
        )
        runtime = util_models.RuntimeOptions()
        try:
            resp = client.recognize_all_text_with_options(recognize_all_text_request, runtime)
            print(resp.body.data)
        except Exception as error:
            # 此处仅做打印展示，请谨慎对待异常处理，在工程项目中切勿直接忽略异常。
            # 错误 message
            print(error.message)
            # 诊断地址
            print(error.data.get("Recommend"))
            UtilClient.assert_as_string(error.message)

    @staticmethod
    async def main_async(
        args: List[str],
    ) -> None:
        client = Sample.create_client()
        recognize_all_text_request = ocr_api_20210707_models.RecognizeAllTextRequest(
            url='https://img.alicdn.com/tfs/TB1q5IeXAvoK1RjSZFNXXcxMVXa-483-307.jpg',
            type='IdCard'
        )
        runtime = util_models.RuntimeOptions()
        try:
            # 复制代码运行请自行打印 API 的返回值
            await client.recognize_all_text_with_options_async(recognize_all_text_request, runtime)
        except Exception as error:
            # 此处仅做打印展示，请谨慎对待异常处理，在工程项目中切勿直接忽略异常。
            # 错误 message
            print(error.message)
            # 诊断地址
            print(error.data.get("Recommend"))
            UtilClient.assert_as_string(error.message)

if __name__ == '__main__':
    Sample.main(sys.argv[1:])
```

**单击查看运行结果**

```json
{
	'Height': 307,
	'SubImageCount': 1,
	'SubImages': [{\
		'Angle': 0,\
		'FigureInfo': {},\
		'KvInfo': {\
			'Data': {\
				'address': '上海市西藏南路-瞿溪路弘辉名苑',\
				'ethnicity': '汉',\
				'sex': '女',\
				'name': '方大呆',\
				'idNumber': '371002200610020000',\
				'birthDate': '2006年10月2日'\
			},\
			'KvCount': 6,\
			'KvDetails': {\
				'address': {\
					'KeyName': 'address',\
					'KeyConfidence': 100,\
					'Value': '上海市西藏南路-瞿溪路弘辉名苑',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				},\
				'ethnicity': {\
					'KeyName': 'ethnicity',\
					'KeyConfidence': 100,\
					'Value': '汉',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				},\
				'sex': {\
					'KeyName': 'sex',\
					'KeyConfidence': 100,\
					'Value': '女',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				},\
				'name': {\
					'KeyName': 'name',\
					'KeyConfidence': 100,\
					'Value': '方大呆',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				},\
				'idNumber': {\
					'KeyName': 'idNumber',\
					'KeyConfidence': 100,\
					'Value': '371002200610020000',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				},\
				'birthDate': {\
					'KeyName': 'birthDate',\
					'KeyConfidence': 100,\
					'Value': '2006年10月2日',\
					'ValueConfidence': 100,\
					'ValuePoints': [],\
					'ValueAngle': 0\
				}\
			}\
		},\
		'QualityInfo': {\
			'IsCopy': False\
		},\
		'SubImageId': 0,\
		'SubImagePoints': [],\
		'Type': '身份证正面'\
	}],
	'Width': 483
}
```

##### **步骤 1：配置 Go环境**

##### **检查Go环境**

在终端中运行以下命令查看当前环境是否安装了Go：

```bash
go version
```

要求Go 1.10或以上版本。您可以查看打印信息中的第一行确认Go版本，例如打印信息：`go version go1.22.2`表明当前Go版本为Go 1.22.2。如果您当前计算环境没有Go，或版本低于1.10，请前往 [Go](https://golang.google.cn/dl/) 进行下载。

##### **安装SDK**

执行以下命令安装Go SDK依赖：

```go
go get github.com/alibabacloud-go/ocr-api-20210707/v3
```

### **步骤 2：** 调用文字识别OCR接口

您可以新建一个Go文件，命名为`hello_ocr.go`，将以下代码复制到`hello_ocr.go`中并保存。

```go
package main

import (
	"encoding/json"
	"fmt"
	openapi "github.com/alibabacloud-go/darabonba-openapi/v2/client"
	ocr_api20210707 "github.com/alibabacloud-go/ocr-api-20210707/v3/client"
	util "github.com/alibabacloud-go/tea-utils/v2/service"
	"github.com/alibabacloud-go/tea/tea"
	"os"
	"strings"
)

func CreateClient() (_result *ocr_api20210707.Client, _err error) {
	config := &openapi.Config{
		// 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_ID。
		AccessKeyId: tea.String(os.Getenv("ALIBABA_CLOUD_ACCESS_KEY_ID")),
		// 必填，请确保代码运行环境设置了环境变量 ALIBABA_CLOUD_ACCESS_KEY_SECRET。
		AccessKeySecret: tea.String(os.Getenv("ALIBABA_CLOUD_ACCESS_KEY_SECRET")),
	}
	// 默认公网接入地址为"ocr-api.cn-hangzhou.aliyuncs.com"，若您需要使用vpc域名访问，请确保您的ecs建立在杭州region，vpc接入地址为"ocr-api-vpc.cn-hangzhou.aliyuncs.com"
	config.Endpoint = tea.String("ocr-api.cn-hangzhou.aliyuncs.com")
	_result = &ocr_api20210707.Client{}
	_result, _err = ocr_api20210707.NewClient(config)
	return _result, _err
}

func _main(args []*string) (_err error) {
	client, _err := CreateClient()
	if _err != nil {
		return _err
	}

	recognizeAllTextRequest := &ocr_api20210707.RecognizeAllTextRequest{
		Url:  tea.String("https://img.alicdn.com/tfs/TB1q5IeXAvoK1RjSZFNXXcxMVXa-483-307.jpg"),
		Type: tea.String("IdCard"),
	}
	runtime := &util.RuntimeOptions{}
	tryErr := func() (_e error) {
		defer func() {
			if r := tea.Recover(recover()); r != nil {
				_e = r
			}
		}()
		resp, _err := client.RecognizeAllTextWithOptions(recognizeAllTextRequest, runtime)
		if _err != nil {
			return _err
		}
		fmt.Println(resp.Body.Data)

		return nil
	}()

	if tryErr != nil {
		var error = &tea.SDKError{}
		if _t, ok := tryErr.(*tea.SDKError); ok {
			error = _t
		} else {
			error.Message = tea.String(tryErr.Error())
		}
		// 此处仅做打印展示，请谨慎对待异常处理，在工程项目中切勿直接忽略异常。
		// 错误 message
		fmt.Println(tea.StringValue(error.Message))
		// 诊断地址
		var data interface{}
		d := json.NewDecoder(strings.NewReader(tea.StringValue(error.Data)))
		d.Decode(&data)
		if m, ok := data.(map[string]interface{}); ok {
			recommend, _ := m["Recommend"]
			fmt.Println(recommend)
		}
		_, _err = util.AssertAsString(error.Message)
		if _err != nil {
			return _err
		}
	}
	return _err
}

func main() {
	err := _main(tea.StringSlice(os.Args[1:]))
	if err != nil {
		panic(err)
	}
}
```

**单击查看运行结果**

```json
{
   "Height": 307,
   "SubImageCount": 1,
   "SubImages": [\
      {\
         "Angle": 0,\
         "KvInfo": {\
            "Data": {\
               "address": "上海市西藏南路-瞿溪路弘辉名苑",\
               "birthDate": "2006年10月2日",\
               "ethnicity": "汉",\
               "idNumber": "371002200610020000",\
               "name": "方大呆",\
               "sex": "女"\
            },\
            "KvCount": 6,\
            "KvDetails": {\
               "address": {\
                  "KeyName": "address",\
                  "KeyConfidence": 100,\
                  "Value": "上海市西藏南路-瞿溪路弘辉名苑",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               },\
               "birthDate": {\
                  "KeyName": "birthDate",\
                  "KeyConfidence": 100,\
                  "Value": "2006年10月2日",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               },\
               "ethnicity": {\
                  "KeyName": "ethnicity",\
                  "KeyConfidence": 100,\
                  "Value": "汉",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               },\
               "idNumber": {\
                  "KeyName": "idNumber",\
                  "KeyConfidence": 100,\
                  "Value": "371002200610020000",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               },\
               "name": {\
                  "KeyName": "name",\
                  "KeyConfidence": 100,\
                  "Value": "方大呆",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               },\
               "sex": {\
                  "KeyName": "sex",\
                  "KeyConfidence": 100,\
                  "Value": "女",\
                  "ValueConfidence": 100,\
                  "ValueAngle": 0\
               }\
            }\
         },\
         "QualityInfo": {\
            "IsCopy": false\
         },\
         "SubImageId": 0,\
         "Type": "身份证正面"\
      }\
   ],
   "Width": 483
}
```

## 后续步骤

- 当您需要长期调用文字识别OCR服务时，可以查阅 [计费](https://help.aliyun.com/zh/ocr/product-overview/product-billing/ "") 文档选择合适的计费模式。

- 当您需要统计接口调用量时，可以前往文字识别控制台-数据监控模块，接口调用量筛选框分别为查询API、时间范围，点击查询后调用量统计及QPS统计展示为图表，横坐标为时间轴。鼠标悬停在图表中，会显示对应横坐标日期的数据量。目前仅支持账号维度的调用量统计，不支持根据调用IP的调用量统计。

- 通过 [API概览](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-overview "") 快速了解全量服务调用信息。

- 如果您在使用过程中遇到任何问题，可以先查阅 [常见问题](https://help.aliyun.com/zh/ocr/support/faq/ "") 文档尝试解决。如问题仍无法解决，可加入钉钉群（35208328）寻求解答和支持。


## **OCR识别清单**

|     |     |
| --- | --- |
| **OCR识别类型** | **名称** |
| [OCR统一识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizealltext "") | - **通用类型**：通用文字识别高精版、通用文字识别基础版本、通用手写体、电商图片文字、通用多语言、表格、二维码、条形码。<br>  <br>- **证照类型**：身份证、银行卡、社保卡、户口本、出生证明、中国护照、国际护照、往来港澳台通行证、来往（大陆）内地通行证、中国香港身份证、国际身份证、不动产权证。<br>  <br>- **车辆物流**：行驶证、驾驶证、车牌、车辆VIN码、车辆合格证、机车注册证、面单。<br>  <br>- **票据类型**：增值税发票、机动车销售统一发票、定额发票、增值税发票卷票、通用机打发票、非税收入发票、二手车销售统一发票、出租车发票、税收完税证明、银行承兑汇票、客运车船票、火车票、航空行程单、酒店流水、购物小票、电商订单页、网约车行程单、支付详情页、过路过桥发票。<br>  <br>- **企业资质**：营业执照、公章、医疗器械经营许可证、医疗器械生产许可证、化妆品生产许可证、国际企业执照识别、商标注册证、食品经营许可证、食品生产许可证、第二类医疗器械经营备案凭证、银行开户许可证。<br>  <br>- **混贴票据**：混贴发票。 |

| [通用文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-general-character-recognition/ "") | 通用文字识别、全文识别高精版、通用手写体、表格、电商图片文字、文档结构化。 |
| [个人证照识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-personal-license-identification/ "") | 身份证、国际护照、户口本、不动产权证、银行卡、出生证明、中国护照、往来港澳台通行证、来往（大陆）内地通行证、中国香港身份证、社保卡、国际身份证。 |
| [企业资质识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-enterprise-qualification-identification/ "") | 营业执照、银行开户许可证、商标注册证、食品经营许可证、食品生产许可证、医疗器械生产许可证、医疗器械经营许可证、第二类医疗器械经营备案凭证、化妆品生产许可证、国际企业执照、营业执照核验。 |
| [票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/ "") | 混贴发票、网约车行程单、增值税发票、火车票、定额发票、航空行程单、出租车发票、增值税发票卷票、机动车销售统一发票、二手车销售统一发票、通用机打发票、过路过桥发票、客运车船票、税收完税证明、电商订单页、支付详情页、非税收入发票、酒店流水、购物小票、银行承兑汇票、发票核验。 |
| [车辆物流识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-vehicle-logistics-identification/ "") | 车牌、行驶证、驾驶证、车辆VIN码、面单、机车注册证、车辆合格证。 |
| [教育场景识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-education-scene-recognition/ "") | 印刷体数学公式、题目、试卷切题、口算判题、整页试卷、精细版结构化。 |
| [小语种文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-small-language-character-recognition/ "") | 通用多语言、英语专项、日语、俄语、韩语、泰语、拉丁语。 |
| [票证核验](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-ticket-verification/ "") | 营业执照、发票。 |