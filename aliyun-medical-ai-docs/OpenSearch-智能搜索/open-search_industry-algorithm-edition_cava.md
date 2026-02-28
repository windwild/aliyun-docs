### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)排序插件 Cava

# 排序插件 Cava

更新时间：2025-02-24 20:56:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管控API说明](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/overview-3)[下一篇：Cava 类与对象](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/classes-and-objects)

该文章对您有帮助吗？

反馈

Cava是OpenSearch引擎团队基于llvm实现的一门高效的编程语言，它的语法和Java类似，性能与c++相当。Cava是一门面向对象的编程语言，支持即时编译（jit），支持各种安全检查保证程序更加健壮。

使用cava和OpenSearch提供的cava库，在OpenSearch中可以定制自己的排序插件，相比于OpenSearch支持的表达式，使用cava实现排序插件具有以下优点：

- 更强的定制能力：cava提供了较表达式更加丰富的语法功能，比如for循环，函数定义，类定义等，用户可以实现自己的业务需求。

- 更易于维护：cava实现的排序插件比表达式更具有可读性，更易于维护。

- 更易于接受：cava的语法和Java类似，熟悉Java的同学很容易使用cava进行开发，学习成本较低。