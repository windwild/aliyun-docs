### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[图形化管理工具ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/graphical-management-tools-ossbrowser-1-0/)安装ossbrowser 1.0

# 安装ossbrowser 1.0

更新时间：2025-12-12 06:02:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图形化管理工具ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/graphical-management-tools-ossbrowser-1-0/)[下一篇：登录ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/logon-to-ossbrowser-1-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Windows系统

macOS系统

Linux 系统

CentOS 7/CentOS 8/Ubuntu 14

后续步骤

当您需要快速使用图形化工具上传文件、下载文件、删除文件、设置权限策略时，可以下载并安装ossbrowser 1.0工具，使用多种方式登录工具，进行相关操作。

**重要**

- 本文以最新版本1.18.0为例进行说明。关于ossbrowser 1.0的所有版本，请参见 [all-releases.md](https://github.com/aliyun/oss-browser/blob/develop/all-releases.md)。

- 在公网环境下上传或下载超过10 GB的大文件时，容易因网络状况不稳定而导致传输失败。如果您处于非内网环境，并且需要传输超过10 GB的大文件，建议您使用 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/#2a4b2fbc2f0a3 "")。


## **Windows系统**

1. 根据Windows系统架构下载对应的 [Windows x32压缩包](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-win32-ia32.zip) 或 [Windows x64压缩包](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-win32-x64.zip)。

2. 解压。

3. 在解压后的文件夹中，双击oss-browser.exe，打开ossbrowser 1.0。


## **macOS系统**

1. 下载 [macOS压缩包](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-darwin-x64.zip)。

2. 解压。

3. 在文件夹oss-browser-darwin-x64中，右键单击oss-browser.app，选择 **打开**。

4. 在对话框中，单击 **打开**。

5. 在对话框中，单击 **允许**。


## **Linux 系统**

### **CentOS 7/CentOS 8/Ubuntu 14**

CentOS 7

CentOS 8

Ubuntu 14

1. 安装图形界面。

如何为CentOS 7安装图形化软件，请参见 [为Linux实例安装图形化界面](https://help.aliyun.com/zh/ecs/user-guide/installing-a-graphical-desktop-environment-for-a-linux-instance#4556985065pzj "")。

2. 安装依赖文件。

1. 执行以下命令更新yum源。















      ```shell
      sudo yum update
      ```

2. 执行以下命令安装依赖文件libgtk-x11-2.0.so.0。















      ```shell
      sudo yum install gtk2-2.24.31-1.el7.x86_64
      ```

3. 执行以下命令安装依赖文件libXtst.so.6。















      ```shell
      sudo yum install libXtst-1.2.3-1.el7.x86_64
      ```

4. 执行以下命令安装依赖文件libXss.so.1。















      ```shell
      sudo yum install libXScrnSaver-1.2.2-6.1.el7.x86_64
      ```

5. 执行以下命令安装依赖文件libgconf-2.so.4。















      ```shell
      sudo yum install GConf2-3.2.6-8.el7.x86_64
      ```
3. 安装ossbrowser 1.0。

1. 执行以下命令下载CentOS 7压缩包。















      ```shell
      sudo wget https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-linux-x64.zip
      ```

2. 执行以下命令解压。















      ```shell
      sudo unzip oss-browser-linux-x64.zip
      ```

3. 执行以下命令进入目录oss-browser-linux-x64。















      ```shell
      cd oss-browser-linux-x64/
      ```

4. 执行以下命令打开ossbrowser 1.0。















      ```shell
      sudo ./oss-browser
      ```

1. 安装图形界面。

如何为CentOS 8安装图形化软件，请参见 [为Linux实例安装图形化界面](https://help.aliyun.com/zh/ecs/user-guide/installing-a-graphical-desktop-environment-for-a-linux-instance#4556985065pzj "")。

2. 安装依赖文件。

1. 执行以下命令更新yum源。















      ```shell
      sudo yum update
      ```

2. 执行以下命令安装依赖文件libgtk-x11-2.0.so.0。















      ```shell
      sudo yum install gtk2-2.24.32-5.el8.x86_64
      ```

3. 执行以下命令安装依赖文件libX11-xcb.so.1。















      ```shell
      sudo yum install libX11-xcb-1.6.8-5.el8.x86_64
      ```

4. 执行以下命令安装依赖文件libXtst.so.6。















      ```shell
      sudo yum install libXtst-1.2.3-7.el8.x86_64
      ```

5. 执行以下命令安装依赖文件libXss.so.1。















      ```shell
      sudo yum install libXScrnSaver-1.2.3-1.el8.x86_64
      ```

6. 执行以下命令安装依赖文件libgconf-2.so.4。















      ```shell
      sudo yum install GConf2-3.2.6-22.el8.x86_64
      ```

7. 执行以下命令安装依赖文件libasound.so.2。















      ```shell
      sudo yum install alsa-lib-1.2.5-4.el8.x86_64
      ```
3. 安装ossbrowser 1.0。

1. 执行以下命令下载CentOS 8压缩包。















      ```shell
      sudo wget https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-linux-x64.zip
      ```

2. 执行以下命令解压。















      ```shell
      sudo unzip oss-browser-linux-x64.zip
      ```

3. 执行以下命令进入目录oss-browser-linux-x64。















      ```shell
      cd oss-browser-linux-x64/
      ```

4. 执行以下命令打开ossbrowser 1.0。















      ```shell
      sudo ./oss-browser
      ```

1. 安装图形界面。

如何为Ubuntu 14安装图形化软件，请参见 [How to Install a Desktop (GUI) on an Ubuntu Server](https://help.aliyun.com/zh/ecs/user-guide/installing-a-graphical-desktop-environment-for-a-linux-instance#4556985065pzj "")。

2. 安装依赖文件。

1. 执行以下命令更新apt源。















      ```shell
      sudo apt update
      ```

2. 执行以下命令安装依赖文件libgtk-x11-2.0.so.0。















      ```shell
      sudo apt install libgtk2.0-0
      ```

3. 执行以下命令安装依赖文件libX11-xcb.so.1。















      ```shell
      sudo apt install libx11-xcb-dev
      ```

4. 执行以下命令安装依赖文件libXtst.so.6。















      ```shell
      sudo apt install libxtst6
      ```

5. 执行以下命令安装依赖文件libXss.so.1。















      ```shell
      sudo apt install libxss1
      ```

6. 执行以下命令安装依赖文件libgconf-2.so.4。















      ```shell
      sudo apt install libgconf-2-4
      ```
3. 安装ossbrowser 1.0。

1. 执行以下命令下载Ubuntu压缩包。















      ```shell
      sudo wget https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-linux-x64.zip
      ```

2. 执行以下命令解压。















      ```shell
      sudo unzip oss-browser-linux-x64.zip
      ```

3. 执行以下命令进入目录oss-browser-linux-x64。















      ```shell
      cd oss-browser-linux-x64/
      ```

4. 执行以下命令打开ossbrowser 1.0。















      ```shell
      sudo ./oss-browser
      ```

## **后续步骤**

安装完ossbrowser 1.0后，接下来您就可以进行 [登录ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/logon-to-ossbrowser-1-0#9ba38e7d178j4 "") 的相关操作。