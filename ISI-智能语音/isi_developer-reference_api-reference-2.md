### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition/)接口说明

# 接口说明

更新时间：2025-10-15 05:17:56

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费和并发限制

使用限制

使用步骤

交互流程

各地域POP调用参数

接口调用方式

服务状态码

通用错误码

录音文件识别/录音文件识别闲时版错误码

历史版本说明

录音文件识别是针对已经录制完成的录音文件，进行离线识别的服务。录音文件识别是非实时的，识别的文件需要提交基于HTTP可访问的URL地址，不支持提交本地文件。

## **计费和并发限制**

- 录音文件识别提供试用版和商用版两种计费模式，详情请参见 [试用版和商用版](https://help.aliyun.com/zh/isi/product-overview/pricing#40ba8a7127hw1 "")。如果您需要将试用版升级为商用版，请参见 [试用版升级为商用版](https://help.aliyun.com/zh/isi/product-overview/billing-10#41bb3ea20c3v4 "")。

- 计费方式详情请参见 [计费方式](https://help.aliyun.com/zh/isi/product-overview/billing-10 "")。

- 并发限制请参见 [并发和QPS说明](https://help.aliyun.com/zh/isi/product-overview/faq-about-concurrency-and-monitoring "")。


## 使用限制

请在编码时严格遵循以下要求，否则可能导致识别失败（识别结果为空）。

- 支持单轨和双轨的WAV、MP3、MP4、M4A、WMA、AAC、OGG、AMR、FLAC格式录音文件识别。

- 音频文件大小不超过512 MB，视频文件大小不超过2 GB，文件总时长不超过12小时。

- 需要识别的录音文件必须存放在某服务上，可以通过URL访问。

  - 推荐使用阿里云OSS：如果OSS中文件访问权限为公开，可参见 [公共读Object](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects#concept-39607-zh/section-st4-efq-v5j "")，获取文件访问链接；如果OSS中文件访问权限为私有，可参见 [私有Object](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects#concept-39607-zh/section-wnz-0he-q20 "")，通过SDK生成有有效时间的访问链接。

  - 您也可以把录音文件存放在自行搭建的文件服务器，提供文件下载。请保证HTTP的响应头（Header）中Content-Length的长度值和Body中数据的真实长度一致，否则会导致下载失败。
- 上传的录音文件URL的访问权限需要设置为公开，URL中只能使用域名不能使用IP地址、不可包含空格，请尽量避免使用中文。




| 可用URL | 不可用URL |
| --- | --- |



|     |     |
| --- | --- |
| 可用URL | 不可用URL |
| https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav | - http://127.0.0.1/sample.wav<br>    <br>  - D:\\files\\sample.wav |

- 录音文件识别属于离线识别服务，对于并发数没有限制，对于QPS（Queries Per Second）的限制如下：

  - POST方式的录音文件识别请求调用接口，用户级别QPS限制为200。

  - GET方式的录音文件识别请求调用接口，用户级别QPS限制为500。

  - 录音文件识别结果查询接口，同一Taskid QPS限制为1。
- 新用户试用期3个月内，每隔24小时可免费识别2小时时长的文件转写服务。免费额度用完后，间隔24小时后可继续试用。

- 提交录音文件识别请求后，免费用户的识别任务在24小时内完成并返回识别文本。
付费用户的识别任务在3小时内完成并返回识别文本。识别结果在服务端可保存72小时。



**重要**





一次性上传大规模数据（半小时内上传超过500小时时长的录音）的除外。有大规模数据识别需求的用户，请联系售前专家。

- 支持调用方式：轮询方式和回调方式。

- 支持语言模型定制。更多信息请参见 [语言模型定制](https://help.aliyun.com/zh/isi/developer-reference/overview-2#topic-2644771 "")。

- 支持热词。更多信息请参见 [热词](https://help.aliyun.com/zh/isi/developer-reference/overview-1#topic-2572262 "")。

- 支持汉语普通话、方言、欧美英语等多种模型识别。语种和方言模型无法在编码时指定，需要在智能语音交互控制台的 [全部项目](https://nls-portal.console.aliyun.com/applist) 中对相关项目执行 **项目功能配置** 操作，选择对应的模型。详情请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

目前支持的语种和方言模型如下：

  - 语种






    |     |     |     |     |     |     |     |     |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | 语言 | 模型名称 | 采样率 | 标点 | ITN | 顺滑 | 语义断句 | 声音和文本对齐 |
    | 英语 | 通用-英文，教育直播-英文，教育内容分析-英文 | 16k | 支持 | 支持 | 支持 | 不支持 | 支持 |
    | 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 日语 | 通用-日语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 支持 |
    | 西班牙语 | 通用-西班牙语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 通用-西班牙客服通用 | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 阿拉伯语 | 通用-阿拉伯语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 哈萨克语 | 通用-哈萨克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 韩语 | 通用-韩语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 泰语 | 通用-泰语 | 16k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 通用-泰语客服通用 | 8k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 印尼语 | 通用-印尼语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 电话客服（通用） | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 俄语 | 通用-俄语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 越南语 | 通用-越南语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 通用-越南语客服通用 | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 法语 | 通用-法语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 德语 | 通用-德语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 意大利语 | 通用-意大利语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 印地语 | 通用-印地语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 马来语 | 通用-马来语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 通用-马来语客服通用 | 8k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 菲律宾语 | 通用-菲律宾语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 电话客服（通用） | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 泰米尔语 | 通用-泰米尔语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 葡萄牙语 | 通用-葡萄牙语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
    | 土耳其语 | 通用-土耳其语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 波兰语 | 通用-波兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 乌克兰语 | 通用-乌克兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 罗马尼亚语 | 通用-罗马尼亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 荷兰语 | 通用-荷兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 希腊语 | 通用-希腊语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 匈牙利语 | 通用-匈牙利语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 爪哇语 | 通用-爪哇语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 孟加拉语 | 通用-孟加拉语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 缅甸语 | 通用-缅甸语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 老挝语 | 通用-老挝语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 斯瓦希里语 | 通用-斯瓦希里语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 阿塞拜疆语 | 通用-阿塞拜疆语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 波斯语 | 通用-波斯语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 僧伽罗语 | 通用-僧伽罗语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 加泰罗尼亚语 | 通用-加泰罗尼亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 高棉语 | 通用-高棉语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 希伯来语 | 通用-希伯来语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 克罗地亚语 | 通用-克罗地亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 豪萨语 | 通用-豪萨语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 马拉地语 | 通用-马拉地语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 泰卢固语 | 通用-泰卢固语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 旁遮普语 | 通用-旁遮普语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 瑞典语 | 通用-瑞典语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 保加利亚语 | 通用-保加利亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 丹麦语 | 通用-丹麦语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 挪威语 | 通用-挪威语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 坎纳达语 | 通用-坎纳达语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 马拉雅拉姆语 | 通用-马拉雅拉姆语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 捷克语 | 通用-捷克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 乌尔都语 | 通用-乌尔都语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 尼泊尔语 | 通用-尼泊尔语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 蒙古语（外蒙） | 通用-蒙古语（外蒙） | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 乌兹别克语 | 通用-乌兹别克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |

  - 方言






    |     |     |     |     |     |     |     |     |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | 语言 | 模型名称 | 采样率 | 标点 | ITN | 顺滑 | 语义断句 | 声音和文本对齐 |
    | 粤语 | 通用-粤语 | 16k | 支持 | 支持 | 支持 | 不支持 | 支持 |
    | 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 不支持 | 支持 |
    | 粤中自由说 | 8k | 支持 | 支持 | 支持 | 不支持 | 不支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 粤语（繁体） | 通用-粤语（繁体） | 8k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 通用-粤语（繁体） | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
    | 四川话 | 通用-四川话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 湖北话 | 通用-湖北话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 通用-湖北话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 上海话 | 通用-上海话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
    | 湖南话 | 通用-湖南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 河南话 | 通用-河南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 通用-河南话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 浙江话 | 通用-浙江话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
    | 东北话 | 通用-东北话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 山东话 | 通用-山东话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 天津话 | 通用-天津话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 陕西话 | 通用-陕西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 山西话 | 通用-山西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 贵州话 | 通用-贵州话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 云南话 | 通用-云南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 甘肃话 | 通用-甘肃话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 苏州话 | 通用-苏州话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
    | 闽南语 | 通用-闽南语 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
    | 江西话 | 通用-江西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 宁夏话 | 通用-宁夏话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 广西话 | 通用-广西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 通用-广西话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 中文普通话 | 识音石 V1 - 端到端模型，教育内容分析，医疗内容分析，新闻媒体内容分析，娱乐视频内容分析，音视频离线转写（升级版），新零售领域识别模型，出行领域识别模型，汽车领域 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 中英自由说 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
    | 识音石 V1 - 端到端模型 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
    | 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |

## 使用步骤

1. 了解您的录音文件格式和采样率，根据业务场景在管控台选择合适的场景模型。

2. 上传录音文件至OSS。

如果OSS中文件访问权限为公开，可参见 [公共读Object](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects#concept-39607-zh/section-st4-efq-v5j "")，获取文件访问链接；如果OSS中文件访问权限为私有，可参见 [私有Object](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects#concept-39607-zh/section-wnz-0he-q20 "")，通过SDK生成有有效时间的访问链接。



**重要**





您也可以把录音文件存放在自行搭建的文件服务器，提供文件下载。请保证HTTP的响应头（Header）中`Content-Length`的长度值和Body中数据的真实长度一致，否则会导致下载失败。

3. 客户端提交录音文件识别请求。

正常情况下，服务端返回该请求任务的ID，用以查询识别结果。

4. 客户端发送识别结果查询请求。

通过步骤3获取的请求任务ID查询录音文件识别的结果，目前识别的结果在服务端可保存72小时。


## 交互流程

客户端与服务端的交互流程如图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5789150671/CAEQShiBgMDs5IiK2RgiIGQ0Nzg1N2MzNDRlNTRmMDA5N2VjMjJhODBiMmVhNTc44024928_20231008170233.737.svg)

**说明**

所有服务端的响应都会在返回信息的header包含表示本次识别任务的TaskId参数。

## 各地域POP调用参数

| 地域 | 调用参数 |
| --- | --- |

|     |     |
| --- | --- |
| 地域 | 调用参数 |
| 华东2（上海） | - regionId="cn-shanghai"<br>  <br>- endpointName="cn-shanghai"<br>  <br>- domain="filetrans.cn-shanghai.aliyuncs.com" |
| 华北2（北京） | - regionId="cn-beijing"<br>  <br>- endpointName="cn-beijing"<br>  <br>- domain="filetrans.cn-beijing.aliyuncs.com" |
| 华南1（深圳） | - regionId="cn-shenzhen"<br>  <br>- endpointName="cn-shenzhen"<br>  <br>- domain="filetrans.cn-shenzhen.aliyuncs.com" |

## 接口调用方式

录音文件识别服务是以RPC风格的POP API方式提供录音文件识别接口，将参数封装到每一个请求中，每个请求即对应一个方法，执行的结果放在response中。需要识别的录音文件必须存放在某服务上（推荐 [阿里云OSS](https://www.aliyun.com/product/oss)），可以通过URL访问。使用阿里云OSS，同一地域可以通过内网访问，不计外网流量费用，具体方法请参见 [使用录音文件识别时如何设置OSS内网地址](https://help.aliyun.com/zh/isi/developer-reference/how-to-set-the-internal-endpoint-of-oss-when-using-recording-file-recognition#topic-2199516 "")。

录音文件识别POP API包括两部分：POST方式的“录音文件识别请求调用接口”（用户级别QPS（queries per second）限制为200）、GET方式的“录音文件识别结果查询接口”（用户级别QPS限制为500）。

- 识别请求调用接口：

  - 当采用轮询方式时，提交录音文件识别任务，获取任务ID，供后续轮询使用。

  - 当采用回调方式时，提交录音文件识别任务和回调URL，任务完成后会把识别结果POST到回调地址，要求回调地址可接收POST请求。



    **说明**





    由于历史原因，早期发布的录音文件识别服务（默认为2.0版本）的回调方式和轮询方式的识别结果在JSON字符串的风格和字段上均有不同，下文将作说明。录音文件识别服务在4.0版本对回调方式做了优化，使得回调方式的识别结果与轮询方式的识别结果保持一致，均为驼峰风格的JSON格式字符串。



    如果您已接入录音文件识别服务，即没有设置录音文件识别服务的版本，默认为2.0版，可以继续使用；如果您新接入录音文件识别服务，请设置服务版本为4.0。





    输入参数及说明：

    提交录音文件识别请求时，需要设置输入参数，以JSON格式的字符串传入请求对象的Body，JSON格式如下：















    ```json
    {
        "appkey": "your-appkey",
        "file_link": "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav",
        "auto_split":false,
        "version": "4.0",
        "enable_words": false,
        "enable_sample_rate_adaptive": true,
        // valid_times：获取语音指定时间段的识别内容，若不需要，则无需填写。
        "valid_times": [\
            {\
                "begin_time": 200,\
                "end_time":2000,\
                "channel_id": 0\
            }\
        ]
    }
    ```






    | 参数 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 参数 | 值类型 | 是否必选 | 说明 |
    | appkey | String | 是 | [管控台](https://nls-portal.console.aliyun.com/applist) 创建的项目Appkey。 |
    | file\_link | String | 是 | 存放录音文件的地址，需要在管控台中将对应项目的模型设置为支持该音频场景的模型。 |
    | version | String | 否 | 设置录音文件识别服务的版本，默认为 **4.0**。 |
    | enable\_words | Boolean | 否 | 是否开启返回词信息，默认为false，开启时需要设置version为 **4.0**。 |
    | enable\_sample\_rate\_adaptive | Boolean | 否 | 大于16 kHz采样率的音频是否进行自动降采样（降为16 kHz），默认为false，开启时需要设置version为 **4.0**。 |
    | enable\_callback | Boolean | 否 | 是否启用回调功能，默认值为false。 |
    | callback\_url | String | 否 | 回调服务的地址，enable\_callback取值为true时，本字段必选。URL支持HTTP和HTTPS协议，host不可使用IP地址。 |
    | auto\_split | Boolean | 否 | 是否开启智能分轨（开启智能分轨，即可在两方对话的语音情景下，依据每句话识别结果中的ChannelId，判断该句话的发言人为哪一方。通常先发言一方ChannelId为0，8k双声道开启分轨后默认为2个人，声道channel0和channel1就是音轨编号）。<br>**说明**<br>8000\\16000 Hz采样率均支持，16k默认只分离首个声道。 |
    | supervise\_type | Integer | 否 | 说话人分离的确定人数方式，需要和 **auto\_split**、 **speaker\_num** 这两个参数搭配使用。<br>    - 默认为空：8k由用户指定，16k由算法决定。<br>      <br>    - 1：用户指定人数，具体人数由参数 **speaker\_num** 确认。<br>      <br>    - 2：算法决定人数。 |
    | speaker\_num | Integer | 否 | 用于辅助指定声纹人数，取值范围为2至100的整数。8k音频默认为2，16k音频默认为100。<br>此参数只能辅助算法尽量输出指定人数，无法保证一定会输出此人数。需要和 **auto\_split**、 **supervise\_type** 这两个参数搭配使用。 |
    | enable\_inverse\_text\_normalization | Boolean | 否 | ITN（逆文本inverse text normalization）中文数字转换阿拉伯数字。设置为True时，中文数字将转为阿拉伯数字输出，默认值：False。 |
    | enable\_disfluency | Boolean | 否 | 过滤语气词，即声音顺滑，默认值false（关闭），开启时需要设置version为4.0。 |
    | enable\_punctuation\_prediction | Boolean | 否 | 是否给句子加标点。默认值true（加标点）。 |
    | valid\_times | List< ValidTime > | 否 | 有效时间段信息，用来排除一些不需要的时间段。 |
    | max\_end\_silence | Integer | 否 | 允许的最大结束静音，取值范围：200~6000，默认值800，单位为毫秒。<br>开启语义断句 **enable\_semantic\_sentence\_detection** 后，此参数无效。 |
    | max\_single\_segment\_time | Integer | 否 | 允许单句话最大结束时间，最小值5000，默认值60000。单位为毫秒。<br>开启语义断句 **enable\_semantic\_sentence\_detection** 后，此参数无效。 |
    | customization\_id | String | 否 | 通过POP API创建的定制模型ID，默认不添加。 |
    | class\_vocabulary\_id | String | 否 | 创建的类热词表ID，默认不添加。 |
    | vocabulary\_id | String | 否 | 创建的泛热词表ID，默认不添加。 |
    | enable\_semantic\_sentence\_detection | Boolean | 否 | 是否启⽤语义断句，取值：true/false，默认值false。 |
    | enable\_timestamp\_alignment | Boolean | 否 | 是否启用时间戳校准功能，取值：true/false，默认值false。 |
    | first\_channel\_only | Boolean | 否 | 是否只识别首个声道，取值：true/false。（如果录音识别结果重复，您可以开启此参数。）<br>    - 默认为空：8k处理双声道，16k处理单声道。<br>      <br>    - false：8k处理双声道，16k处理双声道。<br>      <br>    - true：8k处理单声道，16k处理单声道。<br>      <br>**重要**<br>计费模式：<br>    - 8k处理双声道，按单声道计费，即 **音频时长** 进行计费。<br>      <br>    - 16k处理双声道，按双声道计费，即 **声道数×音频时长** 进行计费。 |
    | special\_word\_filter | String | 否 | 敏感词过滤功能，支持开启或关闭，支持自定义敏感词。该参数可实现：<br>**不处理**（默认，即展示原文）、 **过滤**、 **替换为\*。**<br>具体调用说明请见下文的自定义过滤词调用示例。<br>**说明**<br>开启但未配置敏感词，则会过滤默认词表： [敏感词表](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230602/wucl/%E6%95%8F%E6%84%9F%E8%AF%8D.txt)。 |
    | punctuation\_mark | String | 否 | 自定义标点断句。<br>不填默认使用句号、问号、叹号断句。如果用户填写此值，则会增加使用用户指定的标点符号断句。<br>示例：<br>按英文逗号断句填写","<br>按中文和英文逗号断句填写"，,"<br>**说明**<br>    - 如果用户填写的不是标点符号则不生效。<br>      <br>    - 此字段可填多个标点，且会区分中英文标点，标点间无空格。 |
    | sentence\_max\_length | Integer | 否 | 每句最多展示字数，取值范围：\[4，50\]。默认为不启用该功能。启用后如不填写字数，则按照长句断句。该参数可用于字幕生成场景，控制单行字幕最大字数。 |



    自定义过滤词调用示例如下：















    ```json
                // 以实时转写为例，
                JSONObject root = new JSONObject();
                root.put("system_reserved_filter", true);

                // 将以下词语替换成空
                JSONObject root1 = new JSONObject();
                JSONArray array1 = new JSONArray();
                array1.add("开始");
                array1.add("发生");
                root1.put("word_list", array1);

                // 将以下词语替换成*
                JSONObject root2 = new JSONObject();
                JSONArray array2 = new JSONArray();
                array2.add("测试");
                root2.put("word_list", array2);

    						// 可以全部设置，也可以部分设置
                root.put("filter_with_empty", root1);
                root.put("filter_with_signed", root2);

                transcriber.addCustomedParam("special_word_filter", root);
    ```



    其中，ValidTime对象参数说明如下表所示。




    | 参数 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 参数 | 值类型 | 是否必选 | 说明 |
    | begin\_time | Int | 是 | 有效时间段的起始点时间偏移，单位为毫秒。 |
    | end\_time | Int | 是 | 有效时间段的结束点时间偏移，单位为毫秒。 |
    | channel\_id | Int | 是 | 有效时间段的作用音轨序号（从0开始）。 |



    输出参数及说明：

    服务端返回录音文件识别请求的响应，响应的输出参数为JSON格式的字符串：















    ```json
    {
            "TaskId": "4b56f0c4b7e611e88f34c33c2a60****",
            "RequestId": "E4B183CC-6CFE-411E-A547-D877F7BD****",
            "StatusText": "SUCCESS",
            "StatusCode": 21050000
    }
    ```



    返回HTTP状态：200表示成功，更多状态码请查阅HTTP状态码。




    | 属性 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 属性 | 值类型 | 是否必选 | 说明 |
    | Taskid | String | 是 | 识别任务ID。 |
    | RequestId | String | 是 | 请求ID，仅用于联调。 |
    | StatusCode | Int | 是 | 状态码。 |
    | StatusText | String | 是 | 状态说明。 |
- 识别结果查询接口：

提交完录音文件识别请求后，按照如下参数设置轮询识别结果。

输入参数：

通过提交录音文件识别请求获得的任务ID作为识别结果查询接口参数，获取识别结果。在接口调用过程中，需要设置一定的查询时间间隔。



**重要**





查询接口有QPS限制（500QPS），超过QPS之后则可能报错：`Throttling.User : Request was denied due to user flow control.`。建议查询接口的轮询间隔时长适当延长，不宜过短。








| 属性 | 值类型 | 是否必选 | 说明 |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| 属性 | 值类型 | 是否必选 | 说明 |
| Taskid | String | 是 | 识别任务ID。 |



输出参数及说明：

服务端返回识别结果查询请求的响应，响应的输出参数为JSON格式的字符串。

  - 正常返回：以录音文件 [nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)（文件为单轨）识别结果为例。















    ```json
    {
            "TaskId": "d429dd7dd75711e89305ab6170fe****",
            "RequestId": "9240D669-6485-4DCC-896A-F8B31F94****",
            "StatusText": "SUCCESS",
            "BizDuration": 2956,
            "SolveTime": 1540363288472,
            "StatusCode": 21050000,
            "Result": {
                    "Sentences": [{\
                            "EndTime": 2365,\
                            "SilenceDuration": 0,\
                            "BeginTime": 340,\
                            "Text": "北京的天气。",\
                            "ChannelId": 0,\
                            "SpeechRate": 177,\
                            "EmotionValue": 5.0\
                    }]
            }
    }
    ```



    如果开启enable\_callback/callback\_url，且设置服务版本为4.0，回调识别结果为：















    ```json
    {
            "Result": {
                    "Sentences": [{\
                            "EndTime": 2365,\
                            "SilenceDuration": 0,\
                            "BeginTime": 340,\
                            "Text": "北京的天气。",\
                            "ChannelId": 0,\
                            "SpeechRate": 177,\
                            "EmotionValue": 5.0\
                    }]
            },
            "TaskId": "36d01b244ad811e9952db7bb7ed2****",
            "StatusCode": 21050000,
            "StatusText": "SUCCESS",
            "RequestTime": 1553062810452,
            "SolveTime": 1553062810831,
            "BizDuration": 2956
    }
    ```





    **重要**









    - RequestTime为时间戳（单位为毫秒，例如1553062810452转换为北京时间为2019/3/20 14:20:10），表示录音文件识别提交请求的时间。

    - SolveTime为时间戳（单位为毫秒），表示录音文件识别完成的时间。


  - 排队中：















    ```json
    {
            "TaskId": "c7274235b7e611e88f34c33c2a60****",
            "RequestId": "981AD922-0655-46B0-8C6A-5C836822****",
            "StatusText": "QUEUEING",
            "StatusCode": 21050002
    }
    ```

  - 识别中：















    ```json
    {
            "TaskId": "c7274235b7e611e88f34c33c2a60****",
            "RequestId": "8E908ED2-867F-457E-82BF-4756194A****",
            "StatusText": "RUNNING",
            "BizDuration": 0,
            "StatusCode": 21050001
    }
    ```

  - 异常返回：以文件下载失败为例。















    ```json
    {
            "TaskId": "4cf25b7eb7e711e88f34c33c2a60****",
            "RequestId": "098BF27C-4CBA-45FF-BD11-3F532F26****",
            "StatusText": "FILE_DOWNLOAD_FAILED",
            "BizDuration": 0,
            "SolveTime": 1536906469146,
            "StatusCode": 41050002
    }
    ```





    **说明**





    更多异常情况请查看下面的服务状态码的错误状态码及解决方案。





    返回HTTP状态：200表示成功，更多状态码请查阅HTTP状态码。




    | 属性 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 属性 | 值类型 | 是否必选 | 说明 |
    | TaskId | String | 是 | 识别任务ID。 |
    | StatusCode | Int | 是 | 状态码。 |
    | StatusText | String | 是 | 状态说明。 |
    | RequestId | String | 是 | 请求ID，用于调试。 |
    | Result | Object | 是 | 识别结果对象。 |
    | Sentences | List< SentenceResult > | 是 | 识别的结果数据。当StatusText为SUCCEED时存在。 |
    | Words | List< WordResult > | 否 | 词信息，获取时需设置enable\_words为true，且设置服务version为”4.0”。 |
    | BizDuration | Long | 是 | 识别的音频文件总时长，单位为毫秒。 |
    | SolveTime | Long | 是 | 时间戳，单位为毫秒，录音文件识别完成的时间。 |



    其中，单句结果SentenceResult参数如下。




    | 属性 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 属性 | 值类型 | 是否必选 | 说明 |
    | ChannelId | Int | 是 | 该句所属音轨ID。 |
    | BeginTime | Int | 是 | 该句的起始时间偏移，单位为毫秒。 |
    | EndTime | Int | 是 | 该句的结束时间偏移，单位为毫秒。 |
    | Text | String | 是 | 该句的识别文本结果。 |
    | EmotionValue | Float | 是 | 情绪能量值，取值为音量分贝值/10。取值范围：\[1,10\]。值越高情绪越强烈。 |
    | SilenceDuration | Int | 是 | 本句与上一句之间的静音时长，单位为秒。 |
    | SpeechRate | Int | 是 | 本句的平均语速。<br>    - 若识别语言为中文，则单位为：字数/分钟。<br>      <br>    - 若识别语言为英文，则单位为：单词数/分钟。 |

  - 开启返回词信息：

    如果enable\_words设置为true，且设置服务version为"4.0"，服务端的识别结果将包含词信息。使用轮询方式和回调方式获得的词信息相同，以轮询方式的识别结果为例：















    ```json
    {
            "StatusCode": 21050000,
            "Result": {
                    "Sentences": [{\
                            "SilenceDuration": 0,\
                            "EmotionValue": 5.0,\
                            "ChannelId": 0,\
                            "Text": "北京的天气。",\
                            "BeginTime": 340,\
                            "EndTime": 2365,\
                            "SpeechRate": 177\
                    }],
                    "Words": [{\
                            "ChannelId": 0,\
                            "Word": "北京",\
                            "BeginTime": 640,\
                            "EndTime": 940\
                    }, {\
                            "ChannelId": 0,\
                            "Word": "的",\
                            "BeginTime": 940,\
                            "EndTime": 1120\
                    }, {\
                            "ChannelId": 0,\
                            "Word": "天气",\
                            "BeginTime": 1120,\
                            "EndTime": 2020\
                    }]
            },
            "SolveTime": 1553236968873,
            "StatusText": "SUCCESS",
            "RequestId": "027B126B-4AC8-4C98-9FEC-A031158F****",
            "TaskId": "b505e78c4c6d11e9a213e11db149****",
            "BizDuration": 2956
    }
    ```



    Words对象说明：




    | 属性 | 值类型 | 是否必选 | 说明 |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | 属性 | 值类型 | 是否必选 | 说明 |
    | BeginTime | Int | 是 | 词开始时间，单位为毫秒。 |
    | EndTime | Int | 是 | 词结束时间，单位为毫秒。 |
    | ChannelId | Int | 是 | 该词所属音轨ID。 |
    | Word | String | 是 | 词信息。 |

## 服务状态码

### **通用错误码**

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 40000000 | 默认的客户端错误码，对应了多个错误消息。 | 用户使用了不合理的参数或者调用逻辑。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000001 | The token 'xxx' has expired；<br>The token 'xxx' is invalid | 用户使用了不合理的参数或者调用逻辑。通用客户端错误码，通常是涉及Token相关的不正确使用，例如Token过期或者非法。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000002 | Gateway:MESSAGE\_INVALID:Can't process message in state'FAILED'! | 无效或者错误的报文消息。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000003 | PARAMETER\_INVALID;<br>Failed to decode url params | 用户传递的参数有误，一般常见于RESTful接口调用。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000005 | Gateway:TOO\_MANY\_REQUESTS:Too many requests! | 并发请求过多。 | 如果是试用版调用，建议您升级为商用版本以增大并发。<br>如果已是商用版，可购买并发资源包，扩充您的并发额度。 |
| 40000009 | Invalid wav header! | 错误的消息头。 | 如果您发送的是WAV语音文件，且设置`format`为`wav`，请注意检查该语音文件的WAV头是否正确，否则可能会被服务端拒绝。 |
| 40000009 | Too large wav header! | 传输的语音WAV头不合法。 | 建议使用PCM、OPUS等格式发送音频流，如果是WAV，建议关注语音文件的WAV头信息是否为正确的数据长度大小。 |
| 40000010 | Gateway:FREE\_TRIAL\_EXPIRED:The free trial has expired! | 试用期已结束，并且未开通商用版、或账号欠费。 | 请登录控制台确认服务开通状态以及账户余额。 |
| 40010001 | Gateway:NAMESPACE\_NOT\_FOUND:RESTful url path illegal | 不支持的接口或参数。 | 请检查调用时传递的参数内容是否和官网文档要求的一致，并结合错误信息对比排查，设置为正确的参数。<br>比如您是否通过curl命令执行RESTful接口请求， 拼接的URL是否合法。 |
| 40010003 | Gateway:DIRECTIVE\_INVALID:\[xxx\] | 客户端侧通用错误码。 | 表示客户端传递了不正确的参数或指令，在不同的接口上有对应的详细报错信息，请参考对应文档进行正确设置。 |
| 40010004 | Gateway:CLIENT\_DISCONNECT:Client disconnected before task finished! | 在请求处理完成前客户端主动结束。 | 无，或者请在服务端响应完成后再关闭链接。 |
| 40010005 | Gateway:TASK\_STATE\_ERROR:Got stop directive while task is stopping! | 客户端发送了当前不支持的消息指令。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40020105 | Meta:APPKEY\_NOT\_EXIST:Appkey not exist! | 使用了不存在的Appkey。 | 请确认是否使用了不存在的Appkey，Appkey可以通过登录控制台后查看项目配置。 |
| 40020106 | Meta:APPKEY\_UID\_MISMATCH:Appkey and user mismatch! | 调用时传递的Appkey和Token并非同一个账号UID所创建，导致不匹配。 | 请检查是否存在两个账号混用的情况，避免使用账号A名下的Appkey和账号B名下生成的Token搭配使用。 |
| 403 | Forbidden | 使用的Token无效，例如Token不存在或者已过期。 | 请设置正确的Token。Token存在有效期限制，请及时在过期前获取新的Token。 |
| 41000003 | MetaInfo doesn't have end point info | 无法获取该Appkey的路由信息。 | 请检查是否存在两个账号混用的情况，避免使用账号A名下的Appkey和账号B名下生成的Token搭配使用。 |
| 41010101 | UNSUPPORTED\_SAMPLE\_RATE | 不支持的采样率格式。 | 当前实时语音识别只支持8000 Hz和16000 Hz两种采样率格式的音频。 |
| 41040201 | Realtime:GET\_CLIENT\_DATA\_TIMEOUT:Client data does not send continuously! | 获取客户端发送的数据超时失败。 | 客户端在调用实时语音识别时请保持实时速率发送，发送完成后及时关闭链接。 |
| 50000000 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |
| 50000001 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |
| 52010001 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |

### 录音文件识别/录音文件识别闲时版错误码

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 21050000 | SUCCESS | 成功。 | 无。 |
| 21050001 | RUNNING | 录音文件识别任务运行中。 | 请稍后再发送GET方式的识别结果查询请求。 |
| 21050002 | QUEUEING | 录音文件识别任务排队中。 | 请稍后再发送GET方式的识别结果查询请求。 |
| 21050003 | SUCCESS\_WITH\_NO\_VALID\_FRAGMENT | 识别结果查询接口调用成功，但是VAD模块未检测到有效语音。 | 此种情况下可检查：<br>录音文件是否包含有效语音，如果都是无效语音，例如纯静音。上述情况下没有识别结果是正常现象。 |
| ASR\_RESPONSE\_HAVE\_NO\_WORDS | 识别结果查询接口调用成功，但是最终识别结果为空。 | 此种情况下可检查：<br>录音文件是否包含有效语音，或有效语音是否都是语气词且开启了顺滑参数 **enable\_disfluency**，导致语气词被过滤。<br>上述情况下没有识别结果是正常现象。 |
| 41050001 | USER\_BIZDURATION\_QUOTA\_EXCEED | 单日时间超限（免费用户每日可识别不超过2小时时长的录音文件）。 | 建议从免费版升级到商用版。如业务量较大，请联系商务洽谈，邮件地址： **nls\_support@service.aliyun.com**。 |
| 41050002 | FILE\_DOWNLOAD\_FAILED | 文件下载失败。 | 检查录音文件路径是否正确，以及是否可以通过外网访问和下载。 |
| 41050003 | FILE\_CHECK\_FAILED | 文件格式错误。 | 检查录音文件是否是单轨/双轨的WAV格式或MP3格式。 |
| 41050004 | FILE\_TOO\_LARGE | 文件过大。 | 检查录音文件大小是否超过512 MB，超过则需您对录音文件分段。 |
| 41050005 | FILE\_NORMALIZE\_FAILED | 文件归一化失败。 | 检查录音文件是否有损坏，是否可以正常播放。 |
| 41050006 | FILE\_PARSE\_FAILED | 文件解析失败。 | 检查录音文件是否有损坏，是否可以正常播放。 |
| 41050007 | MKV\_PARSE\_FAILED | MKV解析失败。 | 检查录音文件是否损坏，是否可以正常播放。 |
| 41050008 | UNSUPPORTED\_SAMPLE\_RATE | 采样率不匹配。 | 检查实际语音的采样率和控制台上Appkey绑定的ASR模型采样率是否一致，或者将本篇文档中自动降采样的参数enable\_sample\_rate\_adaptive设置为true。 |
| 41050010 | FILE\_TRANS\_TASK\_EXPIRED | 录音文件识别任务过期。 | TaskId不存在，或者已过期。 |
| 41050011 | REQUEST\_INVALID\_FILE\_URL\_VALUE | 请求file\_link参数非法。 | 确认file\_link参数格式是否正确。 |
| 41050012 | REQUEST\_INVALID\_CALLBACK\_VALUE | 请求callback\_url参数非法。 | 确认callback\_url参数格式是否正确，是否为空。 |
| 41050013 | REQUEST\_PARAMETER\_INVALID | 请求参数无效。 | 确认请求task值为有效的JSON格式字符串。 |
| 41050014 | REQUEST\_EMPTY\_APPKEY\_VALUE | 请求参数appkey值为空。 | 确认是否设置了appkey参数值。 |
| 41050015 | REQUEST\_APPKEY\_UNREGISTERED | 请求参数appkey未注册。 | 确认请求参数appkey值是否设置正确，或者是否与阿里云账号的AccessKey ID同一个账号。 |
| 41050021 | RAM\_CHECK\_FAILED | RAM检查失败。 | 检查您的RAM用户是否已经授权调用语音服务的API，具体操作，请参见 [RAM用户权限配置](https://help.aliyun.com/zh/isi/getting-started/start-here)。 |
| 41050023 | CONTENT\_LENGTH\_CHECK\_FAILED | content-length 检查失败。 | 检查下载文件时，HTTP response中的content-length与文件实际大小是否一致。 |
| 41050024 | FILE\_404\_NOT\_FOUND | 需要下载的文件不存在。 | 检查需要下载的文件是否存在。 |
| 41050025 | FILE\_403\_FORBIDDEN | 没有权限下载需要的文件。 | 检查是否有权限下载录音文件。 |
| 41050026 | FILE\_SERVER\_ERROR | 请求的文件所在的服务不可用。 | 检查请求的文件所在的服务是否可用。 |
| 41050103 | AUDIO\_DURATION\_TOO\_LONG | 请求的文件时长超过12小时。 | 建议将音频进行切分，分多次提交识别任务， [切分命令参考](https://help.aliyun.com/zh/isi/support/faq-about-input-formats-for-speech-recognition#33739064beavy "")。 |
| 40270003 | DECODER\_ERROR | 检测音频文件信息失败。 | 确认文件下载链接中文件为支持的音频格式。 |
| 51050000 | INTERNAL\_ERROR | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复，如无法恢复，请联系技术支持人员。 |

## 历史版本说明

如果您已接入录音文件识别，即没有设置服务版本为4.0，默认会使用录音文件识别4.0版本。回调方式的识别结果与轮询方式的识别结果在JSON字符串的风格和字段上有所不同，
如果开启enable\_callback/callback\_url，回调识别结果为：

```json
{
        "result": [{\
                "begin_time": 340,\
                "channel_id": 0,\
                "emotion_value": 5.0,\
                "end_time": 2365,\
                "silence_duration": 0,\
                "speech_rate": 177,\
                "text": "北京的天气。"\
        }],
        "task_id": "3f5d4c0c399511e98dc025f34473****",
        "status_code": 21050000,
        "status_text": "SUCCESS",
        "request_time": 1551164878830,
        "solve_time": 1551164879230,
        "biz_duration": 2956
}
```