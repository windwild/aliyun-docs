### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[开发者工具](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/developer-tools/)[WebIDE](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/webide/)什么是WebIDE

# 什么是WebIDE

更新时间：2025-08-04 04:55:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：从Funcraft迁移到Serverless Devs](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/migrate-resources-from-funcraft-to-serverless-devs)[下一篇：使用WebIDE打包函数第三方依赖](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/use-webide-to-package-third-party-dependencies-of-a-function)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

使用限制

WebIDE界面概览

通过控制台配置WebIDE

前提条件

操作步骤

常见问题

WebIDE加载异常，如何处理？

什么是专有版WebIDE？

为什么函数在终端中执行成功，单击测试函数执行失败？

如何快速重置函数的WebIDE环境变量、Runtime和层？

Serverless版WebIDE工作空间会保存多久？

函数计算的WebIDE支持的Runtime有哪些？

是否支持在WebIDE进行代码调试？

修改函数，git插件会显示代码差异，是因为WebIDE对函数代码进行了托管吗？

同一个阿里云账号的两个RAM用户打开相同的函数，为什么显示的代码不一样？

WebIDE终端打开很慢或者打不开怎么办？

相关文档

WebIDE是函数计算提供的在线开发IDE，提供接近原生VSCode的云端开发体验。开发者能够直接在线进行代码编写、调试和部署，而不需要在本地安装复杂的开发环境。本文介绍WebIDE的功能、界面概览以及通过函数计算控制台配置WebIDE等。

## 功能介绍

WebIDE支持以下功能。

- 完整的代码开发、部署和调试功能。

- WebIDE的终端环境和线上函数计算的Runtime执行环境一致。

  - 针对不同的Runtime，预置pip、npm和composer等常用的开发工具和编程语言开发环境。您可以直接在终端打包第三方依赖，而无需担心和线上环境有差异。

  - 内置Serverless Devs工具，并能自动根据您当前登录的账号完成Serverless Devs配置，无需再执行`s config`命令。配置的别名默认为`default`。
- 使用通义灵码辅助代码编写。

开发者可以开箱即用使用通义灵码的智能编码能力，提高编码效率。通义灵码能够实时进行代码审查，检测潜在的逻辑错误，且当函数运行异常时，能快速定位问题然后提供修复指导，实现开发效率和代码质量的双重提升。


**说明**

为了获得更好的WebIDE使用体验，建议您使用最新版本的Google Chrome浏览器。

## 使用限制

- WebIDE目前仅支持Python、Node.js、PHP和Custom Runtime运行时。具体信息，请参见 [函数计算的WebIDE支持的Runtime有哪些？](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/what-is-webide#p-ekk-mz4-irg "")。不支持Java、Go和C#运行时在线编辑，以上语言只支持上传编译打包后的ZIP文件或二进制文件。

- WebIDE为每个用户提供的存储空间为5 GB，超出后将无法执行写入操作，请及时清理。

- 打开某个函数的WebIDE后，会自动启用一个实例。此实例约等于一个1核 1.5GB的容器实例。

- WebIDE实例的环境与您函数的Runtime环境一致，但是此实例无法加载您的自定义层和挂载的NAS或OSS，且无法访问您的服务配置的VPC环境。如您有此需求，可以完成代码部署后再调用函数，或者使用专有版WebIDE。

- 专有版WebIDE目前仅支持在华东1（杭州）、华东2（上海）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华南1（深圳）、中国香港、新加坡、日本（东京）、德国（法兰克福）和美国（弗吉尼亚）地域使用。如果您需要在其他地域使用，请加入钉钉用户群（钉钉群号：**64970014484**）申请。


## WebIDE界面概览

下图为全屏模式下的WebIDE界面，划分为 **①资源管理器、②文件编辑区、③函数操作区和④命令行终端** 四个区域。![web-ide](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2303436761/p558952.png)

- **①资源管理器**：查看代码结构，包括代码文件和依赖文件等。

- **②文件编辑区**：完成函数代码的编辑。代码编辑完成后，您可以单击右上角的![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2492481071/p744532.png)按钮开始调试您的代码。如果需要完全实现线上和终端环境一致，需要在 **③函数操作区** 单击 **部署代码**。

- **③函数操作区**：完成函数代码的部署和测试。单击 **退出全屏** 后，函数操作区位于WebIDE界面的左上方。

- **④命令行终端**：在WebIDE界面上方工具栏，选择**Terminal** \> **New Terminal**打开命令行终端。在命令行终端，您可以调试您的代码或者安装第三方依赖。


## 通过控制台配置WebIDE

### **前提条件**

已创建服务和函数。具体操作，请参见 [创建服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-services#section-765-0zj-cc4 "") 和 [创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#section-b9y-zn1-5wr "")。

### **操作步骤**

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称，然后在函数详情页面，单击 **函数代码** 页签。
4. **可选：**在函数详情页面的 **函数代码** 页签，单击右上角的 **配置 WebIDE**，然后在 **配置 WebIDE** 面板，选择WebIDE的类型。



您可以选择 **Serverless 版** WebIDE或者 **专有版** WebIDE。



   - **Serverless 版**

     您可以同时勾选 **关闭专有版 WebIDE**，确保每次打开WebIDE时，都默认选择 **Serverless 版** WebIDE。

   - **专有版**

     如果需要实例能够加载您的自定义层和挂载的NAS或OSS，以及访问服务配置的VPC环境，可以选择 **专有版** WebIDE，同时设置以下配置项。


     - **实例规格方案**

     - **执行超时时间**


如果选择专有版WebIDE，函数计算将根据您函数所属地域的VPC情况，复用或者自动创建一个VPC、一个交换机和一个通用型NAS。关于自动创建资源的费用详情，请参见 [通用型NAS计费](https://help.aliyun.com/zh/nas/product-overview/billing-of-general-purpose-nas-file-systems#task-2567548 "")。

5. 在WebIDE界面，按需执行函数代码编写、测试和安装第三方依赖等操作。



关于WebIDE界面的分区介绍，请参见 [WebIDE界面概览](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/what-is-webide#section-z8g-pqu-872 "")。


**重要**

如果选择专有版WebIDE，请确保您的函数能正常执行，否则可能无法正常打开WebIDE。

## 常见问题

### WebIDE加载异常，如何处理？

尝试刷新函数详情页面或者快速重置WebIDE环境。关于重置WebIDE环境的具体操作，请参见 [如何快速重置函数的WebIDE环境和工作空间内容？](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/what-is-webide#p-vqz-w87-n0t "")。

### 什么是专有版WebIDE？

专有版WebIDE的本质是部署在您的账号下的一个FC函数。函数所属的服务名称以`_webide-server-`开头。

使用专有版WebIDE，实例可以加载您的自定义层和挂载的NAS或OSS，且支持访问您的服务配置的VPC，实现真正的终端与线上Runtime环境一致，便于更好的开发和调试。您还可以选配实例的规格方案，例如，提高CPU和内存规格，提升WebIDE性能。

选择专有版WebIDE后，其本质的函数运行在您自己的账号下，因此，需额外承担以下费用成本。

- 函数计算的函数调用和资源使用等费用。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/billing-overview#concept-2557114 "")。

- 挂载NAS文件存储系统的相关费用。更多信息，请参见 [通用型NAS计费](https://help.aliyun.com/zh/nas/product-overview/billing-of-general-purpose-nas-file-systems#task-2567548 "")。


### 为什么函数在终端中执行成功，单击测试函数执行失败？

WebIDE可以帮助开发者快速进行代码测试、项目构建和依赖安装，但是WebIDE的环境并非函数计算真正的执行环境。在WebIDE中，无法直接测试自定义层和挂载的NAS或OSS，也无法测试通过VPC访问对应资源。

为了避免出现此问题，您可以选择使用专有版WebIDE或者编辑完代码后，单击 **部署代码**，然后单击 **测试函数** 进行测试。

### 如何快速重置函数的WebIDE环境变量、Runtime和层？

当您重新刷新函数详情页面或WebIDE界面时，会将线上函数最新的环境变量、层以及Runtime更新到WebIDE实例。您可以在终端执行`env`查看最新的函数环境变量等信息。

### Serverless版WebIDE工作空间会保存多久？

默认工作空间保存的时间为48小时，即如果您持续48小时未通过WebIDE打开这个函数，这个工作空间内容会被删除。

另外，如果线上代码通过控制台或调用SDK工具等方式被修改，函数的`code checksum`发生变更，刷新或重新打开WebIDE，会自动刷新工作区间的内容为线上最新代码。

### 函数计算的WebIDE支持的Runtime有哪些？

WebIDE支持的Runtime如下所示。

- Python

支持Python 3.10、Python 3.9、Python 3.6和Python 2.7。

- Node.js

支持Node.js 16、Node.js 14、Node.js 12、Node.js 10和Node.js 8。

- PHP

支持PHP 7.2。

- Custom Runtime

支持Custom Runtime和Custom Runtime（Debian10）。


### 是否支持在WebIDE进行代码调试？

支持。您可以直接使用WebIDE内置的各Runtime的VSCode调试插件。如果是Custom Runtime其他小众语言，可以安装合适的VSCode插件。

以Python 3.9为例，需要增加一些辅助代码来完成Handler函数运行。如下图红框所示。![vscode-auxiliary-code](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1338336761/p559450.png)

### 修改函数，git插件会显示代码差异，是因为WebIDE对函数代码进行了托管吗？

不是。WebIDE打开时，第一次打开函数代码包，会自动初始化一个`git init`，用于显示当前代码和线上代码的差异。当您单击一次 **部署函数** 后，会自动生成一个`commit`，即实现终端和线上的代码完全一致（下图中`save function with codechecksum xxxx`表示执行了一次函数部署）。该功能用于提升用户使用体验。![git-init-commit](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2303436761/p559537.png)

### 同一个阿里云账号的两个RAM用户打开相同的函数，为什么显示的代码不一样？

函数计算的WebIDE支持同一个阿里云账号的RAM用户的工作空间隔离。例如，RAM用户A打开的是WebIDE A，RAM用户B打开的是WebIDE B，RAM用户A在自己的工作空间修改代码等，RAM用户B无法感知。此时，RAM用户A和RAM用户B看到的代码显示不同。

RAM用户A和RAM用户B均可以看到自己工作空间和线上函数代码的差异。更多信息，请参见 [修改函数，git插件会显示代码差异，是因为WebIDE对函数代码进行了托管吗？](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/what-is-webide#p-fid-7dn-oxy "")。

### **WebIDE终端打开很慢或者打不开怎么办？**

您可以参照以下步骤进行排查：

1. 检查网络设置是否正确，例如您的本地客户端是否设置了代理限制访问，或者禁用了WebSocket协议。WebIDE使用WebSocket进行实时通信和交互，禁用WebSocket将导致WebIDE无法正常运行。

2. 检查本地客户端是否打开的是海外地域的函数，如果本地客户端网络跨境能力较差，尝试打开海外地域的函数会导致连接缓慢或者无法连接。

3. 检查您的代码包是否过大。如果代码包体积过大，上传或部署代码需要较长的时间，您可以尝试优化代码包后再重试。


如果按照以上步骤排查处理后，问题仍未解决，请 [联系我们](https://help.aliyun.com/zh/functioncompute/fc-2-0/support/contact-us "")。

## **相关文档**

- 您还可以使用WebIDE终端打包函数的第三方依赖。具体操作，请参见 [使用WebIDE打包函数第三方依赖](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/use-webide-to-package-third-party-dependencies-of-a-function "")。

- 如果您的函数代码体积较大，或要安装的第三方依赖包体积较大，可将函数依赖提炼到层或者使用函数计算官方公共层来缩小代码体积。具体操作，请参见 [创建自定义层](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/create-a-custom-layer "")。

- 您也可以通过Serverless Devs工具的本地调试功能在本地对函数进行测试。更多信息，请参见 [本地调试](https://docs.serverless-devs.com/user-guide/aliyun/fc/command/local/)。