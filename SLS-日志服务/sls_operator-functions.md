### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据处理](https://help.aliyun.com/zh/sls/data-processing-sls/)[数据写入后处理（数据加工）](https://help.aliyun.com/zh/sls/sls-data-processing/)[数据加工（旧版）](https://help.aliyun.com/zh/sls/data-transformation/)[数据加工语法](https://help.aliyun.com/zh/sls/data-processing-syntax/)[表达式函数](https://help.aliyun.com/zh/sls/overview-of-expression-functions/)操作符函数

# 操作符函数

更新时间：2024-06-18 02:31:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

函数列表

op\_if

函数格式

参数说明

返回结果

函数示例

op\_ifnull

函数格式

参数说明

返回结果

函数示例

op\_coalesce

op\_nullif

函数格式

参数说明

返回结果

函数示例

op\_and

函数格式

参数说明

返回结果

函数示例

op\_not

函数格式

参数说明

返回结果

函数示例

op\_or

函数格式

参数说明

返回结果

函数示例

op\_eq

函数格式

参数说明

返回结果

函数示例

op\_ge

函数格式

参数说明

返回结果

函数示例

op\_gt

函数格式

参数说明

返回结果

函数示例

op\_le

函数格式

参数说明

返回结果

函数示例

op\_lt

函数格式

参数说明

返回结果

函数示例

op\_ne

函数格式

参数说明

返回结果

函数示例

op\_len

函数格式

参数说明

返回结果

函数示例

op\_in

函数格式

参数说明

返回结果

函数示例

op\_not\_in

函数格式

参数说明

返回结果

函数示例

op\_slice

函数格式

参数说明

返回结果

函数示例

op\_index

函数格式

参数说明

返回结果

函数示例

op\_add

函数格式

参数说明

返回结果

函数示例

op\_max

函数格式

参数说明

返回结果

函数示例

op\_min

函数格式

参数说明

返回结果

函数示例

本文介绍操作符函数的语法规则，包括参数解释、函数示例等。

## 函数列表

**说明**

如果值为负数，请使用`op_neg(positive value)`函数，例如：您要表示`-1`，请使用op\_neg(1)。

| **类型** | **函数** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **类型** | **函数** | **说明** |
| 条件判断函数 | [op\_if](https://help.aliyun.com/zh/sls/operator-functions#section-mig-jki-hlv "") | 根据判断条件返回不同表达式的值。 |
| [op\_ifnull](https://help.aliyun.com/zh/sls/operator-functions#section-ckd-wda-tbl "")， [op\_coalesce](https://help.aliyun.com/zh/sls/operator-functions#section-meh-y8z-mvp "") | 返回第一个值不为None的表达式的值。 |
| [op\_nullif](https://help.aliyun.com/zh/sls/operator-functions#section-4x5-inl-e6f "") | 如果表达式1等于表达式2，返回None。否则返回表达式1的值。 |
| [op\_and](https://help.aliyun.com/zh/sls/operator-functions#section-6dn-e26-731 "") | 使用逻辑运算and，对任意类型值进行真假判断，所有参数值为真时返回True。 |
| [op\_not](https://help.aliyun.com/zh/sls/operator-functions#section-3s2-73o-7q8 "") | 使用逻辑运算not，对任意类型值进行真假判断，返回参数值的反义布尔值。 |
| [op\_or](https://help.aliyun.com/zh/sls/operator-functions#section-43p-je3-xy4 "") | 使用逻辑运算or，对任意类型值进行真假判断。当任意参数值为真时返回True，所有参数值为假时返回False。 |
| 比较 | [op\_eq](https://help.aliyun.com/zh/sls/operator-functions#section-25s-uy4-zym "") | 按照`a==b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| [op\_ge](https://help.aliyun.com/zh/sls/operator-functions#section-2yu-xtl-if2 "") | 按照`a>=b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| [op\_gt](https://help.aliyun.com/zh/sls/operator-functions#section-8ze-80f-4zk "") | 按照`a>b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| [op\_le](https://help.aliyun.com/zh/sls/operator-functions#section-z60-nkx-zqz "") | 按照`a<=b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| [op\_lt](https://help.aliyun.com/zh/sls/operator-functions#section-nz6-t7d-c11 "") | 按照`a<b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| [op\_ne](https://help.aliyun.com/zh/sls/operator-functions#section-azh-rkp-sgy "") | 按照`a!=b`条件进行计算，返回True或False。<br>a和b类型必须一致，例如都是字符串、数字或者列表。 |
| 容器判断 | [op\_len](https://help.aliyun.com/zh/sls/operator-functions#section-51y-aby-i6k "") | 计算文本字符串中的字符数，可用于字符串和其他返回元组、列表、字典的表达式。 |
| [op\_in](https://help.aliyun.com/zh/sls/operator-functions#section-upx-pp8-s8r "") | 判断字符串、元组、列表或字典中是否包含特定元素，返回True或False。 |
| [op\_not\_in](https://help.aliyun.com/zh/sls/operator-functions#section-i5c-dlk-9d9 "") | 判断字符串、元组、列表或字典中是否不包含特定元素，返回True或False。 |
| [op\_slice](https://help.aliyun.com/zh/sls/operator-functions#section-19o-mxu-cpq "") | 对指定字符串、数组、元组进行截取。 |
| [op\_index](https://help.aliyun.com/zh/sls/operator-functions#section-rxw-999-uop "") | 根据字符串、数组、元组的下标返回其对应的元素。 |
| 一般性多值操作 | [op\_add](https://help.aliyun.com/zh/sls/operator-functions#section-9wc-fea-59b "") | 计算多个值的和，可以是字符串或者数字等。 |
| [op\_max](https://help.aliyun.com/zh/sls/operator-functions#section-muw-ccu-4mt "") | 计算多个字段或表达式表示的数值的最大值。 |
| [op\_min](https://help.aliyun.com/zh/sls/operator-functions#section-6ft-fco-n1w "") | 计算多个字段或表达式表示的数值的最小值。 |

## op\_if

根据判断条件返回不同表达式的值。

- ### 函数格式
















```plaintext
op_if(condition, expression1, expression2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| condition | 任意 | 是 | 判断条件。如果该条件为非布尔值，系统将对其采用真假判断。更多信息，请参见 [真假判断](https://help.aliyun.com/zh/sls/basic-syntax#section-ko6-ydn-bll "")。 |
| expression1 | 任意 | 是 | 判断结果为True时，返回该表达式的值。 |
| expression2 | 任意 | 是 | 判断结果为False时，返回该表达式的值。 |

- ### 返回结果


返回相应的表达式的值。

- ### 函数示例


  - 示例1：如果`content`为True，则把表达式1的值赋给`test_if`。

    - 原始日志















      ```plaintext
      content: hello
      ```

    - 加工规则















      ```plaintext
      e_set("test_if", op_if(v("content"),"still origion content","replace this"))
      ```

    - 加工结果















      ```plaintext
      content: hello
      test_if:  still origion content
      ```
  - 示例2：如果`content`为False，则把表达式2的值赋给`test_if`。

    - 原始日志















      ```plaintext
      content: 0
      ```

    - 加工规则















      ```plaintext
      e_set("test_if", op_if(ct_int(v("content", default=0)),"still origion content","replace this"))
      ```

    - 加工结果















      ```plaintext
      content: 0
      test_if:  replace this
      ```

## op\_ifnull

返回第一个值不为None的表达式的值。

- ### 函数格式
















```plaintext
op_ifnull(expression1, expression2, ....)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| expression1 | 任意 | 是 | 表达式1。 |
| expression2 | 任意 | 是 | 表达式2。 |

- ### 返回结果


返回第一个值不为None的表达式的值。

- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      test_if: hello
      escape_name: Etl
      ```

    - 加工规则















      ```plaintext
      e_set("test_ifnull", op_ifnull(v("escape_name"),v("test_if")))
      ```

    - 加工结果















      ```plaintext
      test_if: hello
      escape_name: Etl
      test_ifnull:  Etl
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      test_if: hello
      escape_name: Etl
      ```

    - 加工规则















      ```plaintext
      e_set("test_ifnull", op_ifnull(v("test_if"),v("escape_name")))
      ```

    - 加工结果















      ```plaintext
      test_if: hello
      escape_name: Etl
      test_ifnull:  hello
      ```

## op\_coalesce

返回第一个值不为None的表达式的值。

与`op_ifnull`函数的参数说明和示例类似。更多信息，请参见 [op\_ifnull](https://help.aliyun.com/zh/sls/operator-functions#section-ckd-wda-tbl "")。

## op\_nullif

如果表达式1等于表达式2，返回None。否则返回表达式1的值。

- ### 函数格式
















```plaintext
op_nullif(expression1, expression2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| expression1 | 任意 | 是 | 表达式1。 |
| expression2 | 任意 | 是 | 表达式2。 |

- ### 返回结果


如果表达式1和表达式2相等返回None，否则返回表达式1的值。

- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      content: hello
      escape_name: Etl
      ```

    - 加工规则















      ```plaintext
      e_set("test_ifnull", op_nullif(v("content"),v("escape_name")))
      ```

    - 加工结果















      ```plaintext
      content: hello
      escape_name: Etl
      test_nullif:  hello
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      content: hello
      escape_name: hello
      ```

    - 加工规则















      ```plaintext
      e_set("test_ifnull", op_nullif(v("content"),v("escape_name")))
      ```

    - 加工结果















      ```plaintext
      #因为content与escape_name内容一样，所以没有任何内容返回给test_isnull字段。
      content: hello
      escape_name: hello
      ```

## op\_and

使用逻辑运算and，对任意类型值进行真假判断，所有参数值为真时返回True。

- ### 函数格式
















```plaintext
op_and(value1, value2, ...)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 任意 | 是 | 运算值2。 |

- ### 返回结果


  - 所有参数值为真时返回True。

  - 对任意类型值进行真假判断。更多信息，请参见 [真假判断](https://help.aliyun.com/zh/sls/basic-syntax#section-ko6-ydn-bll "")。
- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      number1: 123
      number2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_and", op_and(v("number1"),v("number2")))
      ```

    - 加工结果















      ```plaintext
      number1: 123
      number2: 234
      op_and:  True
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      number1: 0
      number2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_and", op_and(v("number1"),v("number2")))
      ```

    - 加工结果















      ```plaintext
      number1: 0
      number2: 234
      op_and: True
      ```
  - 示例3：

    - 原始日志















      ```plaintext
      ctx1: False
      ctx2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_and", op_and(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: False
      ctx2: 234
      op_and: False
      ```
  - 示例4：

    - 原始日志















      ```plaintext
      ctx1: True
      ctx2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_and", op_and(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: True
      ctx2: 234
      op_and: True
      ```

## op\_not

使用逻辑运算not，对任意类型值进行真假判断，返回表达式值的反义布尔值。

- ### 函数格式
















```plaintext
op_not(expression)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| expression | 任意 | 是 | 表达式。 |

- ### 返回结果


  - 返回表达式值的反义布尔值。

  - 对任意类型值进行真假判断。更多信息，请参见 [真假判断](https://help.aliyun.com/zh/sls/basic-syntax#section-ko6-ydn-bll "")。
- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      ctx1: True
      ```

    - 加工规则















      ```plaintext
      e_set("op_not", op_not(v("ctx1")))
      ```

    - 加工结果















      ```plaintext
      ctx1: True
      op_not:  False
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      ctx1: 345
      ```

    - 加工规则















      ```plaintext
      e_set("op_not", op_not(v("ctx1")))
      ```

    - 加工结果















      ```plaintext
      ctx1: 345
      op_not:  False
      ```
  - 示例3：

    - 原始日志















      ```plaintext
      ctx1: 0
      ```

    - 加工规则















      ```plaintext
      e_set("op_not", op_not(ct_int(v("ctx1"))))
      ```

    - 加工结果















      ```plaintext
      ctx1: 0
      op_not:  True
      ```
  - 示例4：

    - 原始日志















      ```plaintext
      ctx1: ETL
      ```

    - 加工规则















      ```plaintext
      e_set("op_not", op_not(v("ctx1")))
      ```

    - 加工结果















      ```plaintext
      ctx1: ETL
      op_not:  False
      ```
  - 示例5：

    - 原始日志















      ```plaintext
      ctx1: None
      ```

    - 加工规则















      ```plaintext
      e_set("op_not", op_not(v("ctx1")))
      ```

    - 加工结果















      ```plaintext
      ctx1: None
      op_not:  True
      ```

## op\_or

使用逻辑运算or，对任意类型值进行真假判断。当任意表达式的值为真时返回True，所有表达式值为假时返回False。

- ### 函数格式
















```plaintext
op_or(expression1, expression2, ...)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| expression1 | 任意 | 是 | 表达式1。 |
| expression2 | 任意 | 是 | 表达式2。 |

- ### 返回结果


  - 任意表达式的值为真时返回True，所有表达式的值为假时返回False。

  - 对任意类型值进行真假判断。更多信息，请参见 [真假判断](https://help.aliyun.com/zh/sls/basic-syntax#section-ko6-ydn-bll "")。
- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      ctx1: 123
      ctx2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: 123
      ctx2: 234
      op_or:  True
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      ctx1: 0
      ctx2: 234
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: 0
      ctx2: 234
      op_or:  True
      ```
  - 示例3：

    - 原始日志















      ```plaintext
      ctx1: ETL
      ctx2: ALIYUN
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: ETL
      ctx2: ALIYUN
      op_or:  True
      ```
  - 示例4：

    - 原始日志















      ```plaintext
      ctx1: True
      ctx2: False
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: True
      ctx2: False
      op_or:  True
      ```
  - 示例5：

    - 原始日志















      ```plaintext
      ctx1: 0
      ctx2: False
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(ct_int(v("ctx1")),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: 0
      ctx2: False
      op_or:  False
      ```
  - 示例6：

    - 原始日志















      ```plaintext
      ctx1: 124
      ctx2: True
      ```

    - 加工规则















      ```plaintext
      e_set("op_or", op_or(v("ctx1"),v("ctx2")))
      ```

    - 加工结果















      ```plaintext
      ctx1: 124
      ctx2: True
      op_or:  True
      ```

## op\_eq

按照`a==b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_eq(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1与值2相等返回True，否则返回False。

- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      content: hello
      ctx: hello
      ```

    - 加工规则















      ```plaintext
      e_set("test_eq", op_eq(v("content"),v("ctx")))
      ```

    - 加工结果















      ```plaintext
      content: hello
      ctx: hello
      test_eq: True
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      content: hello
      ctx: ctx
      ```

    - 加工规则















      ```plaintext
      e_set("test_eq", op_eq(v("content"),v("ctx")))
      ```

    - 加工结果















      ```plaintext
      content: hello
      ctx: ctx
      test_eq: False
      ```

## op\_ge

按照`a>=b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_ge(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1大于等于值2返回True，否则返回False。

- ### 函数示例


  - 示例1：假如apple\_price的值大于等于orange\_price的值，则返回True。

    - 原始日志















      ```plaintext
      apple_price: 16
      orange_price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("test_ge", op_ge(ct_int(v("apple_price")),ct_int(v("orange_price"))))
      ```

    - 加工结果















      ```plaintext
      apple_price: 16
      orange_price: 14
      test_ge: True
      ```
  - 示例2：假如apple\_price的值小于orange\_price的值，则返回False。

    - 原始日志















      ```plaintext
      apple_price: 12
      orange_price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("test_ge", op_ge(ct_int(v("apple_price")),ct_int(v("orange_price"))))
      ```

    - 加工结果















      ```plaintext
      apple_price: 12
      orange_price: 14
      test_ge: False
      ```

## op\_gt

按照`a>b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_gt(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1大于值2返回True，否则返回False。

- ### 函数示例


  - 示例1：判断old\_number取值是否大于young\_number取值，大于返回True否则返回False。

    - 原始日志















      ```plaintext
      old_number: 16
      young_number: 14
      ```

    - 加工规则















      ```plaintext
      e_set("op_gt",op_gt(ct_int(v("old_number")),ct_int(v("young_number"))))
      ```

    - 加工结果















      ```plaintext
      old_number: 16
      young_number: 14
      test_ge: True
      ```
  - 示例2：判断priority取值是否大于price取值，大于返回True否则返回False。

    - 原始日志















      ```plaintext
      priority: 14
      price: 16
      ```

    - 加工规则















      ```plaintext
      e_set("op_gt",op_gt(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 14
      price: 16
      test_ge: False
      ```

## op\_le

按照`a<=b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_le(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1小于等于值2返回True，否则返回False。

- ### 函数示例


  - 示例1：如果priority的值小于等于price的值，返回True否则返回False。

    - 原始日志















      ```plaintext
      priority: 16
      price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("op_le",op_le(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 16
      price: 14
      test_ge: False
      ```
  - 示例2：如果priority的值小于等于price的值，返回True否则返回False。

    - 原始日志















      ```plaintext
      priority: 14
      price: 16
      ```

    - 加工规则















      ```plaintext
      e_set("op_le",op_le(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 14
      price: 16
      test_ge: True
      ```

## op\_lt

按照`a<b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_lt(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1小于值2返回True，否则返回False。

- ### 函数示例


  - 示例1： 如果priority的值小于price的值，返回True否则返回False。

    - 原始日志















      ```plaintext
      priority: 16
      price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("op_lt",op_lt(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 16
      price: 14
      op_lt: False
      ```
  - 示例2：如果priority的值小于price的值，返回True否则返回False。

    - 原始日志















      ```plaintext
      priority: 14
      price: 15
      ```

    - 加工规则















      ```plaintext
      e_set("op_lt",op_lt(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 14
      price: 15
      op_lt: True
      ```

## op\_ne

按照`a!=b`条件进行计算，返回True或False。

- ### 函数格式
















```plaintext
op_ne(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1相同 | 是 | 运算值2。 |

- ### 返回结果


如果值1不等于值2返回True，否则返回False。

- ### 函数示例


  - 示例1：

    - 原始日志















      ```plaintext
      priority: 16
      price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("op_ne",op_ne(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 16
      price: 14
      op_ne: True
      ```
  - 示例2：

    - 原始日志















      ```plaintext
      priority: 14
      price: 14
      ```

    - 加工规则















      ```plaintext
      e_set("op_ne",op_ne(ct_int(v("priority")),ct_int(v("price"))))
      ```

    - 加工结果















      ```plaintext
      priority: 14
      price: 14
      op_ne: False
      ```

## op\_len

计算文本字符串中的字符数，可用于字符串和其他返回元组、列表、字典的表达式。

- ### 函数格式
















```plaintext
op_len(value）
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value | 字符串、元组、列表或字典等 | 是 | 运算值。 |

- ### 返回结果


返回字段的长度。

- ### 函数示例


  - 原始日志















    ```plaintext
    content: I,love,this,world
    ```

  - 加工规则















    ```plaintext
    e_set("op_len",op_len(v("content")))
    ```

  - 加工结果















    ```plaintext
    content: I,love,this,world
    op_len: 17
    ```

## op\_in

判断字符串、元组、列表或字典中是否包含特定元素，返回True或False。

- ### 函数格式
















```plaintext
op_in(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 字符串、元组、列表或字典等 | 是 | 字符串、元组、列表或者字典等。 |
| value2 | 任意 | 是 | 判断的元素。 |





**说明**





函数中字符串、元组、列表或字典参数在前，元素在后。

- ### 返回结果


如果字符串、元组、列表或字典a中包含元素b返回True，否则返回False。

- ### 函数示例


  - 原始日志















    ```plaintext
    list:  [1, 3, 2, 7, 4, 6]
    num2:  2
    ```

  - 加工规则















    ```plaintext
    e_set("op_in",op_in(v("list"),v("num2")))
    ```

  - 加工结果















    ```plaintext
    list:  [1, 3, 2, 7, 4, 6]
    num2:  2
    op_in: True
    ```

## op\_not\_in

判断字符串、元组、列表或字典中是否不包含特定元素，返回True或False。

- ### 函数格式
















```plaintext
op_not_in(value1, value2)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 字符串、元组、列表或字典等 | 是 | 字符串、元组、列表或者字典等。 |
| value2 | 任意 | 是 | 判断的元素。 |





**说明**





函数中字符串、元组、列表或字典参数在前，元素在后。

- ### 返回结果


如果字符串、元组、列表或字典中不包含元素返回True，否则返回False。

- ### 函数示例


  - 原始日志















    ```plaintext
    list:  [1, 3, 2, 7, 4, 6]
    num2:  12
    ```

  - 加工规则















    ```plaintext
    e_set("op_not_in",op_not_in(v("list"),v("num2")))
    ```

  - 加工结果















    ```plaintext
    list:  [1, 3, 2, 7, 4, 6]
    num2:  12
    op_in: True
    ```

## op\_slice

对指定字符串、数组、元组进行截取。

- ### 函数格式
















```plaintext
op_slice(value, start, end=None, step=None)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value | String | 是 | 函数要切片的值。 |
| start | Num | 否 | 截取的起始位置，默认为位置0。 |
| end | Num | 否 | 截取的结束位置，不包含该位置，默认为字符串结尾位置。 |
| step | Num | 否 | 每次截取的长度。 |

- ### 返回结果


返回提取后的字符串。

- ### 函数示例


  - 示例1：对word字段从开头到结尾开始进行截取，步长为2。

    - 原始日志















      ```plaintext
      word:  I,love,this,world
      ```

    - 加工规则















      ```plaintext
      e_set("op_slice",op_slice(v("word"),2))
      ```

    - 加工结果















      ```plaintext
      word:  I,love,this,world
      op_slice: I,
      ```
  - 示例2：对word字段从位置2到位置9进行截取，步长为1。

    - 原始日志















      ```plaintext
      word:  I,love,this,world
      ```

    - 加工规则















      ```plaintext
      e_set("op_slice",op_slice(v("word"),2,9,1))
      ```

    - 加工结果















      ```plaintext
      word:  I,love,this,world
      op_slice: love,th
      ```

## op\_index

根据字符串、数组、元组的下标返回其对应的元素。

- ### 函数格式
















```plaintext
op_index(value, index)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value | String | 是 | 字符串、数组、元组等。 |
| index | Num | 否 | 需要传入的字符串、数组或元组的下标。 |

- ### 返回结果


返回下标对应的元素。

- ### 函数示例


  - 示例1：返回word字段下标为0的元素。

    - 原始日志















      ```plaintext
      word:  I,love,this,world
      ```

    - 加工规则















      ```plaintext
      e_set("op_index",op_index(v("word"),0))
      ```

    - 加工结果















      ```plaintext
      word:  I,love,this,world
      op_slice: I
      ```
  - 示例2：返回word字段下标为3的元素。

    - 原始日志















      ```plaintext
      word:  I,love,this,world
      ```

    - 加工规则















      ```plaintext
      e_set("op_index",op_index(v("word"),3))
      ```

    - 加工结果















      ```plaintext
      word:  I,love,this,world
      op_index: o
      ```

## op\_add

计算多个值的和，可以是字符串或者数字等。

- ### 函数格式
















```plaintext
op_add(value1, value2, ...)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 字符串、元组、列表或字典等 | 是 | 运算值1。 |
| value2 | 必须与值1一样 | 是 | 运算值2。 |

- ### 返回结果


返回求和操作后的数值。

- ### 函数示例


  - 示例1：计算price\_orange和price\_apple总金额。

    - 原始日志















      ```plaintext
      price_orange: 2
      price_apple: 13
      ```

    - 加工规则















      ```plaintext
      e_set("account",op_add(ct_int(v("price_orange")),ct_int(v("price_apple"))))
      ```

    - 加工结果















      ```plaintext
      price_orange: 2
      price_apple: 13
      account:  15
      ```
  - 示例2：统计bytes\_in和bytes\_out的和。

    - 原始日志















      ```plaintext
      bytes_in: 214
      bytes_out: 123
      ```

    - 加工规则















      ```plaintext
      e_set("total_bytes", op_add(ct_int(v("bytes_in")), ct_int(v("bytes_out"))))
      ```

    - 加工结果















      ```plaintext
      bytes_in: 214
      bytes_out: 123
      total_bytes:  337
      ```
  - 示例3：给网址添加HTTPS头。

    - 原始日志















      ```plaintext
      host: aliyun.com
      ```

    - 加工规则















      ```plaintext
      e_set("website", op_add("https://", v("host")))
      ```

    - 加工结果















      ```plaintext
      host: aliyun.com
      website: https://aliyun.com
      ```

## op\_max

计算多个字段或表达式表示的数值的最大值。

- ### 函数格式
















```plaintext
op_max(value1, value2, ...)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1一样 | 是 | 运算值2。 |

- ### 返回结果


返回多个数值中的最大值。

- ### 函数示例


  - 原始日志















    ```plaintext
    price_orange:  2
    priority_apple:  13
    ```

  - 加工规则















    ```plaintext
    e_set("max_price", op_max(ct_int(v("price_orange")),ct_int(v("priority_apple"))))
    ```

  - 加工结果















    ```plaintext
    price_orange:  2
    priority_apple:  13
    max_price:  13
    ```

## op\_min

计算多个字段或表达式表示的数值的最小值。

- ### 函数格式
















```plaintext
op_min(value1, value2, ...)
```

- ### 参数说明





| **参数名称** | **参数类型** | **是否必填** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数名称** | **参数类型** | **是否必填** | **说明** |
| value1 | 任意 | 是 | 运算值1。 |
| value2 | 必须与值1一样 | 是 | 运算值2。 |

- ### 返回结果


返回多个数值中的最小值。

- ### 函数示例


  - 原始日志















    ```plaintext
    price_orange:  2
    price_apple:  13
    ```

  - 加工规则















    ```plaintext
    e_set("op_min", op_min(ct_int(v("price_orange")),ct_int(v("price_apple"))))
    ```

  - 加工结果















    ```plaintext
    price_orange:  2
    price_apple:  13
    op_min:  2
    ```