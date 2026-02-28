### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)OpenClaw（原 Clawdbot/Moltbot）

# OpenClaw（原 Clawdbot、Moltbot）

更新时间：2026-02-11 02:46:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Kilo CLI](https://help.aliyun.com/zh/model-studio/kilo-cli)[下一篇：OpenCode](https://help.aliyun.com/zh/model-studio/opencode)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型支持与选型

配置步骤

1\. 开通阿里云百炼

2\. 安装 OpenClaw

3\. 配置百炼模型

4\. 开始对话

常见问题

问题 1：提示找不到模型或回复为空

问题 2：执行 openclaw 命令时提示 "command not found"

OpenClaw 是一个开源的个人 AI 助手平台，支持通过多种消息渠道与 AI 交互。通过配置可接入阿里云百炼的千问系列模型。

**说明**

OpenClaw 原名 Moltbot/Clawdbot，部分命令可能尚未完成迁移。如果在使用新命令（如 `openclaw dashboard`）时遇到 `command not found: openclaw` 的错误，请切换回旧命令（如 `clawdbot dashboard` 或 `moltbot dashboard`）来执行操作。

## 模型支持与选型

OpenClaw 通过 OpenAI 兼容接口支持阿里云百炼的文本生成模型。支持的模型列表如下：

|     |     |
| --- | --- |
| **文本生成-千问** | [千问Max](https://help.aliyun.com/zh/model-studio/models#qwen-max-cn-bj "")、 [千问Plus](https://help.aliyun.com/zh/model-studio/models#03a05ab98953u "")、 [千问Flash](https://help.aliyun.com/zh/model-studio/models#9b418d9a481yp "")、 [千问Coder](https://help.aliyun.com/zh/model-studio/models#5d7f137a6467d "") |
| **文本生成-千问-开源版** | [Qwen3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "")、 [QwQ-开源版](https://help.aliyun.com/zh/model-studio/models#690e39465dvqv "")、 [QwQ-Preview](https://help.aliyun.com/zh/model-studio/models#18e88cc886ll3 "")、 [Qwen2.5](https://help.aliyun.com/zh/model-studio/models#15f2bdc5dd3zd "")、 [Qwen2](https://help.aliyun.com/zh/model-studio/models#4969f9cd9170b "")、 [Qwen1.5](https://help.aliyun.com/zh/model-studio/models#759b2e1092vt2 "")、 [Qwen-Coder](https://help.aliyun.com/zh/model-studio/models#8fa09f2273rf2 "") |
| **文本生成第三方模型** | [DeepSeek](https://help.aliyun.com/zh/model-studio/models#21ab4c25c7lml "")、 [Kimi](https://help.aliyun.com/zh/model-studio/models#0ca6cec0252yp "")、 [GLM](https://help.aliyun.com/zh/model-studio/models#glm4.5 "")、 [MiniMax-M2.1](https://help.aliyun.com/zh/model-studio/models#6194236b53fx0 "") |

如果您需要频繁使用 OpenClaw 或希望降低使用成本，推荐订阅以下套餐：

- [Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan "")：固定月费订阅模式，每月提供最多 90,000 次请求额度，适合高频次编码需求。

- [AI 通用型节省计划](https://help.aliyun.com/zh/model-studio/savings-plan-and-resource-package#universal-savings-plan "")：通过承诺每月消费金额，即可享受阶梯式折扣（最高 5.3 折），可抵扣百炼平台所有模型。


## 配置步骤

### 1\. 开通阿里云百炼

1. **注册账号**：若无阿里云账号，需首先[注册](https://account.aliyun.com/register/qr_register.htm)。


> 如遇问题，请参见 [注册阿里云账号](https://help.aliyun.com/zh/account/step-1-register-an-alibaba-cloud-account "")。

2. **开通阿里云百炼：** 使用 **阿里云主账号** 前往[阿里云百炼大模型服务平台](https://bailian.console.aliyun.com/?tab=model#/model-market)，阅读并同意协议后，将自动开通阿里云百炼，如果未弹出服务协议，则表示您已经开通。


> 如果开通服务时提示"您尚未进行实名认证"，请先进行 [实名认证](https://help.aliyun.com/zh/account/verify-your-identity-individual-account "")。


> 首次开通百炼后，您可领取新人免费额度（有效期：百炼开通后90天内），用于模型推理服务。免费额度领取方法和详情，请查看 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 页面。

**说明**

超出额度或期限将产生费用，开启 [消费限额](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能将避免此情况下产生费用，具体费用请以控制台的实际报价和最终账单为准。

### 2\. 安装 OpenClaw

#### 环境要求

OpenClaw 需要 Node.js 22 或更高版本。可通过以下命令检查 Node.js 版本：

```bash
node --version
```

如果未安装或版本过低，请访问 [Node.js 官网](https://nodejs.org/) 下载安装。

#### 安装方式

macOS / Linux

Windows

推荐使用官方安装脚本：

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

或通过 npm 全局安装：

```bash
npm install -g openclaw@latest
```

在 PowerShell 中执行：

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

或通过 npm 全局安装：

```bash
npm install -g openclaw@latest
```

#### 完成初始配置向导

首次安装后，OpenClaw 会自动启动配置向导，帮助您快速完成初始设置。您也可以手动执行`openclaw onboard`命令进行配置。

|     |     |
| --- | --- |
| **配置项** | **建议配置** |
| I understand this is powerful and inherently risky. Continue? | 选择 **Yes** |
| Onboarding mode | 选择 **QuickStart** |
| Model/auth provider | 选择 **Skip for now**（稍后配置百炼模型） |
| Filter models by provider | 选择 **All providers** |
| Default model | 选择 **Keep current** |
| Select channel (QuickStart) | 选择 **Skip for now**（稍后配置渠道） |
| Configure skills now? (recommended) | 选择 **No** |
| Enable hooks? | 按空格键选中选项，按回车键进入下一步 |
| How do you want to hatch your bot? | 选择 **Do this later** |

接下来，需要为 OpenClaw 配置百炼模型以启用 AI 对话能力。

### 3\. 配置百炼模型

在 OpenClaw 接入阿里云百炼模型服务，需要配置以下参数：

> 请确保 Base URL 、API Key、模型都归属于同一地域下。

|     |     |
| --- | --- |
| **Base URL** | 按地域区分：<br>- 华北2（北京）：`https://dashscope.aliyuncs.com/compatible-mode/v1`<br>  <br>- 新加坡：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`<br>  <br>- 美国（弗吉尼亚）：`https://dashscope-us.aliyuncs.com/compatible-mode/v1` |
| **API Key** | 百炼访问凭证，用于身份验证和计费，请前往[密钥管理（北京）](https://bailian.console.aliyun.com/?tab=model#/api-key)或[密钥管理（新加坡）](https://modelstudio.console.aliyun.com/?tab=model#/api-key)或[密钥管理（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=model#/api-key)页面获取。 |
| **模型 ID** | 指定接入的模型，如`qwen3-max-2026-01-23`、`qwen3-coder-plus`。各地域支持的完整列表请参考 [模型支持与选型](https://help.aliyun.com/zh/model-studio/openclaw#model-config-section "")。<br>> 不同地域支持的模型有所差异，如美国（弗吉尼亚）地域暂不支持`qwen3-max-2026-01-23`模型。 |

**说明**

配置参数时需要关闭思考模式（`"reasoning": false`），否则会导致回复内容为空。

OpenClaw 提供了两种配置方式，推荐使用 **Web 控制台配置**。

方式一：Web 控制台配置

方式二：编辑配置文件

OpenClaw 提供了基于 Web 的编辑器来修改 `openclaw.json` 配置文件。

1. **启动 Web 控制台**

在终端中运行以下命令：















```bash
openclaw dashboard
```



浏览器会自动打开 OpenClaw 的控制台页面（通常是 `http://127.0.0.1:18789`）。如果浏览器没有自动打开，请手动访问该地址。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3677710771/p1052176.png)

2. **进入配置页面**

在左侧菜单栏中依次选择：**Config** \> **Authentication**，点击菜单下方的 **Raw**。

3. **添加百炼配置**

在左侧菜单栏中选择**Config** \> **Authentication** \> **Raw**，复制以下配置信息，替换原`"agents": {...},`部分，并将 `DASHSCOPE_API_KEY` 替换为您的 [百炼 API Key](https://help.aliyun.com/zh/model-studio/openclaw#d6838ddcc5b59 "")。


> 请确保 [baseUrl](https://help.aliyun.com/zh/model-studio/openclaw#2030a0f9ed0zv "") 和您的百炼 API Key 归属于同一地域。当前`reasoning`参数仅支持设置为`false`。
















```json
     "models": {
       "mode": "merge",
       "providers": {
         "bailian": {
           "baseUrl": "https://dashscope.aliyuncs.com/compatible-mode/v1",
           "apiKey": "DASHSCOPE_API_KEY",
           "api": "openai-completions",
           "models": [\
             {\
               "id": "qwen3-max-2026-01-23",\
               "name": "qwen3-max-thinking",\
               "reasoning": false,\
               "input": [\
                 "text"\
               ],\
               "cost": {\
                 "input": 0,\
                 "output": 0,\
                 "cacheRead": 0,\
                 "cacheWrite": 0\
               },\
               "contextWindow": 262144,\
               "maxTokens": 65536\
             }\
           ]
         }
       }
     },
     "agents": {
       "defaults": {
         "model": {
           "primary": "bailian/qwen3-max-2026-01-23"
         },
         "models": {
           "bailian/qwen3-max-2026-01-23": {
             "alias": "qwen3-max-thinking"
           }
         },
         "maxConcurrent": 4,
         "subagents": {
           "maxConcurrent": 8
         }
       }
     },
```

4. **保存并应用配置**

配置完成后，单击右上角 **Save** 保存配置，单击 **Update**。


如果您更习惯直接编辑配置文件，可以按以下步骤操作。配置文件位于 `~/.openclaw/openclaw.json`，OpenClaw 启动时会自动读取。

1. **打开配置文件**

使用文本编辑器打开配置文件。如果文件不存在，编辑器会自动创建：















```bash
# 您也可以使用其他编辑器，如vim。
# vim ~/.openclaw/openclaw.json
nano ~/.openclaw/openclaw.json
```

2. **添加百炼配置**

复制并粘贴以下配置内容，将`DASHSCOPE_API_KEY`替换为百炼 API Key：


> 当前`reasoning`参数仅支持设置为`false`。
















```json
{
     "meta": {
       "lastTouchedVersion": "2026.2.1",
       "lastTouchedAt": "2026-02-03T08:20:00.000Z"
     },
     "models": {
       "mode": "merge",
       "providers": {
         "bailian": {
           "baseUrl": "https://dashscope.aliyuncs.com/compatible-mode/v1",
           "apiKey": "DASHSCOPE_API_KEY",
           "api": "openai-completions",
           "models": [\
             {\
               "id": "qwen3-max-2026-01-23",\
               "name": "qwen3-max-2026-01-23",\
               "reasoning": false,\
               "input": ["text"],\
               "contextWindow": 262144,\
               "maxTokens": 65536\
             },\
             {\
               "id": "qwen3-coder-plus",\
               "name": "qwen3-coder-plus",\
               "reasoning": false,\
               "input": ["text"],\
               "contextWindow": 131072,\
               "maxTokens": 32768\
             }\
           ]
         }
       }
     },
     "agents": {
       "defaults": {
         "model": {
           "primary": "bailian/qwen3-max-2026-01-23"
         }
       }
     },
     "gateway": {
       "mode": "local",
       "auth": {
         "mode": "token",
         "token": "test123"
       }
     }
}
```

3. **保存配置文件**

如果使用 nano 编辑器：


1. 按 `Ctrl+X` 退出编辑器。

2. 提示保存时按 `Y` 确认。

3. 按 `Enter` 确认文件名。


如果使用 vim 编辑器：

1. 按 `Esc` 确保退出插入模式。

2. 输入 `:wq` 并按 `Enter` 保存并退出。
4. **验证配置**

可以使用以下命令查看配置文件内容，确认配置正确：















```bash
cat ~/.openclaw/openclaw.json
```


### 4\. 开始对话

#### 命令行

请在云服务器或本地终端中执行以下命令，即可通过命令行的方式开始对话。

```bash
openclaw tui
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1774069671/p1050228.png)

#### Web 界面

请在云服务器或本地终端中执行以下命令，即可通过 Web 界面的方式开始对话。

```bash
openclaw dashboard
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1774069671/p1050227.png)

#### 连接聊天工具

OpenClaw 支持多渠道交互，能够通过钉钉等聊天工具，让 AI 助手融入您的日常工作，随时随地提供帮助。详情请参考 [基于 Clawdbot 4 步构建 AI 员工](https://www.aliyun.com/solution/tech-solution/clawdbot) 解决方案。

## 常见问题

### 问题 1：提示找不到模型或 **回复为空**

请确认：

1. 模型 ID 拼写正确。

2. 配置中的 `provider` 名称与引用时一致（如配置中是 `bailian`，引用时应为 `bailian/qwen3-max-2026-01-23`）。

3. 配置中的`reasoning`参数必须设置为`false`。


### 问题 2：执行 openclaw 命令时提示 "command not found"

可能是以下原因导致的：

1. OpenClaw 安装没有成功。请在云服务器或本地终端执行`openclaw --version`，若输出版本号证明安装成功。

2. OpenClaw 更名过程中部分命令尚未完全迁移。可以尝试：

1. 使用旧命令 `moltbot` 或 `clawdbot` 替代。

2. 重新安装最新版本：`npm install -g openclaw@latest`。