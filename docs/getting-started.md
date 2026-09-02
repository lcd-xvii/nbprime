# 快速开始

本文档将引导你完成从零开始在 Prime 计算器上运行 Nbprime 二进制程序的全过程。

## 准备工作

### 硬件要求
- **Prime 计算器**：型号 **G1**，固件版本 **20250915**。
  > 你可以在计算器的“帮助 → 关于 HP Prime”中查看硬件和固件版本。硬件版本 A 和 C 对应 G1，D 对应 G2。目前仅支持 G1 版本的 20250915 固件，其他版本（如 G2）暂不兼容。
- **USB 数据线**：用于连接计算器与电脑。

### 软件要求
在电脑端安装以下工具：
- **ARM 交叉编译工具链**：`arm-none-eabi-gcc`、`arm-none-eabi-ld` 等
- **构建工具**：`make`
- **Python 3**：用于辅助脚本
- **Git**：用于克隆仓库

#### 安装示例（Ubuntu/Debian/WSL2）
```bash
sudo apt update
sudo apt install gcc-arm-none-eabi make python3 git
```

#### 安装示例（macOS）
```bash
brew install arm-none-eabi-gcc make python3 git
```

## 获取代码

克隆 Nbprime 仓库到本地：

```bash
git clone https://github.com/lcd-xvii/nbprime.git
cd nbprime
```

## 使用示例程序

项目自带了一些示例程序，位于 `examples/` 目录下。这些程序都是预编译的（即你可以直接将 `*.hpappdir` 文件夹传到 Prime 上，见下一条）。但如果你对其进行了修改，请转至[构建项目](#构建项目)。

## 传输并运行

### 预先检查
1. USB 线支持传输文件。部分仅用于充电的线是无效的。
2. 计算器已开机并处于正常状态。
3. 电脑有空余 USB 2.0 及以上插口，供电充足且稳定。

### 使用 `msd` 脚本（推荐）
1. 如果你未安装 `msd` 传输程序，请用 HP 连接工具包（见[下面](#使用-hp-连接工具包)）向计算器传输 `tools/msd/msd.hpappdir`。
2. **先用 USB 线将计算器连接电脑**，再双击打开 `msd` 应用程序。此时电脑上将弹出容量小于等于 197MB 的 U 盘。
3. 将 `.hpappdir` 文件夹复制到 Prime 的 `C:/DATA/` 下。
4. 拔出 USB 线。
5. 关机并重新开机，防止内存加载问题。不需要重启。

**注意**：该程序为阻塞型，在连接期间 Prime 端的任何操作（除强制重启）都不受响应。该程序实现尚不稳定，可能多次错误识别到插入和弹出 U 盘，我们将尽快修复。

### 使用 Upsilon 系统
同上，将 `.hpappdir` 文件夹复制到 Prime 的 `C:/DATA/` 下。详细请参考[SQY 的教程](https://www.cncalc.org/thread-25992-1-1.html)。

相较于 `msd`，该方法同样是阻塞型的，但连接后**不会**错误识别到 U 盘插入和弹出。

### 使用 HP 连接工具包
即使这种方法因为常导致内存不足而不推荐，但当其他方法都不适用，或你需要传输 `msd` 连接工具时，掌握这项传统技能依旧是必要的。

如果你是 Prime 老手，你应当已经掌握此方法。如果你是新手，请在 HP 官网上下载 HP 连接工具包，并按提示操作。

### 运行程序
传输完成后，计算器屏幕上会显示程序的输出。部分程序可能需要按键交互，请按照屏幕提示操作。

## 构建项目

以下是极简示例，详细内容参考 [`developing.md`](developing.md)。

构建你修改过的 `hello_world` 程序：

```bash
cd examples/hello_world
make
```

构建成功后，会在当前目录生成一个 `.elf` 格式的二进制文件。用其替换 `*.hpappdir/` 下的 `*.elf` 文件。

## 下一步

- 想了解如何开发自己的程序？请阅读 [`developing.md`](developing.md)。
- 想查看可用的 API？请阅读 [`api-reference.md`](api-reference.md)。
