# 阿里云产品文档集合

**医疗AI项目完整技术栈文档库** - 专为医疗AI项目收集整理的阿里云产品官方文档

## 📚 文档概览

- **产品数量**: 10 个核心产品
- **文档总数**: 875 个
- **抓取日期**: 2026-02-27
- **仓库地址**: https://github.com/windwild/aliyun-docs

## 🏥 医疗AI产品列表

### 核心AI能力

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**Model-Studio-百炼**](./Model-Studio-百炼/) | 372 | 大模型服务、通义千问、AI应用开发 |
| [**FC-函数计算**](./FC-函数计算/) | 101 | AI推理、AgentRun、Serverless计算 |
| [**DashVector-向量检索服务**](./DashVector-向量检索服务/) | 3 | 医学文献向量检索、RAG知识库 |

### 搜索与检索

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**OpenSearch-智能搜索**](./OpenSearch-智能搜索/) | 77 | 医学文档全文搜索、知识库检索 |
| [**Elasticsearch**](./Elasticsearch/) | 4 | 医学数据分析、搜索引擎 |

### 智能识别

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**OCR-文字识别**](./OCR-文字识别/) | 86 | 病历识别、化验单识别、处方识别 |

### 数据存储

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**OSS-对象存储**](./OSS-对象存储/) | 133 | 医学电子书、影像、模型文件存储 |
| [**RDS-PostgreSQL**](./RDS-PostgreSQL/) | 5 | 用户数据、病例结构化数据 |

### 应用部署

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**SAE-Serverless应用引擎**](./SAE-Serverless应用引擎/) | 88 | Taro小程序后端部署、API服务 |

### 安全合规

| 产品 | 文档数 | 用途 |
|------|--------|------|
| [**GREEN-内容安全**](./GREEN-内容安全/) | 6 | 医疗内容审核、敏感词过滤 |

## 🚀 快速开始

### 克隆仓库

```bash
git clone https://github.com/windwild/aliyun-docs.git
cd aliyun-docs
```

### 查看文档

```bash
# 查看所有产品
ls -d */

# 搜索特定主题
grep -r "RAG" --include="*.md" .
grep -r "病历识别" --include="*.md" .
```

## 📊 产品能力矩阵

### 医疗AI技术栈完整覆盖

```
┌─────────────────────────────────────────────┐
│          医疗AI完整技术栈                     │
├─────────────────────────────────────────────┤
│                                             │
│  AI模型层                                    │
│  ├─ Model Studio (372) - 大模型服务          │
│  ├─ FC (101) - AI推理 + AgentRun            │
│  └─ DashVector (3) - 向量检索/RAG           │
│                                             │
│  搜索检索层                                   │
│  ├─ OpenSearch (77) - 全文搜索              │
│  └─ Elasticsearch (4) - 数据分析            │
│                                             │
│  智能识别层                                   │
│  └─ OCR (86) - 病历/化验单识别               │
│                                             │
│  数据存储层                                   │
│  ├─ OSS (133) - 对象存储                    │
│  └─ RDS PostgreSQL (5) - 关系数据库         │
│                                             │
│  应用部署层                                   │
│  └─ SAE (88) - Serverless应用引擎           │
│                                             │
│  安全合规层                                   │
│  └─ GREEN (6) - 内容安全审核                 │
│                                             │
└─────────────────────────────────────────────┘
```

### 医疗AI应用场景

| 场景 | 核心产品 | 支持产品 |
|------|----------|----------|
| **智能问诊** | Model Studio + FC | DashVector + OpenSearch |
| **病历识别** | OCR | OSS + FC |
| **医学知识库** | DashVector + OpenSearch | Model Studio + OSS |
| **医患对话** | Model Studio + FC | GREEN + SAE |
| **医学影像** | OSS + FC | Model Studio |
| **合规审核** | GREEN | FC + SAE |

## 🎯 典型架构示例

### 医疗AI问答系统

```
用户提问 → SAE (小程序)
    ↓
FC (API网关) → Model Studio (通义千问)
    ↓
DashVector (向量检索) ← OSS (医学文献)
    ↓
OpenSearch (补充检索)
    ↓
GREEN (内容审核)
    ↓
返回答案 → 用户
```

### 病历智能识别系统

```
患者上传 → SAE (小程序)
    ↓
OSS (存储病历图片)
    ↓
OCR (文字识别)
    ↓
Model Studio (结构化提取)
    ↓
RDS PostgreSQL (存储数据)
    ↓
GREEN (隐私审核)
    ↓
返回结果 → 医生
```

## 📖 详细文档

- [产品详细说明](./PRODUCTS-README.md) - 各产品的详细用途和分类
- [函数计算 FC](./FC-函数计算/) - Serverless AI推理
- [Model Studio](./Model-Studio-百炼/) - 大模型服务
- [其他产品](./) - 查看各产品目录

## ⚠️ 免责声明

- 本仓库仅供学习和参考使用
- 文档版权归原作者及阿里云所有
- 如需最新官方文档，请访问：https://help.aliyun.com/

## 📄 License

本文档集合仅供学习参考，版权归阿里云所有。

---

**维护者**: windwild
**最后更新**: 2026-02-27
**抓取工具**: Firecrawl + Claude Code
