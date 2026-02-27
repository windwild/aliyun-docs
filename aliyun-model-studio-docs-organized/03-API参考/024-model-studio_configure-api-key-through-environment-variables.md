### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[准备工作](https://help.aliyun.com/zh/model-studio/preparations/)配置API Key到环境变量

# 将API Key配置到环境变量

更新时间：2025-10-14 23:33:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key)[下一篇：安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

常见问题

建议您把API Key配置到环境变量，从而避免在代码里显式地配置API Key，降低泄漏风险。

## **前提条件**

已开通百炼并获取API Key，具体请参见 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

## **操作步骤**

Linux系统

macOS系统

Windows系统

添加永久性环境变量

添加临时性环境变量

如果您希望API Key环境变量在当前用户的所有新会话中生效，可以添加永久性环境变量。

1. 执行以下命令来将环境变量设置追加到`~/.bashrc`文件中。















```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
echo "export DASHSCOPE_API_KEY='YOUR_DASHSCOPE_API_KEY'" >> ~/.bashrc
```



也可以手动修改`~/.bashrc`文件。



**手动修改**






执行以下命令，打开`~/.bashrc`文件。

















```zsh
nano ~/.bashrc
```





在配置文件中添加以下内容。

















```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
export DASHSCOPE_API_KEY="YOUR_DASHSCOPE_API_KEY"
```





在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















```bash
source ~/.bashrc
```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















```bash
echo $DASHSCOPE_API_KEY
```


如果您仅希望在当前会话中使用该环境变量，可以添加临时性环境变量。

1. 执行以下命令。















```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
export DASHSCOPE_API_KEY="YOUR_DASHSCOPE_API_KEY"
```

2. 执行以下命令，验证该环境变量是否生效。















```bash
echo $DASHSCOPE_API_KEY
```


添加永久性环境变量

添加临时性环境变量

如果您希望API Key环境变量在当前用户的所有新会话中生效，可以添加永久性环境变量。

1. 在终端中执行以下命令，查看默认Shell类型。















```bash
echo $SHELL
```

2. 根据默认Shell类型进行操作。






Zsh



Bash



















1. 执行以下命令来将环境变量设置追加到 `~/.zshrc` 文件中。















      ```zsh
      # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
      echo "export DASHSCOPE_API_KEY='YOUR_DASHSCOPE_API_KEY'" >> ~/.zshrc
      ```



      也可以手动修改`~/.zshrc` 文件。



      **手动修改**






      执行以下命令，打开Shell配置文件。

















      ```zsh
      nano ~/.zshrc
      ```





      在配置文件中添加以下内容。

















      ```bash
      # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
      export DASHSCOPE_API_KEY="YOUR_DASHSCOPE_API_KEY"
      ```





      在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















      ```zsh
      source ~/.zshrc
      ```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















      ```zsh
      echo $DASHSCOPE_API_KEY
      ```


1. 执行以下命令来将环境变量设置追加到 `~/.bash_profile` 文件中。















      ```zsh
      # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
      echo "export DASHSCOPE_API_KEY='YOUR_DASHSCOPE_API_KEY'" >> ~/.bash_profile
      ```



      也可以手动修改`~/.bash_profile` 文件。



      **手动修改**






      执行以下命令，打开Shell配置文件。

















      ```bash
      nano ~/.bash_profile
      ```





      在配置文件中添加以下内容。

















      ```bash
      # 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
      export DASHSCOPE_API_KEY="YOUR_DASHSCOPE_API_KEY"
      ```





      在nano编辑器中，按Ctrl + X，接着按Y，再按Enter以保存并关闭文件。

2. 执行以下命令，使变更生效。















      ```zsh
      source ~/.bash_profile
      ```

3. 重新打开一个终端窗口，运行以下命令检查环境变量是否生效。















      ```zsh
      echo $DASHSCOPE_API_KEY
      ```


如果您仅希望在当前会话中使用该环境变量，可以添加临时性环境变量。

> 以下命令适用于 Zsh 和 Bash。

1. 执行以下命令。















```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
export DASHSCOPE_API_KEY="YOUR_DASHSCOPE_API_KEY"
```

2. 执行以下命令，验证该环境变量是否生效。















```bash
echo $DASHSCOPE_API_KEY
```


在Windows系统中，您可以通过系统属性、CMD或PowerShell配置环境变量。

系统属性

CMD

PowerShell

**说明**

- 此方式配置的环境变量永久生效。

- 修改系统环境变量需具备管理员权限。

- 配置环境变量后不会立即影响已经打开的命令窗口、IDE或其他正在运行的应用程序。您需要重新启动这些程序或者打开新的命令行使环境变量生效。


1. 在Windows系统桌面中按`Win+Q`键，在搜索框中搜索 **编辑系统环境变量**，单击打开 **系统属性** 界面。

2. 在 **系统属性** 窗口，单击 **环境变量**，然后在 **系统变量** 区域下单击 **新建**， **变量名** 填入`DASHSCOPE_API_KEY`， **变量值** 填入您的DashScope API Key。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8252115371/p894015.png)

3. 依次单击三个窗口的 **确定**，关闭系统属性配置页面，完成环境变量配置。

4. 打开CMD（命令提示符）窗口或Windows PowerShell窗口，执行如下命令检查环境变量是否生效。

   - CMD查询命令：















     ```powershell
     echo %DASHSCOPE_API_KEY%
     ```



     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912522.png)

   - Windows PowerShell查询命令：















     ```powershell
     echo $env:DASHSCOPE_API_KEY
     ```



     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912525.png)

添加永久性环境变量

添加临时性环境变量

如果您希望API Key环境变量在当前用户的所有新会话中生效，可以按如下操作。

1. 在CMD中运行以下命令。















```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
setx DASHSCOPE_API_KEY "YOUR_DASHSCOPE_API_KEY"
```

2. 打开一个新的CMD窗口。

3. 在新的CMD窗口运行以下命令，检查环境变量是否生效。















```bash
echo %DASHSCOPE_API_KEY%
```



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912522.png)


如果您仅希望在当前会话中使用该环境变量，可以在CMD中运行以下命令。

```bash
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
set DASHSCOPE_API_KEY=YOUR_DASHSCOPE_API_KEY
```

您可以在当前会话运行以下命令检查环境变量是否生效。

```bash
echo %DASHSCOPE_API_KEY%
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912522.png)

添加永久性环境变量

添加临时性环境变量

如果您希望API Key环境变量在当前用户的所有新会话中生效，可以按如下操作。

1. 在PowerShell中运行以下命令。















```powershell
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
[Environment]::SetEnvironmentVariable("DASHSCOPE_API_KEY", "YOUR_DASHSCOPE_API_KEY", [EnvironmentVariableTarget]::User)
```

2. 打开一个新的PowerShell窗口。

3. 在新的PowerShell窗口运行以下命令，检查环境变量是否生效。















```powershell
echo $env:DASHSCOPE_API_KEY
```



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912525.png)


如果您仅希望在当前会话中使用该环境变量，可以在PowerShell中运行以下命令。

```powershell
# 用您的百炼API Key代替YOUR_DASHSCOPE_API_KEY
$env:DASHSCOPE_API_KEY = "YOUR_DASHSCOPE_API_KEY"
```

您可以在当前会话运行以下命令检查环境变量是否生效。

```powershell
echo $env:DASHSCOPE_API_KEY
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1317988371/p912525.png)

## **常见问题**

Q：用echo命令确认环境变量设置成功了，为什么运行代码还是提示找不到API Key？

A：具体原因如下：

- 情况一： **没有设置永久性环境变量**。临时环境变量只在当前终端会话有效，对于已经启动的 IDE 或其他应用程序并不会生效。请参考本文中设置永久性环境变量的方法。

- 情况二： **没有重启IDE、命令行工具或应用**。

  - 通常需要重启IDE（如VS Code）或命令行工具，使其能够加载最新的环境变量。

  - 如果在部署应用后设置了环境变量，可能需要重启应用服务，让应用能够重新加载环境变量。
- 情况三： **需要在配置文件添加环境变量**。如果您的应用是通过服务管理器（如systemd、supervisord）启动的，可能需要在服务管理器的配置文件中添加环境变量。

- 情况四： **用了sudo命令**。如果使用`sudo python xx.py`运行脚本，可能会遗漏当前用户环境变量，因为`sudo`默认不继承所有环境变量。您可采用`sudo -E python xx.py`命令，其中的`-E` 参数确保环境变量被传递。如有权限执行该脚本，可以直接执行 `python xx.py`。