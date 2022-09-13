# FAQs

## WSL
### 为什么建议使用 WSL2 而不是 WSL1？

根据 [Microsoft 官方文档](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)，可以了解到二者的不同之处。

优点：

- WSL 2 具有独立的 Linux 内核，这对于后续很多操作（如扩容栈空间大小，使用 CUDA）是必要的；

- WSL 2 完全兼容 Linux 系统调用，WSL 1 可能会在某些情况下有与 Linux 不同的行为，如果需要使用 Docker，必须采用 WSL 2。

缺点：

- WSL 2 下，Windows 目录中文件输入输出速度慢，经实测，二者确实有差距，在大量小文件的情况下非常明显，然而此问题可以通过将需要运行高性能文件输入输出（此情况非常少）的任务放到 WSL `/home` 目录下运行；

- 网络支持差，无法访问外部设备，需要用到网络和外部设备的情况很少，且 WSL 1 支持仍然不好，推荐使用虚拟机；

- 占用内存相对较大。

结论：

除非由于电脑性能不好，WSL 2 运行占用过大，否则我们建议使用 WSL 2。

### 查看 WSL 状态
你可以在 Powershell 中（或 Windows Terminal 中开启一个 Powershell 的 terminal）输入
```bash
wsl -l -v
```
来查看 WSL 的状态。

通常的输出是
```bash
  NAME            STATE           VERSION
* Ubuntu          Running         2
```

## 命令行
### 什么是命令行？

命令行界面是一个仅有文字和符号组成的界面，其必须通过键盘输入来完成绝大多数工作。命令行输入有着更高的自由性。

### 如何打开命令行？

#### Windows
Windows 平台的命令行工具有 cmd、Powershell 以及 Windows Terminal（整合多个命令行工具）。

下面将介绍打开不同终端的最便捷方式。

- cmd

使用 <kbd>⊞ Win</kbd>+<kbd>R</kbd> 组合键，并输入 `cmd` 后回车（或点击运行）。

- Powershell

右键桌面开始图标，选择 Powershell 或 Powershell （管理员）。

- Windows Terminal

Windows Terminal 是一个应用，你可以采用任何打开应用的方式来开启 Windows Terminal。
