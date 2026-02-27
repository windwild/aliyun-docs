### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 使用SGLang和vLLM部署Qwen系列模型的性能测试与评估

# 使用SGLang和vLLM部署Qwen系列模型的性能测试与评估

更新时间：2025-06-12 01:53:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

核心测试维度

测试环境与环境配置

核心压测结论

详细性能数据分析

本文介绍在函数计算的Function AI平台，使用SGLang和vLLM推理框架部署不同规格的Qwen家族大语言模型时的性能表现。通过对单GPU卡和多GPU卡部署方案进行全面的压力测试，对比SGLang与vLLM在关键性能指标（如首字延迟TTFT、每Token输出延迟TPOT、吞吐量Throughput）上的差异，评估多卡部署的性能提升效益。

## **核心测试维度**

- SGLang和vLLM推理框架性能对比

- 单卡和多卡部署性能对比


## **测试环境与环境配置**

本次性能评测基于阿里云函数计算Function AI的标准模型部署流程，具体环境和配置如下：

- **部署平台：** 阿里云函数计算 Function AI

- **测试模型：**

  - Qwen-QWQ-32B-AWQ

  - Qwen-QWQ-32B

  - Qwen2.5-1.5B-Instruct
- **推理框架及版本：**

  - SGLang: `v0.4.6.post2-cu124` (内置镜像)

  - vLLM: `v0.8.5` (内置镜像)
- **函数配置：**

  - 执行超时：6000 秒

  - 单实例并发度上限：10
- **存储配置：**

  - NAS文件系统：通用NAS-性能型

  - 初始带宽：600MB/s
- **实例类型：** 极速模式GPU实例的毫秒级快照，本次测试使用的GPU卡型为Ada系列

- **压测工具：** 魔搭开源工具 [evalscope](https://github.com/modelscope/evalscope)


## **核心压测结论**

基于本次全面的压力测试，可以得出以下结论：

- **推理性能指标 (TTFT/TPOT/Throughput)：** 在大部分测试场景下， **SGLang 表现优于 vLLM**。

- **框架启动耗时：** SGLang 启动速度较 vLLM **快约 30%**，但两者启动耗时均在分钟级别。

- **多卡性能提升：** 多卡（本文指双卡Tensor Parallelism并行）部署的性能提升幅度与模型算力需求正相关。模型越大，双卡带来的性能收益（ **20% ~ 50%**）越明显。

- **资源利用率：** SGLang 和 vLLM 在启动后，无论是单卡还是多卡环境，显存利用率均接近100%（模型参数 + KV Cache）。推理期间，SM利用率达到100%；空闲时，SM利用率为0%。

- **预估并发承载（以性能拐点为参考）：**

  - **Qwen-QWQ-32B-AWQ：** 建议最大并发数 ≤ 5。

    - 单卡吞吐量（tokens/s）：约 35

    - 双卡吞吐量（tokens/s）：约 50
  - **Qwen-QWQ-32B：** 建议最大并发数 ≤ 5。

    - 双卡吞吐量（tokens/s）：约 20（Ada单卡因显存不足无法运行）

## **详细性能数据分析**

Qwen2.5-1.5B-Instruct

Qwen-QWQ-32B-AWQ

Qwen-QWQ-32B

### **单卡性能对比（SGLang vs. vLLM）**

- **TTFT（首字延迟）与 TPOT（每Token输出延迟）:**

  - SGLang 相较于 vLLM 普遍优化 **20% ~ 50%**。
- **Throughput（吞吐量, tokens/s）:**

  - SGLang 相较于 vLLM 提升 **20% ~ 40%**。

### **双卡性能提升（对比各自单卡）**

- **TTFT 与 TPOT:**

  - SGLang: 双卡较单卡提升 **10% ~ 20%**。

  - vLLM: 双卡较单卡提升 **10% ~ 20%**。
- **Throughput (tokens/s):**

  - SGLang: 双卡较单卡提升约 **25%**。

  - vLLM: 双卡较单卡提升约 **15%**。

### **单卡性能对比（SGLang vs. vLLM）**

- **TTFT（首字延迟）:**

  - 并发度为 1 时：SGLang 优于 vLLM 约 **18%**。
- **TPOT（每Token输出延迟）:**

  - SGLang 优于 vLLM **10% ~ 15%**。
- **Throughput（吞吐量, tokens/s）:**

  - SGLang 优于 vLLM 约 **20%**。

### **双卡性能提升（对比各自单卡）**

- **TTFT（首字延迟）:** 随并发度上升，

  - SGLang: 双卡较单卡提升最高可达 **50%**。

  - vLLM: 双卡较单卡提升最高可达 **25%**。
- **TPOT（每Token输出延迟）:**

  - SGLang: 双卡较单卡提升约 **50%**。

  - vLLM: 双卡较单卡提升约 **50%**。
- **Throughput（吞吐量, tokens/s）:**

  - SGLang: 双卡较单卡提升约 **50%**。

  - vLLM: 双卡较单卡提升约 **50%**。

### **单卡性能**

Qwen-QWQ-32B模型权重所需显存超过单张Ada系列GPU卡型的可用显存。因此，该模型无法在Ada系列GPU单卡成功运行，测试中出现CUDA out of memory错误。

### **双卡性能对比（SGLang vs. vLLM）**

- **TTFT（首字延迟）:**

  - SGLang 优于 vLLM **15% ~ 50%**。
- **TPOT（每Token输出延迟）:**

  - SGLang 优于 vLLM 约 **10%**。
- **Throughput（吞吐量, tokens/s）:**

  - SGLang 优于 vLLM 约 **10%**。