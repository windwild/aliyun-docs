### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别闲时版](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition-off-peak-edition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code-1/).NET Demo

# .NET Demo

更新时间：2024-04-16 01:49:48

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Go Demo](https://help.aliyun.com/zh/isi/developer-reference/go-demo-1)[下一篇：Node.js Demo](https://help.aliyun.com/zh/isi/developer-reference/node-js-demo-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

示例说明

SDK安装

调用步骤

代码示例

本文介绍了如何使用阿里云智能语音服务提供的.NET SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference#topic-2170103 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## 示例说明

- 录音文件识别示例使用.Net SDK的CommonRequest提交识别请求和查询识别结果，采用RPC风格的POP API调用方式。

- 关于阿里云.NET SDK的详细介绍请参见 [使用.NET SDK](https://help.aliyun.com/document_detail/53095.html#concept-mkk-vpj-zdb "")。

- .NET SDK CommonRequest的使用方法请参见 [使用CommonRequest进行调用](https://help.aliyun.com/document_detail/61473.html#concept-ivk-p1k-zdb "")。


## SDK安装

您只需安装阿里云.NET SDK核心库，有如下两种安装方式：

- 添加核心库的DLL引用

1. 进入 [.NET SDK发布列表](https://develop.aliyun.com/tools/sdk?spm=a2c4g.11186623.2.14.648f2d7azA0DNp#/dotnet)，在SDK核心库处单击右侧 **适用于.NET 4.0及以上的DLL引用**。

2. 在Visual Studio的解决方案资源管理器，右键单击 **我的项目**，然后单击 **引用**。

3. 在弹出的菜单中单击 **添加引用**。

4. 在弹出的对话框中，单击 **浏览**，选择下载的DLL文件，单击 **确定**。
- 项目引入方式

1. 在命令行执行以下命令，在GitHub中下载SDK的源码。















     ```shell
     git clone https://github.com/aliyun/aliyun-openapi-net-sdk.git
     ```



     在目录aliyun-openapi-net-sdk中的aliyun-net-sdk-core/aliyun-net-sdk-core.vs2017.csproj文件（适用于VS2017），即.NET项目文件。

2. 在Visual Studio的界面中，右键单击 **我的解决方案**。

3. 选择 **添加 \> 现有项目**。

4. 在弹出的对话框中，选择源码中相应的.NET项目文件（如 aliyun-net-sdk-core.vs2010.csproj），单击 **打开**。

5. 右键单击您的项目，选择 **引用 \> 添加引用**。

## 调用步骤

1. 创建并初始化AcsClient。

2. 创建录音文件识别请求，并设置请求参数。

3. 提交录音文件识别请求，处理服务端返回的响应，获取任务ID。

4. 创建识别结果查询请求，设置查询参数为任务ID。

5. 轮询识别结果。


## 代码示例

**说明**

[下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。该录音文件为PCM编码格式16000 Hz采样率，管控台设置的模型为通用模型；如果使用其他录音文件，请在请求参数中填入对应的编码格式和采样率，并在管控台设置对应的模型，模型设置请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

```java
using System;
using Newtonsoft.Json.Linq;
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Exceptions;
using Aliyun.Acs.Core.Profile;
using Aliyun.Acs.Core.Http;
namespace FileTrans
{
    class FileTrans
    {
        // 地域ID，固定值。
        public const string REGIONID = "cn-shanghai";
        public const string PRODUCT = "SpeechFileTranscriberLite";
        public const string DOMAIN = "speechfiletranscriberlite.cn-shanghai.aliyuncs.com";
        public const string API_VERSION = "2021-12-21";
        public const string POST_REQUEST_ACTION = "SubmitTask";
        public const string GET_REQUEST_ACTION = "GetTaskResult";
        // 请求参数
        public const string KEY_APP_KEY = "appkey";
        public const string KEY_FILE_LINK = "file_link";
        public const string KEY_ENABLE_WORDS = "enable_words";
        // 响应参数
        public const string KEY_TASK = "Task";
        public const string KEY_TASK_ID = "TaskId";
        public const string KEY_STATUS_TEXT = "StatusText";
        // 状态值
        public const string STATUS_SUCCESS = "SUCCESS";
        public const string STATUS_RUNNING = "RUNNING";
        public const string STATUS_QUEUEING = "QUEUEING";
        static void Main(string[] args)
        {
            if (args.Length < 3)
            {
                System.Console.WriteLine("FileTrans Demo need params: <AccessKey Id> <AccessKey Secret> <app-key>");
                return;
            }
            string accessKeyId = args[0];
            string accessKeySecret = args[1];
            string appKey = args[2];
            string fileLink = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav";
            /**
             * 创建阿里云鉴权对象
             */
            IClientProfile profile = DefaultProfile.GetProfile(
                REGIONID,
                accessKeyId,
                accessKeySecret
                );
            DefaultAcsClient client = new DefaultAcsClient(profile);
            try
            {
                /**
                 * 创建录音文件识别请求，设置请求参数。
                 */
                CommonRequest request = new CommonRequest();
                request.Domain = DOMAIN;
                request.Version = API_VERSION;
                request.Action = POST_REQUEST_ACTION;
                request.Product = PRODUCT;
                request.Method = MethodType.POST;
                // 设置task，以JSON字符串形式设置到请求Body中。
                JObject obj = new JObject();
                obj[KEY_APP_KEY] = appKey;
                obj[KEY_FILE_LINK] = fileLink;
                // 设置是否输出词信息，默认为false。
                obj[KEY_ENABLE_WORDS] = false;
                string task = obj.ToString();
                request.AddBodyParameters(KEY_TASK, task);
                /**
                 * 提交录音文件识别请求，处理服务端返回的响应。
                 */
                CommonResponse response = client.GetCommonResponse(request);
                System.Console.WriteLine(response.Data);
                if (response.HttpStatus != 200)
                {
                    System.Console.WriteLine("录音文件识别请求失败： " + response.HttpStatus);
                    return;
                }
                // 获取录音文件识别请求任务ID，以供识别结果查询使用。
                string taskId = "";
                JObject jsonObj = JObject.Parse(response.Data);
                string statusText = jsonObj[KEY_STATUS_TEXT].ToString();
                if (statusText.Equals(STATUS_SUCCESS))
                {
                    System.Console.WriteLine("录音文件识别请求成功响应!");
                    taskId = jsonObj[KEY_TASK_ID].ToString();
                }
                else
                {
                    System.Console.WriteLine("录音文件识别请求失败!");
                    return;
                }
                /**
                 * 创建识别结果查询请求，并设置查询参数为任务ID。
                 */
                CommonRequest getRequest = new CommonRequest();
                getRequest.Domain = DOMAIN;
                getRequest.Version = API_VERSION;
                getRequest.Action = GET_REQUEST_ACTION;
                getRequest.Product = PRODUCT;
                getRequest.Method = MethodType.GET;
                getRequest.AddQueryParameters(KEY_TASK_ID, taskId);
                /**
                 * 提交录音文件识别结果查询请求
                 * 以轮询的方式进行识别结果的查询，直到服务端返回的状态描述为“SUCCESS”、“SUCCESS_WITH_NO_VALID_FRAGMENT”，
                 * 或者为错误描述，则结束轮询。
                 */
                statusText = "";
                while (true)
                {
                    CommonResponse getResponse = client.GetCommonResponse(getRequest);
                    System.Console.WriteLine(getResponse.Data);
                    if (getResponse.HttpStatus != 200)
                    {
                        System.Console.WriteLine("识别结果查询请求失败，Http错误码：" + getResponse.HttpStatus);
                        break;
                    }
                    JObject jsonObj2 = JObject.Parse(getResponse.Data);
                    statusText = jsonObj2[KEY_STATUS_TEXT].ToString();
                    if (statusText.Equals(STATUS_RUNNING) || statusText.Equals(STATUS_QUEUEING))
                    {
                        // 继续轮询
                        System.Threading.Thread.Sleep(10 * 1000);
                    }
                    else
                    {
                        // 退出轮询
                        break;
                    }
                }
                if (statusText.Equals(STATUS_SUCCESS))
                {
                    System.Console.WriteLine("录音文件识别成功！");
                }
                else {
                    System.Console.WriteLine("录音文件识别失败！");
                }
            }
            catch (ServerException ex)
            {
                System.Console.WriteLine(ex.ToString());
            }
            catch (ClientException ex)
            {
                System.Console.WriteLine(ex.ToString());
            }
        }
    }
}
```