### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Qwen Code

# Qwen Code

更新时间：2026-02-19 23:05:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Postman](https://help.aliyun.com/zh/model-studio/first-call-to-image-and-video-api)[下一篇：模型调优简介](https://help.aliyun.com/zh/model-studio/model-training-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作步骤

准备工作

安装与配置 Qwen Code

配置环境变量

向 Qwen Code 提问

查看 Token 消耗

免费额度

进阶操作

常见问题

Q：Qwen Code 为什么 Token 消耗快？

Q：如何切换模型？

Q：如何使用每天 2000 次的免费额度？

Q：为什么报 401 Incorrect API key provided 错误？

Qwen Code 是一款专为 [Qwen3-Coder](https://help.aliyun.com/zh/model-studio/qwen-coder#9c99e53843iws "") 模型优化的命令行 AI 工作流工具，通过先进的代码理解能力、自动化任务和智能辅助功能，显著提升开发效率。

**重要**

本文档仅适用于按量付费模式。如果您已订阅阿里云百炼 Coding Plan 并希望在 Qwen Code 中使用，请参考 [Coding Plan 说明文档](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。

## **操作步骤**

### 准备工作

- **获取API Key**：在开始前，请先 [获取阿里云百炼API Key](https://help.aliyun.com/zh/model-studio/get-api-key#c38fb45bc6sje "")。

- **检查 Node.js 版本**：Qwen Code 需要 [**Node.js**](https://nodejs.org/zh-cn/download) 20 或更高版本，请运行 `node -v` 检查版本，若低于 20，请重新安装。


### 安装 **与配置** Qwen Code

1. **安装 Qwen Code**

在终端中执行以下任一命令来安装 Qwen Code。






npm 安装（推荐）



源码安装

































```zsh
# 配置镜像源加速
npm config set registry https://registry.npmmirror.com
npm install -g @qwen-code/qwen-code@latest
```



















```bash
git clone https://github.com/QwenLM/qwen-code.git
cd qwen-code
npm install
npm install -g .
```

2. **启动并配置 Qwen Code**

1. **启动 Qwen Code**

      在终端中输入`qwen`以启动 Qwen Code。

2. **选择认证方式**

      此处以 OpenAI 认证方式为例。选中 **OpenAI**，单击 Enter 后通过阿里云百炼提供的 OpenAI 兼容认证方式接入。

      ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2190505571/p996120.png)

      在页面填入以下信息：


      |     |     |     |
      | --- | --- | --- |
      | **配置项** | **说明** | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7721194571/p995220.png) |
      | **API Key** | 阿里云百炼 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") |
      | **Base URL** | - **北京地域**：`https://dashscope.aliyuncs.com/compatible-mode/v1`<br>        <br>      - **新加坡地域**：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`<br>        <br>      - **弗吉尼亚地域**：`https://dashscope-us.aliyuncs.com/compatible-mode/v1` |
      | **Model** | 模型名。Qwen Code 专为 [Qwen3-Coder](https://help.aliyun.com/zh/model-studio/qwen-coder#9c99e53843iws "") 系列模型优化，并兼容提供 [千问](https://help.aliyun.com/zh/model-studio/qwen-api-reference/#d397bcc41eu3q "") 接口的模型，包括[千问Max](https://help.aliyun.com/zh/model-studio/models#d4ccf72f23jh9 "")、 [千问Plus](https://help.aliyun.com/zh/model-studio/models#5ef284d4ed42p "")、 [千问Flash](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "") 和 [DeepSeek](https://help.aliyun.com/zh/model-studio/models#935bd5ba5cg5d "")等。建议选择代码能力较强的模型，如：<br>      - `qwen3.5-plus`<br>        <br>      - `qwen3-coder-next`<br>        <br>      - `qwen3-coder-plus`<br>        <br>      - `qwen3-max`<br>        <br>> 各模式支持的模型请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。 |


      若您不想每次启动后都输入以上信息，请参见下文配置环境变量。




      ### **配置环境变量**







      可配置全局环境变量，或通过`.env`文件配置。同时配置时，全局环境变量优先于`.env`文件配置生效。







      .env文件



      全局环境变量



















      在项目根目录下创建`.env`文件，写入以下内容并保存。环境变量将仅在当前项目中生效。

















      ```plaintext
      # 用您的百炼API KEY代替YOUR_DASHSCOPE_API_KEY
      OPENAI_API_KEY="YOUR_DASHSCOPE_API_KEY"
      # 以下为北京地域的base_url，不同地域需配置对应的 base_url
      OPENAI_BASE_URL="https://dashscope.aliyuncs.com/compatible-mode/v1"
      # 此处以qwen3-coder-next模型为例，您可按需更换其他模型
      OPENAI_MODEL="qwen3-coder-next"
      ```





      将阿里云百炼提供的 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 、 Base URL 和 Model 设置为全局环境变量。环境变量将对所有项目和终端会话生效。







      macOS



      Windows



















      1. 在终端中执行以下命令，查看默认 Shell 类型。















         ```bash
         echo $SHELL
         ```

      2. 根据 Shell 类型设置环境变量，命令如下：






         Zsh



         Bash

































         ```bash
         # 用您的百炼API KEY代替YOUR_DASHSCOPE_API_KEY
         # 以下为北京地域的base_url，不同地域需配置对应的 base_url
         # 这里以qwen3-coder-next模型为例，您可以根据需要更换其他模型
         echo 'export OPENAI_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.zshrc
         echo 'export OPENAI_BASE_URL="https://dashscope.aliyuncs.com/compatible-mode/v1"' >> ~/.zshrc
         echo 'export OPENAI_MODEL="qwen3-coder-next"' >> ~/.zshrc
         ```



















         ```bash
         # 用您的百炼API KEY代替YOUR_DASHSCOPE_API_KEY
         # 以下为北京地域的base_url，不同地域需配置对应的 base_url
         # 这里以qwen3-coder-next模型为例，您可以根据需要更换其他模型
         echo 'export OPENAI_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.bash_profile
         echo 'export OPENAI_BASE_URL="https://dashscope.aliyuncs.com/compatible-mode/v1"' >> ~/.bash_profile
         echo 'export OPENAI_MODEL="qwen3-coder-next"' >> ~/.bash_profile
         ```

      3. 在终端中执行下列命令，使环境变量生效。






         Zsh



         Bash

































         ```bash
         source ~/.zshrc
         ```



















         ```bash
         source ~/.bash_profile
         ```


CMD

PowerShell

      1. 在CMD中运行以下命令，设置环境变量。















         ```powershell
         # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
         # 以下为北京地域的base_url，不同地域需配置对应的 base_url
         # 这里以qwen3-coder-next模型为例，您可以根据需要更换其他模型
         setx OPENAI_API_KEY "YOUR_DASHSCOPE_API_KEY"
         setx OPENAI_BASE_URL "https://dashscope.aliyuncs.com/compatible-mode/v1"
         setx OPENAI_MODEL "qwen3-coder-next"
         ```

      2. 打开一个新的CMD窗口，运行以下命令，检查环境变量是否生效。















         ```powershell
         echo %OPENAI_API_KEY%
         echo %OPENAI_BASE_URL%
         echo %OPENAI_MODEL%
         ```


      1. 在PowerShell中运行以下命令，设置环境变量。















         ```powershell
         # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
         # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
         # 这里以qwen3-coder-next模型为例，您可以根据需要更换其他模型
         [Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "YOUR_DASHSCOPE_API_KEY", [EnvironmentVariableTarget]::User)
         [Environment]::SetEnvironmentVariable("OPENAI_BASE_URL", "https://dashscope.aliyuncs.com/compatible-mode/v1", [EnvironmentVariableTarget]::User)
         [Environment]::SetEnvironmentVariable("OPENAI_MODEL", "qwen3-coder-next", [EnvironmentVariableTarget]::User)
         ```

      2. 打开一个新的PowerShell窗口，运行以下命令，检查环境变量是否生效。















         ```powershell
         echo $env:OPENAI_API_KEY
         echo $env:OPENAI_BASE_URL
         echo $env:OPENAI_MODEL
         ```

### **向 Qwen Code 提问**

在对话框中输入“如何用python实现一个二叉搜索树？”Qwen Code 会进行规划，并申请创建文件、写入文件和执行文件等操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7165714671/p995289.png)

效果如下图所示：

![20251126192625](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3799654671/p1030857.jpg)

### **查看 Token 消耗**

输入`/stats model`查看本次启动 Qwen Code 后的 Token 消耗与 API 调用次数。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7165714671/p996213.png)

## **免费额度**

阿里云百炼对 Qwen3-Coder 等模型各提供各 100 万 Token 的免费额度（仅北京地域）。系统会优先消耗模型的免费额度，查询剩余额度请前往[模型广场](https://bailian.console.aliyun.com/?tab=model#/model-market)并单击模型卡片。为避免额外消费，可开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 按钮。

![用完即停](<Base64-Image-Removed>)

> 除了阿里云百炼的免费额度，Qwen Code 还提供了 [每天 2000 次的免费额度](https://help.aliyun.com/zh/model-studio/qwen-code#44be39e126jlw "")。

## **进阶操作**

更多 Qwen Code 的进阶功能或其他千问系列代码模型，可以参考 [Qwen Code 文档](https://qwenlm.github.io/qwen-code-docs/zh/)及阿里云百炼 [代码能力（Qwen-Coder）](https://help.aliyun.com/zh/model-studio/qwen-coder "")。

## 常见问题

### Q：Qwen Code **为什么 Token 消耗快？**

A：Qwen Code 可能多次调用 API，从而消耗大量 Token。请参考以下方法控制 Token 消耗：

- **精简工作目录**

建议在具体的项目目录下启动，启动目录（如根目录）中过多的文件会增加 Token 消耗。

- **设置 Token 限额**

在项目的根目录中创建 `.qwen/settings.json` 文件并重启 Qwen Code，通过`sessionTokenLimit`控制单次 API 调用的Token 使用量：















```json
{
    "sessionTokenLimit": 32000
}
```




> Qwen Code 可能多次调用 API，使得单个问题的 Token 消耗量大于`sessionTokenLimit`值。

- **使用压缩/清理指令**

输入以下命令可减少 Token 消耗：

  - `/compress`

    压缩对话历史，以便在 Token 限制内继续对话。

  - `/clear`

    清除所有对话历史并重新开始。

### **Q：如何切换模型？**

A：根据是否 [配置环境变量](https://help.aliyun.com/zh/model-studio/qwen-code#ec20c7b321sn5 "") 选择操作：

- **未配置环境变量**

1. 输入`/quit`退出 Qwen Code；

2. 输入 `qwen`启动，选择 OpenAI 认证方式，输入API Key、Base URL 与目标模型名称。
- **已配置环境变量**

1. 参见 [配置环境变量](https://help.aliyun.com/zh/model-studio/qwen-code#ec20c7b321sn5 "")，修改`OPENAI_MODEL`环境变量为目标模型并使其生效；

2. 输入`/quit`退出 Qwen Code，输入`qwen`启动即可。

### **Q：如何使用每天 2000 次的免费额度？**

A：启动 Qwen Code 后输入`/auth`，选择 **Qwen Oauth** 认证方式，单击 Enter 后通过 [Qwen Chat](https://chat.qwen.ai/) 认证方式接入。在跳转界面登录 Qwen Chat 账号，或扫描二维码进行验证，完成后即可每天免费调用 2000 次 coder 模型 API，该免费额度与阿里云百炼免费额度独立。

> 超过 2000 次 API 调用后如需继续使用，请通过`/auth` 切换为 OpenAI 认证方式。

> 若首次使用 Qwen Chat，请 **[**注册**](https://chat.qwen.ai/auth?action=signup)** 账号。

> 该认证方式无法切换模型，为了维持服务质量，可能会发生模型降级。

### **Q：为什么报** 401 Incorrect API key provided 错误？

A：可能是 API 配置错误，请对比错误信息中的API Key与设置是否一致。全局环境变量配置优先于环境文件配置。如果需要启用环境文件配置，请确保未设置相关环境变量，或临时清除它们。

更多问题请参见 [Qwen Code 故障排查文档](https://qwenlm.github.io/qwen-code-docs/zh/users/support/troubleshooting/)。