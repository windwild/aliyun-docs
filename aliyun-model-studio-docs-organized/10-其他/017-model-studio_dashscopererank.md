### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[框架](https://help.aliyun.com/zh/model-studio/frameworks/)[LlamaIndex](https://help.aliyun.com/zh/model-studio/llamaindex/)DashScopeRerank

# DashScopeRerank

更新时间：2026-02-11 02:32:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用 Embedding 模型](https://help.aliyun.com/zh/model-studio/dashscopeembedding-in-llamaindex)[下一篇：DashScopeParse](https://help.aliyun.com/zh/model-studio/dashscopeparse)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

开始

前提条件

示例代码

参数说明

输入参数

DashScopeRerank提供阿里巴巴通义实验室开发的GTE-Rerank文本排序系列模型，开发者可以通过LlamaIndex框架进行集成高质量文本检索、排序。

## 开始

### **前提条件**

- 已开通阿里云百炼服务： [产品开通](https://help.aliyun.com/zh/model-studio/activate-alibaba-cloud-model-studio "")。

- 创建API\_KEY: [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

- 安装DashScopeRerank的安装包 (python>=3.8,<=3.12）


```python
pip install llama-index-core
pip install llama-index-postprocessor-dashscope-rerank
```

### **示例代码**

设置API-KEY

```shell
export DASHSCOPE_API_KEY=YOUR_DASHSCOPE_API_KEY
```

```python
from llama_index.core.data_structs import Node
from llama_index.core.schema import NodeWithScore
from llama_index.postprocessor.dashscope_rerank import DashScopeRerank

nodes = [\
    NodeWithScore(node=Node(text="text1"), score=0.7),\
    NodeWithScore(node=Node(text="text2"), score=0.8),\
]

dashscope_rerank = DashScopeRerank(top_n=5)
results = dashscope_rerank.postprocess_nodes(nodes, query_str="<user query>")
for res in results:
    print("Text: ", res.node.get_content(), "Score: ", res.score)
```

**示例代码输出**

```plaintext
Text:  text1 Score:  0.25589250620997755
Text:  text2 Score:  0.18071043165292258
```

## 参数说明

### 输入参数

- DashScopeRerank参数说明如下


| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 参数 | 类型 | 默认值 | 说明 |
| model | string | gte-rerank | 支持的模型列表：<br>- gte-rerank |
| top\_n | int | 3 | 排序返回的top文档数量, 如果没有指定则返回全部候选doc，如果指定的top\_n值大于输入的候选doc数量，返回全部doc |
| return\_documents | bool | False | 返回的排序结果列表里面是否返回每一条document原文，默认值False |
| api\_key | str | None | DashScope api key，可以通过环境变量等方法设置 |