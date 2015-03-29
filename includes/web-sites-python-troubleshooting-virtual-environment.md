﻿如果部署脚本检测到兼容的虚拟环境已存在，它将跳过在 Azure 上创建虚拟环境的过程。这可以显著加快部署。通过 pip，将跳过已安装的软件包。

在某些情况下，您可能想要强制删除该虚拟环境。如果您决定将虚拟环境包含为您的存储库的一部分，需要执行此操作。如果您需要删除某些软件包或测试对 requirements.txt 的更改，可能也会执行此操作。

有几个选项用于管理 Azure 上的现有虚拟环境：

### 选项 1：使用 FTP

通过 FTP 客户端，连接到服务器，然后您就可以删除 env 文件夹。请注意，某些 FTP 客户端（例如 Web 浏览器）可能为只读而不允许您删除文件夹，因此您要确保使用具备此功能的 FTP 客户端。在 Azure 门户上，您网站的仪表板页面中显示 FTP 主机名和用户。

### 选项 2：切换运行时

这是利用以下事实的一个替代方法：部署脚本不匹配期望的 Python 版本时，它将删除 env 文件夹。这将有效地删除现有环境，然后创建新环境。

1. 切换到其他版本的 Python（通过 runtime.txt 或网站配置页）
1. git 推送一些更改 （如果有任何 pip 安装错误，请忽略）
1. 切换回初始版本的 Python
1. git 再次推送某些更改

### 选项 3：自定义部署脚本

如果您已自定义部署脚本，则可以更改 deploy.cmd 中的代码以强制其删除 env 文件夹。