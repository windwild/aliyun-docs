### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[缓存配置](https://help.aliyun.com/zh/cdn/user-guide/cache-settings/)[其他缓存配置](https://help.aliyun.com/zh/cdn/user-guide/other-cache-configurations/)自定义Cachekey

# 自定义Cachekey

更新时间：2026-02-08 21:12:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：重写访问URL](https://help.aliyun.com/zh/cdn/user-guide/create-an-access-url-rewrite-rule)[下一篇：配置共享缓存](https://help.aliyun.com/zh/cdn/user-guide/configure-shared-cache)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

使用场景

场景一

场景二

操作步骤

配置示例

URI

请求参数

HTTP Header

自定义变量

配置自定义Cachekey，开发者可以根据HTTP请求的不同部分（例如URI、请求参数、HTTP请求头或自定义变量等）制定规则来生成Cachekey，将访问同一个文件的一类请求转化为统一的Cachekey，避免将同一类请求缓存为不同文件的问题，从而提高缓存的命中率，降低回源率，减少请求的响应时间和带宽消耗。

## **注意事项**

- 由于功能特性，自定义CacheKey和忽略参数配置功能存在冲突。如果您已经配置了忽略参数，那么CDN节点在处理用户请求时，会去除请求URL中携带在`?`之后的参数，这将导致CacheKey中配置的请求参数不可用。开启自定义CacheKey功能前，请确保您的 [忽略参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters "") 没有设置。

- 自定义Cachekey功能不会修改回源的URL，仅会修改请求的缓存标识，回源的请求和客户端发起的请求内容保持一致。

- URL刷新功能目前无法刷新设置了自定义Cachekey以后的缓存内容。


## 使用场景

**重要**

自定义Cachekey功能不会修改回源的URL，仅会修改请求的缓存标识，回源的请求和客户端发起的请求内容保持一致。

Cachekey是一个文件在CDN节点上缓存时唯一的身份ID，每个在CDN节点上缓存的文件都对应一个Cachekey。文件的Cachekey默认为客户端请求的URL（带参数）。

### **场景一**

客户不同请求的URL中含有复杂的参数，因此即使多个请求访问的是同一个文件，但由于URL参数不同，CDN节点会视为请求不同文件而将不同请求缓存成多个文件，造成回源的请求增加。![图一](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7812981561/p87140.png)

可通过自定义Cachekey规则将同一类请求的Cachekey统一，降低回源率。![图二](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7722643561/p87141.png)

### **场景二**

客户端请求的URL一样时，CDN将视为请求同一个文件。但实际上请求的Http Header中携带了client字段区分了客户端系统，希望请求不同文件。![场景一](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7722643561/p87172.png)

此时可通过自定义Cachekey将client字段的值拼接至Cachekey，两个请求即可识别为2个不同的Cachekey。![场景二](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7812981561/p87173.png)

## 操作步骤

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **缓存配置**。

5. 在 **自定义Cachekey** 页签下，单击 **配置**，配置Cachekey。




| **参数类型** | **操作说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数类型** | **操作说明** |
| **规则条件** | 规则条件能够对用户请求中携带的各种参数信息进行识别，以此来决定某个配置是否对该请求生效。<br>   - **不使用**：不使用规则条件。<br>     <br>   - 若需新增或编辑规则条件，请在[规则引擎](https://help.aliyun.com/zh/cdn/user-guide/rules-engine "")中进行管理。 |
| **URI** | 当客户端请求的URI与配置中的 **源URI** 相匹配时，系统会用配置中的 **目标URI** 替换 **源URI**，来生成Cachekey。则使用配置中的 **目标URI** 替换 **源URI** 来拼接Cachekey。<br>支持配置多个URI替换策略。若存在多条策略，则按照从上到下的顺序依次进行匹配。一旦匹配到某个 **源URI**，系统将使用该策略对应的 **目标URI** 执行替换操作，并停止与后续策略的匹配。<br>   - **源URI**：以正斜线（/）开头的URI， **不含http://头及域名**。支持`PCRE`正则表达式。<br>     <br>   - **目标URI**：以正斜线（/）开头的URI， **不含http://头及域名**。 |
| **请求参数** | 操作的对象是用户发起的原始请求URL中携带的参数，可以对参数进行 **新增**、 **删除**、 **修改**、 **保留** 操作，操作后的结果将会拼接到Cachekey中。支持设置多个操作，存在多个操作的情况下，将会从上到下按顺序逐个执行。<br>   - **新增**：将新增的请求参数拼接到Cachekey中。例如：原始URL为`http://image.example.com/cat.jpg`，新增一个请求参数`type=jpg`，则Cachekey为`http://image.example.com/cat.jpg?type=jpg`。<br>     <br>   - **删除**：在生成Cachekey的时候删除原始请求URL中的指定参数。例如：原始URL为 `http://image.example.com/cat.jpg?type=jpg`，删除参数`type`，则Cachekey为`http://image.example.com/cat.jpg`。<br>     <br>   - **修改**：在生成Cachekey的时候修改原始请求URL中的指定参数。例如：原始URL为 `http://image.example.com/cat.jpg?type=jpg`，修改参数`type=png`，则Cachekey为。<br>     <br>   - **保留**：在生成Cachekey的时候仅保留原始请求URL中的指定参数。例如：原始URL为`http://image.example.com/cat.jpg?type=jpg&path=image`，保留参数`type`，则Cachekey为`http://image.example.com/cat.jpg?type=jpg`。 |
| **HTTP Header** | 将客户端原始请求中携带的指定HTTP Header的值拼接到Cachekey中。支持配置多个HTTP Header名称（多个 HTTP Header 名称之间用空格分隔），效果是每个HTTP Header的值将会按顺序拼接到Cachekey中。<br>例如：原始URL为 `http://image.example.com/cat.jpg`，客户端请求携带了一个`HTTP Header（path:image）`；如果 **HTTP Header** 中设置了`path`这个请求头，则Cachekey为`http://image.example.com/cat.jpgimage`。 |
| **自定义变量** | 可以使用正则表达式来匹配客户端原始请求中携带的指定请求参数的值、指定HTTP Header的值、指定Cookie参数的值、指定的URI，正则表达式匹配命中时，将对应的值拼接到Cachekey中。具体使用请参见 [配置示例](https://help.aliyun.com/zh/cdn/user-guide/create-custom-cache-keys#section-5cc-6mo-05b "")。 |



![自定义Cachekey](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9251548471/p87142.png)

6. 单击 **确定**。


## 配置示例

### **URI**

客户端的请求`http://aliyundoc.com/a/b/image.jpg`和`http://aliyundoc.com/a/b/c/image.jpg` 将视为请求同一个文件，该文件的Cachekey为`http://aliyundoc.com/c/image.jpg`。![URI](<Base64-Image-Removed>)

### **请求参数**

客户端的请求`http://aliyundoc.com/a/b/image.jpg?delete_par=1&modify_par=1`将按规则添加`add_par=1`，删除`delete_par`，将`modify_par`的值修改为`2`，最终转化为`http://aliyundoc.com/a/b/image.jpg?modify_par=2&add_par=1`。

**重要**

请求参数中，如对同一个变量同时进行了多个操作，则各种操作的生效优先级：新增>删除>保留>修改。

![参数操作](<Base64-Image-Removed>)

### **HTTP Header**

客户端请求的HTTP Header的`User-Agent`和`Accept-Language`的值将被拼接到Cachekey中。例如请求`http://aliyundoc.com/a/b/image.jpg`中的`User-Agent=Mozilla/5.0 (Linux; X11)`，`Accept-Language=en`，则该请求的Cachekey为：`http://aliyundoc.com/a/b/image.jpgMozilla/5.0(Linux;X11)en`。![HTTP Header](<Base64-Image-Removed>)

### **自定义变量**

**示例一**

变量名为`language`，来源为`Request Header`，来源字段名为`Accept-Language`，匹配规则为 `([%w]+),([%w]+)`，变量表达式为`$1aa`。![自定义变量](<Base64-Image-Removed>)

客户端的请求`http://aliyundoc.com/a/b/image.jpg`且携带HTTP请求头`Accept-Language=en,ch`，则匹配规则将匹配到`en`赋值给变量表达式中的`$1`。变量表达式还将在末尾拼接上`aa`，得到`enaa`的变量并取别名为`language`，拼接在URL后方形成最终的Cachekey：`http://aliyundoc.com/a/b/image.jpgenaa`。

**说明**

变量表达式中的`$n`的含义是匹配规则中第`n`个括号所匹配到的内容。例如示例一中`Accept-Language=en,ch`，匹配规则为`([%w]+),([%w]+)`，则`$1=en`，`$2=ch`。

**示例二**

变量名为`expired`，来源为`Request Cookie`，来源字段名为`a`，匹配规则为`[%w]+:(.*)`，变量表达式为 `$1`。![自定义变量](<Base64-Image-Removed>)

客户端的请求`http://aliyundoc.com/a/b/image.jpg`且携带`Cookie a=expired_time:12635187`，则匹配规则将匹配到`12635187`赋值给变量表达式中的`$1`并取别名为`expired`，拼接在URL后方形成最终的Cachekey：`http://aliyundoc.com/a/b/image.jpg12635187`。

**示例三**

同时设置URI规则和自定义变量。

URI：

将所有URI符合`/abc/.*/abc`的请求都合并成 `/abc`。![示例三](<Base64-Image-Removed>)

自定义变量：

变量名为`testname`，来源为`Path`，匹配规则为`/abc/xyz/(.*)`，变量表达式为`$1`。![示例三](<Base64-Image-Removed>)

客户端的请求URL`http://aliyundoc.com/abc/xyz/abc/image.jpg`，按URI的配置Cachekey将被合并成`http://aliyundoc.com/abc/image.jpg`， 然后根据自定义变量的配置该URL将会命中`/abc/xyz/(.*)`，此时`$1`将被赋值为`abc`并拼接到Cachekey中，形成最终的Cachekey：`http://aliyundoc.com/abc/image.jpgabc`，从而达到两个规则组合使用，实现更复杂的缓存逻辑。

如果没有匹配到CacheKey的自定义变量，则变量表达式`$1`就不会被拼接到CacheKey中。

**示例四**

同时设置规则条件和自定义变量，使来自Mobile端和PC端的请求生成不同的Cachekey。

`Mobile`规则条件：

`User-Agent`包含`*Mobile*,*Android*,*iPhone*,*ipad*`其中任意一个

![image](<Base64-Image-Removed>)

`PC`规则条件：

`User-Agent`不包含`*Mobile*,*Android*,*iPhone*,*ipad*`其中任意一个

![image](<Base64-Image-Removed>)

`Mobile`自定义Cachekey：

**规则条件** 选择`Mobile`， **自定义变量** 的 **变量名** 为`Mobile`， **来源** 为`Path`， **匹配规则** 为`/`， **变量表达式** 为`+mobile`。

![image](<Base64-Image-Removed>)

`PC`自定义Cachekey：

**规则条件** 选择`PC`， **自定义变量** 的 **变量名** 为`PC`， **来源** 为`Path`， **匹配规则** 为`/`， **变量表达式** 为`+pc`。

![image](<Base64-Image-Removed>)

客户端的请求URL`http://aliyundoc.com/image.jpg`，根据`User-Agent`的值，请求分别命中`Mobile`端和`PC`端的自定义Cachekey规则。`Mobile`端最终生成的Cachekey为：`http://aliyundoc.com/image.jpg+mobile`；`PC`端最终生成的Cachekey为：`http://aliyundoc.com/image.jpg+pc`。