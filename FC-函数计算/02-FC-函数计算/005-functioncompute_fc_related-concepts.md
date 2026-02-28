### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[应用-即将下线](https://help.aliyun.com/zh/functioncompute/fc/operation-guide-application-coming-offline/)[流水线](https://help.aliyun.com/zh/functioncompute/fc/what-are-pipelines/)相关概念

# 相关概念

更新时间：2024-04-24 03:45:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景介绍

流水线

流水线模板

任务

任务模板

执行上下文

本文介绍流水线相关概念，包括流水线和流水线模板、任务和任务模板以及执行上下文。

## 背景介绍

应用中心提出了流水线和流水线模板的概念。流水线通过引用流水线模板，提供执行上下文，描述了一次流水线执行以及执行结果。而流水线模板通过描述任务，以及任务之间的依赖关系，描述了一个确定的流程。

应用中心提出了任务（Task）以及任务模板（TaskTemplate）的概念，用于描述流水线中某个具体任务以及它的执行。任务通过引用任务模板，提供执行上下文，描述了一次任务的执行以及执行结果。任务模板通过描述任务的执行方式以及预设上下文（可选），来描述一个任务会怎样执行。

任务以及任务模板的引入将任务执行的描述移出了流水线。应用中心期望通过引入任务以及任务模板的概念，简化流水线的描述负担，让用户像搭建积木一样搭建流水线。

## 流水线

流水线是一个流水线模板的一次具体的执行。例如，为一个代码仓库设置了触发规则，每一次Push事件需要运行一次构建发布行为，那么每次用户向代码仓库推送代码，应用中心就会创建一个流水线对象，用于记录这次执行以及执行结果与细节。如下图所示。

![pipeline-concept1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2209826861/p636685.png)

## 流水线模板

流水线模板是对一个确定的CI/CD场景的描述，例如构建发布。流水线模板通过描述任务，以及任务之间的依赖关系，来确定一个具体CI/CD场景的流程。流水线模板可以被重复使用。例如，构建部署场景，需要先基于代码仓库的代码，构建出一个产物，并在得到人工确认以后，将它发布到云产品中。如下图所示，可以总结出构建、审批和部署三个任务以及它们之间的依赖关系。![pipeline-concept2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2209826861/p636748.png)

## 任务

任务是流水线的主要组成，它描述了流水线中每一个独立任务的执行以及执行结果。一般情况下，用户不会单独运行一个任务，所有的任务都由流水线运行产生。例如，构建部署流水线执行完成后，会依次产生构建、审批和部署三个独立的任务，其中构建是一个独立的执行，负责根据代码仓库中的代码来构建目标产物。

任务支持文本化或结构化输出执行的结果，但如果产生了文件制品或镜像制品，需要在任务执行的过程中进行保存。

任务根据模板限制以及执行上下文输入，可以运行在阿里云沙箱环境中，也可以运行在用户当前账户下。

![pipeline-task-concept](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5965042861/p636925.png)

## 任务模板

任务模板通过描述任务的执行方式以及预设上下文（可选），来描述一个任务会怎样执行。为了降低用户使用门槛，应用中心预置了若干常用的任务模板，包括审批、部署、自定义执行等。用户也可以通过创建新的模板，来实现自定义的逻辑。任务模板可以大大简化流水线的描述复杂度。

## 执行上下文

执行上下文（Context）可以影响流水线与任务的具体行为，它是流水线与任务的输入。当满足条件的Git事件产生或主动触发流水线时，一个流水线对象将被创建，触发者将触发的上下文信息参数化，并传入执行上下文中。

在流水线执行时，会产生任务并执行。此时，执行引擎会将流水线的执行上下文（记作ctx\_pipeline）向流水线模板中预设的执行上下文（记作ctx\_pipelinetemplate）合并，产生新的执行上下文作为任务的执行上下文（记作ctx\_task）。任务在执行时，执行引擎又会将任务执行上下文与任务模板的执行上下文（记作ctx\_tasktemplate）合并，作为任务运行时的执行上下文（记作ctx）。

如果使用运算符`+`描述合并这一行为，那么，执行上下文ctx\_1向执行上下文ctx\_2合并可以记作`ctx_1+ctx_2`。上述合并逻辑可以描述为`ctx_task=ctx_pipeline+ctx_pipelinetemplate`与`ctx=ctx_task+ctx_tasktemplate`，也可以描述为`ctx=ctx_pipeline+ctx_pipelinetemplate+ctx_tasktemplate`。如下图所示。

![pipeline-template-task](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5965042861/p637609.png)

应用中心对合并这一行为有明确的定义，合并的对象为JSON对象，合并的实现标准为 [JSON Merge Patch](https://www.rfc-editor.org/rfc/rfc7386)。例如，ctx\_1+ctx\_2表示ctx\_1的数据拥有更高的优先级，会覆盖ctx\_2中的数据，并产生新的JSON对象。

另外，合并行为不满足交换律的特性，例如，`ctx_1+ctx_2`不等于`ctx_2+ctx_1`，`ctx_1+ctx_2`表示ctx\_1向ctx\_2合并，而`ctx_2+ctx_1`表示ctx\_2向ctx\_1合并。两者代表的行为和结果如下图所示。

![context-merge](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5965042861/p637665.png)

任务执行时，会将任务的执行上下文向模板预设的执行上下文合并，并作为最终的执行上下文。任务所在的节点会收到一个包含执行上下文的请求，并按照上下文执行相应的逻辑。

![pipeline-context-merge](<Base64-Image-Removed>)