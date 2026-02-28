### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别闲时版](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition-off-peak-edition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code-1/)C++ Demo

# C++ Demo

更新时间：2024-04-16 01:49:44

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java Demo](https://help.aliyun.com/zh/isi/developer-reference/java-demo)[下一篇：Go Demo](https://help.aliyun.com/zh/isi/developer-reference/go-demo-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

示例说明

下载安装

关键接口

代码示例

常见问题

C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

为什么连接不到framework？

SDK报错“DNS resolved timeout”是什么问题？

C++ SDK ASR请求有DNS解析失败的情况导致异常，报错“ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."”如何解决？

C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过如何解决？

C++ SDK在Windows上使用，报错缺少nlsCommonSdk.dll如何解决？

C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错“nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known”如何解决？

C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错“\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...”如何解决？

C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

本文介绍了如何使用阿里云智能语音服务提供的C++ SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 当前最新版本：1.2.2。发布日期：2018年11月14日。

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference#topic-2170103 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## 示例说明

录音文件识别示例使用了nlsCommonSDK的`AlibabaNlsCommon::FileTrans`提交识别请求和查询识别结果，采用的是RPC风格的POP API调用方式。

## 下载安装

[下载nlsCommonSDK](https://gw.alipayobjects.com/os/bmw-prod/933cf60b-bdbb-4c62-a67d-f314c47e6952.zip)，文件包含如下几部分：

- CMakeLists.txt：示例代码工程的CMakeList文件。

- readme.txt：SDK说明。

- release.log：更新记录。

- version：版本号。

- build.sh：Demo编译脚本。

- demo：示例文件。




| 文件名 | 描述 |
| --- | --- |



|     |     |
| --- | --- |
| 文件名 | 描述 |
| fileTransDemo.cpp | 录音文件识别示例。 |

- include：包含SDK头文件，以及部分第三方头文件。各文件如下表所示。




| 文件名 | 描述 |
| --- | --- |



|     |     |
| --- | --- |
| 文件名 | 描述 |
| openssl | OpenSSL头文件目录，Linux下使用。 |
| curl | curl头文件目录。 |
| uuid | UUID头文件目录，Linux下使用。 |
| json | jsoncpp头文件目录。 |
| Global.h | 全局声明头文件。 |
| FileTrans.h | 录音文件识别头文件。 |

- lib：包含curl、jsoncpp动态库。

根据平台不同，使用如下版本软件加载库文件：


  - Linux（Glibc：2.5及以上，Gcc4或Gcc5）

  - Windows（VS2013、VS2015）


编译运行操作步骤：

**重要**

  - Linux下安装工具要求如下：

    - Glibc 2.5及以上

    - Gcc4或Gcc5
  - Windows下需要您自行搭建示例工程（请将示例文件修改为含有BOM的`UTF-8`编码格式），依赖库如下：

    - openssl-1.0.2j

    - libuuid-1.0.3

    - curl-7.60.0

    - jsoncpp-0.10.6

假设示例文件已解压至`path/to`路径下，在Linux终端依次执行如下命令编译运行程序。

- 支持Cmake：

确认本地系统已安装Cmake 2.4及以上版本。

1. 切换目录：`cd path/to/sdk/lib`。

2. 解压缩文件：`tar -zxvpf linux.tar.gz`。

3. 切换目录：`cd path/to/sdk`。

4. 执行编译脚本：`./build.sh`。

5. 切换目录：`cd path/to/sdk/demo`。

6. 执行文件识别示例程序：`./fileTransDemo your-AccessKeyId your-AccessKeySecret your-appkey`。
- 不支持Cmake：

1. 切换目录：`cd path/to/sdk/lib`。

2. 解压缩文件：`tar -zxvpf linux.tar.gz`。

3. 切换目录：`cd path/to/sdk/demo`。

4. 使用g++编译命令编译示例程序：`g++ -o fileTransDemo fileTransDemo.cpp -I path/to/sdk/include/ -L path/to/sdk/lib/linux -ljsoncpp -lssl -lcrypto -lcurl -luuid -`lalibabacloud-idst-common `-D_GLIBCXX_USE_CXX11_ABI=0`。

5. 指定库路径：`export LD_LIBRARY_PATH=path/to/sdk/lib/linux/`。

6. 执行文件识别示例程序：`./fileTransDemo your-AccessKeyId your-AccessKeySecret your-appkey`。

## 关键接口

FileTrans：录音文件识别对象。您可以从中获取录音文件识别结果、失败信息等。

## 代码示例

**说明**

[下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav) **。** 该示例录音文件为PCM编码格式16000 Hz采样率，管控台设置的模型为通用模型。如果使用其他录音文件，请填入对应的编码格式和采样率，并在管控台设置对应的模型。关于模型设置，请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

```cpp
#include <iostream>
#include <string>
#include "FileTrans.h"

#ifdef _WIN32
#include <windows.h>
#endif // _WIN32

using std::string;
using std::cout;
using std::endl;
using namespace AlibabaNlsCommon;

#if defined _WIN32
string UTF8ToGBK(const string &strUTF8) {

        int len = MultiByteToWideChar(CP_UTF8, 0, strUTF8.c_str(), -1, NULL, 0);
        unsigned short * wszGBK = new unsigned short[len + 1];
        memset(wszGBK, 0, len * 2 + 2);

        MultiByteToWideChar(CP_UTF8, 0, (char*)strUTF8.c_str(), -1, (wchar_t*)wszGBK, len);

        len = WideCharToMultiByte(CP_ACP, 0, (wchar_t*)wszGBK, -1, NULL, 0, NULL, NULL);

        char *szGBK = new char[len + 1];
        memset(szGBK, 0, len + 1);
        WideCharToMultiByte(CP_ACP, 0, (wchar_t*)wszGBK, -1, szGBK, len, NULL, NULL);

        string strTemp(szGBK);
        delete[] szGBK;
        delete[] wszGBK;

        return strTemp;
}
#endif

// 录音文件识别
int fileTrans(const char* accessKeyId, const char* accessKeySecret, const char* appKey, const char* fileLink) {
    FileTrans request;

    /*设置阿里云账号AccessKey Id*/
    request.setAccessKeyId(accessKeyId);
    /*设置阿里云账号AccessKey Secret*/
    request.setKeySecret(accessKeySecret);
    /*设置阿里云AppKey*/
    request.setAppKey(appKey);
    /*设置音频文件url地址*/
    request.setFileLinkUrl(fileLink);
    /*设置闲时版连接域名,这里默填写的是上海地域,如果要使用其它地域请参考各地域POP调用参数*/
    request.setDomain("speechfiletranscriberlite.cn-shanghai.aliyuncs.com");
    /*设置闲时版连接版本*/
    request.setServerVersion("2021-12-21");
    /*设置连接地域*/
    request.setRegionId("cn-shanghai");

    /*开始文件识别, 成功返回0, 失败返回-1*/
    int ret = request.applyFileTrans();
    if (-1 == ret) {
        cout << "FileTrans failed: " << request.getErrorMsg() << endl; /*获取失败原因*/
        return -1;
    } else {
        string result = request.getResult();

#ifdef _WIN32
        result = UTF8ToGBK(result);
#endif

                cout << "FileTrans successed: " << result << endl;

                return 0;
    }
}

int main(int argc, char* argv[]) {
    if (argc < 4) {
        cout << "FileTransDemo need params : <AccessKey Id> <AccessKey Secret> <app - key>" << endl;
        return -1;
    }

    const char* accessKeyId = argv[1];
    const char* accessKeySecret = argv[2];
    const char* appKey = argv[3];
    const char* fileLink = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav";

    fileTrans(accessKeyId, accessKeySecret, appKey, fileLink);

    return 0;
}
```

## 常见问题

### C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

可以。Linux下支持GCC 4.8.5或以上版本。目前已验证且顺利编译运行的GCC版本包括4.8.5、5.5.0、8.4.0。

### 为什么连接不到framework？

framework中代码采用Objective-C和C++混合编写而成，所以需要使用.mm后缀文件进行调用，同时请确保工程的头文件路径与库文件路径设置正确。

### SDK报错“DNS resolved timeout”是什么问题？

查看`/etc/resolv.conf`文件中nameserver的设置，建议增加并优先使用以下配置：`nameserver 114.114.114.114`。

### C++ SDK ASR请求有DNS解析失败的情况导致异常，报错“ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."”如何解决？

- 旧版（3.0及以前版本）：在高并发或者电脑DNS忙碌的情况下容易出现以上问题，建议您更新到3.1.X版本，或进行再次重启请求。

- 新版（3.0及以后版本）：已经对此问题进行防御，若仍然偶现此问题，则为电脑DNS忙碌，需要再次重启请求。


### C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过如何解决？

除了`CMakeLists.txt`，全工程都需要修改该参数，例如`config/linux.thirdparty.debug.cmake`和`config/linux.thirdparty.release.cmake`，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ SDK在Windows上使用，报错缺少nlsCommonSdk.dll如何解决？

3.1及以后版本无nlsCommonSdk.dll。

### C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

NlsSdkCpp2.0版本的SDK每一个请求为一个线程，且接口为同步接口。

NlsSdkCpp3.X版本的SDK内部由第三方库libevent统一处理事件消息，并发性能更强，且接口为异步接口。

### C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

工程默认为`_GLIBCXX_USE_CXX11_ABI=0`，全工程都需要修改该参数，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错“nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known”如何解决？

1. SDK中会查看当前设备开启的所有协议族（IPv4、IPv6）进行DNS解析请求，`nls-gateway-cn-shanghai.aliyuncs.com`不支持 IPv6，返回解析错误，从而导致SDK DNS解析失败退出。可禁用当前设备的IPv6协议族，后续CppSdk产品改进对这方面进行可配置处理。

2. 建议您升级到3.1.12及以后版本。


### C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错“\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...”如何解决？

以上现象为无法连接网络，查看日志发现DNS域名解析出来的IP链接不成功，进一步通过Ping判断网络不通。由于本地拦截DNS解析，导致SDK内部`libevent`的`evdns_getaddrinfo`获得错误的IP。

解决办法：

- 3.1.12版本以前可将evdns\_getaddrinfo()手动替换成系统的getaddrinfo()。

- 3.1.12版本可在`CMakeLists.txt`中修改`add_definitions(-DNLS_USE_NATIVE_GETADDRINFO)`。

- 3.1.12及以后版本增加setDirectHost()接口，您可以在SDK外部进行DNS解析，获取正确IP后通过该接口设入。

- 3.1.13及以后版本已解决此问题，若运行时仍存在上述问题，建议调用接口setUseSysGetAddrInfo(true)。


### C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

如果传入的文本没有采用UTF-8编码，在文本中含有中文字符时，语音合成SDK调用start函数会失败，返回错误信息`Socket recv failed, errorCode: 0`。错误码为0表示服务端已经关闭了连接，此时应检查传入的文本是否采用UTF-8编码。