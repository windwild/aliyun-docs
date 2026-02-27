### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Kilo CLI

# Kilo CLI

更新时间：2026-02-12 06:33:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Dify](https://help.aliyun.com/zh/model-studio/dify)[下一篇：OpenClaw（原 Clawdbot/Moltbot）](https://help.aliyun.com/zh/model-studio/openclaw)

该文章对您有帮助吗？

反馈

- 本页导读

模型配置

支持的模型

模型选型建议

详细步骤

步骤一：开通阿里云百炼

步骤二：安装 Kilo CLI

步骤三：连接模型服务

常见问题

连接模型后报错或无法获得响应怎么办？

Kilo CLI 是一款开源的终端 AI 编程工具，通过配置可接入阿里云百炼的千问系列模型。

**重要**

**本文档仅适用于按量付费模式**。如果您已订阅阿里云百炼 Coding Plan 并希望在 Kilo CLI 中使用，请参考 [Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。

## 模型配置

### **支持的模型**

| **模型系列** | **支持的模型名称（model）** |
| --- | --- |

|     |     |
| --- | --- |
| **模型系列** | **支持的模型名称（model）** |
| 千问Max<br>（部分模型支持思考模式） | qwen3-max、qwen3-max-2026-01-23（支持思考模式）、qwen3-max-preview（支持思考模式） [查看更多](https://help.aliyun.com/zh/model-studio/models#d4ccf72f23jh9 "") |
| 千问Plus | qwen-plus、qwen-plus-latest、qwen-plus-2025-09-11 [查看更多](https://help.aliyun.com/zh/model-studio/models#5ef284d4ed42p "") |
| 千问Flash | qwen-flash、qwen-flash-2025-07-28 [查看更多](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "") |
| 千问Turbo | qwen-turbo、qwen-turbo-latest [查看更多](https://help.aliyun.com/zh/model-studio/models#947fc66bc1ldf "") |
| 千问Coder<br>（不支持思考模式） | qwen3-coder-plus、qwen3-coder-plus-2025-09-23、qwen3-coder-flash [查看更多](https://help.aliyun.com/zh/model-studio/models#d698550551bob "") |

### 模型选型建议

- **深度研发与架构设计**：推荐使用`qwen3-max-2026-01-23`、`qwen3-coder-plus`。适用于复杂算法实现、系统架构设计等。

- **辅助编码与轻量任务**：推荐使用`qwen3-coder-flash`。适用于代码解释、格式化、单元测试生成等。


## 详细步骤

### 步骤一：开通阿里云百炼

1. **注册账号**：若无阿里云账号，需首先[注册](https://account.alibabacloud.com/register/intl_register.htm)。


> 如遇问题，请参见 [注册阿里云账号](https://help.aliyun.com/zh/account/step-1-register-an-alibaba-cloud-account "")。

2. **开通阿里云百炼：** 使用 **阿里云主账号** 前往[阿里云百炼大模型服务平台](https://bailian.console.aliyun.com/?tab=model#/model-market)，阅读并同意协议后，将自动开通阿里云百炼，如果未弹出服务协议，则表示您已经开通。


> 如果开通服务时提示"您尚未进行实名认证"，请先进行 [实名认证](https://help.aliyun.com/zh/account/verify-your-identity-individual-account "")。


> 首次开通百炼后，您可领取新人免费额度（有效期：百炼开通后90天内），用于模型推理服务。免费额度领取方法和详情，请查看 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 页面。

**说明**

超出额度或期限将产生费用，开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能可避免此情况下产生费用，具体费用请以控制台的实际报价和最终账单为准。

### 步骤二：安装 Kilo CLI

1. 安装 [Node.js](https://nodejs.org/en/download/)（v18.0 或更高版本）。

2. 在终端中执行以下命令安装 Kilo CLI：















```bash
npm install -g @kilocode/cli
```

3. 运行以下命令验证安装。若有版本号输出，则表示安装成功。















```bash
kilo --version
```


### 步骤三：连接模型服务

在 Kilo CLI 中接入阿里云百炼模型服务，需要配置以下参数：

> 请确保 Base URL 、API Key、模型都归属于同一地域下。

|     |     |
| --- | --- |
| **Base URL** | 按地域区分：<br>- 华北2（北京）：`https://dashscope.aliyuncs.com/compatible-mode/v1`<br>  <br>- 新加坡：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`<br>  <br>- 美国（弗吉尼亚）：`https://dashscope-us.aliyuncs.com/compatible-mode/v1` |
| **API Key** | 百炼访问凭证，用于身份验证和计费，请前往[密钥管理（北京）](https://bailian.console.aliyun.com/?tab=model#/api-key)或[密钥管理（新加坡）](https://modelstudio.console.aliyun.com/?tab=model#/api-key)或[密钥管理（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=model#/api-key)页面获取。 |
| **模型 ID** | 指定接入的模型，如`qwen3-max-2026-01-23`、`qwen3-coder-plus`。<br>> 不同地域支持的模型有所差异，如美国（弗吉尼亚）地域暂不支持`qwen3-max-2026-01-23`模型。各地域支持的完整列表请参考 [支持的模型](https://help.aliyun.com/zh/model-studio/kilo-cli#kilo-supported-models "")。 |

您可以通过编辑配置文件来连接阿里云百炼模型服务。

1. 使用文本编辑器打开配置文件 `~/.config/kilo/config.json`。















```bash
vim ~/.config/kilo/config.json
```

2. 复制并粘贴以下配置内容，将其中的“百炼 API Key” 替换为您的百炼 API Key：















```json
{
     "$schema": "https://kilo.ai/config.json",
     "provider": {
       "bailian": {
         "npm": "@ai-sdk/anthropic",
         "name": "Alibaba Cloud Model Studio",
         "options": {
           "baseURL": "https://dashscope.aliyuncs.com/apps/anthropic/v1",
           "apiKey": "百炼 API Key"
         },
         "models": {
           "qwen3-max-2026-01-23": {
             "name": "qwen3-max-2026-01-23",
             "options": {
               "thinking": {
                 "type": "enabled",
                 "budgetTokens": 1024
               }
             }
           },
           "qwen3-coder-plus": {
             "name": "qwen3-coder-plus"
           }
         }
       }
     }
}
```

3. 保存后重启 Kilo CLI，输入 `/models`，搜索`Alibaba Cloud Model Studio`，选择`qwen3-max-2026-01-23`或`qwen3-coder-plus`。您可以根据需要在 `models` 字段中添加更多模型，模型名称请参见 [支持的模型](https://help.aliyun.com/zh/model-studio/kilo-cli#kilo-supported-models "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5695980771/p1054362.png)

4. 开始对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5695980771/p1054364.png)

更多 Kilo CLI 使用技巧及常见命令请参考 [Kilo Code 官方文档](https://kilo.ai/docs/code-with-ai/platforms/cli)。


## 常见问题

### **连接模型后报错或无法获得响应怎么办？**

可能有以下原因：

- API Key 与 Base URL 的地域不匹配，请确认两者对应同一地域。

- 模型名称不正确，支持的模型请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。