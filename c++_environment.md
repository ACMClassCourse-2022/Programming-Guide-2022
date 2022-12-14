# 设定 C++ 环境

本文档将协助设定适合于编写 C++ 程序的开发环境。

关于集成开发环境 (IDE)，为方便后续多文件编译，我们推荐使用 [CLion][clion] 或者 [Visual Studio Code][vsc]。如果你知道如何设定其他开发环境，并能够处理多文件编译，你也可以不使用 CLion 或 VS Code。但如果你是 Windows 用户，也请设定 WSL 环境。

请选择您的系统，以便跳转至适合您的系统的设定方式。

- [Windows](#windows)
- [macOS](#macos)
- [Linux](#linux)

[clion]: https://www.jetbrains.com/clion/
[vsc]: https://code.visualstudio.com/

## Windows

鉴于线上评测系统 (Online Judge) 采用 Linux 环境，为防止出现不同平台行为差异导致结果不同，且 Linux 环境更适合编写 C++ 代码，我们推荐使用 Windows Subsystem for Linux (WSL)，WSL 相对虚拟机来说更为轻量化，性能更好。

关于使用 WSL 1 还是 WSL 2，我们推荐使用 WSL 2。[为什么？][why-wsl2]

[why-wsl2]: FAQs.md#为什么建议使用-wsl2-而不是-wsl1

### 先决条件

必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11。

注：若要检查 Windows 版本及内部版本号，可以按 <kbd>⊞ Win</kbd>+<kbd>R</kbd>，然后键入「winver」，选择「确定」。可通过选择「开始」>「设置」>「Windows 更新」>「检查更新」来更新到最新的 Windows 版本。

### 安装 WSL

如果从未安装 WSL，请打开一个管理员权限的 Windows Terminal（推荐，需要在 Microsoft Store 或 GitHub 下载）、Powershell 或者 cmd（[不知道如何打开？][open-terminal]），并输入以下内容，此命令将启用所需的可选组件，下载最新的 Linux 内核，将 WSL 2 设置为默认值。

```bash
wsl --install
```

请**务必**仔细查看输出的信息，特别注意是否出现 `error` 或 `fail` 相关内容，如出现，请仔细阅读输出信息，然后设定相关的选项。如果没有错误，请**重启**。

[open-terminal]: FAQs.md#如何打开命令行？

#### Windows Terminal

右键 Windows 图标，点击「Windows 终端 (管理员)」或「Powershell (管理员)」。

#### 常见错误

##### 安装过程中出现网络问题导致卡顿

请关注安装到何时出问题：
- 如果没有下载完「WSL 内核」，请下载 [WSL 内核安装包][wsl-kernel]。
- 如果「WSL 内核」已经下载完毕，请直接去 Microsoft Store 下载 Ubuntu。

你也可以查看 [微软官方文档][wsl-install] 来检查问题。

[wsl-kernel]: https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
[wsl-install]: https://docs.microsoft.com/en-us/windows/wsl/install-manual

##### 未开启虚拟化

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

**如果没有显示发行版，请到 Microsoft store 下载 Ubuntu。**

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
如果时间充裕，建议此时升级所有可升级的包。可以使用以下指令
```bash
sudo apt upgrade
```

### 安装并配置 CLion

(若你想使用 VS Code，则可以跳过此节。)

你可以在 JetBrains 官网下载 [CLion][clion-download] 并安装，也可以下载 [JetBrains ToolBox][jb-toolbox]。

如果没有学信网的认证，请使用许可证激活。如需要许可证激活，请参考上海交通大学软件授权中心上 [JetBrains（在线授权版）安装和授权流程][jb-licensing] 操作。

[clion-download]: https://www.jetbrains.com/clion/download/
[jb-toolbox]: https://www.jetbrains.com/zh-cn/toolbox-app/
[jb-licensing]: https://lic.sjtu.edu.cn/Default/huatishow/tag/MDAwMDAwMDAwMLJ4iqE/

#### 设定 CLion 下 WSL 环境

通过 CLion 打开任一项目（如没有项目，请新建一个），从顶栏 File > settings > Build, Execution, Deployment > Toolchains 打开工具链设定，点按「-」去除所有的工具链，然后点按「+」并选择 WSL，CLion 将会自动检查工具链完整性，如有缺少，请安装后重试。

然后尝试运行 hello world。（常见错误： CMake 版本过低，建议把最低版本设定在 3.16。）

#### 设定 CLion 下 Valgrind

在 CLion 设定中搜索 Valgrind，将 Valgrind executable 修改为
- 如果你使用的是 Ubuntu-22.04
```
\\wsl$\Ubuntu-22.04\usr\bin\valgrind
```
- 如果你使用的是 Ubuntu
```
\\wsl$\Ubuntu\usr\bin\valgrind
```

### 安装并配置 VS Code

(若你想使用 CLion，则可以跳过此节。)

你可以在 [VS Code 官网][vsc] 下载并安装 Visual Studio Code。

CLion 是一个专为 C/C++ 设计的 IDE，而 VS Code 是一个较为通用的文本编辑器，你需要自行安装一些扩展以适应 C++ 的开发。

我们推荐使用 [clangd] 而不是微软官方的 C++ 扩展。首先在 Ubuntu 的命令行中安装 clangd:

```sh
sudo apt install clangd
```

然后在 VS Code 里 **依次** 进行以下步骤:

1. 安装扩展 [Remote - WSL][ext-remote-wsl]
   (扩展面板可以用 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> 打开。)
1. 点击左下角绿色「><」按钮，选择 New Window。
1. 确认左下角绿色区域已经显示 WSL 字样。
1. 安装以下扩展:
   - [C/C++ Extension Pack][ext-cxx-pack]
   - [clangd][ext-clangd]
     - 当 clangd 提示禁用 IntelliSense 时，选择禁用。

[clangd]: https://clangd.llvm.org/
[ext-remote-wsl]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl
[ext-cxx-pack]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack
[ext-clangd]: https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd

## macOS

### 切换至 Zsh

旧版本 macOS 默认的 shell 是 Bash，为了获得更好的使用体验，建议切换到 Zsh，在 Terminal 中输入以检查 shell：

```bash
echo $SHELL
```

新版本 macOS 默认的 shell 即为 Zsh，无需切换。

若为 Bash，可以使用以下命令切换至 Zsh：

```bash
chsh -s /bin/zsh
```

### 安装 Homebrew

#### 官方源（推荐）

如若有条件连接绝大多数国际网站，可以在 Terminal 中输入：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 国内源

全部采用国内源，在 Terminal 中输入：

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

#### 使用 Homebrew 的注意事项

可使用 Homebrew 安装任意命令行程序，甚至可以用其管理 GUI 程序。

某些时候，安装完毕后，Homebrew 会显示相关 Caveats，建议遵循相关提醒。

### 安装相关组件

在 Terminal 中输入：

```bash
brew install cmake git 
```

Valgrind 在 macOS 的最新版本中无法使用。若恰为旧版本且希望安装 valgrind，可自行安装。

### 安装 Clion

你可以在 JetBrains 官网下载 [CLion][clion-download] 并安装，也可以下载 [JetBrains ToolBox][jb-toolbox]。

如果没有学信网的认证，请使用许可证激活。如需要许可证激活，请参考上海交通大学软件授权中心上 [JetBrains（在线授权版）安装和授权流程][jb-licensing] 操作。

通常情况下，CLion 会自动配置环境。你也可以通过 CLion 打开任一项目（如没有项目，请新建一个），从顶栏 File > settings > Build, Execution, Deployment > Toolchains 打开工具链设定检查。

### 安装并配置 VS Code（可选）

你可以在 [VS Code 官网][vsc] 下载并安装 Visual Studio Code。

CLion 是一个专为 C/C++ 设计的 IDE，而 VS Code 是一个较为通用的文本编辑器，你需要自行安装一些扩展以适应 C++ 的开发。

我们推荐使用 [clangd] 而不是微软官方的 C++ 扩展，macOS 自带 clangd，无需额外安装。

然后在 VS Code 里安装以下扩展: (扩展面板可以用 <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>x</kbd> 打开。)

- [C/C++ Extension Pack][ext-cxx-pack]
- [clangd][ext-clangd]
  - 当 clangd 提示禁用 IntelliSense 时，选择禁用。

### 安装 LLVM（可选）

由于文件较大，安装时间较长，对网络质量要求高，且并不是特别必要，可自行选择是否安装。

macOS 本身自带 LLVM，但由于其闭源，无法知道其中细节，可选用开源的 LLVM。

```sh
brew install llvm
echo 'export PATH="/opt/homebrew/opt/llvm/bin:$PATH"' >> ~/.zshrc
```

## Linux

### Ubuntu

请打开一个命令行界面，然后输入
```bash
sudo apt install build-essential make cmake gdb valgrind git
```

#### 安装 CLion

(若你想使用 VS Code，则可以跳过此节。)

你可以在 JetBrains 官网下载 [CLion][clion-download] 并安装，也可以下载 [JetBrains ToolBox][jb-toolbox]。

如果没有学信网的认证，请使用许可证激活。如需要许可证激活，请参考上海交通大学软件授权中心上 [JetBrains（在线授权版）安装和授权流程][jb-licensing] 操作。

通常情况下，CLion 会自动配置环境。你也可以通过 CLion 打开任一项目（如没有项目，请新建一个），从顶栏 File > settings > Build, Execution, Deployment > Toolchains 打开工具链设定检查。

#### 安装并配置 VS Code

(若你想使用 CLion，则可以跳过此节。)

你可以在 [VS Code 官网][vsc] 下载并安装 Visual Studio Code。

CLion 是一个专为 C/C++ 设计的 IDE，而 VS Code 是一个较为通用的文本编辑器，你需要自行安装一些扩展以适应 C++ 的开发。

我们推荐使用 [clangd] 而不是微软官方的 C++ 扩展。首先在 Ubuntu 的命令行中安装 clangd:

```sh
sudo apt install clangd
```

然后在 VS Code 里安装以下扩展: (扩展面板可以用 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> 打开。)

- [C/C++ Extension Pack][ext-cxx-pack]
- [clangd][ext-clangd]
  - 当 clangd 提示禁用 IntelliSense 时，选择禁用。

### 其他发行版本

请自行安装以下组件：
- gcc / clang
- make
- CMake
- valgrind
- git
- gdb

安装这些组件后，请安装 CLion 或 VS Code。（如果你觉得应当使用自由软件，你可以自行设定 VSCodium。）
