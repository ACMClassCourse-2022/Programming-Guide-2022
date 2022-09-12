# 设定 C++ 环境

本文档将协助设定适合于编写 C++ 程序的开发环境。

请选择您的系统，以便跳转至适合您的系统的设定方式。
- [Windows](#Windows)
- [MacOS](#MacOS)
- [Linux](#Linux)

## Windows

鉴于线上评测系统 (Online Judge) 采用 Linux 环境，为防止出现不同平台行为差异导致结果不同，且 Linux 环境更适合编写 C++ 代码，我们推荐使用 Windows Subsystem for Linux (WSL)，WSL 相对虚拟机来说更为轻量化，性能更好。

关于使用 WSL 1 还是 WSL 2，我们推荐使用 WSL 2。[为什么？](FAQs.md#为什么建议使用-wsl2-而不是-wsl1)

### 先决条件

必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11。

注：若要检查 Windows 版本及内部版本号，选择 Windows 徽标键 + R，然后键入「winver」，选择「确定」。可通过选择「开始」>「设置」>「Windows 更新」>「检查更新」来更新到最新的 Windows 版本。

### 安装 WSL

如果从未安装 WSL，请打开一个 Windows Terminal（推荐，需要在 Microsoft 商店或 GitHub 下载）、Powershell 或者 cmd（[不知道如何打开？](FAQs.md#如何打开命令行？)），并输入以下内容，此命令将启用所需的可选组件，下载最新的 Linux 内核，将 WSL 2 设置为默认值。
```bash
wsl --install
```

请**务必**仔细查看输出的信息，特别注意是否出现 `error` 或 `fail` 相关内容，如出现，请仔细阅读输出信息，然后设定相关的选项。如果没有错误，请**重启**。

#### 常见错误信息
```bash
请启用虚拟机平台 Windows 功能并确保在 BIOS 中启用虚拟化。
```
此情况是由于 Windows 无法使用虚拟化来启动，请按照以下步骤解决：

1. 请「控制面板」>「程序」>「程序和功能」>「启用或关闭 Windows 功能」中打开「虚拟机平台」。

2. 请在 BIOS 中启动虚拟化。如果不知道怎么打开 BIOS 或在 BIOS 中启动虚拟化，请询问助教。

### 安装发行版

请在 Powershell 或 cmd 输入以下指令以确认是否已有安装 WSL 发行版
```bash
wsl -l -v
```

**如果没有显示发行版，请到 Microsoft store 下载 Ubuntu 或 Ubuntu-22.04。**

### 设定 Windows Terminal （可选）

通常情况下，如果已经安装了 Ubuntu，Windows Terminal 会自动设定打开 Ubuntu。

如果你希望能在 Windows 资源管理器中直接打开当前文件夹的 terminal，你可以在 Windows Terminal 顶栏下拉菜单中点击设置 > 默认配置 > 勾选「使用使用父进程目录」。

### 设定 C++ 开发环境

由于如果发行版包管理器不是最新的，安装应用可能出现问题，因此请先在**发行版的命令行**中输入以下内容更新
```bash
sudo apt update
```

如果感觉下载速度过慢（校内速度尚可），可以考虑更换软件源，具体请自行搜索，此操作随时可更换。

然后安装必要的安装包
- gcc
- make
- CMake
- valgrind
- git
- gdb

可以输入以下指令安装这些组件
```bash
sudo apt install build-essential make cmake gdb valgrind git
```

### 安装 CLion

你可以在 JetBrains 官网下载 [CLion](https://www.jetbrains.com/clion/download/) 并安装，也可以下载 [JetBrains ToolBox](https://www.jetbrains.com/zh-cn/toolbox-app/)。

如果没有学信网的认证，请使用许可证激活。如需要许可证激活，请参考上海交通大学软件授权中心上 [JetBrains（在线授权版）安装和授权流程](https://lic.sjtu.edu.cn/Default/huatishow/tag/MDAwMDAwMDAwMLJ4iqE/)操作。

### 设定 WSL 环境

通过 CLion 打开任一项目（如没有项目，请新建一个），从顶栏 File > settings > Build, Execution, Deployment > Toolchains 打开工具链设定，点按「-」去除所有的工具链，然后点按「+」并选择 WSL，CLion 将会自动检查工具链完整性，如有缺少，请安装后重试。

## MacOS
TODO

## Linux

### Ubuntu

请打开一个命令行界面，然后输入
```bash
sudo apt install build-essential make cmake gdb valgrind git
```

### 其他发行版本

请自行安装以下组件：
- gcc / clang
- make
- CMake
- valgrind
- git
- gdb

安装这些组件后，请安装 CLion。（如果你觉得应当使用自由软件，你可以自行设定 VSCodium。）
