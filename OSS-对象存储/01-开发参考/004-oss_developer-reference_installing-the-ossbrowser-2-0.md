### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[图形化管理工具ossbrowser 2.0（预览版）](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview/)安装ossbrowser 2.0

# 安装ossbrowser 2.0

更新时间：2025-12-03 04:32:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Windows系统

macOS系统

Linux系统

常见问题

后续步骤

本文为您介绍在Windows、macOS以及Linux系统上如何安装ossbrowser 2.0。

**重要**

- Windows系统仅支持Windows 7及以上版本包括Windows Server。

- Linux x64发行版本众多，需要安装图形界面依赖文件，因此不推荐使用。建议您在Windows或macOS上使用ossbrowser 2.0。


## **Windows系统**

1. 单击下载 [Windows x86-64安装包](https://gosspublic.alicdn.com/oss-browser2-prod/2.1.1/oss-browser2-win-x64-2.1.1.exe)。

2. 双击运行下载安装包，选择安装目录后点击 **安装**。

3. 在桌面找到 **oss-browser2** 应用程序双击运行打开。如图所示

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7768831371/p871290.png)


## **macOS** 系统

1. 打开命令行窗口执行`uname -m`查看系统架构，如图所示为arm64架构。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7768831371/p864985.png)

2. 请根据您的系统架构下载对应的安装包：

   - x86\_64架构： [macOS x86-64安装包](https://gosspublic.alicdn.com/oss-browser2-prod/2.1.1/oss-browser2-mac-x64-2.1.1.dmg)。

   - arm64架构： [macOS arm64安装包](https://gosspublic.alicdn.com/oss-browser2-prod/2.1.1/oss-browser2-mac-arm64-2.1.1.dmg)。
3. 双击打开安装包。

4. 根据提示将 **oss-browser2.app** 拖动到Applications文件夹。

5. 打开启动台，找到 **oss-browser2** 应用程序双击运行打开。

1. 提示有风险，依然单击打开。

2. 打开后界面如图所示。

      ![1c5986fd7ee0d3672fbf95135c39ddda](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7768831371/p871283.png)

## **Linux** 系统

**重要**

root用户无法运行ossbrowser 2.0，请使用 **非root用户** 登录系统来使用ossbrowser 2.0。

以下示例以Ubuntu 22.04版本为例。

1. 安装图形界面。

请执行以下命令安装图形界面。其他Linux系统发行版安装图形界面，请参见 [为Linux实例安装图形化界面](https://help.aliyun.com/zh/ecs/user-guide/installing-a-graphical-desktop-environment-for-a-linux-instance#45605c5065pmz "")。















```bash
sudo apt-get update
sudo apt-get install ubuntu-desktop
reboot
```

2. 使用 **非root** 用户登录系统。

使用ECS实例安装完图形界面后，需重启系统 **通过VNC远程连接** 的方式进入系统图形界面。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7768831371/p869906.png)

3. 下载安装包。















```shell
wget https://gosspublic.alicdn.com/oss-browser2-prod/2.1.1/oss-browser2-linux-x86_64-2.1.1.AppImage
```

4. 安装ossbrowser 2.0。

1. 右键单击下载的安装包，点击`Properties`。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7768831371/p871343.png)

2. 单击`Permissions`勾选Execute开关，允许将该文件作为程序执行。

      ![image](<Base64-Image-Removed>)

3. 双击打开ossbrowser 2.0软件包，如图所示。

      ![image](<Base64-Image-Removed>)

## **常见问题**

**Ubuntu 22.04系统无法正常启动ossbrowser 2.0**

- **问题**：若您在启动ossbrowser 2.0时遇到如图所示报错信息，通常是由于AppImage应用里的Chromium沙箱需要特定权限才能正常运行，而当前用户未具备此权限。

![image](<Base64-Image-Removed>)

- **解决方案**：您可以评估并安装AppImageLauncher工具，之后再次启动ossbrowser 2.0时，该工具会自动解决AppImage应用相关的权限和依赖问题。具体的下载与安装步骤如下。















```shell
#下载AppImageLauncher工具
sudo wget https://github.com/TheAssassin/AppImageLauncher/releases/download/v2.2.0/appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb

#安装AppImageLauncher工具
sudo apt install ./appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb
```


## **后续步骤**

登录ossbrowser 2.0以及相关配置项说明，请参见 [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")。