### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/)[Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/)应用部署

# 应用部署

更新时间：2024-10-11 04:00:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速部署Web应用](https://help.aliyun.com/zh/sae/quick-deployment-of-web-applications)[下一篇：通过代码包部署Web应用](https://help.aliyun.com/zh/sae/deploy-a-web-application-through-a-code-package)

该文章对您有帮助吗？

反馈

请您根据需求和业务现状选择合适的Web应用部署方式。

[通过镜像部署Web应用](https://help.aliyun.com/zh/sae/deploying-web-applications-via-mirroring "")：如果您已将应用构建为Docker镜像，或计划迁移到Docker容器技术栈，建议您通过镜像部署Web应用。您需要将Docker镜像推送到阿里云镜像服务（ACR），SAE可以拉取您的镜像并自动部署应用。

[通过源码部署Web应用](https://help.aliyun.com/zh/sae/deploy-web-applications-from-source-code/ "")：如果您正在使用或计划迁移到远程代码仓库管理源码（通常部署于GitHub、Gitee、GitLab或Codeup等服务提供商），建议您通过源码部署Web应用。SAE可以拉取您的源码、根据源码自动构建镜像并部署应用。

[通过代码包部署Web应用](https://help.aliyun.com/zh/sae/deploy-a-web-application-through-a-code-package "")：如果您当前仅在本地开发Java应用源码，希望尽快部署上线且不构建镜像，建议您将应用在本地打包成WAR包或JAR包，直接上传到SAE进行部署。后续您仍可以选择其他部署方式来迭代应用，SAE支持业务流量无损切换到新版应用。