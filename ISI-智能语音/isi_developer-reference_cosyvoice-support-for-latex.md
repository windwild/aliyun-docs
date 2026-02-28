### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/) [开发参考](https://help.aliyun.com/zh/isi/developer-reference/) [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/developer-reference/cosvoice-large-model-for-speech-synthesis/) Latex能力支持说明

# Latex能力支持说明

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：录音操作指南](https://help.aliyun.com/zh/isi/developer-reference/recording-operation-guide)[下一篇：语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)

该文章对您有帮助吗？

反馈

本文档说明CosyVoice大模型在中小学数学场景中对Latex公式的语音合成支持能力。

## **使用场景**

中小学数学教学场景。

## **支持的语种**

仅支持中文。

## **支持的模型**

当前仅支持cosyvoice-v2模型。

## **使用方式**

在待合成文本中，使用`\` 或 `$`标签将Latex公式内容包裹起来，即可将公式转换为自然语言。

支持的格式包括（ `...` 表示实际公式内容）：

- `$...$`

- `$$...$$`

- `\(...\)`

- `\[...\]`


例如，文本“让我们做一道算术题，$2 + 3 = 5$”转成语音后的中文读法为：“让我们做一道算术题，二加三等于五”。

## **注意事项**

- 在字符串字面量中，转义字符应使用双反斜杠 `\\` 进行转义，即：

  - `\a` → `\\a`

  - `\n` → `\\n`

  - `\t` → `\\t`

  - `\f` → `\\f`

  - `\r` → `\\r`

  - `\v` → `\\v`
- 未使用 `\` 或 `$` 分隔符明确标注的公式内容，可能朗读错误或被系统忽略。

- 不支持对 Markdown 格式中的数学公式进行语音朗读。

- 若分隔符（`\` 或 `$` ）中包含中文字符，可能导致语音合成结果不准确。

- 当公式前后存在英文内容时，将会跳过 `\` 或 `$`中的内容。

- 部分未被支持的公式格式将直接以原文形式输出。


## **支持的标签或符号**

内容涵盖基础数学、特殊符号、几何图形、条件表达式、单位等多种常见数学标签与符号，并分别给出其含义说明、公式示例及对应的中文语音读法。

### **基础数学**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **标签或符号** | **作用** | **公式内容示例** | **待合成文本示例** | **中文读法** |
| + | 加 | 2 + 3 = 5 | $2 + 3 = 5$ | 二加三等于五 |
| - | 减 | 3 - 2 = 1 | $3 - 2 = 1$ | 三减二等于一 |
| \\pm | 加减 | \\pm 1 \\pm 2 | $\\pm 1\\pm 2$ | 正负一加减二 |
| 正负 |
| \\times | 乘 | 2 \\times 3 = 6 | $2 \\times 3 = 6$ | 二乘三等于六 |
| × | 2 × 3 = 6 | $$2 × 3 = 6$$ |
| \* | 2 \* 3 = 6 | \\(2 \* 3 = 6\\) |
| \\div | 除 | 6\\div2=3 | \\\[6\\div2=3\\\] | 六除二等于三 |
| ÷ | 6÷2=3 | $6÷2=3$ |
| / | 6/2=3 | $6/2=3$ |
| = | 等于 | 3+5=8 | $3+5=8$ | 三加五等于八 |
| < | 小于 | 1< 2 | $1< 2$ | 一小于二 |
| ≤ | 小于等于 | 3≤5 | $3≤5$ | 三小于等于五 |
| <= | 3<=5 | $3<=5$ |
| \\leq | 3\\leq5 | $3\\leq 5$ |
| \\le | 3\\le5 | $3\\le 5$ |
| \\leqq | 3\\leqq5 | $3\\leqq 5$ |
| \\leqslant | 3\\leqslant5 | $3\\leqslant 5$ |
| > | 大于 | 2>1 | $2>1$ | 二大于一 |
| ≥ | 大于等于 | 5≥3 | $5≥3$ | 五大于等于三 |
| >= | 5>=3 | $5>=3$ |
| \\geq | 5\\geq3 | $5\\geq 3$ |
| \\ge | 5\\ge3 | $5\\ge 3$ |
| \\geqq | 5\\geqq3 | $5\\geqq 3$ |
| \\geqslant | 5\\geqslant3 | $5\\geqslant 3$ |
| \\frac | 分数 | 2\\frac3 | $\\frac {2}{3}$ | 三分之二 |
| ^ | 次方 | 2^1 | $2^{1}$ | 二的一次方 |
| \\sqrt | 开根 | \\sqrt{9} = 3 | $\\sqrt {9} = 3$ | 根号下九等于三 |
| \\sqrt\[3\]{8} = 2 | $\\sqrt\[3\]{8} = 2$ | 三次根号下八等于二 |
| \\% | 百分比 | 5\\% | $5\\%$ | 百分之五 |
| \| | 绝对值 | ∣3∣=3 | $\|3\| =3$ | 绝对值三的绝对值等于三 |
| \\vert | 3\\vert=3 | $\\vert 3\\vert =3$ | 绝对值三绝对值等于三 |
| \\lg | 对数 | lg {10} | $\\lg {10}$ | log十 |
| \\log | 对数 | \\log{5} | $\\log{5}$ | log五 |
| \\ln | 自然对数 | \\lnX | $ln {10}$ | LN十 |
| ! | 阶乘 | 5! | $5!$ | 五的阶乘 |
| () | 括号 | （2+1） | $(2+1)$ | 括号内二加一 |
| \\{ \\} | $\\{2+1\\}$ | 大括号二加一反大括号 |

### **特殊数学符号**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **标签或符号** | **转换** | **公式内容示例** | **待合成文本示例** | **中文读法** |
| \\alpha | alpha | \\alpha | $\\alpha$ | α |
| \\Alpha | \\Alpha | $\\Alpha$ |
| \\beta | beta | \\beta | $\\beta$ | β |
| \\Beta | \\Beta | $\\Beta$ |
| \\gamma | gamma | \\gamma | $\\gamma$ | γ |
| \\Gamma | \\Gamma | $\\Gamma$ |
| \\delta | delta | \\delta | $\\delta$ | Δ |
| \\Delta | \\Delta | $\\Delta$ |
| \\infty | 无穷大（中） | \\infty | $\\infty$ | 无穷大 |
| ∞ | infty （英） | ∞ | $∞$ |

### **几何**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **标签或符号** | **作用** | **公式内容示例** | **公式输入示例** | **中文读法** |
| \\pi | 派 | \\pi=3.14159 | $\\pi =3.14159$ | 派等于三点一四一五九 |
| \\sin (sine | 三角函数 | \\sin (sine30^\\circ=1\\frac2 | $\\sin 30^\\circ =\\frac {1}{2}$ | sine三十度等于二分之一 |
| \\cos (cosine | $\\cos 30^\\circ =\\frac {\\sqrt {2}}{2}$ | cosine三十度等于二分之根号下二 |
| \\tan (tangent | $\\tan 30^\\circ =\\frac {\\sin 30^\\circ}{\\cos 30^\\circ}$ | tangent三十度等于cosine三十度分之sine三十度 |
| \\csc (cosecant | $\\csc A$ | cosecant A |
| \\sec (secant | $\\sec A$ | secant A |
| \\cot (cotangent | $\\cot A$ | cotangent A |
| \\angle | 角 | \\angle AB | $\\angle AB$ | 角A B |
| ∠ | ∠AB | $∠AB$ |
| ^\\circ | 度 | ∠AB = 30^\\circ | $∠AB = 30^\\circ$ | 角A B 等于三十度 |
| \\odot | 圆 | \\odot | $\\odot$ | 圆 |
| \\overset\\frown | 弧 | \\overset\\frown {BC} | $\\overset\\frown {BC}$ | 弧BC |
| \\rm{Rt} | 直角 | \\because \\rm{Rt}\\triangle ABC | $\\because \\rm{Rt}\\triangle ABC$ | 因为直角三角形ABC |
| \\mathrm{Rt} | \\therefore AB \\perp BC | $\\therefore AB \\perp BC$ | 所以AB垂直于BC |
| \\triangle | 三角形 | \\triangleABC | $\\triangle ABC$ | 三角形ABC |
| △ | △ABC | $△ABC$ |
| \\parallelogram | 平行四边形 | \\parallelogramABCD | $\\parallelogram ABCD$ | 平行四边形ABCD |
| \\perp | 垂直 | AB \\perp BC | $AB \\perp BC$ | A B 垂直于 B C |
| \\bot | AB \\bot BC | $AB \\bot BC$ |
| ⊥ | AB ⊥ BC | $AB ⊥ BC$ |
| \\parallel | 平行 | A\\parallel B | $A\\parallel B$ | A平行于B |
| \\equalparallel | 平行且相等于 | A\\equalparallel B | $A\\equalparallel B$ | A平行且相等于B |
| \\cong | 全等 | △ABC\\cong△DEF | $△ABC\\cong△DEF$ | 三角形ABC全等于三角形DEF |

### **条件**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **标签或符号** | **作用** | **公式示例公式内容示例** | **公式输入示例** | **中文读法** |
| \\implies | 推出 | \\implies 1+1=2 | $\\implies 1+1=2$ | 推出一加一等于二 |
| \\iff | 等价 | p\\iffq | $p\\iffq$ | p等价q |
| \\because | 因为 | \\because a = b \\therefore b=a | $\\because a = b \\therefore b=a$ | 因为a等于b所以b等于a |
| \\therefore | 所以 |

### **单位**

单位需要使用 `\unit`、`\quantity`、`\mathit`、`\mathrm` 或 `\rm` 标签进行包裹。例如：`\unit{cm}`。

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **标签或符号** | **读法** | **公式内容示例** | **公式输入示例** | **中文读法** |
| mm | 毫米 | 5\\quantity{mm} | $5\\quantity{mm}$ | 五毫米 |
| cm | 厘米 | 5\\quantity{cm} | $5\\quantity{cm}$ | 五厘米 |
| dm | 分米 | 5\\quantity{dm} | $5\\quantity{dm}$ | 五分米 |
| m | 米 | 5\\quantity{m} | $5\\quantity{m}$ | 五米 |
| km | 千米 | 5\\quantity{km} | $5\\quantity{km}$ | 五千米 |
| g | 克 | 5\\quantity{g} | $5\\quantity{g}$ | 五克 |
| kg | 千克 | 5\\quantity{kg} | $5\\quantity{kg}$ | 五千克 |
| t | 吨 | 5\\quantity{t} | $5\\quantity{t}$ | 五吨 |
| mm^2 | 平方毫米 | 5\\quantity{mm^2} | $5\\quantity{mm^2}$ | 五平方毫米 |
| cm^2 | 平方厘米 | 5\\quantity{cm^2} | $5\\quantity{cm^2}$ | 五平方厘米 |
| dm^2 | 平方分米 | 5\\quantity{dm^2} | $5\\quantity{dm^2}$ | 五平方分米 |
| m^2 | 平方米 | 5\\quantity{m^2} | $5\\quantity{m^2}$ | 五平方米 |
| km^2 | 平方千米 | 5\\quantity{km^2} | $5\\quantity{km^2}$ | 五平方千米 |
| mm^3 | 立方毫米 | 5\\quantity{mm^3} | $5\\quantity{mm^3}$ | 五立方毫米 |
| cm^3 | 立方厘米 | 5\\quantity{cm^3} | $5\\quantity{cm^3}$ | 五立方厘米 |
| dm^3 | 立方分米 | 5\\quantity{dm^3} | $5\\quantity{dm^3}$ | 五立方分米 |
| m^3 | 立方米 | 5\\quantity{m^3} | $5\\quantity{m^3}$ | 五立方米 |
| km^3 | 立方千米 | 5\\quantity{km^3} | $5\\quantity{km^3}$ | 五立方千米 |
| ml | 毫升 | 5\\quantity{ml} | $5\\quantity{ml}$ | 五毫升 |
| s | 秒 | 5\\quantity{s} | $5\\quantity{s}$ | 五秒 |
| min | 分钟 | 5\\quantity{min} | $5\\quantity{min}$ | 五分 |
| h | 小时 | 5\\quantity{h} | $5\\quantity{h}$ | 五小时 |
| km/h | 千米每小时 | 5\\quantity{km/h} | $5\\quantity{km/h}$ | 五千米每小时 |
| g/l | 克每升 | 5\\quantity{g/l} | $5\\quantity{g/l}$ | 五克每升 |