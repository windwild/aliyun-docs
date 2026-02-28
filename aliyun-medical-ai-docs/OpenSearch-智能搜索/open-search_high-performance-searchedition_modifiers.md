### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)Cava 修饰符

# Cava 修饰符

更新时间：2025-03-07 00:16:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cava 类型和变量定义](https://help.aliyun.com/zh/open-search/high-performance-searchedition/data-types-and-variable-types)[下一篇：Cava 运算符](https://help.aliyun.com/zh/open-search/high-performance-searchedition/operators-in-cava)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

static修饰符

访问控制修饰符

本文主要介绍了Cava中的static修饰符与访问控制修饰符。

## static修饰符

`static` 修饰符用于定义 [类函数](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/classes-and-objects)。注：Cava中仅支持成员变量定义，不支持类变量定义，所以在变量定义时使用 `static` 修饰符会引发编译错误：

```java
class Example {
    static int i; // 编译时报错
    static int main() {
        return 0;
    }
}
```

```java
ERROR cava.common.Diagnostics : benchmark/example.cava:1.15-2.16 [30001] static variable is not support:i
```

## 访问控制修饰符

cava对以下修饰符进行了语法上的兼容：

- public

- protected

- private

- final


不过修饰符存在与否并不影响类成员的访问控制：无论类上成员变量的声明是否带有以上修饰符，均等价于使用 `public` 修饰，即不对成员的访问进行限制。

```java
class Example {
    public double PI; // <==
    Example() {
        PI = 3.1415926;
    }
    static int main() {
        Example example = new Example();
        double a = example.PI;
        return 0;
    }
}
```

一般建议，在编写Cava代码时不要使用此类修饰符，以免造成误解。