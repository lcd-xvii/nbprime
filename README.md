# Nbprime

<div align="center">

<p>
  <img alt="logo" src="/images/nb.svg" />
</p>

</div>

**N**ew **B**inary for **Prime**

English | [简体中文](README.zh-CN.md)

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/lcd-xvii/nbprime)]()

***Make Prime Great Again.***

## What is this project?

**Nbprime** is an open-source project for Prime calculators (formerly HP Prime). Its core goals are threefold:
1. **Unlock hardware performance** – by bypassing the official operating system and running bare‑metal binaries directly, tapping into the Prime’s low‑level potential.
2. **Provide a complete toolchain** – offering developers a one‑stop solution for compiling, debugging, and deploying.
3. **Build a community ecosystem** – bringing together Prime enthusiasts worldwide to share technology, experience, and creativity.

The project is currently in its early stages, with a basic binary loader prototype already implemented and several example programs available. We warmly invite you to join and contribute!

![](/images/primetcc-example.jpg)

## I want to get started quickly!

### Requirements
- A Prime calculator (**hardware revision G1, firmware version 20250925**)
- USB data cable
- PC toolchain: `arm-none-eabi-gcc`, `make`, `python3`

### One‑click experience

You can directly download the [`examples/`](examples/) folder – all programs are pre‑compiled! Transfer them to your Prime and run them.

```bash
git clone https://github.com/lcd-xvii/nbprime.git
cd nbprime
```

For detailed steps, refer to [`docs/getting-started.md`](docs/getting-started.md).

## What features are available now?

- [x] Basic binary loader (with text I/O)
- [x] Basic Prime graphics library
- [x] Event handling and response
- [x] Partial OS ABI calls
- [x] Comprehensive math support
- [x] Simple Makefile build system
- [ ] Complete SDK documentation (planned)
- [ ] PC, mobile, and Prime‑compatible toolchain (planned)

## I want to develop my own programs!

You will need:

- **Compiler toolchain**: GNU ARM Embedded Toolchain
- **Target platform**: Prime G1 (ARM9‑based)
- **Development environment**: Linux / WSL2

See [`docs/developing.md`](docs/developing.md) for details.

## Where can I find the files I need?

Here is the structure:

```
nbprime/
├── examples/        # use it on your calculator directly.
├── lib/             # prime-gcc-toolchain
├── prime-xxx/       # project
├── docs/            # 文档
└── Makefile
```

## I want to contribute!!

We welcome all forms of contribution, including but not limited to:
- Reporting bugs (opening issues)
- Suggesting new features (opening issues)
- Submitting code (pull requests)
- Improving documentation
- Writing tutorials or sharing experiences

Please read [`CONTRIBUTING.md`](contributing.md) first.

## Q&A

**Q: My Prime is not G1 or its firmware is not 20250915 – can I still use it?**  
A: Currently only the above hardware and firmware versions are supported. Contributions to adapt other versions are welcome.

**Q: Will flashing affect the original system?**  
A: No. Our loader transfers via USB and uses a backdoor to run, without affecting the original official system functionality.

> This project is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute it.
