### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[开始使用](https://help.aliyun.com/zh/model-studio/get-started-with-models/)选择部署模式

# 如何选择部署模式

更新时间：2026-02-05 03:44:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：限流](https://help.aliyun.com/zh/model-studio/rate-limit)[下一篇：新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

部署模式对比

如何使用

使用中国内地部署模式的模型

使用全球部署模式的模型

使用国际部署模式的模型

使用美国部署模式的模型

异步任务

地域信息

相关文档

部署模式决定了模型推理的计算区域和数据存储位置。选择合适的部署模式可以优化网络延迟，并确保数据在指定范围内进行处理。

## 部署模式对比

部署模式决定模型推理计算的可用算力资源与执行区域，地域决定静态数据的存储位置。当前二者为预设绑定关系，不支持自由组合。

为了降低网络延迟、提升模型响应速度，建议根据您主要用户或业务应用的地理位置选择就近地域对应的部署模式：

| **部署模式** | **绑定地域（数据存储）** | **模型推理计算范围** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **部署模式** | **绑定地域（数据存储）** | **模型推理计算范围** |
| **中国内地** | 华北2（北京） | 仅限中国内地 |
| **全球** | 美国（弗吉尼亚） | 全球动态调度 |
| **国际** | 新加坡 | 全球动态调度（不含中国内地） |
| **美国** | 美国（弗吉尼亚） | 仅限美国境内 |

**重要**

在 **全球** 部署模式和 **国际** 部署模式下，由于 **涉及跨境计算**，您需自行确保用户业务数据跨境处理的合法性。跨区推理请求由所选地域的前端接入点接收。模型调用过程中产生的静态数据（如提示词输入、模型输出等）仅在推理过程中进行瞬时处理，不会在计算节点所在地域进行持久化存储；数据在传输过程中全程加密。

## **如何使用**

### **使用** **中国内地** **部署模式的模型**

使用前，请先配置请求地址、API Key和模型名称：

- **请求地址（Base URL）**：中国内地部署模式绑定华北2（北京）地域，请使用`dashscope.aliyuncs.com`域名。以下为部分请求地址示例，其他 API 请参考对应文档：

  - OpenAI Chat Completions API ：`https://dashscope.aliyuncs.com/compatible-mode/v1`

  - DashScope：`https://dashscope.aliyuncs.com/api/v1`
- **API Key**：请前往[密钥管理（北京）](https://bailian.console.aliyun.com/?tab=model#/api-key)页面获取。

- **模型名称**：请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")，选择中国内地部署模式的模型。


### **使用** **全球** **部署模式的模型**

使用前，请先配置请求地址、API Key和模型名称：

- **请求地址（Base URL）**：全球部署模式绑定美国（弗吉尼亚）地域，请使用`dashscope-us.aliyuncs.com`域名。以下为部分请求地址示例，其他 API 请参考对应文档：

  - OpenAI Chat Completions API ：`https://dashscope-us.aliyuncs.com/compatible-mode/v1`

  - DashScope：`https://dashscope-us.aliyuncs.com/api/v1`
- **API Key**：请前往[密钥管理（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=model#/api-key)页面获取。

- **模型名称**：请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")，选择全球部署模式的模型。


### **使用** **国际** **部署模式的模型**

使用前，请先配置请求地址、API Key和模型名称：

- **请求地址（Base URL）**：国际部署模式绑定新加坡地域，请使用`dashscope-intl.aliyuncs.com`域名。以下为部分请求地址示例，其他 API 请参考对应文档：

  - OpenAI Chat Completions API ：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`

  - DashScope：`https://dashscope-intl.aliyuncs.com/api/v1`
- **API Key**：请前往[密钥管理（新加坡）](https://modelstudio.console.aliyun.com/?tab=model#/api-key)页面获取。

- **模型名称**：请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")，选择国际部署模式的模型。


### **使用** **美国** **部署模式的模型**

使用前，请先配置请求地址、API Key和模型名称：

- **请求地址（Base URL）**：美国部署模式绑定美国（弗吉尼亚）地域，请使用`dashscope-us.aliyuncs.com`域名。以下为部分请求地址示例，其他 API 请参考对应文档：

  - OpenAI Chat Completions API ：`https://dashscope-us.aliyuncs.com/compatible-mode/v1`

  - DashScope：`https://dashscope-us.aliyuncs.com/api/v1`
- **API Key**：请前往[密钥管理（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=model#/api-key)页面获取。

- **模型名称**：请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")，选择美国部署模式的模型（带`-us`后缀）。


### **异步任务**

对于异步任务（如图像生成、视频生成），所有后续操作必须使用创建任务时所用的服务域名和 API Key，否则会导致报错。

以下是在全球部署模式下创建图像生成任务并查询结果的示例：

```curl
# 创建任务（全球部署模式，服务域名dashscope-us.aliyuncs.com）
curl --location 'https://dashscope-us.aliyuncs.com/api/v1/services/aigc/image-generation/generation' \
--header 'Content-Type: application/json' \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header 'X-DashScope-Async: enable' \
--data '{
    "model": "wan2.6-t2i",
    "input": {
        "messages": [\
            {\
                "role": "user",\
                "content": [\
                    {\
                        "text": "一间有着精致窗户的花店，漂亮的木质门，摆放着花朵"\
                    }\
                ]\
            }\
        ]
    },
    "parameters": {
        "n": 1
    }
}'

# 响应示例：{"output":{"task_id":"abc123..."},"request_id":"..."}

# 查询任务（必须使用相同服务域名）
curl -X GET https://dashscope-us.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"

# [错误] 使用其他服务域名查询将导致报错
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

## **地域信息**

地域是指您接入百炼模型服务的物理节点位置，各地域的对应 ID 如下：

- **华北2（北京）**：`cn-beijing`

- **新加坡**：`ap-southeast-1`

- **美国（弗吉尼亚）**：`us-east-1`


各地域支持的平台功能如下：

| **板块** | **功能** | **华北2（北京）** | **新加坡** | **美国（弗吉尼亚）** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **板块** | **功能** | **华北2（北京）** | **新加坡** | **美国（弗吉尼亚）** |
| **使用** | **实时推理** | 支持 | 支持 | 支持 |
| **批量推理** | 支持 | 支持 | 不支持 |
| **模型体验** | 支持 | 支持 | 支持 |
| **管理** | **模型监控** | 支持 | 支持 | 支持 |
| **模型告警** | 支持 | 支持 | 不支持 |
| **传输安全** | 支持 | 支持 | 支持 |
| **权限管理** | 支持 | 支持 | 支持 |
| **优化** | **模型调优** | 支持 | 支持 | 支持 |

## **相关文档**

- [通义千问API参考](https://help.aliyun.com/zh/model-studio/qwen-api-reference/ "")

- [模型列表](https://help.aliyun.com/zh/model-studio/models "")：查看各部署模式支持的模型以及上下文等信息。

- [模型调用计费](https://help.aliyun.com/zh/model-studio/model-pricing "")：查看各部署模式的价格差异。

- [限流](https://help.aliyun.com/zh/model-studio/rate-limit "")：查看各部署模式的RPM、TPM限制。

- [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")：为各部署模式创建和管理 API Key。