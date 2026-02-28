### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 循环属性使用说明

# 循环属性使用说明

更新时间：2026-02-11 02:35:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

循环属性展示

支持范围

结果示例

循环结果调试结果

循环结果展示

**重要**

为满足更丰富的编排需求，流程编排功能已全面升级为工作流应用和智能体编排应用。流程编排功能将逐步下线，但此变动不影响已经使用了流程编排功能的用户。您可以继续使用流程编排功能，也可以改为使用工作流应用或智能体编排应用，以获得更好的使用体验。具体请参见 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 和 [智能体编排应用](https://help.aliyun.com/zh/model-studio/multi-agent-application "")。

本篇文档为您介绍循环使用说明。

## **概述**

在使用大模型的过程中，有些场景下需要使用到循环。例如，用大模型生成测评数据，如果需要生成多条时，可以选择多次执行当前大模型节点，而不需要拉多个节点，更不需要通过多次执行应用调用来实现。考虑到循环的中间结果与业务逻辑实现紧密相关，同时方便控制循环的次数和跳出条件，我们将循环作为节点的属性进行扩展。

## **循环属性展示**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7299676071/p765243.png)

循环属性需要在【是否开启循环】打开后才生效，一共有5项配置可以配置。

1、 **最大循环次数**：循环最大次数，当没有符合【终止条件】时最多循环的次数，默认为2，最大为10，

2、 **循环集合变量**：节点发生循环后，每一轮都会有一个结果，这个变量会存储每次循环的结果，返回结果是一个list。

3、 **当前循环变量**：节点发生循环，当前轮次的结果会保存在当前变量下，方便获取最终的变量，或者用当前变量设置终止条件。
4、 **循环次数变量**：循环最终次数保存在当前变量下，可用于设置终止条件，比如this.loopCount == 2，则循环2次跳出。

5、 **设置终止条件**：可以在【设置终止条件】中设置符合跳出循环的条件组，匹配逻辑和逻辑节点基本一致，不同的是这个条件可以引用当前节点的循环属性，比如this.loopCount为当前循环的次数，this.finalItem为当次循环结果，this.list为循环结果list等。当终止条件符合时，跳出循环。

如下图：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6299676071/p765254.png)

## **支持范围**

当前仅支持大模型设置循环属性，后续其他节点会视情况再开放扩展。

## **结果示例**

### **循环结果调试结果**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7299676071/p765249.png)

### **循环结果展示**

```json
{
  "finalResult": {
    "LLM_UItAJj": {
      "loopResult": {
        "stopReason": "满足跳出条件", // 循环跳出原因，有2种，满足跳出条件、达到循环次数
        "testList": [\
          {\
            "params": {\
              "modelId": "qwen-max", // 此处以qwen-max为例，您可按需更换模型名称。模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models\
              "prompt": "输出一句鲁迅说过的名言，不输出下面提到过的名言：${svcVars.LLM_UItAJj.loopResult.testList.#response.text#}，仅输出到名言本身"\
            },\
            "response": {\
              "text": "“其实地上本没有路，走的人多了，也便成了路。”"\
            }\
          },\
          {\
            "params": {\
              "modelId": "qwen-max",\
              "prompt": "输出一句鲁迅说过的名言，不输出下面提到过的名言：${svcVars.LLM_UItAJj.loopResult.testList.#response.text#}，仅输出到名言本身"\
            },\
            "response": {\
              "text": "“时间就像海绵里的水，只要愿挤，总还是有的。”"\
            }\
          },\
          {\
            "params": {\
              "modelId": "qwen-max",\
              "prompt": "输出一句鲁迅说过的名言，不输出下面提到过的名言：${svcVars.LLM_UItAJj.loopResult.testList.#response.text#}，仅输出到名言本身"\
            },\
            "response": {\
              "text": "“不在沉默中爆发，就在沉默中灭亡。”"\
            }\
          }\
        ],
        "loopCount": 3, // 完成的循环次数
        "isStop": true, // 是否结束
        "testItem": "“不在沉默中爆发，就在沉默中灭亡。”" // 最后一次循环结果
      },
      ……
    }
  }
}
```