### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)配置层

# 配置层

更新时间：2025-02-26 00:36:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：为函数安装第三方依赖](https://help.aliyun.com/zh/functioncompute/fc/user-guide/install-third-party-dependencies-for-a-function)[下一篇：配置自定义层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-custom-layers-for-a-function-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

构建层

使用层

层（Layer）是一种集中管理函数公共依赖或资源的功能，您可以将依赖库、运行时或配置文件等内容提炼到层，供多个函数复用，减少部署函数的代码包体积的同时，实现多个函数之间的资源共享。

## **构建层**

您可以直接使用函数计算官方提供的公共层，也可以打包层文件构建自定义层，具体操作请参见 [创建自定义层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/create-a-custom-layer-1 "") 或 [如何基于Dockerfile构建层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/use-a-dockerfile-to-build-a-layer-1 "")。

## **使用层**

您可以为函数绑定官方公共层或自定义层，具体操作请参见以下文档。

- [配置自定义层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-custom-layers-for-a-function-1 "")

- [配置官方公共层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-common-layers-for-a-function-1 "")

- [官方公共层使用示例](https://help.aliyun.com/zh/functioncompute/fc/user-guide/official-common-layer-usage-example "")

- [如何在自定义运行时中引用层中的依赖](https://help.aliyun.com/zh/functioncompute/fc/user-guide/how-to-reference-dependencies-in-a-layer-in-a-custom-runtime "")