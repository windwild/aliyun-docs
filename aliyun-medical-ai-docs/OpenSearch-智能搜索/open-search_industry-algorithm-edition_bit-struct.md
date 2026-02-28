### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) bit\_struct

# bit\_struct

更新时间：2023-12-19 01:33:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：动态与公告](https://help.aliyun.com/zh/open-search/announcements-and-updates)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能函数项

场景举例

int64\_array 数组值构建介绍

插件功能函数可以用在filter子句作为过滤和筛选条件，而返回值为数值型的功能函数在sort子句中，用来做排序。其中功能函数参数出现的文档字段需根据对应函数文档提示，创建为索引或属性。

## 功能函数项

**1.介绍：**

**bit\_struct: 将INT\_ARRAY字段值进行自定义分组并允许对分组值进行指定operation计算。**

**2.语法：**

```javascript
bit_struct(doc_field,"$struct_definition", operation,...)
```

**3.参数：**

- **doc\_field**: 是一个INT\_ARRAY类型的字段名。

- **$struct\_definition**：用于把int64的值拆分成多个维度的信息。每一维的分组用int64中的起始bit位置和结束bit位置指定，使用横线“-”分隔，bit位置从值的高端开始算起，从0开始，最大不能超过63。多个分组用逗号”，”分隔。每个分组有一个编号，编号从1开始算起。举例：假设用户需要把int64拆分成3个维度的信息， bit0到bit9代表一个值（用$1表示）, bit10到bit48代表一个值（用$2表示）, bit49到bit60代表一个值（用$3表示）, 则该参数可写成：”0-9,10-48,49-60”。

- **operation**：定义计算过程,最少定义1个，最多定义5个,每个operation会有一个编号，这个编号是接着struct\_definition中的编号开始递增，当需要定义多个operation时，后面的operation要用到前面计算过的operation的返回值，这时候就可以用到给operation分配的编号了。operation 可以定义的操作有：


  - "equal,$m,$n": 判断$m代表的值和$n代表的值是否相等，相等返回true,否则返回false。

  - "overlap,$m,$n,$k,$p"：判断($m,$n)和($k,$p）定义的范围在数轴上是否相交。相交时返回true，否则返回false

  - "and,$m,$n,…"：返回$m, $n,..等做and(&&）的结果。【注：上面的这3个操作的参数也可以是整数数字。 例如 “equal,$1,1”】


**4.返回值：**

int64，返回最后一个operation第一次为true时对应的doc\_field中的数组下标（从0开始）。若doc\_field中没有满足operation指定的要求的值，则返回-1。

5. **注意事项：**

- 函数参数依赖字段需创建为属性字段


## 场景举例

**查询给定时间段在营业的店铺有哪些**？
假定用户文档中有一个int64\_array类型的字段open\_time，每个值表示一段营业时间，将int64的高32位表示起始时间，低32位表示结束时间，如果要查询下午14点到15:30点营业的店铺，可以将时间转换为从当天0点开始，按分钟为单位的时间段, 则下午14点到15:30表示为（840,930）,则查询中filter子句可以写为：

```javascript
filter=bit_struct(open_time, "0-31,32-63","overlap,$1,$2,840,930")!=-1
```

- **查询未来某一天,某个餐点（早，中，晚），可以提供Pmin到Pmax人数就餐的店铺**


假设用户文档中有一个int64\_array类型的字段book\_info，对于该字段中的一个值，0-7位表示日期，8-15位餐点，16-41位表示最小人数，42-63位表示最大人数。查询明天（用1表示）晚上（用3表示）能服务3-5个人的店铺，则filter子句可以写为：

```javascript
filter=bit_struct(book_info,"0-7,8-15,16-41,42-63",
"equal,$1,1","equal,$2,3","overlap,$3,$4,3,5","and,$5,$6,$7")!=-1
//解释
这里$1表示book_info中0-7位代表的值，
$2表示book_info中8-15位代表的值
$3表示book_info中16-41位代表的值
$4表示book_info中42-63位代表的值
$5代表operation “equal,$1,1”的返回值
$6代表 operation”equal,$2,3”的返回值
$7代表operation “overlap,$3,$4,3,5”的返回值
返回$5,$6,$7代表的值做and(逻辑与)后第一次为true时候的值 在book_info中对应的数组下标
```

- **查询下午14点到15:30表示为（840,930）之间，库存>10的店铺有哪些？** 因为bit\_struct返回的是下标，所以他可以和multi\_attr函数一起配合使用，取另外一个array类型字段对应下标的值。如该例，可以在查询语句中使用：


```javascript
filter=multi_attr(store, bit_struct(dispatch_time,"0-31,32-63", "equal,$1,840", "equal,$2,930", "and,$3,$4"))>10
//解释
dispatch_time是文档中有一个多值INT64的字段，用于存储商户的配送时间。将时间转换为从当天0点开始，按分钟为单位的时间段, 则下午14点到15:30表示为（840,930）
store是一个int64_array字段，与dispatch_time的时间段分别对应，表示该时间段的库存量。
```

## int64\_array 数组值构建介绍

**样例：**

这里以Python为例，构建一个早上8点~18点的int64

```javascript
#开始时间8：00 以分钟为单位
start=8*60

#结束时间18:00
end=18*60

#将int64的高32位表示起始时间，低32位表示结束时间
#先构造高32
start=start<<32
print("高32",start)#2061584302080

#最终结果
result=start|end
print("结果",result)#2061584303160
```

**结果**：![1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3238921161/p230081.png) **原理图**：二进制：![2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3238921161/p230082.png)将480存到高32位上（原理：左移32位）：![3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3238921161/p230083.png)将构造的高32的结果，在将1080存到这个数的低32位上（原理 \|）：![4](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3238921161/p230084.png)得到该数字的二级制为：0000000000000000000000011110000000000000000000000000010000111000其结果：![5](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3238921161/p230085.png)与以上的Python dome的计算结果一致。

这里简单举个例子：

假设，需要判断数组里是否有某个值，并且数值的值存在低32位中，filter写法可以为：

```javascript
bit_struct(type_arr,"0-31,32-63","equal,$2,40506")!=-1
//解释：
"0-31,32-63"：固定填入
"equal,$2,40506"：判断数组里有没有值为40506
```