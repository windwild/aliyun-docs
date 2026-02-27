### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)OpenCode

# OpenCode

更新时间：2026-02-11 22:35:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenClaw（原 Clawdbot/Moltbot）](https://help.aliyun.com/zh/model-studio/openclaw)[下一篇：Postman](https://help.aliyun.com/zh/model-studio/first-call-to-image-and-video-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

安装 OpenCode

启动 OpenCode

连接模型服务

使用示例

OpenCode 是开源的 AI 编程工具，可配合阿里云百炼提供的模型推理服务实现高效代码开发。

**重要**

**本文档仅适用于按量付费模式**。如果您已订阅阿里云百炼 Coding Plan 并希望在 OpenCode 中使用，请参考 [Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。

## **前提条件**

已安装 Node.js 18 及以上版本。如未安装，请前往 [Node.js 官网](https://nodejs.org/) 下载安装。

运行以下命令可验证 Node.js 版本：

```bash
node -v
```

## **安装 OpenCode**

运行以下命令安装 OpenCode：

```bash
npm install -g opencode-ai
```

运行以下命令验证安装。若有版本号输出，则表示安装成功。

```bash
opencode -v
```

> 若安装失败，请检查 Node.js 版本是否为 18 及以上。可运行`node -v`查看当前版本。

## **启动 OpenCode**

进入您的项目目录后，运行以下命令启动 OpenCode：

```bash
cd your-project  # 进入项目目录
opencode
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3024270771/p1052257.png)

> OpenCode 会以当前目录作为项目上下文，请确保在正确的项目目录中启动。如果还没有项目目录，可以通过`mkdir my-project && cd my-project`创建并进入一个新目录。

## **连接模型服务**

1. 在输入框输入`/connect`并单击 Enter。

2. 在 Provider 列表的搜索框中输入`alibaba`进行搜索，选中`Alibaba (China)`并单击 Enter。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3024270771/p1052260.png)

3. 输入[中国内地地域的 API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/api-key) 后按 Enter。

4. 在模型列表中选择`Qwen3 Coder Plus`并单击 Enter。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3024270771/p1052261.png)


> 也可选择列表中的其他模型。


## **使用示例**

输入：

```plaintext
写一个 html 代码，模拟一个小球在匀速旋转的六边形内部弹跳的物理效果（包括重力、碰撞反作用力、摩擦力等）。球应该受到重力，在碰到六边形的内壁后会回弹，受到碰撞反作用力、摩擦力的影响。注意球的初始化位置在六边形内部的中心。
```

打开OpenCode写好的HTML文件可查看效果：

![钉钉录屏_2026-02-04 102045](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3024270771/p1052268.gif)