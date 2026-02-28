### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/) [使用代码包部署应用](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/) 制作符合SAE要求的代码包

# 制作符合SAE要求的代码包

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用代码包部署应用](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/)[下一篇：部署Java应用](https://help.aliyun.com/zh/sae/deploy-java-applications-by-using-a-jar-package)

该文章对您有帮助吗？

反馈

通过代码包部署应用前，您需要先按照SAE的要求制作代码包。

## Java

1. 制作SAE应用的JAR包或WAR包的方式与您日常打包代码的方式没有任何差异。

2. [通过WAR包或JAR包部署Java应用](https://help.aliyun.com/zh/sae/deploy-java-applications-by-using-a-jar-package "")。


## PHP

1. 下载示例代码包 [hello-sae-php.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250613/grmnyh/hello-sae-php.zip) 并解压，目录结构如下：


```plaintext
.
├── nginx
│   ├── default.conf
│   ├── fastcgi_params
│   └── root.dir
├── php # 程序所在目录
│   ├── index.php # 程序入口文件
│   └── phpinfo.php
```

2. 将`php/`中的代码替换为您的业务代码。

3. 按需修改`nginx/`中的配置文件。


|     |     |     |
| --- | --- | --- |
| **配置项** | **默认值** | **如何修改** |
| 服务端口 | 80 | 修改`default.conf`文件，在`server{ }`中的首行添加`listen <port>;`（例如`listen 8080;`）。 |
| 程序入口文件名称 | index.php（如示例代码所示） | 如果您修改了程序入口文件名称，请同步执行以下操作：<br>修改`default.conf`文件，将`index index.php index.html index.htm;`改为`index <程序入口文件名称>;`，将`fastcgi_index index.php;`改为`fastcgi_index <程序入口文件名称>;`。 |
| 程序所在目录名称 | php（如示例代码所示） | 如果您修改了程序所在目录名称，请同步执行以下操作：<br>修改`root.dir`文件，将`root /home/admin/app/php;`改为`root /home/admin/app/<程序所在目录名称>;` |

4. 将当前目录中的内容打包为ZIP包，注意`nginx`和`php`需位于ZIP包的根路径。

5. [通过ZIP包部署PHP应用](https://help.aliyun.com/zh/sae/deploy-a-php-application-by-using-a-zip-package-in-the-sae-console-2-0 "")。


## Python

1. 了解ZIP打包规范。

   - 打包代码根目录文件或者文件夹，切勿打包外层目录。

   - 如果应用存在requirements.txt，需要将其置于根目录下一同打包，便于部署时SAE自动安装软件依赖。
2. 基于示例 [hello-sae-python.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250613/ikpfhb/hello-sae-python.zip)，将您的Python应用打包为ZIP包。示例的目录结构如下（示例代码依赖Flask、Gunicorn等，详见requirements.txt）：


```plaintext
.
├── app
│   └── hello.py
└── requirements.txt （需在根目录，可选）
```


执行如下命令：


```shell
# 获取示例
wget https://sae-demo-cn-shenzhen.oss-cn-shenzhen.aliyuncs.com/demo/1.0/hello-sae-python.zip
# 解压示例
unzip hello-sae-python.zip -d hello-sae-python && rm -rf hello-sae-python.zip && cd hello-sae-python
# 将示例代码替换为您的Python程序（将/path/to/your-python-project/替换为您的项目路径）
rm -rf app/* requirements.txt
cp -r /path/to/your-python-project/. app/
cp -r /path/to/your-python-project/requirements.txt ./
# 打包成ZIP包
zip -r my-python-app.zip app requirements.txt
```

3. [通过ZIP包部署Python应用](https://help.aliyun.com/zh/sae/deploy-a-python-application-using-a-zip-package "")。


## .NET Core

1. 了解ZIP打包规范。


|     |     |     |
| --- | --- | --- |
| **ZIP目录** | **对应SAE实例运行时目录** | **描述** |
| ./start.sh | /home/admin/start.sh | 存放应用启动脚本。 |
| ./your-dotnet-project | /home/admin/app/nginx/\*.conf | 存放.NET程序。 |


   - 打包代码根目录文件或者文件夹，切勿打包外层目录。

   - 如果应用存在启动脚本，如`start.sh`文件等，需要将其置于根目录下一同打包，便于部署时SAE自动执行启动脚本。
2. [下载](https://dotnet.microsoft.com/zh-cn/download/dotnet) 并 [安装](https://learn.microsoft.com/zh-cn/dotnet/core/install/).NET SDK，确保选择 [SAE支持的.NET Core版本](https://help.aliyun.com/zh/sae/sae-2-microservices-code-package-deployment/#d85bc5302cayo "")。可以通过执行`dotnet --version`验证是否安装成功。如果报错，请按照报错信息安装对应的依赖包。

3. 编译和构建项目，执行如下命令：


```shell
# 进入项目路径（将/path/to/your-dotnet-project/替换为您的项目路径）
cd /path/to/your-dotnet-project/
# 还原项目依赖
dotnet restore
# 编译源码
dotnet build -c Release -o demo
# -c Release：表示优化代码以提高运行时性能，并去除调试信息，适宜于生产环境部署。
# -o demo：表示构建输出的目录为demo。
```

4. 编写项目的启动脚本（如：`start.sh`）并为其添加可执行权限`chmod +x ./start.sh`。

5. 通过tree命令查看当前目录结构。


```plaintext
.
├── appsettings.Development.json
├── appsettings.json
├── appsettings.Production.json
├── your-dotnet-project
...
└── start.sh
```

6. 打包为ZIP包。


```shell
zip -r demo.zip *
# demo.zip：表示需要打包成的zip文件。
# *：表示打包当前目录中的所有文件及文件夹。
```

7. [通过ZIP包部署.NET Core应用](https://help.aliyun.com/zh/sae/deploy-net-core-applications-using-zip-packages "")。