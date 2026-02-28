### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)Cava 循环结构

# Cava 循环结构

更新时间：2025-03-07 00:17:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cava 分支结构](https://help.aliyun.com/zh/open-search/high-performance-searchedition/branch-structures-in-cava)[下一篇：Cava 异常处理](https://help.aliyun.com/zh/open-search/high-performance-searchedition/exception-handling)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

for循环

说明

语法结构

示例代码

本文对Cava中for循环的语法结构进行说明，并提供相关代码示例供您参考。

## 简介

Cava中通过循环结构来支持对同一个操作执行多次，目前Cava仅支持for循环，不支持while和do…while循环。

## for循环

### **说明**

- for循环先执行初始化条件部分，该部分也可以为空。

- for循环检查条件判断是否为true，如果为true则执行循环体部分，为false则循环终止。

- 每次执行完循环体之后都会更新条件，然后再次检查条件判断。

- 在循环体中可以使用continue提前终止本次循环体的执行。

- 在循环体中可以使用break提前终止整个循环。

- 循环中可以嵌套循环。


### **语法结构**

```java
for (初始化条件; 条件判断; 条件更新) {
    //循环体，需要执行的操作
}
```

### **示例代码**

```java
class Example {
    static int main() {
        int a = 0;
        for (int i = 0; i < 10; ++i) {
            if (i == 1) {
                continue;
            }
            if (a > 10) {
                break;
            }
            a += i;
        }
        int j = 0;
        for ( ; i < 10; ++j) {
            a += j;
        }
        return a;
    }
}
```