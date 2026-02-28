### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)access-monitor（访问跟踪）

# access-monitor（访问跟踪）

更新时间：2025-03-12 23:11:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

设置访问跟踪

获取访问跟踪配置

后续操作

如果您希望配置基于最后一次访问时间（Last Access Time）策略的生命周期规则来自动监测Bucket中Object的访问模式并识别冷数据，然后将识别出来的冷数据进行存储类型转换，最终降低存储成本。您需要先通过access-monitor命令为Bucket开启访问跟踪。

## **注意事项**

- 要设置访问跟踪配置，您必须具有`oss:PutBucketAccessMonitor`权限；要获取访问跟踪配置，您必须具有`oss:GetBucketAccessMonitor`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。

- 仅1.7.15及以上版本支持access-monitor命令。


## 设置访问跟踪

- 命令格式















```bash
ossutil access-monitor --method put oss://bucketname/ local_xml_file
```



参数说明如下：




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| bucketname | 待设置访问跟踪状态的Bucket名称。 |
| local\_xml\_file | 用于设置访问跟踪状态的本地文件名称，例如`config.xml`。 |

- 使用示例

1. 在本地XML文件中配置开启或关闭访问跟踪。

     - 开启访问跟踪状态















       ```xml
       <?xml version="1.0" encoding="UTF-8"?>
       <AccessMonitorConfiguration>
           <Status>Enabled</Status>
       </AccessMonitorConfiguration>
       ```

     - 关闭访问跟踪状态















       ```xml
       <?xml version="1.0" encoding="UTF-8"?>
       <AccessMonitorConfiguration>
           <Status>Disabled</Status>
       </AccessMonitorConfiguration>
       ```
2. 通过以下示例为examplebucket设置访问跟踪状态。















     ```bash
     ossutil access-monitor --method put oss://examplebucket/ config.xml
     ```



     输出结果如下：















     ```bash
     0.299514(s) elapsed
     ```

## 获取访问跟踪配置

- 命令格式















```bash
ossutil access-monitor --method get oss://bucketname [local_xml_file]
```



参数说明如下：




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| bucketname | 待获取访问跟踪状态的Bucket名称。 |
| local\_xml\_file | 用于存放访问跟踪状态的本地文件名称，例如`local.xml`。如果未指定此参数，访问跟踪状态结果将直接输出到屏幕。 |

- 使用示例

  - 以下示例用于获取examplebucket的访问跟踪状态，并将结果输出到屏幕上。















    ```bash
    ossutil access-monitor --method get oss://examplebucket
    ```



    输出结果如下：















    ```bash
    <?xml version="1.0" encoding="UTF-8"?>
    <AccessMonitorConfiguration>
      <Status>Enabled</Status>
    </AccessMonitorConfiguration>

    0.154689(s) elapsed
    ```

  - 以下示例用于获取examplebucket的访问跟踪状态，并将结果写入local.xml文件。















    ```bash
    ossutil access-monitor --method get oss://examplebucket/ local.xml
    ```



    输出结果如下：

    - 屏幕显示















      ```bash
      0.214483(s) elapsed
      ```

    - 文件内容















      ```bash
      <?xml version="1.0" encoding="UTF-8"?>
      <AccessMonitorConfiguration>
        <Status>Enabled</Status>
      </AccessMonitorConfiguration>
      ```

## **后续操作**

开启访问跟踪后，您需要配置基于最后一次访问时间的生命周期规则对冷数据存储类型进行转换，最终降低存储成本。具体操作，请参见 [lifecycle（生命周期）](https://help.aliyun.com/zh/oss/developer-reference/lifecycle "")。