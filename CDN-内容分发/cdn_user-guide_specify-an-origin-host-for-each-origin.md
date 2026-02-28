### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/)[回源HOST](https://help.aliyun.com/zh/cdn/user-guide/origin-host/)指定源站回源HOST

# 指定源站回源HOST

更新时间：2026-02-24 02:42:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host)[下一篇：配置默认回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能说明

操作步骤

当您的同一个加速域名配置了多个回源站点并且需要结合HOST头请求不同虚拟站点的资源时，可以使用 **指定源站回源HOST** 功能，为不同的源站配置不同的回源HOST。

## **功能说明**

当您的加速域名绑定了多个源站时，默认回源HOST会将相同的域名发送给所有源站，这要求每个源站都必须配置对应的虚拟站点。而使用 **指定回源HOST** 功能，您可以为每个源站单独设置不同的回源HOST，灵活适配复杂的业务需求，避免不必要的配置麻烦。回源HOST的相关技术原理，请参见 [配置默认回源HOST](https://help.aliyun.com/zh/cdn/user-guide/configure-the-default-origin-host "")。

**说明**

在同时配置了 **默认回源HOST** 和 **指定源站回源HOST** 的情况下，CDN节点访问指定源站时，将会携带指定源站配置的回源HOST。

## 操作步骤

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **指定源站回源HOST** 区域，单击 **添加**。

6. 在弹出的 **指定源站HOST** 对话框中，配置相关参数。



![指定源站HOST](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9519648471/p543487.png)






| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **源站类型** | 在下拉列表中选择当前要配置的源站类型：<br>   - **基础源站地址**：在 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server#task-270231 "") 时添加的源站地址。<br>     <br>   - **所有源站**：CDN回源到的任意一个源站地址。<br>     <br>   - **自定义源站**：需要配置的源站地址不在源站信息列表中时，可以通过 **自定义源站** 来设置。 |
| **源站地址** | 与 **源站类型** 的对应关系如下：<br>   - 如果 **源站类型** 选择 **基础源站地址**，可在下拉列表中选择源站地址。<br>     <br>   - 如果 **源站类型** 选择 **所有源站**，无需配置源站地址。<br>     <br>   - 如果 **源站类型** 选择 **自定义源站**，您可以输入自定义源站地址。 |
| **回源HOST类型** | 在下拉列表中选择当前要配置的回源HOST类型：<br>   - **基础源站域名**：在 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server#task-270231 "") 时添加的源站地址（IP类型的源站除外）。<br>     <br>   - **加速域名**：当前在配置的CDN加速域名。<br>     <br>   - **自定义回源HOST**：需要配置的回源HOST不在源站信息列表中，同时也不是加速域名时，可以通过自定义回源HOST来设置。 |
| **回源HOST** | 与 **回源HOST类型** 的对应关系如下：<br>   - 如果 **回源HOST类型** 选择 **基础源站域名**，可在下拉列表中选择回源HOST。<br>     <br>   - 如果 **回源HOST类型** 选择 **加速域名**，为当前在配置的CDN加速域名，无需配置。<br>     <br>   - 如果 **回源HOST类型** 选择 **自定义回源HOST**，您可以输入自定义回源HOST。 |
| **规则条件** | 规则条件能够对用户请求中携带的各种参数信息进行识别，以此来决定某个配置是否对该请求生效。<br>   - **不使用**：不使用规则条件。<br>     <br>   - 若需新增或编辑规则条件，请在[规则引擎](https://help.aliyun.com/zh/cdn/user-guide/rules-engine "")中进行管理。 |

7. 单击 **确定**。