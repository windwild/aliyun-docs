### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[智能体 AgentRun](https://help.aliyun.com/zh/functioncompute/fc/agentrun/)[Agent运行时](https://help.aliyun.com/zh/functioncompute/fc/agent-runtime/)Agent集成与发布

# Agent集成与发布

更新时间：2025-12-02 03:34:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：低代码创建Agent快速入门](https://help.aliyun.com/zh/functioncompute/fc/quick-start-to-low-code-agent-creation)[下一篇：BrowserTool浏览器](https://help.aliyun.com/zh/functioncompute/fc/sandbox-browsertool)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

前提条件

操作步骤

进入集成与发布页面

配置UI集成

代码集成

## 功能介绍

在AgentRun运行时中创建的Agent，支持被其他系统调用，将已开发好的 Agent 快速集成到前端网页、后端服务等业务系统中

## **前提条件**

- 已创建可用的 Agent （ [快速创建Agent](https://help.aliyun.com/zh/functioncompute/fc/quickly-create-agent-no-code "")/ [代码创建Agent](https://help.aliyun.com/zh/functioncompute/fc/create-agent-by-code-high-code "")）并完成发布；

- 为Agent配置了管理Serverless开发平台（Devs）的权限（AliyunDevsFullAccess）。


## **操作步骤**

### 进入集成与发布页面

1. 进入 [AgentRun运行时](https://functionai.console.aliyun.com/agent/runtime/agent-list) 页面；

2. 在需要被集成的Agent卡片中，点击 **详情**；

3. 在Agent详情页，选择左侧目录的 **集成与发布**，进入集成与发布页面。


此时可以在页面中看到三种集成方式，按需选择被集成方式，分别为：

**UI集成**：

- 支持一键生成前后端一体的 Agent 应用界面；

- 可以将该界面以 iframe、独立域名等形式嵌入到现有网页或其他应用中；

- 适合快速提供“可视化对话界面”的场景（如内部工作台、门户网站等）。


**代码集成**：

- 提供标准的 HTTP API 接口（如兼容 OpenAI Chat Completions 协议）；

- 外部系统可以按标准协议API/SDK直接调用 Agent 的接口，适合多语言、多平台集成。


**生态集成**：

支持在Dify、n8n等平台集成Agent。

### **配置UI集成**

1. 选择 **集成模板**：通过集成模板，来指定UI **集成方式** 与 **风格模板**，选择完成后，可以点击 **预览效果**，查看当前配置的最终效果；

   - **集成方式**： **全屏嵌入**、 **浮窗聊天**、 **侧边栏**；

   - **风格模板**： **简约风格**、 **商务风格**、 **科技风格**、 **温馨风格**。
2. **开始集成**：点击 **开始集成** 后，需要指定集成的Agent对应版本的EndPoint，进行 **API绑定配置**，配置完成后，单击 **下一步**；

3. **等待部署完成**：查看部署日志，等待部署完成；

4. **测试部署结果**：部署成功后，会在页面中显示 **已部署的集成资源**，并生成一个临时的 **访问地址**，可以点击访问地址，进行Agent访问和使用；



**重要**





当前访问地址是 CNCF SandBox 项目 Serverless Devs 社区所提供，仅供学习和测试使用，不可用于任何生产使用；社区会对该域名进行不定期地拨测，并在域名下发 1 天后进行回收，强烈建议您绑定自定义域名以获得更好的使用体验。

5. 绑定 **自定义域名**：点击访问地址右侧的 **增加**，可以选择已有域名或新增域名进行正式域名的绑定，自定义域名配置可以参考 [配置自定义域名](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-custom-domain-names "")。


### **代码集成**

按标准协议API/SDK直接调用 Agent 的接口，适合多语言、多平台集成，代码示例如下：

```curl
curl https://12**********.agentrun-data.cn-hangzhou.aliyuncs.com/agent-runtimes/agent-code-XVe7d/endpoints/Default/invocations/openai/v1/chat/completions -XPOST \
 -H "content-type: application/json" \
 -d '{
 "messages": [{"role": "user", "content": "写一段代码,查询现在是几点?"}],
 "stream":true
 }'
```