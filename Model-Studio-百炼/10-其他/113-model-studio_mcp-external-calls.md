### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[MCP](https://help.aliyun.com/zh/model-studio/model-context-protocol/)外部调用

# 外部调用

更新时间：2025-10-15 02:07:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：自定义MCP服务](https://help.aliyun.com/zh/model-studio/custom-mcp)[下一篇：常见问题](https://help.aliyun.com/zh/model-studio/mcp-faq)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

效果展示

前提条件

开通阿里云百炼

获取百炼 API Key

开通 MCP 服务

外部调用 MCP 服务

集成至第三方应用

通过 SDK 进行开发集成

常见问题

为什么模型无法成功地调用 MCP ？

阿里云百炼提供了全周期 MCP 服务，既支持在平台内部（如智能体、工作流）进行配置，也支持通过外部调用集成至第三方应用或个人项目。针对外部调用场景，可以选择以下两种方式：

- 集成至第三方应用：支持一键自动配置到第三方应用，快速实现外部调用。

- 集成至个人项目：通过 MCP SDK 调用，实现灵活编码和深度定制。


## 效果展示

在 Cherry Studio 中调用阿里云百炼提供的 Amap Maps MCP 服务，搭建一个路线规划智能体应用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996589.png)

## 前提条件

### **开通阿里云百炼**

如果您是首次访问阿里云百炼服务平台，请按照以下步骤进行开通。

1. 登录 [阿里云百炼大模型服务平台](https://bailian.console.aliyun.com/)。

2. 如果页面顶部显示![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8848210571/p968044.png)，您需要开通阿里云百炼的模型服务，并获得免费额度。如果未显示该消息，则表示您已经开通。

如果开通服务时提示“您尚未进行实名认证”，请先进行 [个人实名认证](https://help.aliyun.com/zh/account/verify-your-identity-individual-account "")。


### **获取百炼 API Key**

1. 前往**密钥管理**（ [北京](https://bailian.console.aliyun.com/?tab=model#/api-key) 或 [新加坡](https://modelstudio.console.aliyun.com/?tab=model#/api-key)）页面，在 **API-Key** 页签（下图位置①）下单击 **创建API-KEY**（下图位置②）。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8412544571/p994209.png)

2. 在 **创建API-KEY** 弹窗中，选择API Key的 **归属账号** 及 **归属业务空间**，填写 **描述**，并单击 **确定**。

   - **归属账号：** 可选择主账号或子账号（当人员离职或岗位变动时，只需将其子账号 [移出业务空间](https://help.aliyun.com/zh/model-studio/member-management#baa5507e10prj "")，对应API Key将自动失效，不再具备调用权限）。

   - **归属业务空间：** 通常选择 [**默认业务空间**](https://help.aliyun.com/zh/model-studio/use-workspace#0358d9b5079ck "")（或主账号空间）。若需管控某类用户可调用的模型，或对模型调用的费用进行分账，请创建/选择列表中的 [子业务空间](https://help.aliyun.com/zh/model-studio/use-workspace#0358d9b5079ck "")。详见 [子业务空间的模型调用](https://help.aliyun.com/zh/model-studio/model-calling-in-sub-workspace "")。（单个业务空间最多支持创建 20 个 API Key）



     **说明**





     API Key的调用权限完全由其 **归属业务空间** 决定。 **同一空间内的API Key权限相同**，无需为不同模型（如文生文、文生图、语音合成）创建不同的API Key。



     - **默认业务空间下的API Key：** 可调用所有 [标准模型](https://help.aliyun.com/zh/model-studio/models "")，以及默认业务空间内的 [应用](https://help.aliyun.com/zh/model-studio/application-introduction "")。

     - **子业务空间下的API Key：** 可调用该子业务空间已获得 [授权](https://help.aliyun.com/zh/model-studio/use-workspace#f2e68d7ba7ubk "") 的标准模型，以及该子业务空间内的应用。


**调用在阿里云百炼** [**调优后的模型**](https://help.aliyun.com/zh/model-studio/model-training-overview "") **：** 此类模型部署成功后，仅能用其所在业务空间的API Key调用，无需 [授权](https://help.aliyun.com/zh/model-studio/use-workspace#f2e68d7ba7ubk "")。
3. 点击API Key旁的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8412544571/p994217.png)图标（上图位置③）获取该API Key。


> 主账号可以查看全部API Key，子账号仅能查看自己创建的API Key。


## 开通 MCP 服务

1. 前往 [阿里云百炼 MCP 页面](https://bailian.console.aliyun.com/?tab=mcp#/mcp-market) 选择 MCP 服务。以 Amap Maps 服务为例，点击卡片。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996734.png)

2. 点击 **立即开通**，点击 **确认开通** 后即可开通 Amap Maps MCP 服务。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996657.png)



**说明**





阿里云百炼已部署云端的 Amap Maps MCP 服务，开通试用服务无需填写 **AMAP\_MAPS\_API\_KEY**。如需商业化服务定制，也支持使用个人 **AMAP\_MAPS\_API\_KEY**。





如果涉及输入敏感信息，需通过创建 KMS 凭据进行加密。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p995653.png)


## 外部调用 MCP 服务

### **集成至第三方应用**

阿里云百炼支持配置 MCP 服务至 Cherry Studio 和 Cursor，支持自动配置和手动配置。以 Amap Maps 服务为例。

Cherry Studio

Cursor

1. 安装 [Cherry Studio](https://www.cherry-ai.com/)。

2. 进入 [Amap Maps MCP](https://bailian.console.aliyun.com/?tab=mcp&scm=20140722.S_%E7%99%BE%E7%82%BCprompt._.RL_%E7%99%BE%E7%82%BCprompt-LOC_aillm-OR_chat-V_3-RC_llm#/mcp-market/detail/amap-maps) 服务界面，在 **外部调用** 界面中选择 **Cherry Studio**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996141.png)

3. 点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p995659.png)，选择 API Key，点击 **确定**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996572.png)可以在弹出的 Cherry Studio 界面中看到所配置的 MCP 服务的详细信息。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996573.png)

4. 也可以手动配置 MCP 服务。点击右上角![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996575.png)，在弹出界面选择 API Key 并复制配置文件。在 Cherry Studio 的 **MCP 设置** 页面点击 **添加服务器** > **从JSON导入**，粘贴配置信息，点击 **确定**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996576.png)

5. 在 Cherry Studio中使用 MCP 服务。新建话题，在下方点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p995669.png)，选择 **AliyunBailianMCP\_amap-maps** 服务。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996571.png)

6. 在对话框中输入`现在出发，从杭州萧山国际机场到杭州西湖景区。请你提供三种公共交通出行方案`，可以看到大模型成功调用了 MCP 工具来规划路线。


> 若模型无法调用 MCP，请参考 [常见问题](https://help.aliyun.com/zh/model-studio/mcp-external-calls#a7dddab168yub "")。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996570.png)


1. 安装 [Cursor](https://cursor.com/)。

2. 进入 [Amap Maps MCP](https://bailian.console.aliyun.com/?tab=mcp&scm=20140722.S_%E7%99%BE%E7%82%BCprompt._.RL_%E7%99%BE%E7%82%BCprompt-LOC_aillm-OR_chat-V_3-RC_llm#/mcp-market/detail/amap-maps) 服务界面，在 **外部调用** 界面中选择 **Cursor**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996577.png)

3. 点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996578.png)，选择 API Key，点击 **确定**。在弹出的 Cursor 界面中点击 **Install**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996580.png)

头像右下角状态显示为绿色即为安装成功。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996581.png)


### 通过 SDK 进行开发集成

通过 MCP SDK 调用阿里云百炼 MCP 服务，编码更加灵活。

以下是一个基于 [Qwen Agent](https://github.com/QwenLM/Qwen-Agent) 框架、调用 Amap Maps MCP 服务的智能体应用实例，支持查询杭州市天气。

1. 安装 Qwen Agent 框架。















```bash
pip install -U "qwen-agent[gui,rag,code_interpreter,mcp]"
```

2. [配置百炼 API Key 到环境变量](https://help.aliyun.com/zh/model-studio/first-api-call-to-qwen#688de734136xo "")。

3. 新建文件`hangzhou_weather.py`，代码实例如下：






Python

































```python
# -*- coding: utf-8 -*-
# 使用amap-maps工具查询杭州天气

import os
from qwen_agent.agents import Assistant


def query_hangzhou_weather():
       """查询杭州今日天气"""
       # 检查环境变量
       api_key = os.getenv('DASHSCOPE_API_KEY')
       if not api_key:
           print("错误：请设置环境变量 DASHSCOPE_API_KEY")
           print("例如：export DASHSCOPE_API_KEY=your_api_key")
           return

       llm_cfg = {'model': 'qwen-max'}
       system = (
           '你是一个天气查询智能体。你将调用名为 amap-maps 的 MCP 服务来查询天气信息。'
           '请优先调用工具获取结构化的天气数据，并对天气情况做简明解释。'
       )

       # 配置MCP工具
       tools = [{\
           "mcpServers": {\
               "amap-maps": {\
                   "url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",\
                   "headers": {\
                       "Authorization": f"Bearer {api_key}"\
                   }\
               }\
           }\
       }]

       # 创建智能体
       bot = Assistant(
           llm=llm_cfg,
           name='天气查询智能体',
           description='天气信息查询',
           system_message=system,
           function_list=tools,
       )

       # 查询杭州天气
       messages = []
       query = "今天是几号？查询杭州今日的天气情况"
       messages.append({'role': 'user', 'content': query})

       print("正在查询杭州今日天气...")
       print("=" * 50)

       # 执行查询并收集所有响应
       all_responses = []
       for response in bot.run(messages):
           all_responses.append(response)

       # 提取最终的assistant回复内容
       final_content = ""
       if all_responses:
           last_response = all_responses[-1]
           if isinstance(last_response, list):
               for item in last_response:
                   if isinstance(item, dict) and item.get('role') == 'assistant' and 'content' in item:
                       final_content = item['content']
           elif isinstance(last_response, dict) and 'content' in last_response:
               final_content = last_response['content']

       # 输出最终结果
       if final_content:
           print(final_content)
       else:
           print("未能获取到天气信息")


if __name__ == '__main__':
       query_hangzhou_weather()
```

4. 运行代码，结果如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9558605571/p996635.png)


> 运行代码时，若提示`npx`不是内部或外部命令，请先安装`Node.js`。


## 常见问题

### **为什么模型无法成功地调用 MCP ？**

大模型需要明确的指令才能准确地调用 MCP 服务。请在提示词中明确工具名称和工具能力。示例：调用阿里云百炼 Amap Maps MCP 服务，规划从杭州到上海的自驾路线。