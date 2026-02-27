### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-多模态交互开发套件](https://help.aliyun.com/zh/model-studio/multimodal-products/)[最佳实践](https://help.aliyun.com/zh/model-studio/multimodal-best-practices/)[接入百炼及三方Agent](https://help.aliyun.com/zh/model-studio/bailian-and-tripartite-agent/)接入百炼平台应用

# 接入百炼平台应用

更新时间：2026-02-11 02:10:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

本文介绍如何在多模态交互应用中接入百炼平台应用，以及在客户端调用。

在多模态交互开发套件中，我们预置了多种官方插件和 Agent。当官方能力不能满足您的特定需求时，您也可以将自己开发的百炼平台应用（如智能体应用、工作流应用等）接入到多模态平台，实现能力更丰富的多模态交互。关于推荐应用模板请参考 [百炼应用推荐模板](https://help.aliyun.com/zh/model-studio/agent-template "")。

本文档以创建和接入一个【西游记大全】应用为例，介绍如何在多模态应用中接入百炼平台应用。

### **创建和配置百炼应用**

1. 创建百炼平台应用，参考 [应用类型介绍](https://help.aliyun.com/zh/model-studio/application-introduction "")。

2. 配置应用，调整模型、提示词和其他需要的能力。应用名修改为【西游记大全】。

3. 测试并发布应用。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9888172571/p986224.png)

### **在多模交互应用中接入**

在您的多模交互应用中导入上个步骤配置好的【西游记大全】。

1. 在菜单Agent - 添加 - 我的应用 中选中【西游记大全】，点击确定导入。

2. 发布应用。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9888172571/p986235.png)

### **应用测试和参数配置**

##### **应用测试**

在多模应用中导入【西游记大全】后，我们可以在网页进行测试。

进入【西游记大全】应用的方式为语音说： **打开西游记大全,帮我查一下三清是谁**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9888172571/p986238.png)

##### **参数配置**

在【西游记大全】应用中，我们配置了一个名为${user\_name}的参数。代表用户昵称，默认值为“小宝”。

通过 SDK 调用多模应用，我们可以在代码中配置`${user_name}`。

| 一级参数 | 二级参数 | 三级参数 | 四级参数 | 参数说明 |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 一级参数 | 二级参数 | 三级参数 | 四级参数 | 参数说明 |
| biz\_params |  |  |  | 多模请求参数中的biz\_params |
| user\_defined\_params |  |  | 透传用户自定义参数 |
| user\_defined\_app\_id |  | 导入的百炼 **应用 id** |
| user\_prompt\_params | 类型为 Object <br>对应百炼应用prompt 的自定义变量名和值。 |

- 格式化示例


```json
{
    "biz_params": {
        "user_defined_params": {
            "84***********************acc": {
                "user_prompt_params": {
                    "user_name": "大米"
                }
            }
        }
    }
}
```

##### **客户端验证**

以 Android SDK 为例。

- 在建联参数中设置变量值。


```java
HashMap<String, Object> appParams = new HashMap<>();
appParams.put("user_name","大米");
HashMap<String, Object> userPromptParams = new HashMap<>();
userPromptParams.put("user_prompt_params",appParams);
HashMap<String, Object> userDefinedParams = new HashMap<>();
userDefinedParams.put("67f3ad7d6496475483db4a184c926e77",userPromptParams); //西游记大全的 appid

MultiModalRequestParam.BizParams bizParams = MultiModalRequestParam.BizParams
   .builder()
   .userDefinedParams(userDefinedParams)
   .build();
```

- 运行 Demo 通过语音请求【西游记大全】 Agent。由于端侧设置了用户名为“大米”，可以看到 APP 回复的昵称为“大米”，验证链路测试通过。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9888172571/p986380.png)

### **由百炼平台应用主动退出接管模式**

在多模态交互应用中，您可以为接入的百炼平台应用开启“对话接管”模式。开启后，当用户通过“触发指令”唤起该应用，后续的多轮对话将持续由其处理，直到用户说出“退出指令”，或由应用本身主动结束对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9332574671/p1031331.png)

除了让用户说出“退出指令”外，百炼应用内部也可以根据自身的业务逻辑，主动判断并决定何时退出接管模式。这种方式更为灵活，能实现更智能的对话流程控制。

应用通过在返回内容的开头添加特定的“指令标记”来实现主动退出。目前支持以下两种退出场景：

- 场景1：应用完成任务并回复后退出

指应用判断当前对话可以结束，并已生成了本轮的最终回复。退出后，多模态平台将仅播报该应用返回的回复内容。

  - **指令标记：**`[#blmm-quit#]`

    **使用示例：** 应用返回`[#blmm-quit#]再见啦`。用户将只会听到`再见啦`。随后对话将退出当前应用。
- 场景2：应用无法处理当前问题，交还控制权后退出

指应用判断自己无法处理用户的当前请求，需要退出并将问题交还给多模态交互主流程来处理。

  - **指令标记：**`[#blmm-rejected#]`

    **使用示例：** 应用仅返回 `[#blmm-rejected#]`。多模态平台会接管并根据用户的原始问题寻找其他方式来回复，而不会播报任何来自当前应用的内容。

### **自定义播报音色**

您还可以为接入的百炼平台应用单独指定音色，以便与主链路的音色进行区分。

![image](<Base64-Image-Removed>)

- 除了在管控台为每个接入的百炼平台应用指定音色，您还可以通过API参数进行更精细的音色控制。设置方式


| 入参 | 配置方式 | 是否必传 | 说明 |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 入参 | 配置方式 | 是否必传 | 说明 |
| speaker\_1\_voice | SDK | 否 | 指定播报的声音，音色取值范围取决于应用中配置的tts模型支持的声音列表 |

- 客户端调用示例，在Start消息的payload.biz\_params节点下，通过如下格式设置要使用的播报音色


```json
{
  "user_defined_params": {
    "请替换为百炼应用ID": {
      "speaker_1_voice": "请替换为百炼应用配置的tts模型对应的音色"
    }
  }
}
```

- 百炼应用ID查看方式


![image](<Base64-Image-Removed>)