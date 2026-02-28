### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据处理](https://help.aliyun.com/zh/sls/data-processing-sls/)[数据写入后处理（数据加工）](https://help.aliyun.com/zh/sls/sls-data-processing/)[数据加工（旧版）](https://help.aliyun.com/zh/sls/data-transformation/)[数据加工语法](https://help.aliyun.com/zh/sls/data-processing-syntax/)[通用参考](https://help.aliyun.com/zh/sls/general-reference/)JMES语法

# JMES语法

更新时间：2025-08-28 03:58:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GROK模式参考](https://help.aliyun.com/zh/sls/grok-patterns)[下一篇：日期时间格式化指令](https://help.aliyun.com/zh/sls/date-and-time-formatting-directives)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

通过字段的key获取值

通过层级访问获取值

通过切片操作获取值

多种用法综合使用

通过投影获取值

多值选取

计算数组长度

本文主要介绍JMES的常用语法和示例。

JMES语法

JMES是一个增强型的JSON查询计算语言，不仅可以对JSON数据进行提取，还可以做计算与转换。关于JMES语法的详细介绍请参见 [JMES Tutorial](http://jmespath.org/tutorial.html)。

数据加工中的`json_select`、`e_json`、`e_split`函数支持通过JMES提取字段或JSON表达式的值，或者通过JMES计算特定的值。其用法为：

```plaintext
json_select(值, "jmes表达式", ...)
e_json(字段名, jmes="jmes表达式", ...)
e_split(字段名, ... jmes="jmes表达式", ...)
```

函数的具体用法请参见 [json\_select](https://help.aliyun.com/zh/sls/structured-data-functions#section-xrt-z1k-awb "")、 [e\_json](https://help.aliyun.com/zh/sls/value-extraction-functions#section-o7x-7rl-2qh "") 和 [e\_split](https://help.aliyun.com/zh/sls/event-processing-functions#section-urg-dob-o79 "")。

## 通过字段的key获取值

- 原始日志















```plaintext
json_data: {"a":"foo","b":"bar","c":"baz"}
```

- 加工语法















```plaintext
# 获取JSON表达式中a的值。
e_set("a1", json_select(v("json_data"), "a"))
# 获取JSON表达式中b的值。
e_set("b1", json_select(v("json_data"), "b"))
# 获取JSON表达式中c的值。
e_set("c1", json_select(v("json_data"), "c"))
```

- 加工结果















```plaintext
a1:foo
b1:bar
c1:baz
json_data:{"a":"foo","b":"bar","c":"baz"}
```


## 通过层级访问获取值

- 原始日志















```plaintext
json_data:{"a": {"b":{"c":{"d":"value"}}}}
```

- 加工语法















```plaintext
# 获取JSON表达式中d的值。
e_set("e", json_select(v("json_data"), "a.b.c.d"))
```

- 加工结果















```plaintext
e:value
json_data:{"a": {"b":{"c":{"d":"value"}}}}
```


## 通过切片操作获取值

- 原始日志















```plaintext
json_data:{"a": ["b", "c", "d", "e", "f"]}
```

- 加工语法















```plaintext
# 获取字段a中从切片2开始的值。切片0值为b，切片1值为c。
e_set("key", json_select(v("json_data"), "a[2:]"))
```

- 加工结果















```plaintext
json_data:{"a": ["b", "c", "d", "e", "f"]}
key:["d", "e", "f"]
```


## 多种用法综合使用

- 原始日志















```plaintext
json_data:{"a": {"b": {"c": [{"d": [0, [1, 2]]}, {"d": [3, 4]}]}}}
```

- 加工语法















```plaintext
# c[0]表示{"d": [0, [1, 2]]}部分；d[1]表示[1, 2]]。返回值为1。
e_set("key", json_select(v("json_data"), "a.b.c[0].d[1][0]"))
```

- 加工结果















```plaintext
json_data:{"a": {"b": {"c": [{"d": [0, [1, 2]]}, {"d": [3, 4]}]}}}
key:1
```


## 通过投影获取值

- 示例1

  - 原始日志















    ```plaintext
    json_data:{"people": [{"first": "James", "last": "d"},{"first": "Jacob", "last": "e"},{"first": "Jayden", "last": "f"},{"missing": "different"}],"foo": {"bar": "baz"}}
    ```

  - 加工语法















    ```plaintext
    # 获取people列表中first的值。
    e_set("key", json_select(v("json_data"), "people[*].first"))
    ```

  - 加工结果















    ```plaintext
    json_data:{"people": [{"first": "James", "last": "d"},{"first": "Jacob", "last": "e"},{"first": "Jayden", "last": "f"},{"missing": "different"}],"foo": {"bar": "baz"}}
    key:["James", "Jacob", "Jayden"]
    ```
- 示例2

  - 原始日志















    ```plaintext
    json_data:{"ops": {"functionA": {"numArgs": 2},"functionB": {"numArgs": 3},"functionC": {"variadic": true}}}
    ```

  - 加工语法















    ```plaintext
    # 获取ops中numArgs的值。
    e_set("key", json_select(v("json_data"), "ops.*.numArgs"))
    ```

  - 加工结果















    ```plaintext
    json_data:{"ops": {"functionA": {"numArgs": 2},"functionB": {"numArgs": 3},"functionC": {"variadic": true}}}
    key:[2, 3]
    ```
- 示例3

  - 原始日志















    ```plaintext
    json_data:{"machines": [{"name": "a", "state": "running"},{"name": "b", "state": "stopped"},{"name": "c", "state": "running"}]}
    ```

  - 加工语法















    ```plaintext
    # 获取machines中running状态的name值。
    e_set("key", json_select(v("json_data"), "machines[?state=='running'].name"))
    ```

  - 加工结果















    ```plaintext
    json_data:{"machines": [{"name": "a", "state": "running"},{"name": "b", "state": "stopped"},{"name": "c", "state": "running"}]}
    key:["a", "c"]
    ```

## 多值选取

- 原始日志















```plaintext
json_data:{"people": [{"name": "a","state": {"name": "up"}},{"name": "b","state": {"name": "down"}}]}
```

- 加工语法















```plaintext
# 获取people的name及state值。
e_set("key", json_select(v("json_data"), "people[].[name, state.name]"))
```

- 加工结果















```plaintext
json_data:{"people": [{"name": "a","state": {"name": "up"}},{"name": "b","state": {"name": "down"}}]}
key:[["a", "up"], ["b", "down"]]
```


## 计算数组长度

- 原始日志















```plaintext
json_data:{"a": ["b", "c", "d", "e", "f"]}
```

- 加工语法















```plaintext
# 获取数组a的长度。
e_set("key", json_select(v("json_data"), "length(a)"))
```

















```plaintext
# 获取数组a的长度，若length(a) > 0, 设置no-empty字段为true。
e_if(json_select(v("json_data"), "length(a)", default=0), e_set("no-empty", true))
```

- 加工结果















```plaintext
json_data:{"a": ["b", "c", "d", "e", "f"]}
key:5
```

















```plaintext
json_data:{"a": ["b", "c", "d", "e", "f"]}
no-empty:true
```