### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[实践教程](https://help.aliyun.com/zh/tablestore/use-cases/)[AI生态](https://help.aliyun.com/zh/tablestore/use-cases/ai-ecosystem/)Agent Memory SDK

# Agent Memory SDK

更新时间：2026-01-06 07:39:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：AI生态](https://help.aliyun.com/zh/tablestore/use-cases/ai-ecosystem/)[下一篇：Tablestore MCP Server](https://help.aliyun.com/zh/tablestore/use-cases/tablestore-mcp-server)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

核心架构

快速接入

环境准备

安装SDK

配置环境变量

示例代码：Memory场景

创建会话和写入对话记录

查询历史会话列表

查询指定会话详情

查询指定会话完整对话记录

示例代码：Knowledge场景

创建知识库和写入知识

向量检索

全文检索

通用检索

相关文档

基于Tablestore的Agent Memory SDK框架，主要支持Memory和Knowledge场景，为AI Agent应用提供持久化、高性能的记忆存储和语义检索能力，帮助开发者快速构建具有上下文理解和长期记忆能力的智能应用。

## **核心架构**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2513077671/CAEQYxiBgMCSgZLw0hkiIDQxZGRjNGY3YTQxNDQwZjM4NWEyMzMwOTc0OGM5NThj5858155_20251106174202.684.svg)

#### **架构优势**

- **轻量化设计**：抽象通用存储接口，降低业务开发复杂度，在技术深度与易用性之间实现平衡。开发者无需直接处理底层数据库接口调用，专注于业务逻辑开发即可快速产出结果。

- **场景驱动设计**：针对Memory实时记忆存储和Knowledge长期语义检索两大核心场景，提供完整的解决方案。在满足基础存储需求的同时，集成摘要记录、事实数据提取、用户画像标签挖掘等业务场景功能，实现存储与应用的深度融合。

- **业务价值验证**：基于成熟的业界最佳实践，开发者无需进行复杂的技术调研，可直接在自有业务场景中快速验证和落地AI应用的商业价值。


## **快速接入**

以下通过Python示例演示SDK的完整接入和使用流程，Java接入方式请参考 [使用说明](https://github.com/aliyun/alibabacloud-tablestore-for-agent-memory/blob/main/java/README.md)。

### **环境准备**

确保已安装 [Python](http://www.python.org/) 运行环境，可通过`python3 --version`命令查看版本信息。

### **安装SDK**

```bash
pip3 install tablestore-for-agent-memory
```

### **配置环境变量**

设置以下必需的环境变量：

- `TABLESTORE_ACCESS_KEY_ID`：阿里云账号或RAM用户的 [AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "") ID。

- `TABLESTORE_ACCESS_KEY_SECRET`：阿里云账号或RAM用户的 [AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "") Secret。

- `TABLESTORE_INSTANCE_NAME`：实例名称，可在 [表格存储控制台](https://otsnext.console.aliyun.com/) 获取。

- `TABLESTORE_ENDPOINT`：实例访问地址，可在 [表格存储控制台](https://otsnext.console.aliyun.com/) 获取。


## **示例代码：Memory场景**

Memory场景主要用于管理AI Agent的会话记忆，包括会话管理和消息存储等核心功能。以下示例演示了如何创建会话、记录对话以及查询历史记录的完整流程。

### **创建会话和写入对话记录**

```python
import tablestore
from tablestore_for_agent_memory.base.common import MetaType, microseconds_timestamp
from tablestore_for_agent_memory.memory.memory_store import MemoryStore
from tablestore_for_agent_memory.base.base_memory_store import Session, Message
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    session_secondary_index_meta = {
        "meta_string": MetaType.STRING,
        "meta_long": MetaType.INTEGER,
        "meta_double": MetaType.DOUBLE,
        "meta_boolean": MetaType.BOOLEAN,
        "meta_bytes": MetaType.BINARY,
    }

    session_search_index_schema = [\
        tablestore.FieldSchema(\
            "title",\
            tablestore.FieldType.TEXT,\
            analyzer=tablestore.AnalyzerType.FUZZY,\
            analyzer_parameter=tablestore.FuzzyAnalyzerParameter(1, 4),\
        ),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    message_search_index_schema = [\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    memory_store = MemoryStore(
        tablestore_client=tablestore_client,
        session_secondary_index_meta=session_secondary_index_meta,
        session_search_index_schema=session_search_index_schema,
        message_search_index_schema=message_search_index_schema,
    )

    print("开始创建表和索引...")
    try:
        memory_store.init_table()
        memory_store.init_search_index()
        print("表和索引创建成功")
    except Exception as e:
        print(f"表和索引已存在或创建失败: {e}")

    print("\n====== 创建新会话 ======")

    session = Session(user_id="test_user_1", session_id="session_001")
    session.update_time = microseconds_timestamp()
    session.title = "表格存储咨询"
    session.metadata = {
        "meta_string": "web_source",
        "meta_long": 1,
        "meta_double": 1.0,
        "meta_boolean": True,
        "model_name": "qwen-max"
    }

    memory_store.put_session(session)
    print(f"创建会话成功: user_id={session.user_id}, session_id={session.session_id}")

    print("\n====== 第一轮对话 ======")

    message_1 = Message(
        session_id="session_001",
        message_id="msg_001",
        create_time=microseconds_timestamp()
    )
    message_1.content = "你好，请帮我介绍一下表格存储（Tablestore）是什么？"
    message_1.metadata = {
        "meta_string": "web",
        "message_type": "user",
        "meta_long": 1
    }
    memory_store.put_message(message_1)
    print(f"用户: {message_1.content}")

    session.update_time = microseconds_timestamp()
    memory_store.update_session(session)

    message_2 = Message(
        session_id="session_001",
        message_id="msg_002",
        create_time=microseconds_timestamp()
    )
    message_2.content = "表格存储（Tablestore）是阿里云自研的第一代飞天产品，提供海量结构化数据存储以及快速的查询和分析服务。它支持多种数据模型，包括宽表模型、IM消息模型、时序模型等，可以满足不同场景的数据存储需求。"
    message_2.metadata = {
        "message_type": "assistant",
        "model": "qwen-max"
    }
    memory_store.put_message(message_2)
    print(f"助手: {message_2.content}")

    print("\n====== 第二轮对话 ======")

    message_3 = Message(
        session_id="session_001",
        message_id="msg_003",
        create_time=microseconds_timestamp()
    )
    message_3.content = "表格存储有哪些典型的应用场景？"
    message_3.metadata = {
        "meta_string": "web",
        "message_type": "user",
        "meta_long": 2
    }
    memory_store.put_message(message_3)
    print(f"用户: {message_3.content}")

    session.update_time = microseconds_timestamp()
    memory_store.update_session(session)

    message_4 = Message(
        session_id="session_001",
        message_id="msg_004",
        create_time=microseconds_timestamp()
    )
    message_4.content = """表格存储的典型应用场景包括：
1. AI Agent 记忆存储：存储知识库、长期记忆、AI会话消息等信息
2. 元数据管理：存储海量文件、视频、图片的元信息
3. 消息数据：存储IM聊天消息、Feed流消息等
4. 轨迹溯源：车联网轨迹、物流轨迹等时序数据
5. 科学大数据：气象数据、基因数据等海量数据存储
6. 推荐系统：用户画像、物品特征等数据存储
7. 风控系统：实时风控规则、历史行为数据存储"""
    message_4.metadata = {
        "message_type": "assistant",
        "model": "qwen-max"
    }
    memory_store.put_message(message_4)
    print(f"助手: {message_4.content}")

    print("\n====== 会话创建和对话完成 ======")
    print(f"会话ID: {session.session_id}")
    print(f"用户ID: {session.user_id}")
    print(f"共完成 2 轮对话，4 条消息")

if __name__ == "__main__":
    main()
```

### 查询历史会话列表

```python
import tablestore
from tablestore_for_agent_memory.base.common import MetaType
from tablestore_for_agent_memory.memory.memory_store import MemoryStore
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    session_secondary_index_meta = {
        "meta_string": MetaType.STRING,
        "meta_long": MetaType.INTEGER,
        "meta_double": MetaType.DOUBLE,
        "meta_boolean": MetaType.BOOLEAN,
        "meta_bytes": MetaType.BINARY,
    }

    session_search_index_schema = [\
        tablestore.FieldSchema(\
            "title",\
            tablestore.FieldType.TEXT,\
            analyzer=tablestore.AnalyzerType.FUZZY,\
            analyzer_parameter=tablestore.FuzzyAnalyzerParameter(1, 4),\
        ),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    message_search_index_schema = [\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    memory_store = MemoryStore(
        tablestore_client=tablestore_client,
        session_secondary_index_meta=session_secondary_index_meta,
        session_search_index_schema=session_search_index_schema,
        message_search_index_schema=message_search_index_schema,
    )

    print("====== 查询历史会话列表 ======\n")

    user_id = "test_user_1"
    max_count = 10

    print(f"查询用户 {user_id} 的最近会话...")

    try:
        sessions = list(memory_store.list_recent_sessions(user_id=user_id, max_count=max_count))

        if not sessions:
            print(f"\n用户 {user_id} 暂无历史会话")
        else:
            print(f"\n共找到 {len(sessions)} 个会话:\n")

            for idx, session in enumerate(sessions, 1):
                print(f"会话 {idx}:")
                print(f"  - 会话ID: {session.session_id}")
                print(f"  - 用户ID: {session.user_id}")
                print(f"  - 更新时间: {session.update_time if hasattr(session, 'update_time') else '未知'}")

                if session.metadata:
                    print(f"  - 元数据:")
                    for key, value in session.metadata.items():
                        print(f"      {key}: {value}")
                print()

    except Exception as e:
        print(f"查询会话列表失败: {e}")

    print("====== 查询完成 ======")

if __name__ == "__main__":
    main()
```

### 查询指定会话详情

```python
import tablestore
from tablestore_for_agent_memory.base.common import MetaType
from tablestore_for_agent_memory.memory.memory_store import MemoryStore
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    session_secondary_index_meta = {
        "meta_string": MetaType.STRING,
        "meta_long": MetaType.INTEGER,
        "meta_double": MetaType.DOUBLE,
        "meta_boolean": MetaType.BOOLEAN,
        "meta_bytes": MetaType.BINARY,
    }

    session_search_index_schema = [\
        tablestore.FieldSchema(\
            "title",\
            tablestore.FieldType.TEXT,\
            analyzer=tablestore.AnalyzerType.FUZZY,\
            analyzer_parameter=tablestore.FuzzyAnalyzerParameter(1, 4),\
        ),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    message_search_index_schema = [\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    memory_store = MemoryStore(
        tablestore_client=tablestore_client,
        session_secondary_index_meta=session_secondary_index_meta,
        session_search_index_schema=session_search_index_schema,
        message_search_index_schema=message_search_index_schema,
    )

    print("====== 查询指定会话的详情 ======\n")

    user_id = "test_user_1"
    session_id = "session_001"

    print(f"查询会话详情...")
    print(f"用户ID: {user_id}")
    print(f"会话ID: {session_id}\n")

    try:
        session = memory_store.get_session(user_id=user_id, session_id=session_id)

        if session:
            print("会话详细信息:")
            print("=" * 50)
            print(f"用户ID: {session.user_id}")
            print(f"会话ID: {session.session_id}")
            print(f"更新时间: {session.update_time if hasattr(session, 'update_time') else '未知'}")

            if session.metadata:
                print("\n元数据信息:")
                print("-" * 50)
                for key, value in session.metadata.items():
                    print(f"  {key}: {value}")
            else:
                print("\n元数据: 无")

            print("=" * 50)
        else:
            print(f"未找到指定的会话 (user_id={user_id}, session_id={session_id})")

    except Exception as e:
        print(f"查询会话详情失败: {e}")
        import traceback
        traceback.print_exc()

    print("\n====== 查询完成 ======")

if __name__ == "__main__":
    main()
```

### 查询指定会话完整对话记录

```python
import tablestore
from tablestore_for_agent_memory.base.common import MetaType
from tablestore_for_agent_memory.memory.memory_store import MemoryStore
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    session_secondary_index_meta = {
        "meta_string": MetaType.STRING,
        "meta_long": MetaType.INTEGER,
        "meta_double": MetaType.DOUBLE,
        "meta_boolean": MetaType.BOOLEAN,
        "meta_bytes": MetaType.BINARY,
    }

    session_search_index_schema = [\
        tablestore.FieldSchema(\
            "title",\
            tablestore.FieldType.TEXT,\
            analyzer=tablestore.AnalyzerType.FUZZY,\
            analyzer_parameter=tablestore.FuzzyAnalyzerParameter(1, 4),\
        ),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    message_search_index_schema = [\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    memory_store = MemoryStore(
        tablestore_client=tablestore_client,
        session_secondary_index_meta=session_secondary_index_meta,
        session_search_index_schema=session_search_index_schema,
        message_search_index_schema=message_search_index_schema,
    )

    print("====== 查询指定会话的完整对话记录 ======\n")

    session_id = "session_001"

    print(f"查询会话对话记录...")
    print(f"会话ID: {session_id}\n")

    try:
        messages = list(memory_store.list_messages(session_id=session_id))

        if not messages:
            print(f"会话 {session_id} 暂无对话记录")
        else:
            messages.sort(key=lambda m: m.create_time)

            print(f"共找到 {len(messages)} 条消息\n")
            print("=" * 80)

            round_num = 0
            for idx, message in enumerate(messages):
                message_type = message.metadata.get("message_type", "unknown")

                if message_type == "user":
                    round_num += 1
                    print(f"\n第 {round_num} 轮对话:")
                    print("-" * 80)

                role = "用户" if message_type == "user" else "助手"
                print(f"\n[{role}] (消息ID: {message.message_id})")
                print(f"内容: {message.content}")
                print(f"创建时间: {message.create_time}")

                if message.metadata and len(message.metadata) > 1:
                    print("元数据:")
                    for key, value in message.metadata.items():
                        if key != "message_type":
                            print(f"  - {key}: {value}")

            print("\n" + "=" * 80)
            print(f"\n对话统计: 共 {round_num} 轮对话，{len(messages)} 条消息")

    except Exception as e:
        print(f"查询对话记录失败: {e}")
        import traceback
        traceback.print_exc()

    print("\n====== 查询完成 ======")

if __name__ == "__main__":
    main()
```

## **示例代码：Knowledge场景**

Knowledge场景专注于构建AI知识库，支持海量文档的向量化存储和智能检索。以下示例展示如何创建知识库、导入文档，并通过向量检索、全文检索等方式实现智能问答。

> 示例代码使用阿里云百炼的`text-embedding-v2`模型进行向量化，需要先安装相关依赖并将 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 配置为环境变量`OPENAI_API_KEY`。

```bash
pip3 install openai
```

### **创建知识库和写入知识**

数据写入后，多元索引需要几秒钟完成同步。若使用后续示例代码查询不到数据，需等待多元索引同步完成。

```python
import tablestore
from tablestore_for_agent_memory.knowledge.knowledge_store import KnowledgeStore
from tablestore_for_agent_memory.base.base_knowledge_store import Document
from openai import OpenAI
import os

class OpenAIEmbedding:
    def __init__(self, api_key, base_url=None, model="text-embedding-v2", dimension=1536):
        self.client = OpenAI(
            api_key=api_key,
            base_url=base_url
        )
        self.model = model
        self.dimension = dimension

    def embedding(self, text):
        try:
            response = self.client.embeddings.create(
                model=self.model,
                input=text
            )
            return response.data[0].embedding
        except Exception as e:
            print(f"Embedding 调用异常: {e}")
            return None

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')
    openai_api_key = os.getenv('OPENAI_API_KEY')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name,
        'OPENAI_API_KEY': openai_api_key
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    search_index_schema = [\
        tablestore.FieldSchema("user_id", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("category", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
    embedding_model = OpenAIEmbedding(
        api_key=openai_api_key,
        base_url=base_url,
        model="text-embedding-v2",
        dimension=1536
    )

    knowledge_store = KnowledgeStore(
        tablestore_client=tablestore_client,
        vector_dimension=1536,
        enable_multi_tenant=True,
        search_index_schema=search_index_schema,
    )

    print("开始创建表和索引...")
    try:
        knowledge_store.init_table()
        print("表和索引创建成功")
    except Exception as e:
        print(f"表和索引已存在或创建失败: {e}")

    print("\n====== 写入 Tablestore 知识库文档 ======\n")

    documents_data = [\
        {\
            "id": "doc_001",\
            "text": "表格存储（Tablestore）是阿里云自研的第一代飞天产品，提供海量结构化数据存储以及快速的查询和分析服务。表格存储的分布式存储和强大的索引引擎能够支持单表PB级存储、千万TPS以及毫秒级延迟的服务能力。",\
            "category": "产品介绍",\
            "meta_long": 1\
        },\
        {\
            "id": "doc_002",\
            "text": "表格存储支持宽表模型，单表支持PB级数据存储和千万QPS，适合存储用户画像、订单详情等场景。同时支持时序模型，可以高效存储和查询物联网设备、监控系统产生的时序数据。",\
            "category": "数据模型",\
            "meta_long": 2\
        },\
        {\
            "id": "doc_003",\
            "text": "表格存储提供多种索引类型：主键索引支持快速的点查询和范围查询；全局二级索引可以基于非主键列进行查询；多元索引支持复杂的查询条件组合和全文检索；向量检索支持 AI 场景的相似度搜索。",\
            "category": "索引功能",\
            "meta_long": 3\
        },\
        {\
            "id": "doc_004",\
            "text": "表格存储适用于多种场景：元数据管理可以存储海量文件、视频、图片的元信息；消息数据用于存储 IM 聊天消息、Feed 流消息；轨迹溯源存储车联网轨迹、物流轨迹等时序数据；推荐系统存储用户画像和物品特征。",\
            "category": "应用场景",\
            "meta_long": 4\
        },\
        {\
            "id": "doc_005",\
            "text": "表格存储的多元索引支持丰富的查询能力，包括精确查询、范围查询、前缀查询、通配符查询、全文检索、地理位置查询、嵌套查询等。同时支持排序、聚合、统计分析等高级功能。",\
            "category": "查询能力",\
            "meta_long": 5\
        },\
        {\
            "id": "doc_006",\
            "text": "表格存储提供 Agent Memory 能力，包括 Memory Store 用于存储会话和消息记录，Knowledge Store 用于存储知识库文档并支持向量检索。这些能力可以帮助构建智能问答、对话机器人等 AI 应用。",\
            "category": "AI 能力",\
            "meta_long": 6\
        },\
        {\
            "id": "doc_007",\
            "text": "表格存储的向量检索功能支持海量向量数据的存储和高效检索，可以应用于图像搜索、语义搜索、推荐系统等场景。支持 L2 距离、余弦相似度等多种相似度算法。",\
            "category": "向量检索",\
            "meta_long": 7\
        },\
        {\
            "id": "doc_008",\
            "text": "表格存储提供多种数据保护机制：支持数据备份和恢复；提供数据生命周期管理，可以自动过期和删除旧数据；支持数据加密存储，保障数据安全。",\
            "category": "数据保护",\
            "meta_long": 8\
        }\
    ]

    tenant_id = "user_tablestore_001"
    success_count = 0

    for doc_data in documents_data:
        try:
            document = Document(document_id=doc_data["id"], tenant_id=tenant_id)
            document.text = doc_data["text"]

            document.embedding = embedding_model.embedding(document.text)

            if document.embedding is None:
                print(f"✗ 生成向量失败，跳过文档 {doc_data['id']}")
                continue

            document.metadata["category"] = doc_data["category"]
            document.metadata["meta_long"] = doc_data["meta_long"]
            document.metadata["meta_boolean"] = True
            document.metadata["user_id"] = tenant_id

            knowledge_store.put_document(document)

            success_count += 1
            print(f"✓ 写入文档 {doc_data['id']}: {doc_data['category']}")
            print(f"  内容: {doc_data['text'][:60]}...")
            print()

        except Exception as e:
            print(f"✗ 写入文档 {doc_data['id']} 失败: {e}")

    print("=" * 80)
    print(f"\n写入完成: 成功 {success_count}/{len(documents_data)} 条文档")
    print(f"租户ID: {tenant_id}")
    print(f"文档类别: {', '.join(set([d['category'] for d in documents_data]))}")
    print("\n提示: 数据写入后，多元索引可能需要几秒钟时间完成同步")

if __name__ == "__main__":
    main()
```

### **向量检索**

```python
import tablestore
from tablestore_for_agent_memory.knowledge.knowledge_store import KnowledgeStore
from openai import OpenAI
import os

class OpenAIEmbedding:
    def __init__(self, api_key, base_url=None, model="text-embedding-v2", dimension=1536):
        self.client = OpenAI(
            api_key=api_key,
            base_url=base_url
        )
        self.model = model
        self.dimension = dimension

    def embedding(self, text):
        try:
            response = self.client.embeddings.create(
                model=self.model,
                input=text
            )
            return response.data[0].embedding
        except Exception as e:
            print(f"Embedding 调用异常: {e}")
            return None

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')
    openai_api_key = os.getenv('OPENAI_API_KEY')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name,
        'OPENAI_API_KEY': openai_api_key
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    search_index_schema = [\
        tablestore.FieldSchema("user_id", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("category", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
    embedding_model = OpenAIEmbedding(
        api_key=openai_api_key,
        base_url=base_url,
        model="text-embedding-v2",
        dimension=1536
    )

    knowledge_store = KnowledgeStore(
        tablestore_client=tablestore_client,
        vector_dimension=1536,
        enable_multi_tenant=True,
        search_index_schema=search_index_schema,
    )

    print("====== 向量检索测试 ======\n")

    query_text = "表格存储支持哪些索引类型？"
    tenant_id = "user_tablestore_001"

    print(f"查询问题: {query_text}")
    print(f"租户ID: {tenant_id}")
    print(f"返回结果数: Top 3\n")

    try:
        print("正在生成查询向量...")
        query_vector = embedding_model.embedding(query_text)

        if query_vector is None:
            print("生成查询向量失败")
        else:
            print(f"查询向量生成成功，维度: {len(query_vector)}\n")

            response = knowledge_store.vector_search(
                query_vector=query_vector,
                tenant_id=tenant_id,
                limit=3
            )

            if not response.hits:
                print("未找到相关文档")
            else:
                print("=" * 80)
                print(f"找到 {len(response.hits)} 个相关文档:\n")

                for idx, hit in enumerate(response.hits, 1):
                    doc = hit.document
                    score = hit.score

                    print(f"【结果 {idx}】")
                    print(f"文档ID: {doc.document_id}")
                    print(f"相似度分数: {score:.4f}")

                    if hasattr(doc, 'metadata') and 'category' in doc.metadata:
                        print(f"类别: {doc.metadata['category']}")

                    print(f"内容: {doc.text}")
                    print("-" * 80)

                print()

    except Exception as e:
        print(f"向量检索失败: {e}")
        import traceback
        traceback.print_exc()

    print("\n====== 检索完成 ======")

if __name__ == "__main__":
    main()
```

### **全文检索**

```python
import tablestore
from tablestore_for_agent_memory.knowledge.knowledge_store import KnowledgeStore, Filters
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    search_index_schema = [\
        tablestore.FieldSchema("user_id", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("category", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    knowledge_store = KnowledgeStore(
        tablestore_client=tablestore_client,
        vector_dimension=1536,
        enable_multi_tenant=True,
        search_index_schema=search_index_schema,
    )

    print("====== 全文检索测试 ======\n")

    query_keyword = "向量检索"
    tenant_id = "user_tablestore_001"

    print(f"查询关键词: {query_keyword}")
    print(f"租户ID: {tenant_id}")
    print(f"返回结果数: Top 3\n")

    try:
        response = knowledge_store.search_documents(
            tenant_id=tenant_id,
            metadata_filter=Filters.text_match("text", query_keyword),
            limit=3
        )

        if not response.hits:
            print("未找到包含关键词的文档")
        else:
            print("=" * 80)
            print(f"找到 {len(response.hits)} 个包含关键词的文档:\n")

            for idx, hit in enumerate(response.hits, 1):
                doc = hit.document
                score = hit.score

                print(f"【结果 {idx}】")
                print(f"文档ID: {doc.document_id}")
                print(f"匹配分数: {score if score is not None else 'N/A'}")

                if hasattr(doc, 'metadata') and 'category' in doc.metadata:
                    print(f"类别: {doc.metadata['category']}")

                content = doc.text
                if query_keyword in content:
                    highlighted = content.replace(query_keyword, f"【{query_keyword}】")
                    print(f"内容: {highlighted}")
                else:
                    print(f"内容: {content}")

                print("-" * 80)

            print()

    except Exception as e:
        print(f"全文检索失败: {e}")
        import traceback
        traceback.print_exc()

    print("\n====== 检索完成 ======")

    print("\n补充说明:")
    print("- 全文检索会在文档的 text 字段中搜索包含查询关键词的文档")
    print("- 可以使用通配符、短语查询等高级语法")
    print("- 支持中文分词和模糊匹配")

if __name__ == "__main__":
    main()
```

### **通用检索**

```python
import tablestore
from tablestore_for_agent_memory.knowledge.knowledge_store import KnowledgeStore, Filters
import os

def main():
    endpoint = os.getenv('TABLESTORE_ENDPOINT')
    access_key_id = os.getenv('TABLESTORE_ACCESS_KEY_ID')
    access_key_secret = os.getenv('TABLESTORE_ACCESS_KEY_SECRET')
    instance_name = os.getenv('TABLESTORE_INSTANCE_NAME')

    required_env_vars = {
        'TABLESTORE_ENDPOINT': endpoint,
        'TABLESTORE_ACCESS_KEY_ID': access_key_id,
        'TABLESTORE_ACCESS_KEY_SECRET': access_key_secret,
        'TABLESTORE_INSTANCE_NAME': instance_name
    }

    missing_vars = [var for var, value in required_env_vars.items() if not value]
    if missing_vars:
        print(f"错误: 缺少必需的环境变量: {', '.join(missing_vars)}")
        print("请设置以下环境变量:")
        for var in missing_vars:
            print(f"  export {var}=your_value")
        exit(1)

    tablestore_client = tablestore.OTSClient(
        endpoint,
        access_key_id,
        access_key_secret,
        instance_name,
        retry_policy=tablestore.WriteRetryPolicy(),
    )

    search_index_schema = [\
        tablestore.FieldSchema("user_id", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("category", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_string", tablestore.FieldType.KEYWORD),\
        tablestore.FieldSchema("meta_long", tablestore.FieldType.LONG),\
        tablestore.FieldSchema("meta_double", tablestore.FieldType.DOUBLE),\
        tablestore.FieldSchema("meta_boolean", tablestore.FieldType.BOOLEAN),\
    ]

    knowledge_store = KnowledgeStore(
        tablestore_client=tablestore_client,
        vector_dimension=1536,
        enable_multi_tenant=True,
        search_index_schema=search_index_schema,
    )

    print("====== 通用检索测试 ======\n")

    tenant_id = "user_tablestore_001"

    print("通用检索支持基于元数据的灵活过滤查询，不依赖向量或全文检索")
    print(f"租户ID: {tenant_id}")
    print(f"返回结果数: Top 3\n")

    print("【场景 1】查询类别为 '应用场景' 的文档")
    print("-" * 80)

    try:
        response = knowledge_store.search_documents(
            tenant_id=tenant_id,
            limit=3,
            metadata_filter=Filters.eq("category", "应用场景"),
            meta_data_to_get=["text", "category", "meta_long"]
        )

        if not response.hits:
            print("未找到匹配的文档\n")
        else:
            for idx, hit in enumerate(response.hits, 1):
                doc = hit.document
                print(f"\n结果 {idx}:")
                print(f"  文档ID: {doc.document_id}")
                print(f"  类别: {doc.metadata.get('category', 'N/A')}")
                print(f"  内容: {doc.text[:100]}...")
            print()

    except Exception as e:
        print(f"检索失败: {e}\n")

    print("\n【场景 2】查询 meta_long > 3 且 meta_boolean = True 的文档")
    print("-" * 80)

    try:
        response = knowledge_store.search_documents(
            tenant_id=tenant_id,
            limit=3,
            metadata_filter=Filters.logical_and([\
                Filters.gt("meta_long", 3),\
                Filters.eq("meta_boolean", True)\
            ]),
            meta_data_to_get=["text", "category", "meta_long"]
        )

        if not response.hits:
            print("未找到匹配的文档\n")
        else:
            for idx, hit in enumerate(response.hits, 1):
                doc = hit.document
                print(f"\n结果 {idx}:")
                print(f"  文档ID: {doc.document_id}")
                print(f"  类别: {doc.metadata.get('category', 'N/A')}")
                print(f"  meta_long: {doc.metadata.get('meta_long', 'N/A')}")
                print(f"  内容: {doc.text[:80]}...")
            print()

    except Exception as e:
        print(f"检索失败: {e}\n")

    print("\n【场景 3】查询 meta_long 在 2-5 之间的文档")
    print("-" * 80)

    try:
        response = knowledge_store.search_documents(
            tenant_id=tenant_id,
            limit=3,
            metadata_filter=Filters.logical_and([\
                Filters.gte("meta_long", 2),\
                Filters.lte("meta_long", 5)\
            ]),
            meta_data_to_get=["text", "category", "meta_long"]
        )

        if not response.hits:
            print("未找到匹配的文档\n")
        else:
            for idx, hit in enumerate(response.hits, 1):
                doc = hit.document
                print(f"\n结果 {idx}:")
                print(f"  文档ID: {doc.document_id}")
                print(f"  类别: {doc.metadata.get('category', 'N/A')}")
                print(f"  meta_long: {doc.metadata.get('meta_long', 'N/A')}")
                print(f"  内容: {doc.text[:80]}...")
            print()

    except Exception as e:
        print(f"检索失败: {e}\n")

    print("\n【场景 4】获取所有文档（不带过滤条件）")
    print("-" * 80)

    try:
        response = knowledge_store.search_documents(
            tenant_id=tenant_id,
            limit=3,
            meta_data_to_get=["text", "category", "meta_long"]
        )

        if not response.hits:
            print("未找到任何文档\n")
        else:
            print(f"\n共找到 {len(response.hits)} 个文档（显示前3个）:")
            for idx, hit in enumerate(response.hits, 1):
                doc = hit.document
                print(f"\n结果 {idx}:")
                print(f"  文档ID: {doc.document_id}")
                print(f"  类别: {doc.metadata.get('category', 'N/A')}")
                print(f"  内容: {doc.text[:60]}...")

            if response.next_token:
                print(f"\n还有更多结果，可使用 next_token 进行翻页查询")
            print()

    except Exception as e:
        print(f"检索失败: {e}\n")

    print("\n" + "=" * 80)
    print("\n====== 检索完成 ======")

    print("\n通用检索特点:")
    print("- 支持基于元数据字段的灵活过滤")
    print("- 支持精确匹配、范围查询、逻辑组合等")
    print("- 不需要向量或全文检索，适合结构化查询")
    print("- 可以指定返回的字段，减少数据传输量")

if __name__ == "__main__":
    main()
```

## **相关文档**

- 项目地址： [Tablestore for Agent Memory](https://github.com/aliyun/alibabacloud-tablestore-for-agent-memory)