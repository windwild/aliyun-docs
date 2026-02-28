### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 智能语音交互移动端SDK更新通知

# 智能语音交互移动端SDK更新通知

更新时间：2025-10-27 23:43:09

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

重要更新说明

快速自检指南

步骤一：检查SDK发布日期

步骤二：判断更新需求

SDK更新实施指南

更新步骤

更新包结构说明

更新包结构示例

更新成功验证

方法一：代码接口验证

方法二：日志验证（通用方法）

更新包下载地址：移动端SDK选择与下载

仅在线功能（包括语音识别、语音合成）更新包（APP\_CODE : 01B）

带在线功能的离线语音合成更新包(APP\_CODE : 028)：

带在线功能的离线唤醒+离线语音合成更新包(APP\_CODE : 029)：

## **重要更新说明**

**2025年11月服务端SSL证书将会变化，为避免对您的业务造成影响，请务必在2025年11月10日之前将相关移动端SDK更新到V2.5.14-0XX-202303XX（即2023年3月发布的移动端SDK）及以后版本，否则将无法正常运行语音交互功能，包括但不限于唤醒、在线/离线语音合成、语音识别。**

**此说明仅针对使用2023年3月（不含3月）之前发布的移动端SDK的用户，如已更新可忽略。**

如遇问题，可随时通过工单或者服务热线与我们联系。

## **快速自检指南**

### **步骤一：检查SDK发布日期**

通过直接查看包（库）名日期（Android库后缀名为`.aar`，iOS库后缀名为`.framework`或`.a`），或者通过以下命令检查SDK的发布日期：

Android

iOS

```bash
# 1. 解压获得其中动态库
unzip nuisdk-release.aar

# 2. 打印信息
strings jni/arm64-v8a/libneonui_shared.so | grep '\[time\]'

# 3. 打印信息如下，[time]后即为发布日期
"[sha1]:fb5c6c4 [author]:shichen.fsc [time]:2023-03-30 12:12:33 +0800 [commit]:[Update] change openssl to Mbedtls in project unit [branch]: (HEAD -> develop/2.5.14-01B/unit_merge_taobaozhibo, origin/develop/2.5.14-01B/unit_merge_taobaozhibo)"
```

```bash
strings nuisdk.framework/nuisdk| grep '\[time\]'

# 2. 打印信息如下，[time]后即为发布日期
"[sha1]:e4ddba5 [author]:joseph.zgd [time]:2022-03-17 10:51:37 +0800 [commit]:fix a dead lock when request was canceled and when starting. [branch]: (grafted, HEAD -> develop/2.5.14-01B/unit_merge_taobaozhibo, origin/develop/2.5.14-01B/unit_merge_taobaozhibo)"
```

### **步骤二：判断更新需求**

✅ **发布日期为2023年3月以后（含3月）：** 无需更新

❌ **发布日期为2023年3月以前：** 通过如下命令进一步判断，若无法判断，建议更新

Android

iOS

```bash
# 1. 解压获得其中动态库
unzip nuisdk-release.aar

# 2. 打印结果，若有结果则需要更新，否则无需更新
strings jni/arm64-v8a/libneonui_shared.so | grep mbedtls
```

```bash
# 打印结果，若有结果则需要更新，否则无需更新
nm nuisdk.framework/nuisdk| grep mbedtls
```

## **SDK更新实施指南**

### **更新步骤**

**说明**

**更新原则**：采用同版本包平替原则，确保兼容性

1. 第一步：确认APP\_CODE（版本编号）

可根据包名进行确认APP\_CODE，例如：


   - 包名：V2.7.0-01B-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 01B

   - 包名：V2.7.0-028-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 028

   - 包名：V2.7.0-029-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 029


若无法通过包名判断，可通过SDK日志确定：

1. 通过初始化接口开启SDK日志功能，或者直接用移动端连接IDE工具查看运行日志。

2. 搜索日志 NUI SDK VER

      如：NUI SDK VER <V2.5.14-028-20230426> DATE <Apr 26 2023> V2.5.14-028-20230426 表示版本编号为028


若依然无法确定版本编号，请工单或者服务热线获取帮助。

**APP\_CODE说明：**

   - **01B：** 在线功能（语音识别、语音合成）更新包。此更新包仅包含在线功能（一句话识别、实时转写、语音合成、文件转写），不包含任何离线功能。

   - **028：** 带在线功能的离线语音合成更新包。此更新包可运行离线语音合成功能，同时也包含在线功能（一句话识别、实时转写、语音合成、文件转写）。

   - **029：** 带在线功能的离线唤醒+离线语音合成更新包。此更新包可运行离线唤醒/命令词和离线语音合成功能，同时也包含在线功能（一句话识别、实时转写、语音合成、文件转写）。
2. 第二步： [下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "") 更新包

根据APP\_CODE和平台类型下载相应的更新包。

3. 第三步：进行更新






Android



iOS



















   - 使用动态库集成（如libneonui\_shared.so）：用更新包中的同名库文件替换，头文件可从aar中获得

   - 使用nuisdk-release.aar集成：直接用更新包中的aar文件替换同名aar文件


   - 使用静态库（如libneonui.a）集成：用更新包中的同名库文件替换，头文件可从framework中获得

   - 使用nuisdk.framework集成：直接用更新包中的framework替换同名framework


**重要**

⚠️ 资源文件（resources）保持原有配置，请勿随意更新已在使用的资源文件。

### **更新包结构说明**

Android

iOS

- MinSizeRel 最小体积成果物

  - V2.5.14-029-20230404\_Android.zip demo工程文件

  - android\_libs 各架构动态库

  - nuisdk-minifyEnabled-release.aar 混淆后的aar

  - nuisdk-release.aar 未混淆的aar
- RelWithDebugInfo 待调试信息发布成果物

  - V2.5.14-029-20230404\_Android.zip demo工程文件

  - android\_libs 各架构动态库

  - nuisdk-minifyEnabled-release.aar 混淆后的aar

  - nuisdk-release.aar 未混淆的aar
- resources 资源包

- 版本记录和特殊说明.txt 版本更新记录


- V2.5.14-01B-20230415\_iOS.zip demo工程

- libs 静态库

- nuisdk.framework framework包

- resources 资源包

- 版本记录和特殊说明.txt 版本更新记录


### **更新包结构示例**

Android

iOS

```plaintext
V2.5.14-029-20230404_Android
├── [ 192]  MinSizeRel
│   ├── [ 28M]  V2.5.14-029-20230404_Android.zip
│   ├── [ 192]  android_libs
│   │   ├── [ 128]  arm64-v8a
│   │   ├── [ 128]  armeabi-v7a
│   │   ├── [ 128]  x86
│   │   └── [ 128]  x86_64
│   ├── [ 14M]  nuisdk-minifyEnabled-release.aar
│   └── [ 14M]  nuisdk-release.aar
├── [ 192]  RelWithDebugInfo
│   ├── [ 35M]  V2.5.14-029-20230404_Android.zip
│   ├── [ 192]  android_libs
│   │   ├── [ 128]  arm64-v8a
│   │   ├── [ 128]  armeabi-v7a
│   │   ├── [ 128]  x86
│   │   └── [ 128]  x86_64
│   ├── [ 17M]  nuisdk-minifyEnabled-release.aar
│   └── [ 17M]  nuisdk-release.aar
├── [ 256]  resources
│   ├── [2.8K]  cei.json
│   ├── [  38]  copylist.txt
│   ├── [2.8M]  kws.bin
│   ├── [1.3K]  nui.json
│   ├── [ 160]  tts
│   │   ├── [4.6M]  languagedata_embedded.bin
│   │   ├── [ 539]  parameter.cfg
│   │   └── [ 128]  voices
│   │       ├── [2.5M]  aijia
│   │       └── [9.0K]  voicefont.bin
│   └── [244K]  vad.bin
└── [2.3K]  版本记录和特殊说明.txt
```

```plaintext
V2.5.14-01B-20230415_iOS
├── [2.2M]  V2.5.14-01B-20230415_iOS.zip
├── [ 128]  libs
│   ├── [ 18M]  libneonui_static_full.a
│   └── [5.8M]  libspeechcei.a
├── [ 224]  nuisdk.framework
│   ├── [ 160]  Headers
│   │   ├── [5.3K]  NeoNui.h
│   │   ├── [5.5K]  NeoNuiCode.h
│   │   └── [2.0K]  NeoNuiTts.h
│   ├── [ 747]  Info.plist
│   ├── [ 192]  Resources.bundle
│   │   ├── [2.8K]  cei.json
│   │   ├── [  22]  copylist.txt
│   │   ├── [1.3K]  nui.json
│   │   └── [  96]  tts
│   │       └── [ 535]  parameter.cfg
│   └── [4.9M]  nuisdk
├── [ 224]  resources
│   ├── [2.8K]  cei.json
│   ├── [  22]  copylist.txt
│   ├── [1.3K]  nui.json
│   └── [  96]  tts
│       └── [ 535]  parameter.cfg
└── [2.9K]  版本记录和特殊说明.txt
```

## **更新成功验证**

更新完成后，请使用以下方法验证更新是否成功：

### **方法一：代码接口验证**

Android

iOS

调用Android接口获得版本号：

```java
String version = NativeNui.GetInstance().GetVersion();
Log.i(TAG, "current sdk version: " + version);
```

将打印类似如下内容：

`current sdk version: V2.5.14-028-20230426`

若日期晚于202303，则说明更新成功。

调用iOS接口获得版本号：

```objectc
NSString *version = [NSString stringWithUTF8String:[_nui nui_get_version]];
```

将打印类似如下内容：

`V2.5.14-028-20230426`

若日期晚于202303，则说明更新成功。

### **方法二：** 日志验证（通用方法 **）**

1. 通过初始化接口开启SDK日志功能，或者直接连接IDE工具查看运行日志。

2. 搜索日志 NUI SDK VER

如：NUI SDK VER <V2.5.14-028-20230426> DATE <Apr 26 2023> V2.5.14-028-20230426 表示当前为20230426更新包。


## **更新包下载地址**： [移动端SDK选择与下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")

### 仅在线功能（包括语音识别、语音合成）更新包（APP\_CODE : 01B）

如V2.7.0-01B-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 01B

此更新包仅包含在线功能（一句话识别、实时转写、语音合成、文件转写），不包含任何离线功能。

### 带在线功能的离线语音合成更新包(APP\_CODE : 028)：

如V2.7.0-028-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 028

此更新包可运行离线语音合成功能，同时也包含在线功能（一句话识别、实时转写、语音合成、文件转写）。

### 带在线功能的离线唤醒+离线语音合成更新包(APP\_CODE : 029)：

如V2.7.0-029-20251010\_Android\_OpenSSL.tar.gz，APP\_CODE : 029

此更新包可运行离线唤醒/命令词和离线语音合成功能，同时也包含在线功能（一句话识别、实时转写、语音合成、文件转写）。