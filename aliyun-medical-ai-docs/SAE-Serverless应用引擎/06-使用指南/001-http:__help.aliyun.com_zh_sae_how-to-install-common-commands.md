### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[常见问题](https://help.aliyun.com/zh/sae/faq-1/)[其他FAQ](https://help.aliyun.com/zh/sae/other-faq/)[Webshell FAQ](https://help.aliyun.com/zh/sae/faq-about-webshells/)如何安装常见命令？

# 如何安装常见命令？

更新时间：2024-09-02 14:37:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：如何将托管在EDAS的HSF应用，迁移并托管到SAE？](https://help.aliyun.com/zh/sae/how-to-migrate-an-hsf-application-hosted-in-edas-to-sae)[下一篇：如何单独控制Webshell权限？](https://help.aliyun.com/zh/sae/how-to-manage-the-permissions-on-webshells)

该文章对您有帮助吗？

反馈

**说明**

在Webshell中安装的命令，会在下次容器重建后消失。对于常用的命令，建议您在制作镜像时提前安装。

在排查问题的过程中，经常需要执行各种命令，包括ps、curl、telnet、vi和less等。如果镜像中不存在此类命令，可以通过SAE的 [一键复制安装命令](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/use-the-webshell-feature-to-check-the-health-status-of-applications#section-xl3-5fj-5is "") 功能进行安装。![db_copy_installation_commands_with_one_click](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0346717561/p463830.png)

如果需要安装其他命令，例如tcpdump，可以复制上图中 **预览命令** 文本框内的命令，修改代码中最后需要安装的软件。以上图为例，您可以把`net-tools`改为`tcpdump`，然后在 **Webshell** 内执行修改后的命令。