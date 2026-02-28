### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/) [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/) [最佳实践](https://help.aliyun.com/zh/oss/developer-reference/best-practices-for-ossutil2-0/) 基于对象元数据进行筛选

# 基于对象元数据进行筛选

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：下载大文件到本地硬盘](https://help.aliyun.com/zh/oss/developer-reference/breakpoint-file-hard-drive)[下一篇：批量解冻文件](https://help.aliyun.com/zh/oss/developer-reference/restore-files-using-ossutil2-0)

该文章对您有帮助吗？

反馈

本文将详细为您介绍如何通过ossutil根据对象的元数据进行过滤，筛选出您需要的内容。

## **使用场景**

对于包含大量对象（Object）的Bucket，直接浏览或处理会非常耗时。因此，ossutil 2.0提供了一系列高效的基于元数据进行过滤的选项，允许用户根据特定元数据属性对Object进行精准筛选。

## **前提条件**

- 已[开通OSS服务](https://oss.console.aliyun.com/overview)。

- 已 [创建Bucket](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4 "")。

- 已 [安装ossutil 2.0命令行工具](https://help.aliyun.com/zh/oss/install-ossutil2 "")。


## **元数据过滤**

ossutil 2.0 支持基于Object元数据的精细化操作筛选，这一功能主要适用于多个高级命令，如 `ls`（列举资源）、`cp`（上传、下载、拷贝文件）和 `rm`（删除）。用户可以根据对象的特定元数据属性（如对象类型）进行筛选，提高效率。

## **参数说明**

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| --metadata-include | stringArray | 指定需包含的元数据规则，即仅显示符合这些规则的Object。 |
| --metadata-exclude | stringArray | 指定需排除的元数据规则，符合条件的Object将不被显示。 |
| --metadata-filter | stringArray | 直接定义元数据过滤规则，支持更灵活的匹配逻辑。 |
| --metadata-filter-from | stringArray | 从外部文件读取元数据过滤规则，便于复杂规则的管理和复用。 |

- 使用`--metadata-include`时，自动隐式追加一条排除所有其他类型文件的规则`- **`至列表末尾。

- 使用` --metadata-filter "+ 规则"` 添加包含规则时，不会自动添加所有的排除规则，即 `--metadata-include "规则"`等于 `--metadata-filter "+ 规则"`+`--metadata-filter "- **"`。例如，若要精确筛选出bucket中的所有JPEG图像文件，需要设置为`--metadata-filter "+ content-type=image/jpeg" --metadata-filter "- **"`

- 在处理多文件规则列表时，文件顺序遵循从左到右的规则执行，而每个文件内部的规则是按照自上而下顺序执行，并忽略空行及以`#`或`;`开始的注释行。

- 匹配到首个规则后，会停止后续的规则检查。


## **支持的元数据类型**

- 存储类型：采用x-oss-storage-class=value，value取值Standard、IA、Archive、ColdArchive、DeepColdArchive。

- Object类型：采用x-oss-object-type=value，value取值Normal、Multipart、Appendable、Symlink。

- 解冻恢复状态：采用x-oss-restore=value，value根据实际值填写。

- Content-Type：采用 content-type=value，value根据实际值填写。

- 用户自定义元数据：用户自定义元数据应遵循规范格式`x-oss-meta-aaa=value`，其中`x-oss-meta-`是固定前缀，表示用户自定义元数据的开始，而`aaa`部分允许您根据需求自定义键名，value根据实际值填写。例如`x-oss-meta-location:hangzhou`。


## **示例**

## 筛选特定存储类型的对象

- 以下命令用于筛选`examplebucket`中存储类型为标准存储的对象。


```bash
ossutil ls oss://examplebucket --metadata-include "x-oss-storage-class=Standard"
```

- 以下命令用于筛选`examplebucket`中归档，冷归档和深度冷归档类型的对象。


```bash
ossutil ls oss://examplebucket --metadata-include "x-oss-storage-class=*Archive"
```


## 筛选特定解冻状态的对象

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **示例值** | **描述** |
| x-oss-restore | 字符串 | - 正在解冻：ongoing-request="true"<br>  <br>- 已解冻：ongoing-request="false", expiry-date="Thu, 04 Jan 2024 03:28:54 GMT" | 您可以调用`HeadObject`接口并检查返回头`x-oss-restore`来获取解冻状态信息<br>- 如果没有进行解冻操作，或者解冻操作已经超时，那么`x-oss-restore`字段不会返回。<br>  <br>- 如果进行了解冻操作，但解冻未完成，`x-oss-restore`字段会显示`ongoing-request="true"`。<br>  <br>- 如果进行了解冻操作，且解冻完成，`x-oss-restore`字段将会显示`ongoing-request="false"`，并且会包含一个`expiry-date`，它表示对象可读状态的截止时间。 |

- 以下示例用于筛选`examplebucket`中正处于解冻状态的对象，其中\*\*标识用来匹配任何时间。


```bash
ossutil ls oss://examplebucket --metadata-include "x-oss-restore=ongoing-request=\"true\"**"
```

- 以下示例用于筛选`examplebucket`中已经解冻完成的对象，其中\*\*标识用来匹配任何时间。


```bash
ossutil ls oss://examplebucket --metadata-include "x-oss-restore=ongoing-request=\"false\"**"
```


## 筛选特定元数据属性的对象

- 以下命令用于筛选`examplebucket`中所有JPEG格式的图片文件，以便进行特定的操作或数据分析：


```bash
ossutil ls oss://examplebucket --metadata-include "content-type=image/jpeg"
```

- 以下命令用于筛选`examplebucket`中所有txt格式的文件，其后的`*5.txt`规则实际上不会产生额外效果：


```bash
ossutil ls oss://examplebucket --metadata-include "*.txt"  --metadata-include "*5.txt"
```


## 筛选特定格式的对象

以下命令用于筛选`examplebucket`中所有JPEG格式的图片文件。使用`--metadata-filter`参数，并结合`+`和`-`符号来指定包含和排除条件。将列出存储桶`examplebucket`中所有`Content-Type`为`image/jpeg`的文件，而其他类型的文件将被排除在外。

```bash
ossutil ls oss://examplebucket --metadata-filter "+ content-type=image/jpeg" --metadata-filter "- **"
```

## 通过规则文件实现复杂条件筛选

当过滤条件较为复杂或者需要同时应用多个不同的过滤规则时，可以预先创建规则文件进行筛选。

以下规则文件`metadata_filters.txt`用于筛选出存储类型为标准存储的所有JPEG图片：

```plaintext
# rules file: metadata_filters.txt
+ content-type=image/jpeg
+ x-oss-storage-class=Standard
- **
```

使用`--metadata-filter-from`选项调用该规则文件来进行筛选：

```bash
ossutil ls oss://examplebucket --metadata-filter-from metadata_filters.txt
```