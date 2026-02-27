### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-通义听悟Agent](https://help.aliyun.com/zh/model-studio/official-application-tingwu-agent/)RAM子账号使用方式和授权操作

# RAM子账号使用方式和授权操作

更新时间：2026-02-11 02:04:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：产品简介](https://help.aliyun.com/zh/model-studio/product-introduction-2)[下一篇：语音转写（ASR）资源包](https://help.aliyun.com/zh/model-studio/purchase-and-use-discount-asr)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

创建RAM用户

通过RAM控制台授权

通过阿里云百炼控制台授权

如果您有让子账号授权管理阿里云百炼服务调用的需求，首先需要创建RAM用户。您既需要通过RAM控制台进行RAM授权，也需要通过阿里云百炼控制台进行控制台授权。

## 创建RAM用户

请参考文档 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "") 完成RAM用户创建。

## **通过RAM控制台授权**

1. 请访问 [RAM控制台](https://ram.console.aliyun.com/users)。

2. 在左侧导航栏选择**身份管理** \> **用户**。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9484877961/p729387.png)

3. 在待授权的RAM子账号的 **操作** 列，点击 **添加权限**。在 **权限策略** 区域的搜索框中搜索并勾选管理听悟服务（Tingwu）的权限（AliyunTingwuFullAccess），并单击 **确认新增授权**，完成授权操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4989047571/p1004855.png)


## **通过阿里云百炼控制台授权**

1. 访问 **[权限管理](https://bailian.console.aliyun.com/?tab=app#/authority)** 页面，单击 **新增用户**。

2. 选择需要管理阿里云百炼服务的RAM用户，并定义用户名称，单击 **确定，即完成添加用户。**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0954505571/p996195.png)

3. 对新增的用户需要进行权限配置，找到目标用户，点击其右侧的 **权限管理**，进行授权操作。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0954505571/p996199.png)

4. 进入 **权限管理** 页面后，点击 **添加权限** 按钮，选择 **管理员**，点击 **确定** 按钮，完成授权操作。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0954505571/p996206.png)