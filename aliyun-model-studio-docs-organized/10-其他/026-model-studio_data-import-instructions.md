### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用数据](https://help.aliyun.com/zh/model-studio/application-data/)数据导入

# 数据导入

更新时间：2026-02-11 02:04:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作指南

下一步

更多

从OSS导入文件配置说明

配额与限制

计费说明

常见问题

权限与安全

导入OSS文件

导入MySQL数据

在构建知识库前，请先将知识数据导入阿里云百炼，作为知识库的初始知识来源。

## **操作指南**

导入本地文件

导入本地表格

导入OSS文件

导入RDS MySQL数据

导入自建MySQL数据

1. 进入[文件](https://bailian.console.aliyun.com/?tab=app#/data-center?dataType=0)页签。

2. 在左侧 **类目** 下，选择一个现有类目，或点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0077764271/p839829.png)图标新建类目。


> 阿里云百炼通过类目管理导入的文件。

3. 点击 **导入数据，** 进入 **导入数据** 界面 **。** 导入方式选择 **本地上传**。


> 目前平台不支持直接导入JSON、CSV、YAML格式文件。请自行用相应工具将其转换为XLSX或XLS格式再导入。

4. **解析方式** 可选 **默认设置** 或 **自定义设置**（ **自定义设置** 可针对不同格式配置解析规则，以提升解析效果）。



**解析方式说明**






请根据实际需求配置解析策略，如不确定建议保持默认设置。有关 **文档智能解析**、 **大模型文档解析** 和 **电子文档解析** 的详细说明，请参阅 [文档理解](https://help.aliyun.com/zh/document-mind/product-overview/overview-of-document-understanding#9a4f5fb91fpps "")。



   - **电子文档解析**：不支持解析文件中的插图与图表。

   - **文档智能解析：** 对于文件中的插图，解析器会识别并提取图中的文本，并生成文本摘要。这些摘要将与文件中其它非图片内容一起被切分并转换为向量，参与知识库的检索。

   - **大模型文档解析：** 使用 [千问VL](https://help.aliyun.com/zh/model-studio/models#3f1f1c8913fvo "") 模型的智能体应用支持用户对文件中插图和图表的内容进行提问。如需识别和理解文件中的插图与图表，请选择 **大模型文档解析**。

   - **Qwen VL解析：** 仅支持解析图片格式。可自主选择千问VL模型，并通过传入Prompt指定模型需要识别的版面、元素及内容，其余功能与大模型文档解析一致。

   - **音视频解析：** 对文件进行语音识别、视频帧提取（仅限视频）和剧情解析（仅限视频），最终将所有声画信息按时间轴结构化对齐。

     - **语音识别：** 字幕内容解析器通过 [录音文件识别](https://help.aliyun.com/zh/model-studio/recording-file-recognition "") 将人类语音转为文本。暂不支持识别音乐或自然环境声（如喇叭声、钟声、雷声等）。

     - **视频帧提取：** 从原始视频中抽取有代表性的视觉画面，并生成相应的文本描述。

     - **剧情解析（需手动开启）：** 分析视频内容，定位具体事件并标注时间戳，同时生成相应的文本描述。

|     |     |
| --- | --- |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6412935471/p946164.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4548753471/p935554.png) |

[如何让阿里云百炼应用在回答中正常展示文件中的插图](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#9e13851641b37 "")

5. 为文件 **配置标签**（可选）。


> [通过API调用应用](https://help.aliyun.com/zh/model-studio/application-calling-guide#4100253b7chc3 "") 时，可以在请求参数`tags`中指定标签。应用在检索知识库时，会先根据标签筛选相关文件，从而提高检索效率。对于 [智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "")，可在控制台调试知识库时设置标签。

6. 点击 **确认**，系统将开始解析和导入，可在页面查看任务进度。


> 文件将被转换成阿里云百炼可处理的格式。在请求高峰时段，该过程可能需要数小时，请耐心等待。

7. 导入完成后，点击相应文件右侧的 **详情** 即可查看导入的文件。


> 文件导入阿里云百炼后，将作为独立副本（与原始数据没有关联）存储在平台提供的免费空间中，当前无容量限制。



> 仅支持查看最近 **90** 天内导入的文件。超过此时间范围后，导入的文件将无法查看，但不会被删除。



> 导入的文件仅供当前业务空间的用户使用。阿里云百炼不会将其用于任何商业用途或对外公开。


1. 进入[表格](https://bailian.console.aliyun.com/?tab=app#/data-center?dataType=1)页签。

2. 在左侧 **数据表** 下，选择一个现有数据表，或点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0077764271/p839829.png)图标新建数据表。


> 阿里云百炼通过数据表管理导入的数据。







导入到新数据表



导入到现有数据表



















1. 输入 **数据表名称**。并配置数据表，选择可 **直接上传Excel** 或 **自定义表头**。

      - **直接上传Excel：** 阿里云百炼将自动识别上传文件中的表头，并据此来创建数据表结构，并将其余内容作为数据记录导入该表。

      - **自定义表头：** **列名** 为必填参数， **描述** 为选填参数， **类型** 为必填参数。



        **重要**





        - 数据表的结构（列名、描述以及类型）一旦确定，无法修改。

        - 上传文件的表结构必须与待导入数据文件的结构（列数、列名）完全一致，否则导入会失败。例如，待导入的数据表有2列，这里的表结构必须配置2个字段，且列名需一一对应。可通过点击 **新增字段** 或 **操作** 列的 **删除**，来增加或删减字段。

        - 为帮助模型理解各字段含义（如 `age` 表示年龄），请在“描述”中提供清晰的自然语言说明。

        - 若字段类型设为 `image_url`，请确保链接是 **公开可访问** 的图片URL。知识库会用此链接抓取图片并为其生成向量索引，用于以图搜图等场景。


          > image\_url格式示例：https://example.com/downloads/pic.jpg



          > 创建知识库时，image\_url类型字段用于生成 **图片索引**。阿里云百炼会访问目标图片并提取其特征，然后通过图片Embedding转换为向量并保存。知识库检索时，会用该向量与用户上传图片的向量进行相似度比对。
2. 点击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2312799171/p816622.png)图标选择并上传文件（XLSX或XLS格式）。


      > 文件必须包含表头，否则会导入失败。



      > 目前平台不支持直接导入JSON、CSV、YAML格式文件。请自行用相应工具将其转换为XLSX或XLS格式再导入。

3. 点击 **确定**，开始导入。完成后，左侧的 **数据表** 导航树中将出现新数据表。


1. 在左侧的 **数据表** 列表中选择相应的数据表，然后点击 **导入数据**。

2. 导入类型选择 **覆盖上传** 或 **增量上传**。


      > 点击界面上的 **下载模板**，可获取一个仅包含表头的空白文件。您可直接在该文件中插入新数据，然后将其用于覆盖上传或增量上传。

3. 点击![image](<Base64-Image-Removed>)图标选择并上传文件（XLSX或XLS格式）。


      > 文件必须包含表头，且与当前数据表的表头结构一致，否则会导入失败。



      > 目前平台不支持直接导入JSON、CSV、YAML格式文件。请自行用相应工具将其转换为XLSX或XLS格式再导入。


1. 进入[文件](https://bailian.console.aliyun.com/?tab=app#/data-center?dataType=0)页签。

2. 在左侧 **类目** 下，选择一个现有类目，或点击![image](<Base64-Image-Removed>)图标新建类目。


> 阿里云百炼通过类目管理导入的文件。

3. 点击 **导入数据，** 进入 **导入数据** 界面 **。** 导入方式选择 **OSS**。


> 首次从 OSS 向阿里云百炼导入数据，需按界面提示完成授权，并为目标 Bucket 添加`bailian-datahub-access`标签以供阿里云百炼访问。操作指南请参见 [从OSS导入文件配置说明](https://help.aliyun.com/zh/model-studio/data-import-instructions#a2b61704136bj "")。



> 不支持归档、冷归档或深度冷归档存储类型的 Bucket。



> 不支持访问 Bucket 根目录下的文件，请选择已有的子目录或新建一个子目录供阿里云百炼访问。



> 支持内容加密的 Bucket。支持私有的 Bucket。



> 如需使用开启 [Referer防盗链](https://help.aliyun.com/zh/oss/configure-referer-policy-to-prevent-other-websites-from-referring-to-oss-files "") 的Bucket，须参考 [防盗链](https://help.aliyun.com/zh/oss/user-guide/hotlink-protection#8a560a5cc91od "") 将域名`*.console.aliyun.com`添加到白名单Referer中。

4. **解析方式** 可选 **默认设置** 或 **自定义设置**（ **自定义设置** 可针对不同格式配置解析规则，以提升解析效果）。



**解析方式说明**






请根据实际需求配置解析策略，如不确定建议保持默认设置。有关 **文档智能解析**、 **大模型文档解析** 和 **电子文档解析** 的详细说明，请参阅 [文档理解](https://help.aliyun.com/zh/document-mind/product-overview/overview-of-document-understanding#9a4f5fb91fpps "")。



   - **电子文档解析**：不支持解析文件中的插图与图表。

   - **文档智能解析：** 对于文件中的插图，解析器会识别并提取图中的文本，并生成文本摘要。这些摘要将与文件中其它非图片内容一起被切分并转换为向量，参与知识库的检索。

   - **大模型文档解析：** 使用 [千问VL](https://help.aliyun.com/zh/model-studio/models#3f1f1c8913fvo "") 模型的智能体应用支持用户对文件中插图和图表的内容进行提问。如需识别和理解文件中的插图与图表，请选择 **大模型文档解析**。

   - **Qwen VL解析：** 仅支持解析图片格式。可自主选择千问VL模型，并通过传入Prompt指定模型需要识别的版面、元素及内容，其余功能与大模型文档解析一致。

   - **音视频解析：** 对文件进行语音识别、视频帧提取（仅限视频）和剧情解析（仅限视频），最终将所有声画信息按时间轴结构化对齐。

     - **语音识别：** 字幕内容解析器通过 [录音文件识别](https://help.aliyun.com/zh/model-studio/recording-file-recognition "") 将人类语音转为文本。暂不支持识别音乐或自然环境声（如喇叭声、钟声、雷声等）。

     - **视频帧提取：** 从原始视频中抽取有代表性的视觉画面，并生成相应的文本描述。

     - **剧情解析（需手动开启）：** 分析视频内容，定位具体事件并标注时间戳，同时生成相应的文本描述。

|     |     |
| --- | --- |
| ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |

[如何让阿里云百炼应用在回答中正常展示文件中的插图](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#9e13851641b37 "")

5. 为文件 **配置标签**（可选）。


> [通过API调用应用](https://help.aliyun.com/zh/model-studio/application-calling-guide#4100253b7chc3 "") 时，可以在请求参数`tags`中指定标签。应用在检索知识库时，会先根据标签筛选相关文件，从而提高检索效率。对于 [智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "")，可在控制台编辑应用时直接设置标签（启用**知识库** \> **+知识库** \> **知识库高级配置** \> **标签过滤**）。

6. 点击 **确认**，系统将开始解析和导入，可在页面查看任务进度。


> 文件将被转换成阿里云百炼可处理的格式。在请求高峰时段，该过程可能需要数小时，请耐心等待。

7. 导入完成后，点击相应文件右侧的 **详情** 即可查看导入的文件。


> 文件导入阿里云百炼后，将作为独立副本（与原始数据没有关联）存储在平台提供的免费空间中，当前无容量限制。



> 导入的文件仅供当前业务空间的用户使用。阿里云百炼不会将其用于任何商业用途或对外公开。


**重要**

- 新建数据源前需开通阿里云事件总线 [EventBridge](https://eventbridge.console.aliyun.com/) 服务。

- 阿里云百炼与RDS实例 **必须归属同一阿里云账号**。否则请按照 **导入自建MySQL数据** 中步骤操作。

- 导入大数据表（ **1,000,000** 行以上）时，耗时可能超过数据库本地日志的保留时长，造成数据重复导入。 [如何解决](https://help.aliyun.com/zh/model-studio/data-import-instructions#d152117985mus "")


1. 进入 [数据源](https://bailian.console.aliyun.com/?tab=app#/data-center/data-source) 页面，点击**创建数据源** \> **创建自定义数据源**。

2. 输入 **数据源名称**， **数据源类型** 选择 **阿里云RDS MySQL**。


> **RDS实例限制：** 目前只支持 **MySQL** 引擎（版本无限制），暂不支持 **PostgreSQL** 等其它引擎；实例地域不限；只支持 **基础系列** 和 **高可用系列**；创建RDS实例时，网络类型必须是 **专有网络**，加入白名单需选 **是**（将VPC网段加入到RDS实例白名单中）。



> **数据库和表限制：** 知识库只能关联单个数据库中的一张表，不支持多表关联；关联表中的数据量最大为 **10,000,000** 行，且每一行记录的大小必须控制在 **100** KB以内（超出将被截断）。若最大行数限制无法满足实际业务需求，可提交工单申请调整。

3. **网络类型** 选择 **公网** 或 **私网**。


> 私网数据源 [仅支持部分地域](https://help.aliyun.com/zh/model-studio/data-import-instructions#6e4bedffaedcy "") 的RDS实例；其他地域请选择公网数据源。私网数据源在安全性和性能方面更具优势。







新建公网数据源



新建私网数据源



















1. 为确保知识库能正常接收RDS数据，请为RDS实例设置EventBridge白名单。



      > 若未正确设置白名单，创建数据源时会提示`Communications link failure`。




      **如何设置EventBridge白名单**






      1. 访问 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表**，然后点击包含数据表的RDS实例。接着，点击左侧导航栏中的 **数据库连接**，点击外网地址旁的 **设置白名单**。![image](<Base64-Image-Removed>)

      2. 点击 **添加白名单分组**，并将以下 EventBridge 公网 IP 地址 **全部添加** 至白名单分组中。

         - 39.105.55.188,39.105.110.43,47.95.35.213,47.95.33.100,39.106.255.198,47.93.177.159,47.95.32.154,39.107.99.72
      3. 点击 **确定**，白名单生效。


2. 填写数据源相关配置：


      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **数据源名称** | 数据源名称在同一个 [业务空间](https://help.aliyun.com/zh/model-studio/use-workspace "") 中应是唯一的。即使数据源创建失败，该名称也无法再次使用。 |
      | **数据库实例** | 填写RDS实例ID。请前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表** 获取。 |
      | **数据库地址** | 填写RDS实例的外网地址。您可以在RDS实例的 **数据库连接** 界面获取该信息：前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表**，然后点击包含数据表的RDS实例。接着，点击左侧导航栏中的 **数据库连接**，即可查看该实例对应的外网地址。<br>> 若该 RDS 实例未开通外网地址，请先按照界面指引完成 RDS 外网地址开通。<br>> 高可用系列RDS请勿使用 **数据库代理连接** 区域的 **代理连接地址** 或 **内网地址**。<br>![image](<Base64-Image-Removed>) |
      | **数据库端口** | 填写RDS实例的外网端口。该信息同样可以在RDS实例的 **数据库连接** 界面获取。 |
      | **数据库用户名** | 数据库账号类型需为 **高权限账号**，关于账号说明和获取方式请参见 [创建账号](https://help.aliyun.com/zh/rds/apsaradb-rds-for-mysql/create-an-account-on-an-apsaradb-rds-for-mysql-instance#section-b3f-whz-q2b "")。<br>> 使用普通账号创建数据源时会提示`There is no permission:RELOAD`。 |

3. 点击 **创建数据源**，提交新建任务。系统将自动配置 RDS 数据源，期间业务空间将被锁定，无法同时创建其他数据源。


      > 首次提交任务时，请根据界面指引开通EventBridge服务关联角色，请使用 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 操作。如需使用RAM用户，需主账号为该RAM用户 [配置必要权限](https://help.aliyun.com/zh/model-studio/data-import-instructions#b0cbc9b177wvb "")。



      > 在请求高峰时段，创建数据源过程可能需要几分钟，请耐心等待。



      |     |     |
      | --- | --- |
      | **状态** | **说明** |
      | **创建成功** | 表示数据源创建成功。请选择该数据源并执行 [下一步](https://help.aliyun.com/zh/model-studio/data-import-instructions#fe7af7262307m "")。 |
      | **创建失败** | 表示数据源创建失败。请检查各项参数是否正确，修改后点击 **重试** 重新创建数据源。您可点击 **删除**，删除创建失败的数据源。 |


1. 填写数据源相关配置：


      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **数据源名称** | 数据源名称在同一个 [业务空间](https://help.aliyun.com/zh/model-studio/use-workspace "") 中应是唯一的。即使数据源创建失败，该名称也无法再次使用。 |
      | **所属地域** | 选择RDS实例 [所在地域](https://help.aliyun.com/zh/model-studio/data-import-instructions#6e4bedffaedcy "")。请前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表** 获取。 |
      | **数据库实例** | 填写RDS实例ID。请前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表** 获取。 |
      | **数据库地址** | 填写RDS实例的 **内网地址**。您可以在RDS实例的 **数据库连接** 界面获取该信息：前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表**，然后点击包含数据表的RDS实例。接着，点击左侧导航中的 **数据库连接**，即可查看该实例对应的 **内网地址**。<br>> 高可用系列RDS请勿使用 **数据库代理连接** 区域的 **代理连接地址** 或 **内网地址**。<br>![image](<Base64-Image-Removed>) |
      | **数据库端口** | 填写RDS实例的 **内网端口**。该信息同样可以在RDS实例的 **数据库连接** 界面获取。 |
      | **数据库用户名** | 数据库账号类型需为 **高权限账号**，关于账号说明和获取方式请参见 [创建账号](https://help.aliyun.com/zh/rds/apsaradb-rds-for-mysql/create-an-account-on-an-apsaradb-rds-for-mysql-instance#section-b3f-whz-q2b "")。<br>> 使用普通账号创建数据源时会提示`There is no permission:RELOAD`。 |

2. 连通性检测：点击 **开始检测**，对阿里云百炼与数据源之间的网络连通性进行检查。


      > 首次检测时，请根据界面指引开通EventBridge服务关联角色，请使用 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 操作。如需使用RAM用户，需主账号为该RAM用户 [配置必要权限](https://help.aliyun.com/zh/model-studio/data-import-instructions#b0cbc9b177wvb "")。



      |     |     |
      | --- | --- |
      | **VPC ID** | 应填写RDS实例的 **VPC ID**。该信息同样可以在RDS实例的 **数据库连接** 界面获取。<br>![image](<Base64-Image-Removed>) |
      | **VSwitch ID** | 将鼠标悬浮于RDS实例的VPC ID上即可显示VSwitch ID。<br>> RDS MySQL高可用系列实例可能拥有多个 VSwitch ID，请完整填写该实例关联的所有 VSwitch ID。<br>![image](<Base64-Image-Removed>) |
      | **安全组ID** | 可直接 **使用托管安全组**；如需使用指定安全组，该安全组应为直接创建，非由第三方产品或服务间接创建。您可以前往 [ECS控制台](https://ecs.console.aliyun.com/home) 的 **安全组** 界面创建安全组。该安全组需满足以下要求：<br>      - 安全组的地域需与上方 **所属地域** 保持一致；<br>        <br>      - 安全组的网络需选择RDS所在的VPC；<br>        <br>        ![image](<Base64-Image-Removed>)<br>        <br>      - 安全组类型支持普通安全组和企业级安全组。<br>        <br>      - 安全组的网络 **入方向** 未设置任何访问限制；<br>        <br>        - **正确示例：**<br>          <br>          ![image](<Base64-Image-Removed>)<br>          <br>        - **错误示例：**![image](<Base64-Image-Removed>) |

3. 连通性检测通过后，点击 **创建数据源**，提交新建任务。系统将为您自动配置RDS数据源，期间当前业务空间会被锁定，禁止同时创建其他数据源。


      > 在请求高峰时段，创建数据源过程可能需要几分钟，请耐心等待。



      |     |     |
      | --- | --- |
      | **状态** | **说明** |
      | **创建成功** | 表示数据源创建成功。请选择该数据源并执行 [下一步](https://help.aliyun.com/zh/model-studio/data-import-instructions#fe7af7262307m "")。 |
      | **创建失败** | 表示数据源创建失败。请检查各项参数是否正确，修改后点击 **重试** 重新创建数据源。您可点击 **删除**，删除创建失败的数据源。 |


**重要**

- 新建数据源前需开通阿里云事件总线 [EventBridge](https://eventbridge.console.aliyun.com/) 服务。

- 导入大数据表（ **1,000,000** 行以上）时，耗时可能超过数据库本地日志的保留时长，造成数据重复导入。 [如何解决](https://help.aliyun.com/zh/model-studio/data-import-instructions#d152117985mus "")


1. 进入 [数据源](https://bailian.console.aliyun.com/?tab=app#/data-center/data-source) 页面，点击**创建数据源** \> **创建自定义数据源**。

2. 输入 **数据源名称**， **数据源类型** 选择 **自建MySQL**。


> **自建MySQL限制：** 必须部署在阿里云ECS实例（地域不限）上；目前只支持MySQL 5.6、5.7和8.0；不支持MySQL代理Proxy。



> **数据库和表限制：** 知识库只能关联单个数据库中的一张表，不支持多表关联；关联表中的数据量最大为 **10,000,000** 行，且每一行记录的大小必须控制在 **100** KB以内（超出将被截断）。若最大行数限制无法满足实际业务需求，可提交工单申请调整。

3. **网络类型** 选择 **公网** 或 **私网**。


> 私网数据源 [仅支持部分地域](https://help.aliyun.com/zh/model-studio/data-import-instructions#6e4bedffaedcy "") 的ECS实例；其他地域请选择公网数据源。私网数据源在安全性和性能方面更具优势。







新建公网数据源



新建私网数据源



















1. 为确保知识库能正常接收数据，请为您的自建MySQL配置EventBridge白名单。



      > 若未正确配置白名单，创建数据源时会提示`Communications link failure`。




      **如何设置EventBridge白名单**






      1. 访问 [ECS控制台](https://ecs.console.aliyun.com/home)，点击左侧导航栏中的 **安全组**，找到与您自建MySQL关联的安全组，然后点击 **操作** 栏中的 **管理规则。**

         ![image](<Base64-Image-Removed>)

      2. 在安全组详情页，点击 **增加规则**，将以下EventBridge公网IP地址 **全部添加** 至该安全组中，并且需要放行 **所有流量** 和 **全部端口**。


         > 不可使用由第三方产品或服务间接创建的安全组。



         - 39.105.55.188,39.105.110.43,47.95.35.213,47.95.33.100,39.106.255.198,47.93.177.159,47.95.32.154,39.107.99.72


![image](<Base64-Image-Removed>)

      3. 点击 **确定**，安全组生效。

      4. 在您的MySQL中，创建一个允许全部来源流量的数据库账号（也可以使用已有账号）然后执行以下GRANT授权命令。


         > 请根据您的实际情况，将下方命令中的user1替换为您的实际数据库账号。
















         ```sql
         -- 创建用户（合并为单条语句），请将user1替换为您的实际数据库账号
         CREATE USER 'user1'@'%' IDENTIFIED BY 'user1的密码';

         -- 授予基础权限（合并为单条语句），请将user1替换为您的实际数据库账号
         GRANT ALL PRIVILEGES ON *.* TO 'user1'@'%' WITH GRANT OPTION;

         -- 刷新权限（仅需一次）
         FLUSH PRIVILEGES;
         ```

      5. 通过修改MySQL配置文件开启Binlog和GTID。以Linux系统为例，MySQL配置文件一般位于：/etc/my.cnf 或 /etc/mysql/my.cnf。















         ```plaintext
         [mysqld]
         log-bin=mysql-bin
         server-id=1
         binlog_format=ROW
         gtid_mode=ON
         enforce_gtid_consistency=ON
         ```

      6. 重启MySQL，配置文件生效。


2. 填写数据源相关配置：


      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **数据源名称** | 数据源名称在同一个 [业务空间](https://help.aliyun.com/zh/model-studio/use-workspace "") 中应是唯一的。即使数据源创建失败，该名称也无法再次使用。 |
      | **数据库地址** | 填写您自建MySQL的公网地址。 |
      | **数据库端口** | 填写您自建MySQL的端口。 |
      | **数据库用户名** | 填写您在前面加白步骤中执行过GRANT授权的数据库账号。 |

3. 点击 **创建数据源**，提交新建任务。系统将为您自动配置自建MySQL数据源，期间当前业务空间会被锁定，禁止同时创建其他数据源。


      > 首次提交任务时，请根据界面指引开通EventBridge服务关联角色，请使用 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 操作。如需使用RAM用户，需主账号为该RAM用户 [配置必要权限](https://help.aliyun.com/zh/model-studio/data-import-instructions#b0cbc9b177wvb "")。



      > 在请求高峰时段，创建数据源过程可能需要几分钟，请耐心等待。



      |     |     |
      | --- | --- |
      | **状态** | **说明** |
      | **创建成功** | 表示数据源创建成功。请选择该数据源并执行 [下一步](https://help.aliyun.com/zh/model-studio/data-import-instructions#fe7af7262307m "")。 |
      | **创建失败** | 表示数据源创建失败。请检查各项参数是否正确，修改后点击 **重试** 重新创建数据源。您可点击 **删除**，删除创建失败的数据源。 |


1. 为确保知识库能正常接收数据，请为您的自建MySQL配置EventBridge白名单。



      > 若未正确配置白名单，创建数据源时会提示`Communications link failure`。




      **如何设置EventBridge白名单**






      1. 在您的MySQL中，创建一个允许全部来源流量的数据库账号（也可以使用已有账号）然后执行以下GRANT授权命令。


         > 请根据您的实际情况，将下方命令中的user1替换为您的实际数据库账号。
















         ```sql
         -- 创建用户（合并为单条语句），请将user1替换为您的实际数据库账号
         CREATE USER 'user1'@'%' IDENTIFIED BY 'user1的密码';

         -- 授予基础权限（合并为单条语句），请将user1替换为您的实际数据库账号
         GRANT ALL PRIVILEGES ON *.* TO 'user1'@'%' WITH GRANT OPTION;

         -- 刷新权限（仅需一次）
         FLUSH PRIVILEGES;
         ```

      2. 通过修改MySQL配置文件开启Binlog和GTID。以Linux系统为例，MySQL配置文件一般位于：/etc/my.cnf 或 /etc/mysql/my.cnf。















         ```plaintext
         [mysqld]
         log-bin=mysql-bin
         server-id=1
         binlog_format=ROW
         gtid_mode=ON
         enforce_gtid_consistency=ON
         ```

      3. 重启MySQL，配置文件生效。


2. 填写数据源相关配置：


      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **数据源名称** | 数据源名称在同一个 [业务空间](https://help.aliyun.com/zh/model-studio/use-workspace "") 中应是唯一的。即使数据源创建失败，该名称也无法再次使用。 |
      | **所属地域** | 请选择您自建MySQL所部署ECS实例所在地域。该信息可以前往 [ECS控制台](https://ecs.console.aliyun.com/home) 获取。 |
      | **数据库地址** | 填写您自建MySQL的 **私网地址**。您可以在ECS的 **实例** 界面获取该信息：前往 [ECS控制台](https://ecs.console.aliyun.com/home)，点击左侧导航栏中的 **实例**，即可查看对应实例的 **私网地址**。<br>![image](<Base64-Image-Removed>) |
      | **数据库端口** | 填写您自建MySQL的端口。 |
      | **数据库用户名** | 填写您在前面加白步骤中执行过GRANT授权的数据库账号。 |

3. 连通性检测：点击 **开始检测**，对阿里云百炼与数据源之间的网络连通性进行检查。


      > 首次提交任务时，请根据界面指引开通EventBridge服务关联角色，请使用 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 操作。如需使用RAM用户，需主账号为该RAM用户 [配置必要权限](https://help.aliyun.com/zh/model-studio/data-import-instructions#b0cbc9b177wvb "")。



      |     |     |
      | --- | --- |
      | **VPC ID** | 填写您自建MySQL所部署ECS实例所在VPC的 **实例ID**（vpc-xxxxxx）。该信息同样可以前往 [ECS控制台](https://ecs.console.aliyun.com/home) 获取。<br>![image](<Base64-Image-Removed>) |
      | **VSwitch ID** | 实例VPC ID下方即是VSwitch ID（vsw-xxxxxx）。<br>![image](<Base64-Image-Removed>) |
      | **安全组ID** | 可直接 **使用托管安全组**；如需使用指定安全组，该安全组应为直接创建，非由第三方产品或服务间接创建。您可以前往 [ECS控制台](https://ecs.console.aliyun.com/home) 的 **安全组** 界面创建安全组。该安全组需满足以下要求：<br>      - 安全组的地域需与上方 **所属地域** 保持一致；<br>        <br>      - 安全组的网络需选择ECS所在的VPC；<br>        <br>        ![image](<Base64-Image-Removed>)<br>        <br>      - 安全组类型支持普通安全组和企业级安全组。<br>        <br>      - **入方向** 未设置任何访问限制；<br>        <br>        - **正确示例：**<br>          <br>          ![image](<Base64-Image-Removed>)<br>          <br>        - **错误示例：**![image](<Base64-Image-Removed>) |

4. 连通性检测通过后，点击 **创建数据源**，提交新建任务。系统将为您自动配置MySQL数据源，期间当前业务空间会被锁定，禁止同时创建其他数据源。


      > 在请求高峰时段，创建数据源过程可能需要几分钟，请耐心等待。



      |     |     |
      | --- | --- |
      | **状态** | **说明** |
      | **创建成功** | 表示数据源创建成功。请选择该数据源并执行 [下一步](https://help.aliyun.com/zh/model-studio/data-import-instructions#fe7af7262307m "")。 |
      | **创建失败** | 表示数据源创建失败。请检查各项参数是否正确，修改后点击 **重试** 重新创建数据源。您可点击 **删除**，删除创建失败的数据源。 |


## 下一步

[创建知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#6028cfefaauhu "")

## **更多**

### **从OSS导入文件配置说明**

首次从OSS导入文件时，需要授权阿里云百炼访问OSS资源。 [主账号](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 与子账号的授权流程不同。

主账号授权

子账号授权

1. 如下图所示，点击 **前往授权**。

![image](<Base64-Image-Removed>)

2. 在弹出的对话框中，点击 **确认授权**，系统将自动创建 [OSS服务关联角色](https://help.aliyun.com/zh/model-studio/bailian-service-linked-role#32a41eac73z64 "")，允许阿里云百炼访问OSS资源。


> 通常秒级生效，服务高峰期可能会稍有延迟。



> [遇到“本次请求失败，尝试重新提交试试或联系管理员，错误码：10041495”怎么办](https://help.aliyun.com/zh/model-studio/data-import-instructions#bf7d28022839s "")


![image](<Base64-Image-Removed>)

3. 为目标 OSS Bucket 添加`bailian-datahub-access`标签。


> 该标签用于标记阿里云百炼可访问的 Bucket，未标记的 Bucket 阿里云百炼无法访问。


1. 访问 [OSS管理控制台](https://oss.console.aliyun.com/)，点击左侧导航栏中的 **Bucket 列表**，找到目标 Bucket。

2. 悬停鼠标在其![image](<Base64-Image-Removed>)图标上，点击 **编辑**（若未设置过标签）或 **前往编辑**。

3. 在Bucket标签页面，点击 **创建标签**（若未设置过标签）或 **设置**。

4. 点击 **标签**，添加标签名为`bailian-datahub-access`，标签值为`read`的标签，然后点击 **保存**。

      ![image](<Base64-Image-Removed>)
4. 返回 **导入数据** 页面，重新选择目标 Bucket 再尝试导入。


> **注意：阿里云百炼不支持访问 Bucket 根目录下的文件**，请选择已有的子目录或新建一个子目录供阿里云百炼访问。


1. 如下图所示，点击 **前往授权**。

![image](<Base64-Image-Removed>)

2. 在弹出的对话框中，点击 **确认授权**。若界面提示 **授权失败**、 **当前用户没有创建服务关联角色的权限**，需先授予子账号创建服务关联角色的权限。

![image](<Base64-Image-Removed>)

1. **需主账号登录** [RAM控制台](https://ram.console.aliyun.com/)，在左侧导航栏，选择**权限管理** \> **权限策略**，然后点击页面上的 **创建权限策略**。

2. 点击 **脚本编辑**，将下方提供的完整JSON策略复制并粘贴至编辑框，点击 **确定**。















      ```plaintext
      {
          "Action": [\
              "ram:CreateServiceLinkedRole"\
          ],
          "Resource": "*",
          "Effect": "Allow",
          "Condition": {
              "StringEquals": {
                  "ram:ServiceName": "datahub.sfm.aliyuncs.com"
              }
          }
      }
      ```



      ![image](<Base64-Image-Removed>)

3. 输入权限策略名称后，点击 **确定**。

      ![image](<Base64-Image-Removed>)

4. 在左侧导航栏，选择**身份管理** \> **用户**。在页面列表中找到待授权的子账号，然后点击子账号 **操作** 列的 **添加权限**。

5. 在权限策略中选择刚才创建的权限策略（自定义策略），点击 **确认新增授权**。至此，子账号拥有了创建服务关联角色的权限。

      ![image](<Base64-Image-Removed>)
3. 授权子账号通过阿里云百炼访问OSS。

1. 返回 **导入数据** 页面，点击 **前往授权**。

      ![image](<Base64-Image-Removed>)

2. 在弹出的对话框中，点击 **确认授权**，系统将自动创建 [OSS服务关联角色](https://help.aliyun.com/zh/model-studio/bailian-service-linked-role#32a41eac73z64 "")（必要条件）。


      > 通常秒级生效，服务高峰期可能会稍有延迟。



      > [遇到“本次请求失败，尝试重新提交试试或联系管理员，错误码：10041495”怎么办](https://help.aliyun.com/zh/model-studio/data-import-instructions#bf7d28022839s "")


      ![image](<Base64-Image-Removed>)
4. 为目标 OSS Bucket 添加`bailian-datahub-access`标签。


> 该标签用于标记阿里云百炼可访问的 Bucket，未标记的 Bucket 阿里云百炼无法访问。


1. 访问 [OSS管理控制台](https://oss.console.aliyun.com/)，点击左侧导航栏中的 **Bucket 列表**，找到目标Bucket。

2. 悬停鼠标在其![image](<Base64-Image-Removed>)图标上，点击 **编辑**（若未设置过标签）或 **前往编辑**。

3. 在Bucket标签页面，点击 **创建标签**（若未设置过标签）或 **设置**。

4. 点击 **标签**，添加标签名为`bailian-datahub-access`，标签值为`read`的标签，然后点击 **保存**。

      ![image](<Base64-Image-Removed>)
5. 返回 **导入数据** 页面，重新选择目标 Bucket 再尝试导入。


> **注意：阿里云百炼不支持访问 Bucket 根目录下的文件**，请选择已有的子目录或新建一个子目录供阿里云百炼访问。


## **配额与限制**

关于支持的数据格式与容量，请参见 [知识库配额与限制](https://help.aliyun.com/zh/model-studio/rag-knowledge-base-specifications "")。

## **计费说明**

- **从本地或对象存储OSS导入：** 免费。

- **从云数据库RDS或自建MySQL导入：** 将知识库与 RDS / 自建 MySQL 数据源关联，数据同步即开始。此过程通过 [EventBridge](https://help.aliyun.com/zh/eventbridge/product-overview/what-is-eventbridge "") 实现，需支付其费用，价格以 [事件流计费说明](https://help.aliyun.com/zh/eventbridge/product-overview/billing-of-event-streams "") 为准。

  - **空置费用：** 若已关联 RDS/自建 MySQL 的知识库，在一个月内无任何数据导入，将按 1 元/天收取空置费用；一旦有数据导入，或删除该知识库，空置计费停止。

  - **数据导入费用：** 按产生的事件量计费，单价为 2.8 元/百万条。

    - 单行数据大小 ≤ 64 KB，按 1 条计费；

    - 单行数据大小 \> 64 KB，按每 64 KB 拆分为多条计费。


      > 例如：导入 100 行数据，且每行都不超过 64 KB，则计费为 100 条；如其中有某一行大于 64 KB，则该行会被拆分为多条分别计费。

## **常见问题**

### **权限与安全**

- **数据导入时，遇到报错“缺少该模块的权限”，应如何处理？**






[RAM用户（子账号）](https://help.aliyun.com/zh/model-studio/permission-management-overview#24ca2dad7djzs "") 默认无法执行数据导入、创建知识库等写入类操作，需阿里云账号（主账号）为其授予`管理员`（或至少包含`应用数据-操作`与`知识库-操作`） [页面权限](https://help.aliyun.com/zh/model-studio/member-management#febd776ce5lbx "")。


### **导入OSS文件**

- **导入OSS文件遇到“10041495”报错，应如何处理？**






一般是由于主账号尚未开通对象存储服务 OSS，处理步骤：



1. 需主账号前往 [OSS管理控制台](https://oss.console.aliyun.com/)，按界面指引开通 OSS。

2. 返回阿里云百炼 **导入数据** 页面，再尝试授权。


### **导入MySQL数据**

- **私网数据源支持哪些地域的RDS与ECS实例？**






  - 华东1（杭州）

  - 华东2（上海）

  - 华南1（深圳）

  - 华南2（河源）

  - 华南3（广州）

  - 华北1（青岛）

  - 华北2（北京）

  - 华北3（张家口）

  - 华北5（呼和浩特）

  - 华北6（乌兰察布）

  - 西南1（成都）


- **我想使用RAM用户开通EventBridge服务关联角色，应如何为该RAM用户配置权限？**






1. 主账号为RAM用户配置如下三个系统策略：`AliyunBailianFullAccess`、`AliyunEventBridgeFullAccess`和`AliyunRDSReadOnlyAccess`。具体操作请参考 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。

2. 主账号为RAM用户配置 **创建服务关联角色** 系统策略。

     1. 使用主账号登录 [RAM控制台](https://ram.console.aliyun.com/)，在左侧导航栏，选择**权限管理** \> **权限策略**，然后点击页面上的 **创建权限策略**。

     2. 在 **脚本编辑** 的`Effect`、`Action`、`Resource`、`Condition`中分别输入以下脚本中的对应内容后，点击 **确定**。















        ```plaintext
        {
            "Version": "1",
            "Statement": [\
                {\
                    "Action": "ram:CreateServiceLinkedRole",\
                    "Resource": "*",\
                    "Effect": "Allow"\
                }\
            ]
        }
        ```

     3. 输入权限策略名称`CreateServiceLinkedRole`后，点击 **确定**。

     4. 在左侧导航栏，选择**身份管理** \> **用户**。从页面列表中找到待授权的子账号，然后点击子账号 **操作** 列的 **添加权限**。

     5. 从 **权限策略** 列表中，选择刚创建的权限策略（CreateServiceLinkedRole），然后点击 **确认新增授权**。至此，子账号拥有了创建服务关联角色的权限。
3. 完成以上步骤1和2后，返回 **创建数据源** 界面，使用RAM用户再尝试开通 **EventBridge服务关联角色**。


- **系统提示“数据库配置校验不通过，您选择的表数据量较大”，应如何处理？**










阿里云RDS MySQL



自建MySQL



















![image](<Base64-Image-Removed>)



上方仅为示意图，提示中的建议项和建议值会根据您表中数据量不同而不同。若无对应建议项，则无需调整。



以下步骤请使用阿里云账号（主账号）操作。



  - **如何配置本地日志保留时长：**

    1. 前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表**，然后点击包含该数据表的RDS实例。接着点击左侧导航栏中的 **备份恢复**，再点击 **备份策略** 选项卡，即可看到 **保留时长** 设置项。

       ![image](<Base64-Image-Removed>)

    2. 修改 **保留时长** 为提示中提供的建议值。
  - **如何配置wait\_timeout：**

    1. 前往 [RDS控制台](https://rdsnext.console.aliyun.com/)，点击左侧导航栏中的 **实例列表**，然后点击包含数据表的RDS实例。接着点击左侧导航栏中的 **参数设置**，再点击 **可修改参数** 选项卡，即可看到`wait_timeout`设置项。

       ![image](<Base64-Image-Removed>)

    2. 改为提示中提供的建议值。

![image](<Base64-Image-Removed>)

> 仅为示意图，提示中的建议项和建议值会根据您表中数据量不同而不同。若无对应建议项，则无需调整。

  - **如何设置本地日志保留时长：**

    - 方式一（临时生效）：通过执行SET GLOBAL命令修改`expire_logs_days`（MySQL 5.7及以下版本）或`binlog_expire_logs_seconds`（MySQL 8.0及以上版本），该修改将在下次MySQL重启后失效。






      MySQL 5.7及以下版本



      MySQL 8.0及以上版本



















      1. 执行命令：


         > 请将下方参数值 15 替换为提示中提供的建议值。
















         ```sql
         SET GLOBAL expire_logs_days = 15;
         ```

      2. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'expire_logs_days';
         ```


      1. 执行命令：


         > 请将下方参数值 1296000 替换为提示中提供的建议值。
















         ```sql
         SET GLOBAL binlog_expire_logs_seconds = 1296000;
         ```

      2. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'binlog_expire_logs_seconds';
         ```


    - 方式二（永久生效）：通过MySQL配置文件设置`expire_logs_days`（MySQL 5.7及以下版本）或`binlog_expire_logs_seconds`（MySQL 8.0及以上版本），但该方式需重启MySQL服务。






      MySQL 5.7及以下版本



      MySQL 8.0及以上版本



















      1. 以Linux系统为例，MySQL配置文件一般位于：/etc/my.cnf 或 /etc/mysql/my.cnf。若文件中已包含`expire_logs_days`，可直接修改；若不存在，请手动添加。


         > 请将下方参数值 15 替换为提示中提供的建议值。
















         ```bash
         [mysqld]
         expire_logs_days = 15
         ```

      2. 保存配置文件后，请您手动重启MySQL服务。

      3. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'expire_logs_days';
         ```


      1. 以Linux系统为例，MySQL配置文件一般位于：/etc/my.cnf 或 /etc/mysql/my.cnf。若文件中已包含`binlog_expire_logs_seconds`，可直接修改；若不存在，请手动添加。


         > 请将下方参数值 15 替换为提示中提供的建议值。
















         ```bash
         [mysqld]
         binlog_expire_logs_seconds = 1296000
         ```

      2. 保存配置文件后，请您手动重启MySQL服务。

      3. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'binlog_expire_logs_seconds';
         ```
  - **如何设置wait\_timeout：**

    - 方式一（临时生效）：通过执行SET GLOBAL命令修改`wait_timeout`（单位是秒），该修改将在下次MySQL重启后失效。

      1. 执行命令：


         > 请将下方参数值 1159200 替换为提示中提供的建议值。



         > 该命令将影响所有新建立的连接。已存在的连接不受此设置影响。
















         ```sql
         SET GLOBAL wait_timeout = 1159200;
         ```

      2. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'wait_timeout';
         ```
    - 方式二（永久生效）：通过MySQL配置文件设置`wait_timeout`（单位是秒），但该方式需重启MySQL服务。

      1. 以Linux系统为例，MySQL配置文件一般位于：/etc/my.cnf 或 /etc/mysql/my.cnf。若文件中已包含`wait_timeout`，可直接修改；若不存在，请手动添加。


         > 请将下方参数值 1159200 替换为提示中提供的`wait_timeout`建议值。
















         ```bash
         [mysqld]
         wait_timeout = 1159200
         ```

      2. 保存配置文件后，请您手动重启MySQL服务。

      3. 验证修改是否已生效，执行命令：















         ```sql
         SHOW VARIABLES LIKE 'wait_timeout';
         ```