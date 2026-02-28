### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)OpenCode

# OpenCode

更新时间：2026-02-26 05:04:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenClaw](https://help.aliyun.com/zh/model-studio/openclaw-coding-plan)[下一篇：Claude Code](https://help.aliyun.com/zh/model-studio/claude-code-coding-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

安装 OpenCode

在 OpenCode 中配置 Coding Plan

使用 OpenCode

OpenCode 是一款开源 AI 编程工具，本文介绍如何在 OpenCode 中配置与使用阿里云百炼 Coding Plan。

## 安装 OpenCode

1. 安装或更新 [Node.js](https://nodejs.org/en/download/)（v18.0 或更高版本）。

2. 在终端中执行以下命令安装 OpenCode。















```bash
npm install -g opencode-ai
```



在终端中执行以下命令，若输出版本号，则表示安装成功。















```bash
opencode -v
```


## **在 OpenCode 中配置 Coding Plan**

复制以下内容并将`YOUR_API_KEY`替换为您的 Coding Plan 专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，写入 OpenCode 配置文件`~/.config/opencode/opencode.json`中并保存。您可以自行设置并切换 [支持的模型列表](https://help.aliyun.com/zh/model-studio/coding-plan-overview "") 中的模型。

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "bailian-coding-plan": {
      "npm": "@ai-sdk/anthropic",
      "name": "Model Studio Coding Plan",
      "options": {
        "baseURL": "https://coding.dashscope.aliyuncs.com/apps/anthropic/v1",
        "apiKey": "YOUR_API_KEY"
      },
      "models": {
        "qwen3.5-plus": {
          "name": "Qwen3.5 Plus",
          "modalities": {
            "input": [\
              "text",\
              "image"\
            ],
            "output": [\
              "text"\
            ]
          },
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 1024
            }
          }
        },
        "qwen3-max-2026-01-23": {
          "name": "Qwen3 Max 2026-01-23"
        },
        "qwen3-coder-next": {
          "name": "Qwen3 Coder Next"
        },
        "qwen3-coder-plus": {
          "name": "Qwen3 Coder Plus"
        },
        "MiniMax-M2.5": {
          "name": "MiniMax M2.5",
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 1024
            }
          }
        },
        "glm-5": {
          "name": "GLM-5",
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 1024
            }
          }
        },
        "glm-4.7": {
          "name": "GLM-4.7",
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 1024
            }
          }
        },
        "kimi-k2.5": {
          "name": "Kimi K2.5",
          "modalities": {
            "input": [\
              "text",\
              "image"\
            ],
            "output": [\
              "text"\
            ]
          },
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 1024
            }
          }
        }
      }
    }
  }
}
```

## **使用 OpenCode**

在终端中执行以下命令进入 OpenCode。

```bash
opencode
```

在命令行输入`/models`，输入`Model Studio Coding Plan`，选择模型后即可使用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8769341771/p1053279.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8769341771/p1053280.png)