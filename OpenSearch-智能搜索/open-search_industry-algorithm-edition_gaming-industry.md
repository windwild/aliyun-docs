### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[实践教程](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/best-practices-2/)[行业篇](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry/)游戏行业

# 游戏行业

更新时间：2023-04-06 04:17:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：教育搜题](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/search-for-test-questions)[下一篇：内容社区行业](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/content-community)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

客户背景

搜索业务背景

开放搜索游戏行业增强版解决方案

客户价值

游戏行业增强版最佳实践。

## 客户背景

中国知名的文化社区和视频平台，其游戏板块为玩家提供游戏下载、游戏测试、社区讨论、攻略等多元化内容，并且游戏收入占据总营收结构中的重要部分。

## 搜索业务背景

- 内容形式多样，包含视频、wiki、攻略、用户等多个类目，需同时满足上述综合搜索需求；

- 业务围绕在游戏搜索、社区论坛攻略搜索等场景，搜索是引导业务转化最重要的功能；

- 自研搜索效果不满足业务需求，无结果率较高，点击率较低；

- 游戏行业专属分词复杂垂直，涉及游戏名称、版本、角色、装备、主播等Query，且新词迭代快，搜索效果直接影响终端用户搜索体验；

- 游戏场景分词涉及别称、术语、昵称，需要运营同学参与业务调优，自研搜索无法满足运营需求；

- 搜索引导需要满足个性化搜索需求；


## 开放搜索游戏行业增强版解决方案

开放搜索（OpenSearch）是阿里云自主研发的大规模分布式搜索引擎搭建的一站式智能搜索业务开发平台，无需开发，一键接入即可获得高质量搜索服务，内置阿里系技术多年沉淀的核心搜索引擎，行业前沿的搜索能力和算法能力，并充分开放支持内部调用客户自己的算法模型，满足各行业各场景的业务需求，与客户彼此成就、共同成长；

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6509670861/p620829.png)

1. **客户数据定制分词**


针对客户业务场景为特定领域的情况，在文本搜索的分词算法上，通过自动化基于客户数据的定制分词模型流程，可以在天级别完成适配，提供客户专属的文本分词器。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5509670861/p620826.png)

**通用版VS游戏增强版分词效果对比：**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6509670861/p620828.png)

**2\. 游戏行业向量召回模型**

相比传统文本搜索需要通过分词、同义词、纠错、词权重改写等算法技术增强语义搜索效果，基于深度学习的语义向量召回模型具备更强大的表征能力，可以更好地处理用户查询词中的简写、别名、拼写错误等情况。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5509670861/p620825.png)![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6509670861/p620824.png)

**3.个性化搜索引导**

- 下拉提示实现了

**基于用户文档内容的query智能抽取**

，可以通过中文前缀，拼音全拼，拼音首字母简拼查询以及汉字加拼音，分词后前缀，中文同音别字等查询下拉提示的候选query。

- 热搜和底纹是一个完整搜索引擎必备的基本功能，通常占据着

**搜索框入口的重要位置**

，提供不可或缺的业务价值.


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6509670861/p620827.png)![](https://ucc.alicdn.com/pic/developer-ecology/5b6f32b39fa74e6b9edfcbf446af0567.png)

## 客户价值

1. 仅用1周时间高效接入上线，几乎无需额外调试，快速响应客户侧业务需求；

2. 游戏行业增强版搜索效果明显优于自建搜索，核心指标无结果PV下降10%，无结果率下降40%，提升业务转化效果；

3. 直接解决大部分之前自建搜索的badcase，游戏行业智能语义理解功能优化了用户产品体验，用户黏性得以提审；

4. 测试了客户在维护中的重要运营词，搜索效果均符合预期，运营侧同学可通过控制台直接调优维护，与产品技术协同，对搜索指标负责，持续跟进搜索能力迭代；


了解更多【开放搜索游戏行业增强版】产品能力，可查看 [产品文档](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/configure-an-application-of-industry-algorithm-edition-for-gaming)