### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用开发](https://help.aliyun.com/zh/model-studio/llm-application/)高代码应用

# 高代码应用

更新时间：2026-02-26 00:43:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/)[下一篇：文件问答](https://help.aliyun.com/zh/model-studio/file-q-a)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

应用管理

应用网关

API 开发指南

环境准备

开发规范

应用观测植入

应用上传

应用测试

应用更新

常见问题

阿里云百炼平台的高代码应用功能，允许开发者基于完整的 Python 项目结构部署 AI 后端服务。

- 与“低代码/无代码”拖拽式开发不同，高代码应用允许您 **使用代码编程的方式构建复杂 AI 服务**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041759.png)

- 使用单条命令即可快速将 Python 项目部署为 **公网可访问云上后端 API 服务**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041753.png)

- 支持 **自动化运维、可观测、日志服务、API网关等** 企业级能力。


|     |     |
| --- | --- |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041749.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1010619.png) |


## **快速开始**

1. 前往 [阿里云百炼-应用观测](https://bailian.console.aliyun.com/?tab=app#/app-observe) 页面，授权开通 **应用观测** 功能。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1042042.png)

2. 前往 [阿里云百炼-应用管理](https://bailian.console.aliyun.com/?tab=app#/app-center)，单击 **创建应用**，选择 **高代码应用**，再选择 **控制台创建**。


> 创建时需按照页面引导授权函数计算FC、API 网关两个服务的相关角色和权限。如遇权限不足，请联系您的账号管理员或 IT 管理员 [获取相关授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1045034.png)

3. 在应用部署页面选择任意的模板， **部署资源**、 **规格方案** 等参数保持默认，不进行修改，立即部署模板应用。


> 部署成功后，将开始收取少量函数、网关、存储、日志等费用。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1045036.png)

4. 等待几分钟完成应用函数的部署和发布。等待过程中可实时查看函数构建和部署日志。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041832.png)

5. 待部署完成后，配置阿里云百炼的 API-Key后，即可使用右侧的 **文本对话体验** 模式，进行体验和调试。 API-Key 获取方式请参考： [获取 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041899.png)

也可使用 **API 测试** 模式在控制台手动调试定制的 API 接口：




| **应用模板** | **支持的接口** |
| --- | --- |



|     |     |
| --- | --- |
| **应用模板** | **支持的接口** |
| 基础对话 Agent | 健康检查接口：`GET /health`，用于告知应用函数，服务已成功启动。预期响应：`"OK"`。<br>联调接口：`/process`，用于与大模型通信。模板的请求样例：<br>```curl<br>curl -X POST https://xxxxxxxx/process \<br>  -H "Content-Type: application/json" \<br>  -d '{<br>    "input": [<br>      {<br>        "role": "user",<br>        "content": [<br>          { "type": "text", "text": "你好，世界！" }<br>        ]<br>      }<br>    ],<br>    "session_id": "test-session",<br>    "user_id": "test-user"<br>  }'<br>```<br>预期输出为流式输出内容，请拷贝到本地解析。 |
| 工具调用 Agent，内置天气查询 MCP。<br>` { "type": "text", "text": "今天杭州天气怎么样?"}'` |
| 深度研究 Agent，内置互联网搜索 MCP。<br>` { "type": "text", "text": "帮我分析下近期的金价走势" }'` |


## **应用管理**

在高代码 [应用](https://bailian.console.aliyun.com/?tab=app#/app-center) 的详情页面中单击 **重新部署** 按钮，可以更新应用部署相关的所有设置，包含 **上传新的代码包**， **调整应用性能**（修改资源规格、资源实例数和并发度）、 **修改部署地域**。

> 更新配置或重启服务后，应用都将重新构建和部署， **应用网关** 也需要重新关联。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6744838671/p1045286.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6744838671/p1045287.png)

### **应用网关**

当 **应用测试稳定、性能满足预期** 后，需要在生产环境部署应用，建议开启 **应用网关** 功能，通过自定义域名和网关路由访问云上服务。

1. 在高代码应用的详情页面中，单击 **应用网关**，根据控制台引导，根据需求创建阿里云的 [云原生 API 网关](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/product-overview/what-is-cloud-native-api-gateway "")。（将会产生少量的使用费用，具体价格表请参考： [云原生 API 网关计费概述](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/product-overview/billing-overview "")）


> 应用 **部署** 地域应与应用 **网关** 所在地域 **相同**。

2. 新的 API 路由和 Token 鉴权生效后也能正常访问高代码应用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041984.png)

3. 在 **生产环境** 中使用应用：推荐 **打开** 测试域名的“ **禁止公网访问**”开关，测试用 **触发器** 将不再能够通过公网访问。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1009677.png)

4. 调用示例：















```curl
curl -i -X POST "http://{change-to-your-domain}/{change-to-your-agentCode}/process" \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer 替换为应用网关鉴权token" \
     -d '{
       "input": [\
         {\
           "role": "user",\
           "content": [\
             { "type": "text", "text": "帮我说一下什么是四书五经" }\
           ]\
         }\
       ],
       "session_id": "xxxxxx",
       "user_id": "xxxxx"
     }'
```


## **API 开发指南**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6264802771/CAEQaxiBgMDoh.XA3RkiIGQ3ODMyNThlYzJiNDRmM2E4NzQxNTBmOTQzZGQxOGY46098517_20260106202118.816.svg)

### **环境准备**

1. Python 开发环境要求`python >= 3.10`。

2. 为了能够将 Python 代码上传并部署到阿里云百炼，安装 [AgentScope-AI](https://github.com/agentscope-ai) 的相关依赖，用于向阿里云百炼上传代码包：















```shell
pip install agentscope-runtime==1.0.0
pip install "agentscope-runtime[deployment]==1.0.0"
```


### **开发规范**

1. Python 后端程序必须提供`GET /health`接口。若该接口无法调用，百炼将判定程序启动失败。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1010191.png)

2. Python 后端程序的入口文件 **必须** 为`main.py`。

3. 对话接口路径，默认使用`/process`，协议可参考 [Agent API 协议规范](https://runtime.agentscope.io/zh/protocol.html?spm=a2ty02.30260277.d_app-center.1.a70474a1x8Ajdg)。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1042079.png)

4. 开发参考代码包： [mcp\_server\_with\_chat.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260106/yqdvue/mcp_server_with_chat.zip)。


### **应用观测植入**

通过使用 AgentScope-runtime 包提供的`@trace`装饰器，可以自动上报日志，统计耗时。

针对大模型调用函数的装饰器示例：

```python
from agentscope_runtime.engine.tracing import trace, TraceType

@trace(trace_type=TraceType.LLM, trace_name="llm_func")
def llm_func():
  pass
```

示例输出：

```json
{"time": "2025-08-13 11:23:41.808", "step": "llm_func_start", "model": "", "user_id": "", "code": "", "message": "", "task_id": "", "request_id": "", "context": {}, "interval": {"type": "llm_func_start", "cost": 0}, "ds_service_id": "test_id", "ds_service_name": "test_name"}
{"time": "2025-08-13 11:23:41.808", "step": "llm_func_end", "model": "", "user_id": "", "code": "", "message": "", "task_id": "", "request_id": "", "context": {}, "interval": {"type": "llm_func_end", "cost": "0.000"}, "ds_service_id": "test_id", "ds_service_name": "test_name"}
```

如需自定义日志上报、支持流式输出函数、设置日志公共属性等功能，请参考： [AgentScope-runtime 的 Tracing 模块](https://github.com/agentscope-ai/agentscope-runtime/blob/main/src/agentscope_runtime/engine/tracing/README.md)。

- 如果从控制台上创建应用时，需要打开 **应用观测** 开关。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1045042.png)

- 如果使用`AgentScope-AI`上传构建好的`.whl` 软件包，需要添加`--telemetry enable`来开启应用观测功能。















```shell
runtime-fc-deploy --deploy-name 我的第一个高代码应用  --whl-path <PATH_TO_YOUR_NEW_WHL_FILE> --telemetry enable
```


应用运行后，可在 [阿里云百炼-应用观测](https://bailian.console.aliyun.com/?tab=app#/app-observe) 页面查看收集到的相关信息。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1010178.png)

### **应用上传**

1. 获取并配置以下环境变量（以 Linux 系统为例）

1. 获取阿里云的 [AccessKey（AK 和 SK）](https://help.aliyun.com/zh/model-studio/get-accesskey-appid-and-agentkey "")，用于上传软件包时的鉴权。

2. （ **可选**）获取阿里云百炼的 [Workspace ID](https://help.aliyun.com/zh/model-studio/obtain-the-app-id-and-workspace-id#732535cfc959h "")，以`llm-`开头，用于指定存储高代码应用的百炼业务空间，不设置将使用默认业务空间。

3. 将以上获取到的内容配置为环境变量：















      ```shell
      export ALIBABA_CLOUD_ACCESS_KEY_ID=LTAI************            #替换为阿里云AccessKey(AK)
      export ALIBABA_CLOUD_ACCESS_KEY_SECRET=****************        #替换为阿里云SecretKey(SK)
      export MODELSTUDIO_WORKSPACE_ID=llm-****************           #可选，替换为百炼的业务空间ID，该空间将部署高代码应用，不设置将使用默认业务空间
      ```
2. 使用`AgentScope-AI`上传构建好的`.whl` 软件包，并自动部署到阿里云百炼。


> `--telemetry enable`用于打开可观测能力，并需要结合 AgentScope 的 [Tracing 模块](https://github.com/agentscope-ai/agentscope-bricks/blob/main/src/agentscope_bricks/utils/tracing_utils/README.md) 进行应用开发。
















```shell
runtime-fc-deploy --deploy-name 我的第一个高代码应用  --whl-path <PATH_TO_YOUR_NEW_WHL_FILE> --telemetry enable
```



部署成功后会打印出 应用名、百炼业务空间、访问应用的控制台链接、应用 ID。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1010649.png)

3. 前往 [阿里云百炼-应用管理控制台](https://bailian.console.aliyun.com/?tab=app#/app-center)，等待应用发布。应用发布后将会根据部署时长，产生较少的费用。（<0.1元/小时）

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1009456.png)


### **应用测试**

建议前往 [阿里云百炼-应用管理](https://bailian.console.aliyun.com/?tab=app#/app-center)，在应用详情页测试并查看构建、部署、调用日志。

### **应用更新**

当高代码应用需要更新时，可以使用 AgentScope-AI 的更新命令重新上传`.whl` 软件包。软件包上传成功后，高代码应用将自动更新并重新部署运行。

1. 前往 [阿里云百炼-应用管理](https://bailian.console.aliyun.com/?tab=app#/app-center)，复制应用 ID。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0145468571/p1009594.png)

2. 在本地使用以下命令，上传更新的本地`.whl` 软件包。


> 应用更新后，应用将重新构建、部署。
















```shell
runtime-fc-deploy --update <HIGH_CODE_APP_ID> --whl-path <PATH_TO_YOUR_NEW_WHL_FILE>
```



更新成功后显示：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1009662.png)


## **常见问题**

#### **RAM 账号最小化授权**

RAM 账号需要 **最小化** 赋权使用高代码应用时，可以基于以下规则创建高代码应用的 [自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy#section-kwn-gu8-48m "")。

```json
{
  "Version": "1",
  "Statement": [\
    {\
      "Effect": "Allow",\
      "Action": [\
        "sfm:ApplyTempStorageLease",\
        "fc:ListTriggers",\
        "fc:GetFunction",\
        "fc:GetFunctionCode",\
        "fc:UpdateFunction",\
        "log:GetProject",\
        "log:GetLogStore",\
        "log:GetIndex"\
      ],\
      "Resource": "*"\
    }\
  ]
}
```

#### **上传失败了如何排查？**

1. 请检查阿里云的 AK/SK 与 阿里云百炼的 Workspace ID 是否属于同一个账号。

2. 请检查各项 [前置条件](https://help.aliyun.com/zh/model-studio/high-code-application#a58c79de190a7 "") 均已满足或开通。

3. 请尝试使用一个干净的`python >= 3.10`的环境，比如使用 `Python` 的 `venv` 命令创建一个干净的虚拟环境：

1. 创建环境：















      ```shell
      python --version
      python -m venv venv
      ```

2. 加载环境















      ```shell
      # Linux / macOS
      source venv/bin/activate

      # Windows (CMD)
      venv\Scripts\activate.bat

      # Windows (PowerShell)
      venv\Scripts\Activate.ps1
      ```
4. 上传时代码运行报错 “ **RAM user is not assigned to any workspace in Bailian**”，请联系阿里云 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 的拥有者进行以下操作：

1. 由阿里云 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 为阿里云 [子账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "")（ [RAM用户](https://help.aliyun.com/zh/ram/user-guide/overview-of-ram-users "")）在 [RAM 控制台](https://ram.console.aliyun.com/users) 添加 **AliyunBailianDataFullAccess** 权限。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1042134.png)

2. 为子账号（RAM用户）在 [百炼账号管理页面](https://bailian.console.aliyun.com/?tab=globalset#/user_management/user_management) 添加 **特定业务空间** 的 **智能体-操作** 权限。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6887052671/p1024733.png)

#### **控制台一直显示部署中（超过 5 分钟）或部署失败可能是什么原因？**

1. Python 后端程序的`GET /health` 接口无法调用，导致百炼认为程序启动失败。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9045468571/p1010191.png)

2. Python 后端程序的入口文件必须为`main.py`。

3. 可以前往高代码应用详情页中，查看具体的运行日志。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1041832.png)


#### **API 调用报错**`Invalid API-key Provided` **?**

说明高代码应用的环境变量中未正确配置百炼的 API-Key， 获取方式请参考： [获取 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8023838671/p1044946.png)