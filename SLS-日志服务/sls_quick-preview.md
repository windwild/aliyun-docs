### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/) [数据处理](https://help.aliyun.com/zh/sls/data-processing-sls/) [数据写入后处理（数据加工）](https://help.aliyun.com/zh/sls/sls-data-processing/) [数据加工（旧版）](https://help.aliyun.com/zh/sls/data-transformation/) [预览调试](https://help.aliyun.com/zh/sls/preview-mode-overview/) 快速预览

# 快速预览

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：预览调试](https://help.aliyun.com/zh/sls/preview-mode-overview/)[下一篇：高级预览](https://help.aliyun.com/zh/sls/advanced-preview)

该文章对您有帮助吗？

反馈

快速预览可免费、快速检验数据加工脚本语法正确性，验证加工语句的输出结果是否符合预期。本文介绍快速预览的操作步骤及示例。

## 前提条件

已采集数据。具体操作，请参见 [数据采集](https://help.aliyun.com/zh/sls/data-collection-overview#concept-ikm-ql5-vdb "")。

## 操作步骤

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。

2. 进入数据加工页面。

1. 在Project列表区域，单击目标Project。

2. 在**日志存储** \> **日志库**页签中，单击目标Logstore。

3. 在查询和分析页面，单击 **数据加工**。
3. 在页面右上角，选择数据的时间范围。



选择时间范围后，请确认 **原始日志** 页签中存在日志。

4. 在编辑框中，输入数据加工语句。



加工语句的语法请参见 [数据加工语法](https://help.aliyun.com/zh/sls/language-introduction#concept-1130584 "")。









**说明**

编辑框中的加工语句支持注释，您可以使用此功能逐行调试。

5. 预览数据。

1. 在页面右上角，单击 **快速**。

2. 在页面下方，单击 **测试数据**。

3. 在 **测试数据** 页签中，输入测试数据。



      测试数据包括基础数据和维表数据。![数据](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8546983261/p132513.png)



      - 在 **数据** 页签中设置测试数据。

        您可以在 **原始日志** 页签中，找到一条目标日志，单击 **加入测试数据**，将该日志加入到测试数据中。您也可以手动输入一条测试数据。







        **说明**

        - 单次预览的测试数据大小不超过1 MB。

        - 多条测试数据之间用空行分隔。

        - 跨行字段值使用Markdown编辑格式，通过`````````，识别整个字段。

        - 在 **数据** 页签中配设置的测试数据可以为KV格式或者JSON格式，其中KV格式数据使用英文冒号（:）连接字段名和字段值。


        - 样例1：包含2条测试数目，第1条是KV格式（包含1个跨行字段traceback），第2条是JSON格式。


          ````plaintext
          time_local: 25/May/2020:01:56:22
          user agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.18 (KHTML, like Gecko) Chrome/11.0.661.0 Safari/534.18
          "request:method": GET
          ```
          traceback: Traceback (most recent call last):
            File "traceback_print_exc.py", line 20, in <module>
              produce_exception()
            File "/home/user/code/test.py", line 16, in produce_exception
              produce_exception(recursion_level-1)
            File "/home/user/code/test.py", line 18, in produce_exception
              raise RuntimeError()

          RuntimeError
          ```

          {
            "time_local": "25/May/2020:01:56:22",
            "user agent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.18 (KHTML, like Gecko) Chrome/11.0.661.0 Safari/534.18",
            "request:method": "GET",
            "remote user": "john"
          }
          ````

        - 样例2：1个完整的JSON实例，包含3条测试数据。


          ```plaintext
          [\
            {\
              "time_local": "25/May/2020:01:56:22",\
              "user agent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.18 (KHTML, like Gecko) Chrome/11.0.661.0 Safari/534.18",\
              "request:method": "GET",\
              "remote user": "john"\
            },\
            {\
              "time_local": "25/May/2020:01:56:22",\
              "user agent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.18 (KHTML, like Gecko) Chrome/11.0.661.0 Safari/534.18",\
              "request:method": "GET",\
              "remote user": "john"\
            },\
            {\
              "time_local": "25/May/2020:01:56:22",\
              "user agent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.18 (KHTML, like Gecko) Chrome/11.0.661.0 Safari/534.18",\
              "request:method": "GET",\
              "remote user": "john"\
            }\
          ]
          ```
      - 在 **维表** 页签中设置测试数据。

        维表用于快速预览资源函数所涉及的资源。您可以输入对应的维表数据样本，用于数据预览调试。







        **说明**

        在 **维表** 页签中配设置的测试数据，如果是res\_rds\_mysql、res\_log\_logstore\_pull资源函数对应的数据样例必须为CSV格式，如果是res\_oss\_file、res\_local资源函数对应的数据样例可以为CSV格式，也可以为JSON格式。





        样例：包含2条测试数据，第1条是CSV格式，第2条是JSON格式。


        ```plaintext
        ip,country,province
        127.0.0.1,China,Shanghai
        192.168.0.0,China,Zhejiang

        [\
          {\
            "ip": "127.0.0.1",\
            "country": "China",\
            "province": "Shanghai"\
          },\
          {\
            "ip": "192.168.0.0",\
            "country": "China",\
            "province": "Zhejiang"\
          }\
        ]
        ```


4. 单击 **预览数据**。









      **说明**

      单次预览最多返回100条加工结果。









      完成预览设置后，您可以在 **加工结果** 页签中查看预览结果。



      - 如果加工语句错误或者权限配置错误，导致数据加工失败，请根据页面提示处理。

      - 如果确认数据加工结果无误，可保存加工结果。具体操作，请参见 [创建数据加工任务](https://help.aliyun.com/zh/sls/create-a-data-transformation-job#task-1181217 "")。

## 快速预览示例

- 加工语句

在编辑框中输入如下加工语句。


```plaintext
# e_set("insert_field", "test_value")
e_table_map(
      res_rds_mysql(
          address="rm-uf6wjk5****.mysql.rds.aliyuncs.com",
          username="test_username",
          password="****",
          database="test_db",
          table="test_table",
      ),
      "ip",
      ["country", "province"],
)
```

- 测试数据

在**测试数据** \> **数据**页签中输入如下内容。


```plaintext
{
      "id": "1001",
      "ip": "127.0.0.1"
}
```

- 维表数据

在**测试数据** \> **维表**页签中输入如下内容。


```plaintext
ip,country,province
127.0.0.1,China,Shanghai
192.168.0.0,China,Zhejiang
```

- 预览结果![预览调试](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5131434261/p285989.png)