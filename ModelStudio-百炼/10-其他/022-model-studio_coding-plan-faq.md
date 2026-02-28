### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)常见问题

# 常见问题

更新时间：2026-02-26 08:06:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：添加图片理解Skill](https://help.aliyun.com/zh/model-studio/add-vision-skill)[下一篇：文本生成模型概述](https://help.aliyun.com/zh/model-studio/text-generation)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

接入与配置相关问题

常见报错及解决方案

Claude Code 提示 “Claude Code has switched from npm to native installer”怎么办？

计费与额度相关问题

为什么无法享受优惠？

为什么开通了Coding Plan还有模型 API 调用费用产生？

Coding Plan 额度用完后会转为按量计费吗？

Coding Plan 可以使用百炼的模型免费试用吗？

购买Coding Plan不勾选自动续费，次月还能享受5折优惠吗？

为什么 2 月购买的 Coding Plan 只有 28 天，而不是 31 天？

产品功能相关问题

每个百炼账号支持同时开通几个 Coding Plan？

是否可以使用支持的模型列表以外的模型？

Coding Plan 的 API Key 可以重新生成吗？

Coding Plan 可以生成多个 API Key吗？

VSCode 如何使用 Coding Plan？

Coding Plan 模型支持开启思考模式吗？

data\_inspection\_failed报错如何处理？

Coding Plan到期不续费，重新开通后API Key会重置吗？

## **接入与配置相关问题**

### **常见报错及解决方案**

| **报错信息** | **可能原因** | **解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **报错信息** | **可能原因** | **解决方案** |
| **401 invalid access token or token expired** | API Key 无效、过期、为空、格式错误，或与端点环境不匹配 | 检查 API Key 是否为 Coding Plan 套餐专属 Key，复制完整且无空格；确认订阅状态有效。 |
| **model 'xxx' is not supported** | 模型名称拼写错误、大小写错误、包含空格，或使用了不支持的模型 | 模型名称必须为 [Coding Plan概述](https://help.aliyun.com/zh/model-studio/coding-plan#dc0d98da6ev4j "") 中的模型 ID，区分大小写，前后无空格。 |
| **403 invalid api-key** | 误用了百炼通用 Base URL | Anthropic 兼容端点：`https://coding.dashscope.aliyuncs.com/apps/anthropic`<br>OpenAI 兼容端点：`https://coding.dashscope.aliyuncs.com/v1` |
| **404 status code (no body)** | Base URL 路径错误。例如：在 claude code 中错误地将 Base URL 配置为`https://coding.dashscope.aliyuncs.com/v1`，正确的配置应该是`https://coding.dashscope.aliyuncs.com/apps/anthropic`。 | Anthropic 兼容端点：`https://coding.dashscope.aliyuncs.com/apps/anthropic`<br>OpenAI 兼容端点：`https://coding.dashscope.aliyuncs.com/v1` |
| **Connection error** | Base URL 拼写错误或网络问题 | 检查 Base URL 域名拼写及网络连接。 |
| **hour allocated quota exceeded** | 每 5 小时请求额度已用完 | 等待 5 小时后额度自动恢复，或升级至 Pro 套餐。 |
| **week allocated quota exceeded** | 每周请求额度已用完 | 等待至每周一 00:00:00（UTC+8）额度重置，或升级至 Pro 套餐。 |
| **month allocated quota exceeded** | 每月请求额度已用完 | 等待至订阅月对应日 00:00:00（UTC+8）额度重置，或升级至 Pro 套餐。 |

### **Claude Code 提示 “Claude Code has switched from npm to native installer”怎么办？**

不影响 Claude Code 的正常使用。你可以选择在终端执行`claude install` 将 Claude Code 迁移到官方原生安装版本，并参照终端中返回的命令完成配置迁移。

## **计费与额度相关问题**

### **为什么无法享受优惠？**

可能有以下原因：

1. 限时优惠活动仅限 Coding Plan 新用户，即从未购买过 Coding Plan 套餐的阿里云用户。

2. 限时优惠仅限首次购买和首次续费，后续购买和续费将按原价（Lite 基础套餐 ¥ 40/月，Pro 高级套餐 ¥ 200/月）计费。


### **为什么开通了Coding Plan还有模型 API 调用费用产生？**

可能有以下原因：

1. 如果在 AI 工具中配置的是百炼通用 API Key（格式为`sk-xxxxx`）和通用 Base URL（不含 coding 关键字），系统会将这些调用识别为百炼按量计费请求，无法抵扣 Coding Plan 套餐额度，仍会产生按量计费的账单。您需要正确地配置套餐专属的凭证信息，详情参见 [2、获取Coding Plan API Key 和 Base URL](https://help.aliyun.com/zh/model-studio/coding-plan#2782cf93b1w8h "")。

2. 该费用可能产生于开通 Coding Plan 之前的模型 API 调用。因账单按小时结算，如遇高峰期可能存在小时级延时。例如：在 16:00 调用 API，19:00 开通 Coding Plan 并使用，19:30 系统出账时显示的费用实为 16:00 调用所产生的。具体以实际出账时间为准，详情请参见 [账单查询与成本管理](https://help.aliyun.com/zh/model-studio/bill-query-and-cost-management "")。


### **Coding Plan 额度用完后会转为按量计费吗？**

Coding Plan 额度消耗完毕后，继续调用会失败报错，并且不会自动转为按量付费模式计费。如需继续使用，请升级至 Pro 版本获取更多额度或等待下一订阅周期额度刷新。

### **Coding Plan 可以使用百炼的模型免费试用吗？**

Coding Plan 是一个独立的订阅产品，其计费和配额系统 **不参与** 百炼的通用模型免费试用计划。

### 购买Coding Plan不勾选自动续费，次月还能享受5折优惠吗？

可以，手动首次续费仍可享受优惠。

### **为什么 2 月购买的 Coding Plan 只有 28 天，而不是 31 天？**

套餐自开通时刻起生效，有效期至次月对应日 23:59:59（UTC+8）结束。若次月没有对应日期，则有效期至该月最后一日。

例如：2026 年 1 月 31 日开通 Coding Plan，因 2 月没有 31 日，套餐将于 2026 年 2 月 28 日到期。

## **产品功能相关问题**

### **每个百炼账号支持同时开通几个 Coding Plan？**

每个百炼账号同时只能订阅一个 Coding Plan（不区分 Lite 和 Pro 套餐版本）。

### **是否可以使用** [**支持的模型列表**](https://help.aliyun.com/zh/model-studio/coding-plan\#dc0d98da6ev4j "") **以外的模型？**

Coding Plan 当前仅可以使用 [支持的模型列表](https://help.aliyun.com/zh/model-studio/coding-plan#dc0d98da6ev4j "") 中的模型，使用其他模型会报错。

### **Coding Plan 的 API Key 可以重新生成吗？**

暂不支持。

### **Coding Plan 可以生成多个 API Key吗？**

当前仅支持一个 API Key。

### **VSCode 如何使用 Coding Plan？**

使用支持接入兼容OpenAI / Anthropic API 协议的插件，如 Qwen Code、Claude Code 等。

### **Coding Plan 模型支持开启思考模式吗？**

Coding Plan 支持深度思考的模型多为默认支持思考模式，常见工具开启方式为：

> 使用的模型需支持思考模式。

Claude Code

OpenCode

Qwen Code

输入`/config`，移动到`Thinking mode`，通过`Enter`切换为`true`开启思考模式。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7325012771/p1055133.png)

参见 [OpenCode](https://help.aliyun.com/zh/model-studio/opencode-coding-plan "")，配置options参数为：

```json
{
  "thinking": {
    "type": "enabled",
    "budgetTokens": 1024
  }
}
```

> budgetTokens 为最大思考Token数，可根据需求调整。

打开`~/.qwen/settings.json`，在`modelProviders`属性中设置`enable_thinking`参数为`true`开启思考模式：

```json
{
  "ide": {
    "hasSeenNudge": true
  },
  "env": {
    "BAILIAN_CODING_PLAN_API_KEY": "sk-sp-xxx"
  },
  "modelProviders": {
    "openai": [\
      {\
        "id": "qwen3.5-plus",\
        "name": "[Bailian Coding Plan] qwen3.5-plus",\
        "baseUrl": "https://coding.dashscope.aliyuncs.com/v1",\
        "envKey": "BAILIAN_CODING_PLAN_API_KEY",\
        "generationConfig": {\
          "extra_body": {\
            "enable_thinking": true\
          }\
        }\
      },\
      ...\
    ]
  },
  "security": {
    "auth": {
      "selectedType": "openai"
    }
  },
  "codingPlan": {
    "region": "china",
    "version": "xxx"
  },
  "model": {
    "name": "qwen3.5-plus"
  },
  "$version": 3
}
```

### data\_inspection\_failed报错如何处理？

请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code#inappropriate-content "") 文档。

### Coding Plan到期不续费，重新开通后 **API Key** 会重置吗？

会重置，到期前续费则不会重置。