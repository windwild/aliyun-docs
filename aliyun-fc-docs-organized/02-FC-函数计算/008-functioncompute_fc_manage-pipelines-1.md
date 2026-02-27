### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[应用-即将下线](https://help.aliyun.com/zh/functioncompute/fc/operation-guide-application-coming-offline/)[流水线](https://help.aliyun.com/zh/functioncompute/fc/what-are-pipelines/)管理流水线

# 管理流水线

更新时间：2024-12-05 05:15:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：相关概念](https://help.aliyun.com/zh/functioncompute/fc/related-concepts)[下一篇：使用YAML文件描述流水线](https://help.aliyun.com/zh/functioncompute/fc/use-a-yaml-file-to-define-a-pipeline)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

流水线配置

流水线触发方式

流水线执行环境

资源描述YAML

钉钉机器人通知

流水线环境变量

流水线详情

平台托管

仓库读取

流程预览

任务模板

默认流水线流程

查看流水线执行历史

升级流水线构建环境运行时

流水线runtime-setup插件（推荐方式）

资源描述文件环境变量

Serverless应用中心提供可定制的流水线执行能力，支持用户通过配置流水线、编排任务流程，将代码发布至函数计算。本文介绍如何通过控制台管理流水线，包括流水线配置、流水线详情设置和查看流水线执行历史。

## 背景信息

创建应用时，平台会为应用创建默认环境，您可以为默认环境指定流水线Git事件触发方式，并进行相应的流水线配置。您可以选择自动配置和自定义配置两种配置方案。如果选择自动配置，平台会按照各配置项的默认值创建流水线。若选择自定义配置，您可以指定该环境的流水线Git事件触发方式，还可以选择流水线执行环境。Git信息、应用信息等将作为执行上下文传递到流水线中。

在编辑流水线配置项时，除了触发方式、执行环境外，您还可以对钉钉通知、资源描述YAML进行配置。

- 在创建应用或创建环境时配置流水线


在创建应用或创建环境时，可以为环境指定流水线的Git触发方式、执行环境。



![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0727668961/p733097.png)

- 在环境中编辑流水线


对已有的环境，在流水线管理页签，可以编辑环境的流水线Git事件触发方式、执行环境、钉钉通知、资源描述YAML。



![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0727668961/p733095.png)


## **流水线配置**

流水线配置主要包括流水线触发方式、流水线执行环境、资源描述YAML、钉钉机器人通知四个配置项，其中只有流水线触发方式、流水线执行环境可以在创建应用、创建环境阶段进行配置，这四项都可以在创建成功后单击编辑按钮配置。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0727668961/p733105.png)

### **流水线触发方式**

应用中心支持用户自定义触发流水线的Git事件。应用中心通过Webhook来接收Git事件，当接收到满足触发规则的事件时，将按照用户配置的流水线YAML创建并执行流水线。当前支持的触发方式如下：

- 分支触发：需要环境关联指定分支，匹配指定分支所有的Push事件。

- Tag触发：匹配指定Tag表达式的所有Tag创建事件。

- 分支合并触发：匹配指定来源分支到环境所关联的目标分支的Merge/Pull Request合并事件。


### **流水线执行环境**

**流水线执行环境** 分为 **默认执行环境** 和 **专有执行环境** 两种模式。

#### **默认执行环境**

**默认执行环境** 下，流水线的资源由平台完全托管，由阿里云函数计算为您承担流水线执行过程中的费用成本，您无需付出任何费用。流水线的每个任务都会运行在独立安全沙箱环境中，平台会保证您的流水线执行环境的安全隔离。默认执行环境的使用限制如下：

- 实例资源规格：4vCPU、8GB内存。

- 临时磁盘空间：10 GB。

- 任务执行超时：15分钟。

- 地域限制：模板直接部署、GitHub代码源使用海外新加坡地域，Gitee、公网GitLab、Codeup使用中国杭州地域。

- 网络限制：不支持固定IP地址以及网段，不支持IP白名单方式访问指定网站，不支持访问您的VPC内的资源。


#### **专有执行环境**

**专有执行环境** 会将流水线任务在用户的账号下执行，提供更多自定义的能力。应用中心会根据用户的授权完全代管专有执行环境的任务，实时在用户账户下调度函数计算实例运行流水线。和默认执行环境类似，专有执行环境提供完全Serverless化的能力，用户无需运维基础设施。

通过 **专有执行环境**，您可以使用如下自定义能力：

- 地域及网络：您可以指定执行环境的地域以及VPC，实现访问内网代码仓库、制品仓库、镜像仓库、Maven私服等场景。支持的地域请参见 [开服地域](https://help.aliyun.com/zh/functioncompute/fc/product-overview/supported-regions "")。

- 实例资源规格：您可以指定执行环境的CPU、内存规格。例如，指定更大规格的实例来加快构建速度。



**说明**





vCPU大小（单位为核）与内存大小（单位为GB）的比例必须设置在1:1到1:4之间。

- 持久化存储：您可以指定NAS挂载以及OSS挂载配置。例如通过NAS挂载来进行文件缓存，实现加速构建的效果。

- 日志：您可以指定SLS的日志项目和日志仓库，实现流水线执行日志的持久化。

- 超时时间：您可以自定义流水线任务的执行超时。默认为600秒，最长为86400秒。


**重要**

专有执行环境会让流水线任务在您自己的账号的函数计算下执行，因此会产生相关费用。具体操作，请参见 [计费概述](https://help.aliyun.com/zh/functioncompute/fc/product-overview/billing-overview-of-fc "")。

### **资源描述YAML**

Serverless应用中心和ServerlessDevs开发者工具进行了深度集成，你可以通过ServerlessDevs的资源描述文件来声明业务的资源配置。关于资源描述YAML的规范，请参见 [ServerlessDevs YAML规范](https://docs.serverless-devs.com/user-guide/aliyun/fc/yaml/readme/)。默认的资源描述文件名为s.yaml，您也可以指定其他文件名。指定资源描述文件后，在流水线中有两种使用方式：

- 当使用部署插件`@serverless-cd/s-deploy`时，插件执行时会自动使用指定的资源描述文件进行部署，执行的原理是在Serverless Devs的操作指令中增加`-t/--template`命令。下面的示例，指定的资源描述YAML文件为`demo.yaml`，插件执行的命令就是`s deploy -t demo.yaml`。


```yaml
- name: deploy
  context:
    data:
      deployFile: demo.yaml
      steps:
      - plugin: '@serverless-cd/s-setup'
      - plugin: '@serverless-cd/checkout'
      - plugin: '@serverless-cd/s-deploy'
  taskTemplate: serverless-runner-task
```

- 当使用脚本方式执行时，可以通过`${{ ctx.data.deployFile }}`来引用具体的资源描述文件名。例如下面的示例，效果是当指定了资源描述文件时就使用指定文件执行s plan命令，否则使用默认的s.yaml执行s plan命令。


```yaml
- name: pre-check
  context:
    data:
      steps:
      - run: s plan -t ${{ ctx.data.deployFile || s.yaml }}
      - run: echo "s plan finished."
  taskTemplate: serverless-runner-task
```

### **钉钉机器人通知**

开启该配置后，需要配置钉钉机器人的 **Webhook地址**、 **加签密钥**、通知规则以及 **自定义消息** 等。您可以在此集中管理需要通知的任务，也可以通过流水线YAML对各个任务分别开启通知。在此处完成通知的整体配置后，您也可以进一步在 **流水线详情** 中进行各个任务的通知细化配置。

## **流水线环境变量**

在 **流水线环境变量** 区域，点击 **编辑**，选择配置环境的方式，按照下方步骤完成配置，然后单击部署。

- 使用表单编辑（默认方式）

1. 单击 **+添加变量**。

2. 配置环境变量的键值对：

     - **变量**：自定义。

     - **值**：自定义。
- 使用JSON格式编辑

1. 单击 **使用JSON格式编辑**。

2. 在文本框内，输入对应的JSON格式的键值对，格式如下。















     ```json
     {
         "key": "value"
     }
     ```



     示例如下。















     ```json
     {
         "REGION": "MY_REGION",
         "LOG_PROJECT": "MY_LOG_PROJECT"
     }
     ```

当前环境变量会在Serverless Devs流水线中生效，可以通过`${env(key)}` 在s.yaml中引用，也可以通过` $Key`在Shell命令中引用，示例如下。

```yaml
vars:
  region: ${env(REGION)}
  service:
    name: demo-service-${env(prefix)}
    internetAccess: true
    logConfig:
      project: ${env(LOG_PROJECT)}
      logstore: fc-console-function-pre
    vpcConfig:
      securityGroupId: ${env(SG_ID)}
      vswitchIds:
        - ${env(VSWITCH_ID)}
      vpcId: ${env(VPC_ID)}
```

## **流水线详情**

在 **流水线详情** 区域，您可以配置流水线流程，对流水线中的任务、任务间的关系进行详细配置。平台会自动生成默认流水线流程，您可以基于该流程进行二次编辑。

流水线通过YAML进行管理，当前提供了 **平台托管** 和 **仓库读取** 两种配置方式：

**说明**

- 平台托管 **不支持** YAML预定义变量，具体请参见 [使用YAML文件描述流水线](https://help.aliyun.com/zh/functioncompute/fc/use-a-yaml-file-to-define-a-pipeline "")。

- 仓库托管支持YAML文件预定义变量。


### **平台托管**

流水线YAML默认由平台托管，即配置在平台中心化管理，更新后下次部署时生效。

### **仓库读取**

流水线的YAML描述文件存储在远端Git仓库，在控制台中编辑保存后平台会实时向您的Git仓库提交Commit，该提交不触发流水线的执行。当您的代码仓库事件触发流水线执行时，平台使用您指定的Git仓库中的流水线YAML创建流水线并执行。

您可以在 **流水线详情** 区域上方指定 **仓库读取**，输入YAML的文件名。如下图所示。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0727668961/p732673.png)

**流水线详情** 区域的主体由左侧的辅助工具区与右侧的YAML编辑区构成：

- YAML编辑区：您可以直接对流水线YAML进行编辑，来实现对流水线流程的修改，参考使用YAML文件描述流水线。

- 辅助工具区：提供了针对YAML编辑的辅助工具，包含：

  - **流程预览**：提供了对流水线流程的可视化预览与简单编辑能力。

  - **任务模板**：提供了一系列常用的任务YAML模板。

区域右上角有保存、全屏模式、重置三个按钮：

- 保存按钮会保存页面中对YAML的更改，并同步到流水线YAML中。

- 全屏模式按钮可以将主题编辑区域放大到全屏操作。

- 重置按钮则将取消从上次保存YAML之后的所有更改，退回初始状态。


**重要**

如果选择重置，在上次保存之后的所有更改都将丢失，请谨慎使用，做好备份。

### **流程预览**

**流程预览** 区域提供对流水线流程的可视化预览能力，并支持对任务基本内容、任务间关系的简单编辑，支持对模板任务的快捷创建添加。流程图节点主要分为三类，起始的代码源与触发方式节点、结束节点、任务节点。节点之间有表示 **依赖关系** 的连线连接。当鼠标移到任务节点上，会显示 **新建任务** 按钮和 **删除任务** 按钮，用于便捷地进行任务增删。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1658668961/p733121.png)

- **代码源与触发方式节点（开始节点）**

用于显示当前流水线 **代码源** 信息与 **触发方式**，此处只做显示不支持编辑。若要修改流水线触发方式，可以到 **流水线配置** 中进行修改。



**重要**





如果需要修改代码仓库，请在应用详情处进行修改。具体操作，请参见 [管理应用](https://help.aliyun.com/zh/functioncompute/fc/manage-applications-1 "")。修改代码仓库后，会涉及到所有流水线的失效，请谨慎操作。

- **结束节点**

标志流水线流程的终点，流水线中的任务至此全部完成。该节点只读不可编辑，无实际含义。

- **任务节点**

用于显示与维护指定任务的基本信息。任务节点默认显示任务名称，单击节点会弹出气泡框，用于查看和编辑 **任务名称**、 **前置任务**、是否 **开启任务** 等基本信息。如果选择不开启任务，则该任务会在执行时被自动跳过，并显示为灰色。

- **依赖关系**

反映任务之间关系的单向箭头。若箭头由任务A指向任务B，则代表A是B的前置任务，B依赖A，A被B依赖，B为依赖方，A为被依赖方。每个任务都可以被多个任务依赖，也可以依赖多个任务。

依赖关系可以通过编辑被依赖方的 **前置任务** 来进行更改。例如，想取消B对A的依赖，可以单击B的任务节点，将A从B的前置任务中移除。


- **新建任务**

该按钮表现为“＋”图标，分别存在于任务节点的上、下、右三个方位。单击任务A的上方新建任务按钮，会创建一个A的前置任务B，A依赖B；单击任务A的下方新建任务按钮，会创建一个A的后继任务C，C依赖A，A是C的前置任务；点击任务A的右侧新建任务按钮，会创建一个A的兄弟任务D，D具有和A相同的依赖关系，即D和A有相同的前置任务，且所有依赖A的任务也都依赖D。

- **删除任务**

该按钮表现为“×”图标，存在于任务节点右上角，用于删除被选中的任务。平台会进行二次确认避免误删除。


![image.png](<Base64-Image-Removed>)

### **任务模板**

**任务模板** 提供了一系列常用的流水线任务的YAML模板，包含 **代码检查**、 **构建**、 **部署**、 **通用** 等四种任务的YAML模板，任务内部的 **高级配置** YAML模板，以及 **任务插件** 的YAML模板。

您可以在模板列表中选择您所需要的模板，点击后可以查看模板的详细介绍和YAML内容，并将YAML内容复制粘贴到流水线YAML中的对应位置。

![image.png](<Base64-Image-Removed>)

### **默认流水线流程**

流水线的默认流程包含 **线上配置比对**、 **人工审核**、 **构建与部署** 三个任务，这三个任务依次执行。其中，人工审核默认不开启，需要手动开启。

- **线上配置比对**

判断流水线所涉及到的资源描述文件与线上配置内容是否一致，便于提前发现非预期的配置变化。

- **人工审核**

为确保应用的安全发布以及保障发布后的稳定，可以在此阶段开启人工审核机制，当流水线走到此处将被阻塞，并等待人工审核确认。只有人工审核通过后才能继续进行后续操作，否则将终止当前流水线。该任务默认不开启，需要手动开启。

- **构建与部署**

进行应用构建并将应用部署到云上，默认进行全量部署。


![image.png](<Base64-Image-Removed>)

## 查看流水线执行历史

在指定环境详情页面，选择 **流水线管理** 页签，然后在下方 **流水线执行历史** 区域，您可以查看指定流水线的历史执行记录。![pipeline-history](<Base64-Image-Removed>)

您可以点击具体的流水线执行版本，查看当前流水线历史的具体信息。通过此信息，可以快速地查看流水线的执行日志以及状态等，便于掌握流水线的执行情况或排查问题。

## 升级流水线构建环境运行时

当前默认流水线构建环境支持的运行时如下所示，内置的包管理工具包括Maven、PIP、NPM。目前仅支持操作系统为Debian 10的运行时环境。

| **运行时** | **支持版本** |
| --- | --- |

|     |     |
| --- | --- |
| **运行时** | **支持版本** |
| Node.js | - Node.js 12<br>  <br>- **Node.js 14：默认版本**<br>  <br>- Node.js 16<br>  <br>- Node.js 18<br>  <br>- Node.js 20 |
| Java | - **Java 8：默认版本**<br>  <br>- Java 11<br>  <br>- Java 17 |
| Python | - Python 2.7<br>  <br>- Python 3.6<br>  <br>- Python 3.7<br>  <br>- **Python 3.9：默认版本**<br>  <br>- Python 3.10 |
| Golang | - **Go 1.18：默认版本**<br>  <br>- Go 1.19<br>  <br>- Go 1.20<br>  <br>- Go 1.21 |
| PHP | - PHP 7.2 |
| .NET | - .NET 3.1 |

您可以使用 **流水线runtime-setup插件** 或者修改 **资源描述文件环境变量** 的方式来设置流水线运行时版本。

### **流水线runtime-setup插件（** 推荐方式 **）**

您可以通过 [函数计算控制台](https://fcnext.console.aliyun.com/)，找到应用，在 **流水线管理** 页签的 **流水线详情** 区域，选择设置Runtime任务插件模板，使用任务模板更新右侧流水线YAML。操作流程为 **任务模板**（下图中①）-> **任务插件**（下图中②）-> **设置Runtime**（下图中③）-> **更新右侧YAML**（下图中④）-> **保存**（下图中⑤）。

**说明**

建议您将runtime-setup插件放到第一个位置，以保证后面所有步骤执行都能生效。

![image.png](<Base64-Image-Removed>)

runtime-setup插件的详细参数请参见 [使用runtime-setup插件初始化运行环境](https://help.aliyun.com/zh/functioncompute/fc/use-the-runtime-setup-plug-in-to-initialize-the-runtime-environment-2 "")。

### **资源描述文件环境变量**

您也可以在资源描述文件中使用Action钩子来切换Node.js或Python的版本。具体说明如下。

- Node.js


  - export PATH=/usr/local/versions/node/v12.22.12/bin:$PATH

  - export PATH=/usr/local/versions/node/v16.15.0/bin:$PATH

  - export PATH=/usr/local/versions/node/v14.19.2/bin:$PATH

  - export PATH=/usr/local/versions/node/v18.14.2/bin:$PATH


示例如下。

```yaml
services:
  upgrade_runtime:
    component: 'fc'
    actions:
      pre-deploy:
        - run: export PATH=/usr/local/versions/node/v18.14.2/bin:$PATH && npm run build
    props:
...
```

- Python


  - export PATH=/usr/local/envs/py27/bin:$PATH

  - export PATH=/usr/local/envs/py36/bin:$PATH

  - export PATH=/usr/local/envs/py37/bin:$PATH

  - export PATH=/usr/local/envs/py39/bin:$PATH

  - export PATH=/usr/local/envs/py310/bin:$PATH


示例如下。

```yaml
services:
  upgrade_runtime:
    component: 'fc'
    actions:
      pre-deploy:
        - run: export PATH=/usr/local/envs/py310/bin:$PATH && pip3 install -r requirements.txt -t .
    props:
...
```