# Nbprime 
<div align="center">

<p>
  <img alt="logo" src="/images/nb.svg" />
</p>

</div>

**N**ew **B**inary for **Prime**

简体中文 | [English](README.md)

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/lcd-xvii/nbprime)]()

***Make Prime great again.***

## 这是什么项目？

**Nbprime** 是一个为 Prime 计算器（原 HP Prime）打造的开源项目，核心目标有三：
1. **释放硬件性能**：通过绕过官方操作系统，直接运行裸机二进制程序，挖掘 Prime 的底层潜力。
2. **提供完整工具链**：为开发者提供编译、调试、部署的一站式解决方案。
3. **构建社区生态**：汇集全球 Prime 爱好者的力量，共同分享技术、经验和创意。

项目目前处于早期阶段，已实现基本的二进制加载器原型，并支持几个示例程序。我们诚邀你参与共建！

![](/images/primetcc-example.jpg)

## 我想要快速开始！

### 环境要求
- 一台 Prime 计算器（**硬件版本 G1，固件版本 20250915**）
- USB 数据线
- 电脑端工具链：`arm-none-eabi-gcc`、`make`、`python3`

### 一键体验

你可以直接下载 [`examples/`](examples/) 文件夹，这些程序都是预编译的！你可以直接传输到 Prime 上运行。

```bash
git clone https://github.com/lcd-xvii/nbprime.git
cd nbprime
```

详细步骤请参考 [`docs/getting-started.md`](docs/getting-started.md)。

## 现在有哪些功能啊？

- [x] 基础二进制加载器（含文本 IO）
- [x] 基础 Prime 图形库
- [x] 事件响应与处理
- [x] 部分操作系统 ABI 调用
- [x] 完善的数学计算支持
- [x] 简单的 Makefile 构建系统
- [ ] 完整的 SDK 文档（规划中）
- [ ] PC、移动端、Prime 端兼容工具链

## 我要开发自己的程序！

你需要准备：

- **编译工具链**：GNU ARM Embedded Toolchain
- **目标平台**：Prime G1（基于 ARM9）
- **开发环境**：Linux / WSL2

详见 [`docs/developing.md`](docs/developing.md)。

## 怎么找到我想要的文件？

看这里：

```
nbprime/
├── examples/        # 可以直接扔进计算器使用的东西
├── lib/             # prime-gcc-toolchain
├── prime-xxx/       # 项目文件
├── docs/            # 文档
└── Makefile
```

## 我要贡献！！

我们欢迎任何形式的贡献，包括但不限于：
- 报告 Bug（提 Issue）
- 建议新功能（提 Issue）
- 提交代码（Pull Request）
- 完善文档
- 撰写教程或分享经验

请先阅读 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

## 主播主播，……

**Q：我的 Prime 型号不是 G1 或者固件不是 20250915，能用吗？**\
A：目前仅支持以上硬件和固件版本，欢迎开发和适配其他版本。

**Q：刷写后会影响原系统吗？**
A：不会，我们的加载器通过 USB 传输，利用后门运行，不影响原有官方系统功能。

> 本项目采用 [MIT 许可证](LICENSE)，你可以自由使用、修改和分发。
