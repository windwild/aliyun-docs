### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/)[高级命令](https://help.aliyun.com/zh/oss/developer-reference/advanced-commands/)[cp（上传、下载和拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/cp-upload-download-and-copy-files/)cp（拷贝文件）

# cp（拷贝文件）

更新时间：2026-02-06 03:49:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：cp（下载文件）](https://help.aliyun.com/zh/oss/developer-reference/cp-download-file)[下一篇：du（获取大小）](https://help.aliyun.com/zh/oss/developer-reference/du-get-size)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

命令格式

使用示例

拷贝文件（Object）是指在不改变文件内容的情况下，将同一地域下的源存储空间（Bucket）内的文件复制到目标Bucket，或者将文件复制到相同存储空间（Bucket）的其他目录。您可以通过ossutil的cp命令完成拷贝。

## 注意事项

- 要拷贝文件，您必须具有`oss:GetObject`、`oss:ListObjects`和`oss:PutObject`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 只支持拷贝对象，不支持拷贝未合并的分片。

- 默认同时复制标签和对象属性。可以使用--copy-props选项设置属性和标签的复制规则。

- 不支持跨账号或者跨区域拷贝。如果您需要跨账号或者跨地域拷贝（迁移）文件，请使用 [ossimport](https://help.aliyun.com/zh/data-online-migration/user-guide/ossimport-overview "") 或者 [在线迁移服务](https://help.aliyun.com/zh/oss/use-data-online-migration-to-migrate-data-between-accounts#task-2134221 "")。


## 命令格式

```bash
ossutil cp oss://src_bucket[/src_prefix] oss://dest_bucket[/dest_prefix] [flags]
```

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| src\_bucket | string | 源Bucket名称。 |
| src\_prefix | string | 源Bucket下的某个文件目录或指定前缀。 |
| dest\_bucket | string | 目标Bucket名称。 |
| dest\_prefix | string | 目标Bucket下的某个文件目录或指定前缀。 |
| --acl | string | 对象的访问权限。取值：<br>- private：私有。<br>  <br>- public-read：公共读。<br>  <br>- public-read-write：公共读写。<br>  <br>- default：继承Bucket。 |
| --bandwidth-limit | SizeSuffix | 用于限制网络带宽，控制数据传输的速率。最小值为1024 B/s。单位默认为B/s。<br>配置此参数时，可以根据需要为带宽值指定单位，可选单位包括B（字节）、K（千字节）、M（兆字节）和G（吉字节）。例如 50 M表示带宽限制为50 MB/s。 |
| --bigfile-threshold | SizeSuffix | 开启大文件分片上传、下载或拷贝的阈值（默认值104857600）。 |
| --cache-control | string | 指定该对象被下载时网页的缓存行为。 |
| --checkers | int | 并行运行的检查器数量（默认值为16）。 |
| --checkpoint-dir | string | 断点续传信息的指定目录（默认值`.ossutil_checkpoint/`）。 |
| --checksum | / | 仅拷贝文件大小和校验和（如果存在）不一致的源文件，仅当对象间拷贝有效。 |
| --content-disposition | string | 指定对象的展示形式。 |
| --content-encoding | string | 声明对象的编码方式。 |
| --content-type | string | 对象的内容类型。 |
| --copy-props | string | 用于设置对象间拷贝时的属性和标签复制规则，支持以下三种设置：<br>- default（默认值）：同时拷贝对象属性和标签。对象属性包括content-type、content-language、content-encoding、content-disposition、cache-control、expires和metadata（自定义元数据）。<br>  <br>- metadata：只拷贝对象属性。<br>  <br>- none：只复制数据，忽略掉对象属性和标签。 |
| -d, --dirs | string | 处理当前目录下的文件和子目录，而非递归处理所有子目录下的所有文件。 |
| --encoding-type | string | 输入的对象名或文件名的编码方式。取值：url。 |
| --end-with | string | 按字母排序，返回设定值之前的对象，包含设定值。 |
| --exclude | stringArray | 路径或文件名的排除规则。 |
| --exclude-from | stringArray | 从规则文件里读取排除规则。 |
| --expires | string | 指定缓存内容的绝对过期时间。 |
| --files-from | stringArray | 从文件中读取源文件名列表，忽略空行或注释行。 |
| --files-from-raw | stringArray | 从文件中读取源文件名列表。 |
| --filter | stringArray | 路径或文件名过滤规则。 |
| --filter-from | stringArray | 从规则文件读取过滤规则。 |
| -f, --force | / | 强制操作，不进行询问提示。 |
| --ignore-existing | / | 跳过已存在的目标文件。 |
| --include | stringArray | 路径或文件名的包含规则。 |
| --include-from | stringArray | 从规则文件里读取包含规则。 |
| -j, --job | int | 并发任务数，默认值为 3。<br>**说明**<br>仅在同时指定 `-f`、`--update`、`--size-only` 或 `--ignore-existing` 中任意一个参数时生效。 |
| --list-objects | / | 使用ListObjects接口列举对象。 |
| --max-size | SizeSuffix | 限制传输的最大文件大小，默认是字节，或单位后缀形式B\|K\|M\|G\|T\|P，1K(KiB)=1024B。 |
| --metadata | strings | 指定对象的用户元数据，使用key=value格式。 |
| --metadata-directive | string | 指定如何设置目标对象的元数据。取值：<br>- COPY<br>  <br>- REPLACE |
| --metadata-exclude | stringArray | 对象元数据的排除规则。 |
| --metadata-filter | stringArray | 对象元数据过滤规则。 |
| --metadata-filter-from | stringArray | 从规则文件读取对象元数据过滤规则。 |
| --metadata-include | stringArray | 对象元数据的包含规则。 |
| --min-age | Duration | 仅拷贝修改时间在指定时间间隔前的文件，默认单位是秒，可以使用单位后缀形式。例如 1h，表示1小时。<br>**说明**<br>`--min-age 1h` 表示仅拷贝修改时间在1小时前或更早的文件。 |
| --max-age | Duration | 仅拷贝修改时间在指定时间间隔内的文件，默认单位是秒，可以使用单位后缀形式。例如 1h，表示1小时。<br>**说明**<br>`--max-age 1h` 表示仅拷贝修改时间在1小时内的文件。 |
| --min-mtime | Time | 仅拷贝修改时间在指定时间之后的文件，时间格式：UTC时间。例如2006-01-02T15:04:05。<br>**说明**<br>`--min-mtime "2006-01-02T15:04:05"` 表示仅拷贝在 2006 年 1 月 2 日 15:04:05 之后修改的文件。 |
| --max-mtime | Time | 仅拷贝修改时间在指定时间之前的文件，时间格式：UTC时间，例如 2006-01-02T15:04:05。 |
| --min-size | SizeSuffix | 限制传输的最小文件大小，默认是字节，或单位后缀形式B\|K\|M\|G\|T\|P，1K(KiB)=1024B。 |
| --no-progress | / | 不显示进度条。 |
| --no-error-report | / | 批处理时不生成错误报告文件 |
| --output-dir | string | 指定批处理过程中生成的错误报告文件所在的目录（默认为 `ossutil_output`） |
| --page-size | int | 批量拷贝时分页列举的对象的最大值（默认值1000），取值范围1~1000。 |
| --parallel | int | 单文件内部操作的并发任务数。 |
| --part-size | SizeSuffix | 分片大小，默认情况下根据文件大小自行计算合适的分片大小值。取值范围100KiB~5GiB。 |
| -r, --recursive | / | 递归进行操作。当指定该选项时，命令会对存储空间下所有符合条件的对象进行操作，否则只对路径指定的对象进行操作。 |
| --request-payer | string | 请求的支付方式，如果为请求者付费模式，请设置该值。取值：requester。 |
| --size-only | / | 仅拷贝文件大小不一致的源文件。 |
| --start-after | string | 按字母排序，返回设定值之后的对象，不包含设定值。 |
| --storage-class | string | 对象的存储类型, 取值：<br>- Standard：标准存储。<br>  <br>- IA：低频存储。<br>  <br>- Archive：归档存储。<br>  <br>- ColdArchive：冷归档存储。<br>  <br>- DeepColdArchive：深度冷归档存储。 |
| --tagging | string | 指定对象的标签，使用key=value格式。 |
| --tagging-directive | string | 指定如何设置目标对象的标签。取值：<br>- COPY<br>  <br>- REPLACE |
| -u, --update | / | 仅拷贝源文件新于目标文件。 |
| --version-id | string | 指定对象的版本 ID（VersionId）。 |

**说明**

关于支持的全局命令行选项，请参见 [支持的全局命令行选项](https://help.aliyun.com/zh/oss/command-line-options#65785a4884d85 "")。

目标文件命名规则如下：

- 单文件复制时，如果dest\_prefix为空，则对象的名字为源文件相对路径。

- 单文件复制时，如果dest\_prefix以"/"结尾，则对象的名字为dest\_prefix + 源文件相对路径。

- 单文件复制时，如果dest\_prefix不以"/"结尾, 则与dest\_prefix保持一致。

- 批量复制时，如果dest\_prefix以"/"结尾，则对象的名字为dest\_prefix + 源文件相对路径。

- 批量复制时，如果dest\_prefix不以"/"结尾，则对象的名字为dest\_prefix + "/" +源文件相对路径。


## **使用示例**

- 拷贝单个文件















```bash
ossutil cp oss://examplebucket1/examplefile.txt oss://examplebucket1/desfolder/
```

- 拷贝增量文件



批量拷贝时，如果指定**--update**选项，只有当目标文件不存在，或源文件的最后修改时间晚于目标文件时，ossutil才会执行拷贝操作。命令如下：

















```bash
ossutil cp oss://examplebucket1/srcfolder1/ oss://examplebucket1/desfolder/ -r --update
```





该选项可用于当批量拷贝失败重传时，跳过已经拷贝成功的文件，实现增量拷贝。

- 重命名文件















```bash
ossutil cp oss://examplebucket1/examplefile.txt oss://examplebucket1/example.txt
```



通过**cp**命令重命名文件时，原文件仍存在，您可以在重命名后删除原文件。

- 修改文件对象标签















```bash
ossutil cp oss://examplebucket1/examplefile.txt oss://examplebucket1/ --tagging "abc=1&bcd=2&……"
```