### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[开始使用](https://help.aliyun.com/zh/oss/user-guide/product-introduction/)功能特性

# 功能特性

更新时间：2025-01-12 22:06:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：什么是对象存储OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss)[下一篇：选型指导](https://help.aliyun.com/zh/oss/user-guide/selection-guidance-selection-guidance)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据管理

数据安全和保护能力

数据处理

常用工具

部署形态

## **数据管理**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能集** | **功能** | **功能描述** | **参考文档** |
| 存储类型 | 标准存储 | 提供高可靠、高可用、高性能的对象存储服务，面向温热数据，适合支持频繁的数据访问。 | [标准存储](https://help.aliyun.com/zh/oss/user-guide/overview-53/ "") |
| 低频访问存储 | 提供高持久性、较低存储成本的对象存储服务。有最小计量单位（64 KB）和最低存储时间（30天）的要求。支持数据实时访问，访问数据时会产生数据取回费用，适用于较低访问频率（平均每月访问频率1到2次）的业务场景。 | [低频访问存储](https://help.aliyun.com/zh/oss/user-guide/overview-53/ "") |
| 归档存储 | 提供高持久性、更低存储成本的对象存储服务。有最小计量单位（64 KB）和最低存储时间（60天）要求。数据需解冻（约1分钟）后访问，解冻会产生数据取回费用。适用于数据长期保存的业务场景，例如档案数据、医疗影像、科学资料、影视素材等。 | [归档存储](https://help.aliyun.com/zh/oss/user-guide/overview-53/ "") |
| 冷归档存储 | 提供高持久性、比归档存储的存储成本更低的对象存储服务。有最小计量单位（64 KB）和最低存储时间（180天）的要求。数据需解冻后访问，解冻时间根据数据大小和选择的解冻模式决定，解冻会产生数据取回费用以及取回请求费用。适用于需要超长时间存放的冷数据。 | [冷归档存储](https://help.aliyun.com/zh/oss/user-guide/overview-53/ "") |
| 深度冷归档存储 | 提供高持久性、比冷归档存储成本更低的对象存储服务。有最小计量单位（64 KB）和最低存储时间（180天）的要求。数据需解冻后访问，解冻时间根据数据大小和选择的解冻模式决定，解冻会产生数据取回费用以及取回请求费用。存储成本最低，但需要较长时间的解冻。 | [深度冷归档存储](https://help.aliyun.com/zh/oss/user-guide/overview-53/ "") |
| 存储空间管理（Bucket） | 镜像回源 | 配置了镜像回源规则后，当请求者访问Bucket中一个不存在的Object时，OSS会向回源规则指定的源站获取这个文件。在获取到目标文件后，OSS会将文件返回给请求者并存入Bucket。 | [镜像回源](https://help.aliyun.com/zh/oss/back-to-origin-configuration-overview "") |
| 静态网站托管 | OSS支持静态网站托管功能，您可以将您的存储空间配置成静态网站托管模式，并通过存储空间域名访问该静态网页。 | - |
| 传输加速 | OSS支持传输加速服务，可优化互联网传输链路和协议栈，大幅减少数据远距离传输超时的比例，极大地提升用户上传和下载体验。 | [传输加速](https://help.aliyun.com/zh/oss/user-guide/transfer-acceleration "") |
| 创建存储空间 | 在上传文件（Object）到OSS之前，您需要创建一个用于存储文件的存储空间（Bucket）。存储空间具有各种配置属性，包括地域、访问权限、存储类型等。您可以根据实际需求，创建不同类型的存储空间来存储不同的数据。 | [创建存储空间](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4 "") |
| 存储空间清单 | OSS支持清单功能，您可以使用存储空间清单功能导出指定对象的元数据信息，如文件大小、加密状态等。 | [存储空间清单](https://help.aliyun.com/zh/oss/user-guide/bucket-inventory#concept-2381539 "") |
| 归档直读 | 归档直读是指直接访问归档存储类型的文件，而无需先对其解冻。归档直读适用于实时读取极低频访问数据的场景。 | [归档直读](https://help.aliyun.com/zh/oss/user-guide/archive-direct-reading "") |
| 资源组 | 资源组是一种基于资源的权限管理方式。您可以根据不同的业务需求对存储空间（Bucket）进行分组，为不同的资源组设置不同的访问权限，实现资源组范围内的权限管理。 | [资源组](https://help.aliyun.com/zh/oss/user-guide/configure-a-resource-group "") |
| 请求者付费 | 请求者付费模式是指由请求者支付访问Bucket内数据时产生的费用，而Bucket拥有者仅支付存储费用。当您希望共享数据，但又不希望支付因共享数据产生的额外费用时，您可以开启此功能。 | [请求者付费](https://help.aliyun.com/zh/oss/user-guide/enable-pay-by-requester-1 "") |
| 删除存储空间 | 当您不再需要保留某个存储空间时，可将其删除，以免产生额外费用。 | [删除存储空间](https://help.aliyun.com/zh/oss/user-guide/delete-buckets "") |
| 存储空间标签 | 您可以通过Bucket的标签功能， 对Bucket进行分类管理。例如通过不同的标签来标记不同用途的Bucket，对拥有指定标签的Bucket设置访问权限等。 | [存储空间标签](https://help.aliyun.com/zh/oss/user-guide/manage-bucket-tags "") |
| 对象管理（Object） | 对象标签 | OSS支持使用标签对Bucket中的Object进行分类，您可以针对同标签的Object设置生命周期规则、访问权限等。 | [对象标签](https://help.aliyun.com/zh/oss/user-guide/object-tagging-8 "") |
| 上传文件 | 创建存储空间后，您可以通过多种上传方式将任意类型文件上传到该存储空间。 | [上传文件](https://help.aliyun.com/zh/oss/user-guide/upload-objects-to-oss/ "") |
| 下载文件 | 文件上传至存储空间后，您可以通过多种下载方式将文件下载至浏览器默认路径或本地指定路径。 | [下载文件](https://help.aliyun.com/zh/oss/user-guide/download-files/ "") |
| 列举文件 | Bucket内的Object默认按照字母序排列。您可以结合实际场景列举当前Bucket的所有Object、指定前缀的Object、指定个数的Object等。 | [列举文件](https://help.aliyun.com/zh/oss/user-guide/list-objects-18 "") |
| 删除文件 | OSS支持一次删除单个或者多个文件、碎片等。您可以定期删除过期文件，节省您的存储空间。 | [删除文件](https://help.aliyun.com/zh/oss/user-guide/delete-objects-18 "") |
| 拷贝文件 | 拷贝文件是指在不改变文件内容的情况下，将同一地域下的源Bucket内的文件复制到目标Bucket。 | [拷贝文件](https://help.aliyun.com/zh/oss/user-guide/copy-objects-16 "") |
| 解冻文件 | 归档存储、冷归档存储或者深度冷归档存储类型的Object需要解冻（Restore）之后才能读取。 | [解冻文件](https://help.aliyun.com/zh/oss/user-guide/restore-objects-for-access "") |
| 重命名文件 | OSS不支持直接对Object进行重命名。如果您需要在同一个Bucket内对Object进行重命名，您可以通过CopyObject接口将源Object拷贝至目标Object，然后通过DeleteObject接口删除源Object。 | [重命名文件](https://help.aliyun.com/zh/oss/user-guide/rename-objects "") |
| 分享文件 | 文件上传至存储空间后，您可以将文件URL分享给第三方，供其下载或预览。 | [分享文件](https://help.aliyun.com/zh/oss/user-guide/share-objects-by-url "") |
| 搜索文件 | OSS支持文件和文件夹搜索功能，您可以在存储空间中快速查找目标文件。 | [搜索文件](https://help.aliyun.com/zh/oss/user-guide/search-for-objects "") |
| 软链接 | 软链接功能用于快速访问Bucket内的常用Object。设置软链接后，您可以使用类似于Windows的快捷方式，通过软链接文件快速打开Object。 | [软链接](https://help.aliyun.com/zh/oss/user-guide/configure-symbolic-links "") |
| 管理文件元信息 | OSS存储的文件（Object）信息包含Key、Data和Object Meta。Object Meta是对文件的属性描述，包括HTTP标准属性（HTTP Header）和用户自定义元数据（User Meta）两种。您可以通过设置HTTP标准属性来自定义HTTP请求的策略，例如文件（Object）缓存策略、强制下载策略等。您还可以通过设置用户自定义元数据来标识Object的用途或属性等。 | [管理文件元信息](https://help.aliyun.com/zh/oss/user-guide/manage-object-metadata-10/ "") |
| 管理目录 | 与传统文件系统中的层级结构不同，OSS内部使用扁平结构存储数据。即所有数据均以Object的形式保存在Bucket中。为方便您对Object进行分组并简化权限管理，您可以创建目录，然后将目标Object存放至指定目录。当您不需要保留该目录时，还可以通过多种方式删除目录。 | [管理目录](https://help.aliyun.com/zh/oss/user-guide/manage-directories "") |
| 数据索引 | 如果您希望从Bucket存储的海量Object中快速查找与指定的Object名称、ETag、存储类型、大小、最后修改时间等条件匹配的Object，您可以使用数据索引功能。通过数据索引功能，您可以在查找目标Object时指定过滤条件，对查询结果按需选择排序和聚合的方式，提升查找目标Object的效率。 | [数据索引](https://help.aliyun.com/zh/oss/user-guide/scalar-retrieval/ "") |
| 通过云存储网关挂载OSS | 通过云存储网关挂载OSS，您可以将OSS映射为一个共享的文件存储系统，实现多个用户在不同地点和设备上共享访问OSS数据。挂载完成后，您可以像使用本地文件夹和磁盘一样操作OSS资源。 | [通过云存储网关挂载OSS](https://help.aliyun.com/zh/oss/user-guide/use-csg-to-attach-oss-buckets-to-ecs-instances "") |

## **数据安全和保护能力**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能集** | **功能** | **功能描述** | **参考文档** |
| 访问控制 | Bucket ACL | 当您希望粗粒度地控制某个Bucket的读写权限，即Bucket内的所有Object均为统一的读写权限时，您可以选择使用Bucket ACL的方式。Bucket ACL包含公共读、公共读写和私有。您可以在创建Bucket时设置Bucket ACL，也可以在创建Bucket后根据自身的业务需求修改Bucket ACL。 | [Bucket ACL](https://help.aliyun.com/zh/oss/user-guide/bucket-acl-2 "") |
| Object ACL | 当您希望针对Bucket中的某个具体的Object设置特定的读写权限时，可以使用Object ACL。通过设置Object ACL，可以精确控制某个Object的访问权限，且不影响Bucket中其他Object的访问权限。Object ACL包含公共读、公共读写、私有。您可以在上传Object时设置ACL，也可以在Object上传后根据自己的业务需求随时修改ACL。 | [Object ACL](https://help.aliyun.com/zh/oss/user-guide/object-acl "") |
| Bucket Policy | OSS支持面向资源的授权方式，允许在Bucket级别而不是用户级别设置权限策略。使用Bucket Policy可以授权当前云账号或者其他阿里云账号下单个或多个RAM用户、RAM角色等访问Bucket内的指定资源。Bucket Policy除提供策略语法的授权方式以外，还提供了图形化界面的授权方式，助力您结合业务场景，快速完成授权。 | [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") |
| 防盗链 | 通过在OSS中配置基于请求标头Referer的访问规则，可以阻止某些Referer访问您的OSS文件，从而防止其他网站盗用您的文件，并避免由此引起的不必要的流量费用增加。 | [防盗链](https://help.aliyun.com/zh/oss/user-guide/hotlink-protection/ "") |
| 跨域资源共享CORS | 默认情况下，由于同源策略（Same-Origin Policy）的限制，网页浏览器在执行JavaScript时会限制跨域请求，只允许请求同一域或源的资源。跨域资源共享CORS（Cross-Origin Resource Sharing）简称跨域访问，允许网页浏览器向不同域或源的服务器发起跨域请求。通过跨域设置可以实现在您的网站上使用JavaScript请求非同源的OSS对象链接而不会出现跨域问题。 | [跨域资源共享CORS](https://help.aliyun.com/zh/oss/user-guide/configure-cross-origin-resource-sharing/ "") |
| 数据保护 | 同城冗余 | OSS采用多可用区（AZ）内的数据冗余存储机制，将用户的数据冗余存储在同一地域（Region）的多个可用区。当某个可用区不可用时，仍然能够保障数据的正常访问。OSS同城冗余存储提供99.9999999999%（12个9）的数据设计持久性。 | [同城冗余](https://help.aliyun.com/zh/oss/user-guide/zrs "") |
| 跨区域复制 | 跨区域复制（Cross-Region Replication）是指将相同或者不同账号某个地域下源存储空间（Bucket）中Object的创建、更新和删除等操作自动、异步（近实时）地复制到另一个地域下的目标Bucket，以实现合规、降低延时、确保安全性和可用性等目的。 | - |
| 同区域复制 | 同区域复制（Same-Region Replication）是指将源存储空间（Bucket）中的文件（Object）的创建、更新和删除等操作自动、异步（近实时）地复制到相同地域下的目标Bucket。 | [同区域复制](https://help.aliyun.com/zh/oss/user-guide/srr/ "") |
| 版本控制 | 版本控制是针对Bucket级别的数据保护功能。开启版本控制后，针对数据的覆盖和删除操作将会以历史版本的形式保存下来。您在错误覆盖或删除Object后，能够将存储在Bucket中的Object恢复至任意时刻的历史版本。 | - |
| 数据复制时间控制（RTC） | OSS数据复制时间控制RTC（Replication Time Control）可满足您在跨区域复制数据的合规性要求或者业务需求。开启RTC后，OSS会在几秒内复制您上传到OSS的大多数对象（Object），并在10分钟内复制99.99%的对象。此外，RTC功能还提供了数据复制的准实时监控，方便您查看复制任务的各项指标。 | [数据复制时间控制（RTC）](https://help.aliyun.com/zh/oss/user-guide/rtc "") |
| 定时备份 | 为了避免因误删除、误修改、误覆盖操作等情况引起的数据丢失或受损，您可以通过云备份对存储空间（Bucket）内的文件（Object）进行定期备份。当您的Object意外丢失时，可通过云备份进行恢复。云备份对支持配置灵活备份策略，将数据备份至云端，您可以随时查看和恢复数据。 | [定时备份](https://help.aliyun.com/zh/oss/user-guide/configure-scheduled-backup "") |
| 安全合规 | 服务器端加密 | 当您在设置了服务器端加密的Bucket中上传Object时，OSS对收到的文件进行加密，再将得到的加密文件持久化保存。当您通过GetObject请求下载文件时，OSS自动将加密文件解密后返回给用户，并在响应头中返回x-oss-server-side-encryption，用于声明该文件进行了服务器端加密。 | [服务器端加密](https://help.aliyun.com/zh/oss/user-guide/server-side-encryption-8 "") |
| 客户端加密 | OSS客户端加密是在数据上传至OSS之前，由用户在本地对数据进行加密处理，确保只有密钥持有者才能解密数据，增强数据在传输和存储过程中的安全性。 | [客户端加密](https://help.aliyun.com/zh/oss/user-guide/client-side-encryption "") |
| 合规保留策略 | OSS保留策略具有WORM（Write Once Read Many）特性，满足用户以不可删除、不可篡改方式保存和使用数据。如果您希望指定时间内任何用户（包括资源拥有者）均不能修改和删除OSS某个Bucket中的Object，您可以选择为Bucket配置保留策略。在保留策略指定的Object保留时间到期之前，仅支持在Bucket中上传和读取Object。Object保留时间到期后允许修改或删除。 | [合规保留策略](https://help.aliyun.com/zh/oss/user-guide/oss-retention-policies "") |
| 敏感数据保护 | 敏感数据保护是一款识别、分类、分级和保护Bucket中敏感数据的原生服务，可满足数据安全、个人信息保护等相关法规的合规要求。 | [敏感数据保护](https://help.aliyun.com/zh/oss/user-guide/sddp "") |
| OSS高防 | OSS高防是OSS结合DDoS高防推出的DDoS攻击代理防护服务。当受保护的Bucket遭受大流量攻击时，OSS高防会将攻击流量牵引至高防集群进行清洗，并将正常访问流量回源到目标Bucket，确保业务的正常进行。 | [OSS高防](https://help.aliyun.com/zh/oss/user-guide/oss-ddos-protection "") |
| 日志转存 | 访问OSS的过程中会产生大量的访问日志。您可以通过日志转存功能将这些日志按照固定命名规则，以小时为单位生成日志文件写入您指定的Bucket。对于已存储的日志，您可以通过阿里云日志服务或搭建Spark集群等方式进行分析。 | [日志转存](https://help.aliyun.com/zh/oss/user-guide/logging "") |
| 实时日志查询 | 访问OSS的过程中会产生大量的访问日志。实时日志查询功能将OSS与日志服务SLS相结合，允许您在OSS控制台直接查询OSS的访问日志，帮助您完成OSS访问的操作审计、访问统计、异常事件回溯和问题定位等工作，提升您的工作效率并更好地帮助您基于数据进行决策。 | [实时日志查询](https://help.aliyun.com/zh/oss/user-guide/real-time-log-query/ "") |
| OSS 内容安全功能 | 如果您希望检测OSS存储的图片是否包含违规内容，例如图片内容是否涉黄、涉政、涉恐、涉暴等，您可以选择OSS提供的内容安全检测服务。OSS内容安全服务具有通用性强、易用性高、价格实惠的特点。通过OSS内容安全检测服务可以帮助您提高图片内容审核效率，及时发现并处理违规图片，提升内容安全和用户体验。 | [内容安全检测](https://help.aliyun.com/zh/oss/user-guide/check-content-security "") |

## **数据处理**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能集** | **功能** | **功能描述** | **参考文档** |
| 数据湖 | OSS Select | 您可以使用SelectObject对目标文件执行SQL语句，返回执行结果。 | [OSS Select](https://help.aliyun.com/zh/oss/user-guide/query-objects "") |
| OSS加速器 | 随着AI、数据仓库、大数据分析等业务发展，越来越多运行在OSS上的业务对于数据的访问延迟和吞吐量有了更高的要求。OSS推出加速器功能，可以将OSS中的热点Object缓存在NVMe SSD高性能存储介质上，提供毫秒级低延迟和高吞吐量的数据访问服务。 | - |
| OSS-HDFS服务 | OSS-HDFS服务（JindoFS服务）是一个云原生数据湖存储功能。基于统一的元数据管理能力，完全兼容HDFS文件系统接口，满足大数据和AI等领域的数据湖计算场景。 | [OSS-HDFS服务](https://help.aliyun.com/zh/oss/user-guide/oss-hdfs/ "") |
| 数据处理 | 图片处理 | 针对OSS内存储的图片文件，您可以在GetObject请求中携带图片处理参数对图片文件进行处理。例如添加图片水印、转换格式等。 | - |
| ZIP包解压 | 当您需要批量上传文件、按特定目录结构上传文件、上传完整的文件或对文件快速进行资源分发时，可以配置解压规则，上传ZIP文件到OSS指定路径，触发函数计算自动解压，并将解压后内容保存回OSS。 | [ZIP包解压](https://help.aliyun.com/zh/oss/user-guide/zip-package-decompression "") |
| 智能媒体 | OSS与智能媒体管理（IMM）深度结合，支持媒体处理、文档处理等丰富的数据分析处理操作。 | [智能媒体](https://help.aliyun.com/zh/oss/user-guide/intelligent-media-management-imm/ "") |
| 事件通知 | 当您需要对OSS中的文件变动进行实时处理、同步、监听、业务触发、日志记录等操作时，您可以通过设置OSS的事件通知规则，自定义关注的文件，并及时收到相关通知。 | [事件通知](https://help.aliyun.com/zh/oss/user-guide/event-notifications/ "") |
| OSS 对象 FC（Object FC） | 基于OSS 对象 FC（Object FC），用户可以在发送OSS GetObject等请求时自动触发函数计算服务，并将处理后的数据结果进行返回。OSS 对象 FC（Object FC）帮助用户在保持对象存储语义的情况下，无缝集成自定义的数据处理能力。 | [对象FC接入点](https://help.aliyun.com/zh/oss/user-guide/create-object-fc-access-point "") |

## **常用工具**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能集** | **功能** | **功能描述** | **参考文档** |
| 客户端管理 | 命令行工具ossutil | ossutil支持通过Windows、Linux和macOS系统以命令行方式管理OSS数据。 | - |
| 图形化工具ossbrowser | ossbrowser 2.0是一款用于管理OSS的免费图形化桌面客户端。该客户端支持Windows、macOS和Linux操作系统，提供直观的图形用户界面，使您能够高效地执行各种操作，包括文件的上传、下载和删除。由于其本地部署特性，ossbrowser 2.0可在您的设备上直接运行，确保操作的流畅性。 | [图形化工具ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview/ "") |
| 访问接入 | ossfs | 对于原来需要直接读写本地文件的应用程序，为了让应用程序能在不作修改的情况下直接访问对象存储OSS的数据，您可以使用ossfs将OSS的Bucket挂载到Linux系统中，并将其映射到本地目录，从而能够像处理本地文件那样直接操作OSS中的数据，实现文件共享。 | - |
| ossftp | ossftp是一个特殊的FTP server，可以将对文件、文件夹的操作映射为对OSS的操作，使您可以基于FTP协议来管理存储在OSS上的文件。 | - |
| OSS Connector | 提供计算生态直接读写OSS的能力 | [OSS Connector](https://help.aliyun.com/zh/oss/developer-reference/oss-connector-overview/ "") |

## **部署形态**

|     |     |     |     |
| --- | --- | --- | --- |
| **功能集** | **功能** | **功能描述** | **参考文档** |
| 部署形态 | OSS ON云盒 | OSS ON云盒为云盒（CloudBox）产品提供了非结构化数据本地存储、本地访问、以及本地处理的能力。您可以在OSS ON云盒中创建Bucket，并使用与公共云一致的API、SDK访问云盒中的OSS。 | - |