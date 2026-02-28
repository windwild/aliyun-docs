### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别闲时版](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition-off-peak-edition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code-1/)Go Demo

# Go Demo

更新时间：2025-04-08 02:26:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：C++ Demo](https://help.aliyun.com/zh/isi/developer-reference/c-demo)[下一篇：.NET Demo](https://help.aliyun.com/zh/isi/developer-reference/net-demo-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

示例说明

SDK安装

调用步骤

代码示例

本文介绍了如何使用阿里云智能语音服务提供的Go SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference#topic-2170103 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## 示例说明

- 录音文件识别示例使用Go SDK的CommonRequest提交识别请求和查询识别结果，采用RPC风格的POP API调用方式。

- 关于阿里云Go SDK请参见 [使用阿里云Go SDK](https://help.aliyun.com/document_detail/66217.html#concept-mkk-vpj-zdb "")。

- Go SDK CommonRequest的使用方法请参见 [使用CommonRequest进行调用](https://help.aliyun.com/document_detail/66221.html#concept-ivk-p1k-zdb "")。


## SDK安装

阿里云Go SDK支持Go 1.7及以上版本，您可以通过如下方式安装：

- 使用Glide（推荐）















```go
glide get github.com/aliyun/alibaba-cloud-sdk-go
```

- 使用govendor：















```go
go get -u github.com/aliyun/alibaba-cloud-sdk-go/sdk
```


## 调用步骤

1. 创建并初始化阿里云鉴权对象。鉴权使用阿里云账号的AccessKey ID和AccessKey Secret。

2. 创建录音文件识别请求，并设置请求参数。

3. 提交录音文件识别请求，处理服务端返回的响应同时获取任务ID。

4. 创建识别结果查询请求，设置查询参数为任务ID。

5. 轮询识别结果。


## 代码示例

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。该录音文件为PCM编码格式16000 Hz采样率，管控台设置的模型为通用模型。如果使用其他录音文件，请填入对应的编码格式和采样率，并在管控台设置对应的模型，模型设置请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


```go
package main
import (
    "github.com/aliyun/alibaba-cloud-sdk-go/sdk/requests"
    "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
    "fmt"
    "encoding/json"
    "time"
)
func main() {
    // 地域ID，固定值。
    const REGION_ID string = "cn-shanghai"
    const ENDPOINT_NAME string = "cn-shanghai"
    const PRODUCT string = "SpeechFileTranscriberLite"
    const DOMAIN string = "speechfiletranscriberlite.cn-shanghai.aliyuncs.com"
    const API_VERSION string = "2021-12-21"
    const POST_REQUEST_ACTION string = "SubmitTask"
    const GET_REQUEST_ACTION  string = "GetTaskResult"
    // 请求参数
    const KEY_APP_KEY string = "appkey"
    const KEY_FILE_LINK string = "file_link"
    const KEY_ENABLE_WORDS string = "enable_words"
    // 响应参数
    const KEY_TASK string = "Task"
    const KEY_TASK_ID string = "TaskId"
    const KEY_STATUS_TEXT string = "StatusText"
    const KEY_RESULT string = "Result"
    // 状态值
    const STATUS_SUCCESS string = "SUCCESS"
    const STATUS_RUNNING string = "RUNNING"
    const STATUS_QUEUEING string = "QUEUEING"
    var accessKeyId string = os.Getenv("ALIYUN_AK_ID")     //获取AccessKey ID和AccessKey Secret请前往控制台：https://ram.console.aliyun.com/manage/ak
    var accessKeySecret string = os.Getenv("ALIYUN_AK_SECRET")
    var appKey string = os.Getenv("NLS_APP_KEY")
    var fileLink string = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav"
    c := sdk.NewConfig()
    credential := credentials.NewAccessKeyCredential(accessKeyId, accessKeySecret)
    client, err := sdk.NewClientWithOptions(REGION_ID, c, credential)
    if err != nil {
        panic(err)
    }
    postRequest := requests.NewCommonRequest()
    postRequest.Domain = DOMAIN
    postRequest.Version = API_VERSION
    postRequest.Product = PRODUCT
    postRequest.ApiName = POST_REQUEST_ACTION
    postRequest.Method = "POST"
    mapTask := make(map[string]string)
    mapTask[KEY_APP_KEY] = appKey
    mapTask[KEY_FILE_LINK] = fileLink
    // 设置是否输出词信息，默认为false。
    mapTask[KEY_ENABLE_WORDS] = "false"
    task, err := json.Marshal(mapTask)
    if err != nil {
        panic(err)
    }
    postRequest.FormParams[KEY_TASK] = string(task)
    postResponse, err := client.ProcessCommonRequest(postRequest)
    if err != nil {
        panic(err)
    }
    postResponseContent := postResponse.GetHttpContentString()
    fmt.Println(postResponseContent)
    if (postResponse.GetHttpStatus() != 200) {
        fmt.Println("录音文件识别请求失败，Http错误码: ", postResponse.GetHttpStatus())
        return
    }
    var postMapResult map[string]interface{}
    err = json.Unmarshal([]byte(postResponseContent), &postMapResult)
    if err != nil {
        panic(err)
    }
    var taskId string = ""
    var statusText string = ""
    statusText = postMapResult[KEY_STATUS_TEXT].(string)
    if statusText == STATUS_SUCCESS {
        fmt.Println("录音文件识别请求成功响应!")
        taskId = postMapResult[KEY_TASK_ID].(string)
    } else {
        fmt.Println("录音文件识别请求失败!")
        return
    }
    getRequest := requests.NewCommonRequest()
    getRequest.Domain = DOMAIN
    getRequest.Version = API_VERSION
    getRequest.Product = PRODUCT
    getRequest.ApiName = GET_REQUEST_ACTION
    getRequest.Method = "GET"
    getRequest.QueryParams[KEY_TASK_ID] = taskId
    statusText = ""
    for true {
        getResponse, err := client.ProcessCommonRequest(getRequest)
        if err != nil {
            panic(err)
        }
        getResponseContent := getResponse.GetHttpContentString()
        fmt.Println("识别查询结果：", getResponseContent)
        if (getResponse.GetHttpStatus() != 200) {
            fmt.Println("识别结果查询请求失败，Http错误码：", getResponse.GetHttpStatus())
            break
        }
        var getMapResult map[string]interface{}
        err = json.Unmarshal([]byte(getResponseContent), &getMapResult)
        if err != nil {
            panic(err)
        }
        statusText = getMapResult[KEY_STATUS_TEXT].(string)
        if statusText == STATUS_RUNNING || statusText == STATUS_QUEUEING {
            time.Sleep(10 * time.Second)
        } else {
            break
        }
    }
    if statusText == STATUS_SUCCESS {
        fmt.Println("录音文件识别成功！")
    } else {
        fmt.Println("录音文件识别失败！")
    }
}
```