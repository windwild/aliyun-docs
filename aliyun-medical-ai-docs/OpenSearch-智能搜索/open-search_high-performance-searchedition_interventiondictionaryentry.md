### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/high-performance-searchedition/control-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/high-performance-searchedition/data-structures/)InterventionDictionaryEntry

# InterventionDictionaryEntry

更新时间：2025-03-25 04:11:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：InterventionDictionary](https://help.aliyun.com/zh/open-search/high-performance-searchedition/interventiondictionary)[下一篇：实体类型重要性设置](https://help.aliyun.com/zh/open-search/high-performance-searchedition/priority-settings-of-entity-types)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

示例

结构

共有字段

特有字段

stopword 停用词

synonym 同义词

correction 拼写纠错

category\_prediction 类目预测

term\_weighting 词权重

ner 实体识别

suggest\_allowlist 下拉提示白名单

suggest\_denylist下拉提示黑名单

hot\_allowlist  热搜白名单

hot\_denylist  热搜黑名单

hint\_allowlist  底纹白名单

hint\_denylist  底纹黑名单

本文将为您详细介绍干预词典中的词条内容。

## 示例

```json
{
    "cmd": "add",
    "word": "过儿",
    "created": 1536661485,
    "updated": 1537320187,
    "status": "ACTIVE",
    "relevance": {
        "100": "0",
        "200": "2"
    }
}
```

## 结构

各干预词典的词条结构各有不同，区分为共有字段 \+ 特有字段，详情如下 ：

**说明**

- [stopword 停用词](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [synonym 同义词](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [correction 拼写纠错](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [category\_prediction 类目预测](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [term\_weighting 词权重](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [ner 实体识别](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [suggest\_allowlist 下拉提示白名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [suggest\_denylist 下拉提示黑名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [hot\_allowlist  热搜白名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [hot\_denylist  热搜黑名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [hint\_allowlist  底纹白名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)

- [hint\_denylist  底纹黑名单](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/interventiondictionaryentry)


## **共有字段**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| cmd | String | 操作命令：<br>- add 新增<br>  <br>- delete 删除 |
| word | String | 词条。 |
| status | String | 状态：<br>- ACTIVE 已生效 |
| created | Integer | 创建时间戳。 |
| updated | Integer | 更新时间戳。 |

## **特有字段**

### **stopword 停用词**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| stopword | Boolean | 干预类型：<br>- true 添加<br>  <br>- false 屏蔽 |

### **synonym 同义词**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| alias | Array | 添加的同义词。 |
| antiAlias | Array | 屏蔽的同义词。 |

### **correction 拼写纠错**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| correction | String | 纠正词。 |
| enabled | Boolean | 干预类型：<br>- true 添加<br>  <br>- false 屏蔽 |

### **category\_prediction 类目预测**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| relevance | Object | 干预内容键为类目预测ID，值为相关度（0：不相关；1：略相关；2：相关）例：{“2”:1,”100”:0}。 |

### **term\_weighting 词权重**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| tokens\[\] | Object | 词权重内容。 |
| tokens\[\].token | String | term |
| tokens\[\].weight | int | term权重，有7（权重高）、4（权重中）、1（权重低）。 |

**示例**

```json
{
  "word": "谭浩强c语言程序设计",
  "tokens": [\
    {\
      "token": "谭浩强",\
      "weight": 7\
    },\
    {\
      "token": "c语言",\
      "weight": 7\
    },\
    {\
      "token": "程序",\
      "weight": 1\
    },\
    {\
      "token": "设计",\
      "weight": 1\
    }\
  ]
}
```

### **ner 实体识别**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| tokens\[\] | Object | 干预内容。 |
| tokens\[\].tag | String | - 识别结果的英文名<br>  <br>- brand 品牌<br>  <br>- category 品类<br>  <br>- material 材质<br>  <br>- element 款式元素<br>  <br>- style 风格<br>  <br>- color 颜色<br>  <br>- function 功能功效<br>  <br>- scenario 场景<br>  <br>- people 人群<br>  <br>- season 时间季节<br>  <br>- model 型号<br>  <br>- region 地点地域<br>  <br>- name 人名<br>  <br>- adjective 修饰<br>  <br>- category-modifier 品类修饰词<br>  <br>- size 尺寸规格<br>  <br>- quality 品质成色<br>  <br>- suit 套装<br>  <br>- new-release 新品<br>  <br>- series 系列<br>  <br>- marketing 营销服务<br>  <br>- entertainment 文娱书文曲<br>  <br>- organization 机构实体<br>  <br>- movie 影视名称<br>  <br>- game 游戏名称<br>  <br>- number 数字<br>  <br>- unit 单位<br>  <br>- common 普通词<br>  <br>- new-word 新词<br>  <br>- proper-noun 专有名词<br>  <br>- symbol 符号<br>  <br>- prefix 前缀<br>  <br>- suffix 后缀<br>  <br>- gift 赠送<br>  <br>- negative 否定<br>  <br>- agent 代理 |
| tokens\[\].tagLabel | String | 识别结果的中文名，同上， **注意**：传参时不需要此字段 |
| tokens\[\].token | String | 实体词 |
| tokens\[\].order | Integer | 序号。 |
| matchType | Integer | 匹配类型，0 表示全query匹配时干预生效，1 表示query中有部分匹配干预也生效默认：0。 |

**示例**

```json
{
    "cmd": "add",
    "word": "豆本豆豆奶",
    "created": 1593429234,
    "updated": 1593429242,
    "status": "ACTIVE",
    "tokens": [{\
            "tag": "category",\
            "tagLabel": "品类",\
            "token": "豆",\
            "order": 1\
        },\
        {\
            "tag": "category",\
            "tagLabel": "品类",\
            "token": "本",\
            "order": 2\
        },\
        {\
            "tag": "common",\
            "tagLabel": "普通词",\
            "token": "豆豆",\
            "order": 3\
        },\
        {\
            "tag": "category",\
            "tagLabel": "品类",\
            "token": "奶",\
            "order": 4\
        }\
    ]
}
```

### **suggest\_allowlist 下拉提示白名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| score | Float | 分数。 |
| matchType | Integer | 匹配类型：<br>- 0<br>  <br>- 1<br>  <br>- 2 |

**重要**

score和matchType两个字段目前只读，不支持传参。

### **suggest\_denylist下拉提示黑名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| matchType | Integer | 匹配类型：<br>- 0<br>  <br>- 1<br>  <br>- 2 |

**重要**

matchType字段目前只读，不支持传参。

### **hot\_allowlist  热搜白名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| rank | Integer | 位置，取值范围：\[1-10\]。 |
| expirationTime | Integer | 过期时间戳（秒）。 |

### **hot\_denylist  热搜黑名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| matchType | Integer | 匹配类型：<br>- 0<br>  <br>- 1<br>  <br>- 2 |

**重要**

matchType字段目前只读，不支持传参。

### **hint\_allowlist  底纹白名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| expirationTime | Integer | 过期时间戳（秒）。 |

### **hint\_denylist  底纹黑名单**

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| matchType | Integer | 匹配类型：<br>- 0<br>  <br>- 1<br>  <br>- 2 |

**重要**

matchType字段目前只读，不支持传参。

若有收获，就点个赞吧