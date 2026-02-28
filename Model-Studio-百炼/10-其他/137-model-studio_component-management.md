### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Assistant API](https://help.aliyun.com/zh/model-studio/assistant-api/)最佳实践

# Assistant API 最佳实践

更新时间：2026-02-11 02:20:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：工具调用-代码解释器](https://help.aliyun.com/zh/model-studio/code-interpreter)[下一篇：权限管理](https://help.aliyun.com/zh/model-studio/application-permission-management-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

1\. 什么是核心组件

2\. 为什么要使用这些组件

2.1 Assistant

2.2 Thread

2.3 Message

2.4 Run

2.5 Step

2.6 总结

3\. 生命周期、数据存储与删除策略

3.1 DashScope 服务器端存储

3.2 删除机制

3.3 本地数据库存储（可选）

4\. 生产环境实践

4.1 并发与多用户管理

4.2 负载均衡与扩容策略

4.3 安全与权限控制

4.4 业务空间（workspace）管理

5\. 参考示例：构建一个简易聊天机器人

6\. 常见问题 (FAQ)

7\. 总结

为了帮助您在生产环境中更有效地使用 Assistant API 开发大模型应用，您需要掌握 Assistant、Thread、Message、Run、Step 等组件的基本操作，并深入了解生命周期、数据存储、业务空间、高并发等进阶主题。

## 1\. 什么是核心组件

在使用 Assistant API 构建对话式应用时，一般需要管理以下几种核心对象：

- **Assistant**：大模型对话应用的“主体”，包括所使用的语言模型（model）、系统指令（instructions）、工具（tools）、名称（name）等。

- **Thread**：独立的对话上下文容器。所有与该对话相关的消息与调用都属于同一个 `Thread`。

- **Message**：对话中的单条消息，包含角色（`role`）、内容（`content`）、元数据（`metadata`）等。

- **Run**：一次具体的模型调用请求。当您让 Assistant 生成回复时，就会触发一个 `Run`。

- **Step**：一次 `Run` 中更细粒度的执行步骤（如先检索资料，再生成答案；或多次外部工具调用等）。


**对象间关系示意：**

```plaintext
Assistant
 ┣─ (manages multiple) Thread
      ┣─ (has many) Message
      ┗─ (has many) Run
            ┗─ (has multiple) Step
```

这些对象在阿里云百炼服务器端保存，都有唯一的 `id`。您可以使用它们各自的 `retrieve`（或 `get`）方法检索，或使用 `delete` 方法删除。

* * *

## 2\. 为什么要使用这些组件

Assistant API 在对话式应用开发中提供了五个核心组件：`Assistant`、`Thread`、`Message`、`Run`、`Step`。这些组件既相互独立，又能在应用层面紧密配合，实现从全局配置到多用户多轮对话管理的完整功能链。下面我们将从“功能定位”和“常见使用场景”两个维度对各组件进行介绍。

* * *

### 2.1 Assistant

**功能定位：**

- `Assistant` 是管理模型配置和对话策略的核心对象，决定了对话的整体“人格”、目标以及使用的工具或知识库。

- 你可以把它视为“对话机器人的大脑”，里面存放了基础模型、辅助指令（instructions）、可调用的外部工具（tools）列表，以及一些通用的元数据（metadata）。


**常见使用场景：**

1. **角色设定与系统指令**：在某些场景中，你会给助手注入特定的角色或指令（例如“你是一位编程专家”），让其对话风格或侧重点与普通模式区分开来。

2. **工具与知识库整合**：对话需要外部信息支持（如插件、数据库检索等）时，可在 `Assistant` 的配置中定义可用的工具，进而在对话流程中自动调度。

3. **多模型或多版本管理**：当需要在不同情境下使用不同模型（例如，千问-Plus、千问-Max）时，可创建多个 `Assistant` 对象来分而治之。


* * *

### 2.2 Thread

**功能定位：**

- `Thread` 代表独立的对话上下文或会话实例，所有与该会话相关的消息和应用调用都会归属于此线程。

- 可将其理解为某个用户与助手之间的“聊天频道”，或是一个工作流上下文容器。


**常见使用场景：**

1. **多用户多会话管理**：在实际应用中，往往有多个并发用户同时交互。通过为每位用户或每个会话创建独立的 `Thread`，可以有效隔离彼此的对话上下文。

2. **保持对话历史**：`Thread` 保存了与之相关的所有 `Message` 及 `Run` 记录，使得后续可以在同一上下文中继续交流或审计历史。

3. **工作流上下文**：对于需要在多步操作或长流程中保持状态的业务场景，`Thread` 提供了上下文载体，避免中途丢失信息。


* * *

### 2.3 Message

**功能定位：**

- `Message` 是对话过程中的单条的消息实体，记录了消息发送者（`role` ）、内容（`content`）以及相关的元数据（如时间戳、过滤标记等）。

- 在业务层看来，`Message` 就像一条聊天记录；在系统内部，它也是构建 Prompt 或上下文的重要信息源。


**常见使用场景：**

1. **用户与系统的输入输出**：每次用户输入一句话，或助手生成一段回复时，都会创建新的 `Message`。

2. **对话流可视化**：前端需要展示对话历史时，可直接基于 `Message` 进行列表或气泡式渲染。

3. **数据过滤和标记**：在业务流程中，可能需要对输入内容进行敏感词检测、纠错、分词分析等。可以将处理结果或标记存放在 `Message` 的元数据中，方便后续审计和处理。


* * *

### 2.4 Run

**功能定位：**

- `Run` 指的是一次针对大语言模型或其他推理服务的调用过程。每当你让助手生成回复或进行推理，就会产生一个新 `Run`。

- `Run` 通常包含了输入 Prompt、输出结果、以及执行状态与耗时等元信息。


**常见使用场景：**

1. **推理过程跟踪**：在调试或监控中，你可以通过查看每个 `Run` 的输入输出，了解模型的响应质量、运行时长以及可能的错误信息。

2. **计费或统计需求**：如果底层模型按调用次数或 Token 用量计费，可以在 `Run` 中附加成本统计字段，用于后续结算或报表分析。

3. **多轮对话分步管理**：尽管一个 `Thread` 可能会有多次对话往返，每次模型调用都可以独立记录为一个 `Run`，便于追踪和溯源。


* * *

### 2.5 Step

**功能定位：**

- `Step` 是更细粒度的执行环节，用于在一次 `Run` 内部拆分多个阶段或调用过程，尤其适合复杂场景（如多次外部检索、插件调用、链式推理等）。

- 可以把 `Step` 理解为“子任务”或“中间过程”，帮助开发者或运维人员对模型在一次生成 / 推理过程中的行为进行深度观测。


**常见使用场景：**

1. **复杂工具链调用**：在一些场景下，模型会先调用外部插件，再拿结果进行二次分析，然后生成消息；每次消息生成或外部调用都可视为一个 `Step`。

2. **问题排查和可视化**：当出现模型回答缓慢或结果异常时，开发者可查看各个 `Step` 的执行时间和输出情况，快速定位卡点或失败环节。

3. **可选的详细日志**：在生产环境，为了节省存储，可能只记录 `Run` 级信息。但在测试环境或需要深度审计的应用中，可以启用 `Step` 记录来获得更细致的运行过程日志。


* * *

### 2.6 总结

- **Assistant** 决定了“对话能力”和“工具资源”。

- **Thread** 确定了“对话对象和上下文”以及对话生命周期。

- **Message** 为每一轮具体的对话内容做记录。

- **Run** 代表一次实际调用，衡量或审计模型在对话中的工作表现。

- **Step** 可以进一步细化多步骤推理或外部调用，助力开发者在复杂场景中进行可视化和问题排查。


从功能性上看，这五类组件相互协作，共同体现了 Assistant API 在对话管理上的易用性与可扩展性，让您能够自定义和追踪对话流程。在接下来的章节中，我们将进一步讨论它们在 **生命周期管理**、 **数据存储**、 **并发与多用户** 等方面的实践要点。如需调用细节或 API 示例，请参阅 [Assistant API 开发参考](https://help.aliyun.com/zh/model-studio/assistantapi/ "")。

* * *

## 3\. 生命周期、数据存储与删除策略

### 3.1 DashScope 服务器端存储

- 当您调用 `Assistants.create` / `Threads.create` / `Messages.create` 等方法时，DashScope 都会在服务器端创建对应的记录并返回对象实例（包含 `id`）。

- 目前 **暂无过期时间**，后续可能会设置过期时间。


### 3.2 删除机制

- **删除**`Assistant`
通过 `Assistants.delete(assistant_id)`：会删除这个 Assistant 及其关联的资源。需要格外谨慎。

- **删除**`Thread`
通过 `Threads.delete(thread_id)`：会级联删除该会话下所有 `Message`、`Run`、`Step` 记录。

- **单条消息 / 单次 Run / 单个 Step**
目前 DashScope 默认不支持单独删除，只能通过上层对象删除整条会话或整条 Assistant 的方式进行级联清理。


### 3.3 本地数据库存储（可选）

在某些业务场景下，您可能需要将 DashScope 端的对话数据（`Thread`、`Message` 等）在本地数据库中进行二次存储，以满足 **长期历史留存**、 **数据挖掘**、 **统计分析** 或 **消息回放** 的需求。同时，为了避免数据库无限增长或堆积大量过期数据，也常会引入 TTL（Time to Live，存活时间）策略，对不再需要的会话进行清理或归档。

以下示例展示了如何在创建 / 更新 `Thread` 时，将关键信息保存到本地数据库，以及如何结合定时任务清理过期的本地数据并同步删除 DashScope 服务器端的资源。

#### **3.3.1 在创建 Thread 时进行本地存储**

假设您使用 **SQLite** 或 **PostgreSQL** 来存储对话数据，这里以伪代码形式展示关键逻辑：

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
import sqlite3
from dashscope import Threads

# 假设您已经初始化了 SQLite 数据库，并有一个表 threads(thread_id TEXT PRIMARY KEY, user_id TEXT, created_at TIMESTAMP, last_active TIMESTAMP, metadata TEXT)

def create_thread_in_db(user_id: str) -> str:
    """
    1. 创建DashScope Thread
    2. 将thread_id与user_id等信息写入本地数据库
    3. 返回新的thread_id
    """
    # 1. 在DashScope上创建
    thread = Threads.create(metadata={"created_by": user_id})

    # 2. 保存到本地数据库
    conn = sqlite3.connect("app.db")
    cursor = conn.cursor()
    cursor.execute(
        "INSERT INTO threads (thread_id, user_id, created_at, last_active, metadata) VALUES (?, ?, datetime('now'), datetime('now'), ?)",
        (thread.id, user_id, str(thread.metadata))
    )
    conn.commit()
    conn.close()

    return thread.id

def update_thread_activity(thread_id: str):
    """
    每当有消息进来时，更新本地数据库里该thread的last_active
    """
    conn = sqlite3.connect("app.db")
    cursor = conn.cursor()
    cursor.execute(
        "UPDATE threads SET last_active = datetime('now') WHERE thread_id = ?",
        (thread_id, )
    )
    conn.commit()
    conn.close()
```

- 当用户启动一个新对话，调用 `create_thread_in_db()` 获取 `thread_id`；

- 后续有消息到来时，可调用 `update_thread_activity()` 更新活跃时间，为后面做过期判断提供依据。


#### **3.3.2 清理过期对话并在 DashScope 服务端同步删除**

假设您的业务需求是： **只保留最近 7 天内活跃过的对话**，超过 7 天不活跃的对话视为过期，需要删除。下面示例演示一个 **定时任务**（可用 Celery、cron job 等）扫描本地数据库，并删除过期记录及其在 DashScope 服务器上的资源。

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
import datetime
import sqlite3
from dashscope import Threads

def cleanup_expired_threads(days: int = 7):
    """
    删除本地数据库内超过指定天数未活跃的Thread，并在DashScope端同步删除
    """
    cutoff_time = datetime.datetime.utcnow() - datetime.timedelta(days=days)

    conn = sqlite3.connect("app.db")
    cursor = conn.cursor()
    cursor.execute(
        "SELECT thread_id FROM threads WHERE last_active < ?",
        (cutoff_time.strftime("%Y-%m-%d %H:%M:%S"),)
    )

    expired_threads = cursor.fetchall()

    for (thread_id,) in expired_threads:
        try:
            # 先删除DashScope端的Thread
            Threads.delete(thread_id)
        except Exception as e:
            print(f"Error deleting thread {thread_id} from DashScope: {e}")

        # 然后删除本地数据库记录
        cursor.execute("DELETE FROM threads WHERE thread_id = ?", (thread_id,))

    conn.commit()
    conn.close()

# 您可以将该函数通过调度器在每天凌晨跑一次：
# 0 0 * * * /path/to/python your_script.py
```

这样，在本地数据库和 DashScope 服务端都能保持数据一致，确保 **不会长期存留无用的历史**，也 **减少了数据泄露或存储资源浪费** 的风险。

* * *

## 4\. 生产环境实践

在实际生产环境中，DashScope 的 Assistant API 通常需要应对多用户并发、高可用需求、工作空间隔离以及安全审计等一系列挑战。下文将从并发与多用户管理、负载均衡与扩容策略、安全与权限控制、业务空间（workspace）管理四个方面展开介绍。

* * *

### 4.1 并发与多用户管理

许多对话式应用都需要面向多用户提供实时交互服务，因此在 **并发环境** 下如何管理 `Assistant`、`Thread`、`Message` 等对象显得尤为重要。

在一些场景下，您可能希望不同用户（或不同业务租户）使用 **独立的 Assistant** 配置（各自的模型、系统指令、工具集等），以进一步强化安全和隔离。下面是一个简化示例：

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
def get_assistant_for_user(user_id: str):
    """
    根据user_id检索/创建专属Assistant。适用于多租户场景。
    """
    # 从本地数据库查找是否已有assistant_id
    record = get_assistant_record_by_user(user_id)
    if record:
        return record.assistant_id

    # 若无则创建一个
    user_assistant = Assistants.create(
        model="qwen-plus",
        instructions=f"You are personal assistant for {user_id}.",
        metadata={"owner": user_id}
    )
    save_assistant_to_db(user_id, user_assistant.id)
    return user_assistant.id

def user_send_message(user_id: str, content: str):
    # 获取用户专属Assistant
    assistant_id = get_assistant_for_user(user_id)
    # 根据assistant创建thread或检索现有thread...
    # 省略具体实现
```

在 **并发** 场景下，每个用户各自的 Assistant 互不影响，极大地降低了上下文和配置冲突的风险。当然，这会带来对 **Assistant 对象数量** 和 **数据存储** 的额外管理要求，需要在数据库及 DashScope 端做统一规划。

* * *

### 4.2 负载均衡与扩容策略

在并发需求不断增长时，为了保证 DashScope Assistant API 的稳定性和响应速度，通常需要设计 **负载均衡（Load Balancing）** 和 **扩容（Scaling）** 策略。以下是几种常见方式与示例：

#### 4.2.1 多实例服务 + 负载均衡

如果您的应用部署在云上，可通过 **负载均衡器** 将用户请求分发到多个后端实例。每个实例都可运行一套 DashScope SDK 逻辑，与 DashScope 服务器进行交互。

- **优点**：简单易行、弹性扩容；

- **缺点**：如果应用内部有本地内存缓存，会话状态需要做跨实例共享（可借助 Redis / Memcached）。


```bash
# 示例代码仅供参考，请勿直接在生产环境中使用
# 示例：NGINX负载均衡配置片段
upstream dashscope_app_cluster {
    server 192.168.1.10:8000;
    server 192.168.1.11:8000;
}
server {
    listen 80;
    location / {
        proxy_pass http://dashscope_app_cluster;
    }
}
```

在后端应用层，您可以运行多个 `gunicorn` 或 `uvicorn` 进程，每个进程都加载 DashScope SDK，并处理部分请求。

#### 4.2.2 任务排队与异步处理

对于可能触发大模型高负载或长时任务的场景，可以引入 **消息队列**（如 RabbitMQ、Kafka）或 **异步任务执行器**（如 Celery）将用户请求排队或分发给工作进程。此举可以防止瞬时高并发导致服务崩溃，也能提高系统的可观察性和容错率。

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
# Celery 伪代码示例
from celery import Celery
from dashscope.threads import Runs

celery_app = Celery('tasks', broker='redis://localhost:6379/0')

@celery_app.task
def process_run(thread_id, assistant_id):
    run = Runs.create(thread_id=thread_id, assistant_id=assistant_id)
    final_run = Runs.wait(run.id, thread_id=thread_id, timeout_seconds=60)
    return final_run.id
```

#### 4.2.3 水平扩容 vs 垂直扩容

- **水平扩容（Scale Out）**：增加更多应用实例或容器节点，每个节点都可以调用 DashScope API；

- **垂直扩容（Scale Up）**：升级服务器配置（CPU、内存、带宽），单机支持更多并发请求。


在现代云原生环境中，更常见的是 **水平扩容**。配合容器编排（如 Kubernetes）或自动伸缩（Auto Scaling），可在请求量高峰时自动增加副本数，并在低峰时收缩，节省成本。

* * *

### 4.3 安全与权限控制

在多用户、多租户、生产环境使用 DashScope 时，安全合规是不可忽视的重要环节。以下从 **数据传输与存储**、 **API Key 与访问控制**、 **敏感内容过滤**、 **审计与合规** 四方面给出示例说明。

#### 4.3.1 数据传输与存储安全

- **传输层加密**：DashScope 默认使用 HTTPS，确保与服务器之间的数据通信加密；

- **敏感信息加密 / 脱敏**：如果用户消息包含个人隐私或商业机密，可在调用 `Messages.create` 之前先进行敏感字段的加密或脱敏处理。

- **本地数据库安全**：将 DashScope 返回的 `Message`、`Thread`、`Run` 等信息二次存储到本地数据库时，可启用行级加密或敏感字段加密，并做好访问权限管控。


#### 4.3.2 API Key 与访问控制

DashScope 通过 **API Key** 验证调用者身份。务必将您的 API Key 存放在安全的环境变量或密钥管理系统中，避免硬编码在公开仓库里。此外，可考虑以下策略：

1. **分环境 / 分角色**：为开发、测试、生产环境配置不同的 API Key；或为不同租户配置独立的 Key；

2. **最小权限**：只授予必要的 workspace 访问权限，防止 Key 泄露后影响到其它业务空间的数据；

3. **定期轮换**：根据安全策略，定期更新 API Key，并在 DashScope 控制台撤销旧 Key。


#### 4.3.3 敏感内容过滤

- **敏感词检测**：在调用 `Messages.create` 前，对 `content` 做关键字或模型检测；

- **业务规则限制**：若用户消息不符合平台策略（如包含不良信息），可在应用层拒绝发送并提示用户；

- **审计日志**：对发送的内容和生成的结果进行日志记录，以备安全审查或合规检查。


#### 4.3.4 审计与合规

在一些合规严格的行业（医疗、金融、政府机构等），需要保存操作审计日志，并对用户产生的对话内容做敏感操作记录。您可以：

1. **记录操作日志**：每次调用 DashScope 的 API，记录请求时间、操作人（用户 ID）、目标对象（Thread ID、Assistant ID）等；

2. **加密或脱敏存储**：保留敏感对话内容时先做脱敏或加密，保障数据安全合规。


* * *

### 4.4 业务空间（workspace）管理

阿里云百炼提供了 workspace 业务空间管理功能。开发者可以在控制台创建多个业务空间，这些空间彼此之间是完全隔离的，通过 **workspace id** 进行标识。Assistant API 的所有操作都支持传入 `workspace` 参数，以区分不同业务空间的业务。

#### 4.4.1 概念简介

- **多租户隔离**：不同 workspace 之间的 `Assistant`、`Thread`、`Message`、`Run` 等记录互不影响；

- **数据安全与可管理性**：可以独立地进行删除、归档、访问权限控制；

- **权限与计费**：可在控制台对每个 workspace 的访问进行单独管理，也能更方便地统计和计费。


#### 4.4.2 如何使用 `workspace` 参数

所有主要操作（如 `Assistants.create`、`Threads.retrieve`、`Runs.list` 等）都可以接受可选的 `workspace` 参数，用来指定目标业务空间。若不传，则默认使用“默认工作空间”或当前 Key 绑定的空间。

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
assistant = Assistants.create(
    model="qwen-plus",
    workspace="WSID123"
)
thread = Threads.create(
    metadata={"key": "value"},
    workspace="WSID123"
)
```

若要检索或删除对象，也需同时提供正确的 `id` 与 `workspace`：

```python
# 示例代码仅供参考，请勿直接在生产环境中使用
retrieved_assistant = Assistants.retrieve(
    assistant_id="AID_XXX",
    workspace="WSID123"
)
Assistants.delete(
    assistant_id="AID_XXX",
    workspace="WSID123"
)
```

#### 4.4.3 典型使用场景

1. **多租户 SaaS 平台**：为每个企业客户分配独立 workspace，数据相互隔离；

2. **跨业务线管理**：不同部门或项目分别使用独立 workspace，方便各自管理配置与统计；

3. **开发 / 测试 / 生产环境分离**：在控制台中创建 dev、test、prod 等 workspace，将不同环境的数据分离管理，避免相互干扰。


#### 4.4.4 注意要点

- **API Key 与 workspace**：需要在控制台配置相应的访问权限；

- **对象 id 的查找范围**：检索某对象时，必须在对应的 workspace 下检索；

- **删除操作**：只能删除该 workspace 中的对象，不会影响其他 workspace 的数据。


通过将工作空间与多用户场景结合使用，开发者能够轻松地搭建起 **多租户**、 **跨业务线** 或者 **多环境** 的对话系统，既保证了隔离性，又提升了可维护性。

* * *

## 5\. 参考示例：构建一个简易聊天机器人

下面给出一个综合示例，演示如何用 DashScope SDK 来管理从 `Assistant` 到 `Thread`、`Message`、`Run` 的基本流程。

```python
from dashscope import Assistants, Threads, Messages, Runs

def init_assistant() -> str:
    """创建并返回一个assistant_id"""
    assistant = Assistants.create(
        model="qwen-plus",  # 模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models
        name="ChatAssistant",
        instructions="You are a helpful assistant.",
        metadata={"env": "test"}
    )
    return assistant.id

def start_session(assistant_id: str, user_input: str) -> str:
    """创建线程并发送第一条用户消息"""
    # 创建一个线程
    thread = Threads.create(
        metadata={"session_owner": "User123"}
    )
    # 发送用户的第一条消息
    Messages.create(
        thread_id=thread.id,
        content=user_input,
        role="user"
    )
    return thread.id

def get_assistant_reply(assistant_id: str, thread_id: str) -> str:
    """让assistant在该thread上生成回复并返回文本"""
    run = Runs.create(
        thread_id=thread_id,
        assistant_id=assistant_id,
        # 可以覆盖model, instructions等
        model="qwen-plus"
    )
    # 等待run完成
    final_run = Runs.wait(run.id, thread_id=thread_id, timeout_seconds=60)
    # 生成的assistant消息会记录在thread中，第一条是assistant消息（注意：Messages.list 返回的信息是按照创建时间逆序排列的）。
    thread_messages = Messages.list(thread_id=thread_id)
    if thread_messages.data:
        last_msg = thread_messages.data[0]
        return last_msg.content[0].text.value if last_msg.content else "No reply."
    return "No reply."

def end_session(thread_id: str):
    """删除thread，级联删除所有消息和run"""
    Threads.delete(thread_id)

# 例子演示
assistant_id = init_assistant()
thread_id = start_session(assistant_id, "你好，请告诉我今天的天气如何？")
reply = get_assistant_reply(assistant_id, thread_id)
print("Assistant reply:", reply)
end_session(thread_id)
```

在此示例中：

1. `init_assistant()`：先创建一个全局的 Assistant（指定模型、默认指令等）。

2. `start_session()`：创建一个新的对话 `Thread` 并添加用户消息。

3. `get_assistant_reply()`：创建一个 `Run` 来调用模型生成回复。由于是异步执行，需要 `Runs.wait()` 等待完成；完成后，新的 `Message` 就会插入到该线程里。拉取所有消息并返回最后一条（一般就是 Assistant 的回复）。

4. `end_session()`：在完成会话后删除 `Thread`，从服务器端移除所有资源。


* * *

## 6\. 常见问题 (FAQ)

1. **Q: 我如何在本地对话框中显示消息历史？**

**A:** 您可以在后端通过 `Messages.list(thread_id=xxx)` 获取所有消息，然后根据角色（user/assistant）渲染到前端。也可将它们存到自己数据库中进行分页展示。

2. **Q: 如何对用户消息进行拦截或过滤？**

**A:** 在调用 `Messages.create` 前，对 `content`进行文本检测或清洗；也可以在 `metadata` 中标记敏感度。

3. **Q: 有办法只删除单条 Message 吗？**

**A:** 目前暂不支持单条删除，需要通过 `Threads.delete(thread_id)` 进行整会话级联删除。

4. **Q: 线程（Thread）什么时候应该结束？**

**A:** 根据业务需求决定。可以在用户退出或会话超时后调用 `Threads.delete`，或者保留一段时间以便用户再次进来继续对话。

5. **Q:**`Run` **等待超时时有什么应对方式？**

**A:** 可以使用 `Runs.wait(run_id, thread_id, timeout_seconds=...)`。若超时，SDK 会抛 `TimeoutException`，可在捕获后进行重试或提示用户“请求超时”。

6. **Q: 如何对多步骤推理场景做更详细的监控？**

**A:** 您可以查看 `Steps.list(run_id, thread_id)` 来获取每一个步骤执行信息，也可以在本地做日志记录或触发警报（如对超时步骤发送告警）。


* * *

## 7\. 总结

通过以上内容与示例，对 DashScope SDK 中的 `Assistants`、`Threads`、`Messages`、`Runs` 和 `Steps` 各模块做了全面讲解：

1. **创建 / 检索 / 更新 / 删除**：每个对象在服务器端都有增、删、查、改的方法；

2. **生命周期与存储**：对象默认保存在 DashScope 服务器，没有自动过期，需自行调用 `delete` 或采用本地数据库二次管理；

3. **并发多用户管理**：在业务层面进行线程安全、上下文隔离和权限控制；

4. **最佳实践**：


   - 将 DashScope 返回的对象 ID 与自己业务数据关联；

   - 必要时做日志与审计；

   - 严格管理敏感信息与删除策略；

   - 使用 `Runs.wait()` 或者 `stream=True` 处理生成的过程；

   - 在复杂场景下可查看 `Steps` 获取多阶段的执行信息。

您还可以了解更多高级用法（例如 [流式输出](https://help.aliyun.com/zh/model-studio/streaming-output "")、 [工具调用-概述](https://help.aliyun.com/zh/model-studio/tool-calling-overview/ "") 等）。您可以在“ [Assistant API 开发参考](https://help.aliyun.com/zh/model-studio/assistantapi/ "")”中找到所有组件的详细示例和参数解释。