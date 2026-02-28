### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)cp（上传、下载和拷贝文件）

# 上传、下载和拷贝文件

更新时间：2025-11-10 20:40:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：cors-options（检测跨域请求）](https://help.aliyun.com/zh/oss/developer-reference/cors-options)[下一篇：cp（上传文件）](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

工作机制

上传文件

下载文件

拷贝文件

应用于生产环境

并发性能调优

流量控制

后续参考

cp命令用于在本地与OSS之间，或在OSS内部传输文件或目录。该命令统一处理上传、下载和拷贝操作，并支持并发传输与断点续传。

使用cp命令前，请确保已完成 [ossutil的安装和配置](https://help.aliyun.com/zh/oss/developer-reference/install-ossutil "")。

## 注意事项

在执行任何上传、下载或拷贝操作之前，请确保您使用的访问凭证所关联的 RAM 用户或 RAM 角色拥有对目标 Bucket 和文件的相应操作权限，具体授权操作请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

## 工作机制

`ossutil cp` 命令根据源路径（source）和目标路径（destination）的类型，自动判断执行上传、下载或拷贝操作。

使用cp命令文件时，ossutil会根据文件大小自动选择不同的传输方式：

- 当文件大小小于断点续传文件的大小阈值（可通过 `--bigfile-threshold` 选项指定，默认值为 100 MB）时，直接一次性完成文件传输。

- 当文件大小大于或等于该阈值时使用 **断点续传**。若上传意外中断，已传输的部分将作为碎片（Part）临时存储在Bucket中。为避免产生存储费用，需定期清理这些碎片。可手动 [删除碎片](https://help.aliyun.com/zh/oss/developer-reference/rm#li-n3o-5sr-xg9 "")，或配置 [生命周期规则](https://help.aliyun.com/zh/oss/configure-lifecycle-rules#concept-bmx-p2f-vdb "") 自动删除。


断点续传操作失败时，ossutil会自动创建名为`.ossutil_checkpoint`的目录，并在该目录下记录checkpoint信息，断点续传成功后会删除该目录。还可以配置--checkpoint-dir参数指定断点续传记录信息所在的目录。

## 上传文件

通过 [cp（上传文件）](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6 "") 命令，可以将本地的文件、图片、视频等各类资源上传到指定的 OSS 存储空间中。

- 单个文件上传：将指定路径的文件上传到 Bucket。

- 批量上传：上传整个目录及其所有子目录和文件。

- 条件筛选：结合 `--include` 和 `--exclude` 选项，可以实现精细化的批量上传。例如，仅上传所有 `.log` 文件，或排除所有临时文件（`.tmp`）。


## 下载文件

通过 [cp（下载文件）](https://help.aliyun.com/zh/oss/developer-reference/download-objects-5 "") 命令，可以将已上传至OSS的文件、图片、视频等资源下载到本地时，支持下载多个文件、下载时限速，或者在已开启版本控制的Bucket内下载指定版本文件。

- 单个文件下载：下载指定文件。

- 批量下载：下载 Bucket 中的整个目录结构到本地。

- 下载指定版本：如果您的 Bucket 开启了版本控制，可以下载文件的特定历史版本。


## 拷贝文件

通过 [cp（拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/copy-objects-4 "") 命令，在不改变文件内容的情况下，将同地域下的Bucket内的文件复制到目标Bucket，或者复制到当前Bucket的其他目录。

- 跨 Bucket 拷贝：将同一地域（Region）下的一个 Bucket 内的文件，复制到另一个 Bucket。

- Bucket 内拷贝（移动/重命名）：将文件从 Bucket 内的一个目录复制到另一个目录。这常被用作实现文件的“移动”或“重命名”操作（本质是拷贝+删除原文件）。


`ossutil cp` 命令不直接支持跨地域拷贝。如果需要在不同地域的Bucket间拷贝文件，建议使用 [跨区域复制](https://help.aliyun.com/zh/oss/user-guide/cross-region-replication-overview/ "") 功能。

## 应用于生产环境

### **并发性能调优**

当默认并发数达不到用户的性能要求时，可以调整**-j，--jobs**和**--parallel**选项来升降性能。默认情况下，ossutil根据文件大小来计算parallel。当批量传输大文件时，实际的并发数为jobs数乘以parallel数。

- 若执行命令的ECS或服务器的资源（网络、内存、CPU）有限，建议将并发数调低（如100以下）。如果资源未占满，可适当增加并发数。

- 并发数过高可能因线程切换开销和资源竞争导致性能下降，甚至引发EOF错误。请根据机器的实际资源状况调整**-j，--jobs**和**--parallel**。进行性能压测时，建议从较低的并发数开始，逐步增加以找到最佳值。


### **流量控制**

使用 `--maxupspeed` 或 `--maxdownspeed` 参数可限制上传或下载的速率，以避免占用过多带宽。

## 后续参考

- [cp（上传文件）](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6 "")

- [cp（下载文件）](https://help.aliyun.com/zh/oss/developer-reference/download-objects-5 "")

- [cp（拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/copy-objects-4 "")