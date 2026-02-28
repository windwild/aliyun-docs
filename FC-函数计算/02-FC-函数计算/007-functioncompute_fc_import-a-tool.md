### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[智能体 AgentRun](https://help.aliyun.com/zh/functioncompute/fc/agentrun/)[工具管理](https://help.aliyun.com/zh/functioncompute/fc/tool-management/)导入现有工具

# 导入现有工具

更新时间：2025-12-02 03:34:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用代码创建工具](https://help.aliyun.com/zh/functioncompute/fc/using-the-code-creation-tool)[下一篇：API打包](https://help.aliyun.com/zh/functioncompute/fc/api-packaging)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能简介

支持的导入类型

三、操作步骤

步骤 1：创建工具并选择导入工具

步骤 2：编辑导入工具配置

2.2 导入 MCP 工具

2.3 导入 FunctionCall 工具（OpenAPI）

步骤 3：配置第三方访问凭证（可选）

步骤 3：第三方凭证配置

3.1 模式选择

步骤 4：创建工具并查看导入详情

当已经在外部系统中拥有成熟的 API 或 MCP Server，希望直接在 AgentRun 中作为工具复用时，可以使用导入工具方式。

## **功能简介**

通过 **导入工具**，你可以：

- 将符合 MCP 协议 或 OpenAPI 规范 的现有服务快速接入 AgentRun，无需改写代码；

- 在 AgentRun 中统一管理工具的配置、凭证与调用；

- 让 Agent 以 MCP 工具 或 Function Call 工具 的形式调用这些已有能力。


## 支持的导入类型

在 **导入工具配置** 中，目前支持两类工具类型：

1. **MCP 工具**

   - 通过 MCP 配置（JSON）导入符合 Model Context Protocol 规范的工具；

   - 适用于已有 MCP Server 或已生成 MCP 配置的工具。
2. **FunctionCall 工具**

   - 通过 OpenAPI 3.0 规范导入；

   - 平台根据 OpenAPI 描述生成 Function Call 工具，用于支持具备函数调用能力的大模型。

## 三、操作步骤

### 步骤 1： **创建工具** 并选择 **导入工具**

1. 登录 [AgentRun 控制台](https://functionai.console.aliyun.com/cn-hangzhou/agent/runtime/agent-list)，在顶部菜单栏，点击 **其他**；

2. 在左侧目录选择 **工具管理**，单击 **创建工具**；

3. 在 **选择创建方式** 中选择 **导入工具**；


> 其他选项包括 **[代码创建](https://help.aliyun.com/zh/functioncompute/fc/using-the-code-creation-tool "")**、 **API 打包**、 **[工具市场](https://help.aliyun.com/zh/functioncompute/fc/tool-market "")**，本节只介绍 **导入工具**。

4. 在 **基本信息** 区域填写：

   - 工具名称：必填，用于在 AgentRun 中标识该工具，如 `tool-4ohq`；

   - 工具描述：可选，简要说明工具用途，便于后续管理与协作。

### 步骤 2：编辑导入工具配置

在 **导入工具配置** 区域，根据实际情况选择工具类型并填写对应配置。

#### 2.1 选择工具类型

在 **工具类型** 下拉中选择：

- **MCP 工具：** 导入 MCP 协议工具；

- **FunctionCall 工具**：导入 Function Call 工具（基于 OpenAPI）。


后续配置项会根据所选工具类型自动切换。

### 2.2 导入 MCP 工具

当 **工具类型** 选择 **MCP 工具** 时，界面显示MCP 协议说明。

#### 2.2.1 直接粘贴 MCP 配置

1. 在 **直接粘贴 MCP 配置** 文本框中，粘贴完整的 MCP JSON 配置内容；

2. 也可以点击 **示例** 查看 MCP 配置示例，以确保格式正确；

3. 确认 JSON 结构合法，并符合 MCP 规范（包括 tools、transport、parameters 等字段）。


#### 2.2.3 远程 MCP Server 的传输协议说明

如果导入的是远程 MCP Server，MCP JSON 中通常需要明确指定 `transportType` 字段，用于告诉 AgentRun 如何与该 MCP Server 通信：

- `streamable-http`：通过 HTTP（可流式）方式访问；

- `sse`：通过 Server-Sent Events 方式访问。


请根据你的 MCP Server 实际实现填入相应配置。如果配置不正确，可能导致 Agent 无法成功调用该工具。

### 2.3 导入 FunctionCall 工具（OpenAPI）

当工具类型选择 **FunctionCall 工具** 时，界面显示 **OpenAPI 规范** 说明，并支持以下两种导入方式：

1. 通过 **OpenAPI规范URL** 导入；

2. 直接粘贴 OpenAPI 规范内容。


#### 2.3.1 通过 OpenAPI URL 导入

1. 在 **OpenAPI 规范 URL** 输入框中填写 OpenAPI 3.0 地址，例如：















```http
https://api.example.com/openapi.json
```

2. 点击右侧 **导入** 按钮，平台会从该 URL 拉取 OpenAPI 文档并解析为工具定义；

3. 确认导入结果无误（可查看生成的工具方法和参数）。


#### 2.3.2 直接粘贴 OpenAPI 规范

1. 在 **或直接粘贴 OpenAPI 规范** 文本框中，粘贴完整的 OpenAPI JSON 或 YAML 内容；

2. 你可以点击 **示例** 查看支持的 OpenAPI 格式样例；

3. 确保符合 OpenAPI 3.0 规范，尤其是 `paths`、`components.schemas` 等部分定义清晰。


平台会根据 OpenAPI 文档中的接口信息生成对应的 Function Call 工具描述。

### 步骤 3：配置第三方访问凭证（可选）

- OpenAPI 规范 URL（可选）

- 或直接粘贴 OpenAPI 规范（必填其一）


#### 2.3.1 通过 OpenAPI URL 导入

1. 在 「OpenAPI 规范 URL」 输入框中填入文档地址，例如：















```pre
text

https://api.example.com/openapi.json
```

2. 点击右侧 「导入」 按钮，平台会从该 URL 拉取并解析 OpenAPI 3.0 文档；

3. 确认生成的工具定义符合预期。


#### 2.3.2 直接粘贴 OpenAPI 文档

1. 在 「或直接粘贴 OpenAPI 规范」 文本框中粘贴完整的 OpenAPI JSON 或 YAML 内容；

2. 可点击「示例」查看支持的 OpenAPI 样例；

3. 确保文档符合 OpenAPI 3.0 规范。


* * *

## 步骤 3：第三方凭证配置

配置工具服务访问工具后端的凭证，如导入的工具一个远程的http地址，这个地址是需要鉴权，此时需要配置第三方凭证用于工具服务访问工具后端的鉴权。

点击页面底部的 **访问凭证** 区域中的 **出站：第三方凭证配置**，会弹出如下配置面板：

### 3.1 模式选择

可以看到三种模式：

1. **不使用凭证**：调用第三方服务的请求不会携带任何认证信息，适用于完全公开、无需鉴权的 API，或开发阶段临时调试。

2. **API 密钥**：需要传入简单的 API Key/Token，但不希望提前在 **凭证管理** 里创建持久凭证，该密钥仅用于当前导入的工具，不会保存到全局凭证管理中。

1. 在 **访问密钥** 输入框中，直接输入要传给第三方服务的 API Key；

2. 保存配置后，平台在调用该工具时会将该密钥注入到请求中（具体携带方式由工具协议和集成方式决定）。
3. **使用已有凭证**（推荐）：希望统一管理和轮转密钥或多个工具或 Agent 需要复用同一组凭证的场景。选择的凭证将从凭证管理中读取，可以在凭证管理中统一维护（更新、禁用、轮转）这些凭证。

1. 选择 **使用已有凭证**；

2. 在 **选择已有凭证** 下拉框中选择一条已在 [凭证管理](https://help.aliyun.com/zh/functioncompute/fc/voucher-management "") 中创建好的凭证；

3. 如列表为空，可点击旁边的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3492664671/p1030964.png)或进入 **凭证管理** 页面先创建凭证，再返回刷新列表（使用刷新按钮）。

### 步骤 4：创建工具并查看导入详情

1. 检查基本信息、导入配置和访问凭证无误后，点击右上角创建工具；

2. 创建成功后，会跳转到该工具的详情页，在此可以看到：


你可以在工具详情中进一步：

- 查看或更新导入配置（如更新 MCP / OpenAPI URL 或内容）；

- 调试工具调用，确认接口行为与预期一致；

- 作为 MCP 工具/Function Call 工具在 [快速创建Agent](https://help.aliyun.com/zh/functioncompute/fc/quickly-create-agent-no-code "") 或 [代码创建Agent](https://help.aliyun.com/zh/functioncompute/fc/create-agent-by-code-high-code "") 时引用。