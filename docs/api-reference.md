# API 参考

***注意：当前文档为 AI 撰写，仅用于占位，请开发者尽快更改为人工版本。***

本文档详细描述 Nbprime 核心库提供的所有公共 API。

## 目录

- [初始化与基础 IO](#初始化与基础-io)
- [图形库](#图形库)
- [事件处理](#事件处理)
- [数学函数](#数学函数)
- [ABI 调用](#abi-调用)

---

## 初始化与基础 IO

### `prime_init()`

```c
void prime_init(void);
```

初始化 Nbprime 运行时环境。**必须在使用任何其他 API 之前调用**。

**功能**：
- 设置栈指针
- 初始化串口通信
- 清空屏幕（默认）

**示例**：
```c
prime_init();
```

---

### `prime_printf()`

```c
void prime_printf(const char *format, ...);
```

向屏幕输出格式化字符串。支持有限的格式说明符（`%d`、`%x`、`%s`、`%c`）。

**参数**：
- `format`：格式化字符串
- `...`：可变参数

**示例**：
```c
prime_printf("Value: %d, Hex: 0x%x\n", 42, 0xDEAD);
```

---

### `prime_putchar()`

```c
void prime_putchar(char c);
```

向屏幕输出单个字符。

**参数**：
- `c`：要输出的字符

---

## 图形库

### `prime_gfx_clear()`

```c
void prime_gfx_clear(uint16_t color);
```

以指定颜色清空屏幕。

**参数**：
- `color`：16 位 RGB565 颜色值

**示例**：
```c
prime_gfx_clear(0xFFFF);  // 白色清屏
```

---

### `prime_gfx_pixel()`

```c
void prime_gfx_pixel(int x, int y, uint16_t color);
```

在指定位置绘制一个像素点。

**参数**：
- `x`、`y`：屏幕坐标（原点在左上角）
- `color`：16 位 RGB565 颜色值

**屏幕尺寸**：320 × 240 像素

---

### `prime_gfx_line()`

```c
void prime_gfx_line(int x1, int y1, int x2, int y2, uint16_t color);
```

绘制一条直线（Bresenham 算法）。

---

### `prime_gfx_rect()`

```c
void prime_gfx_rect(int x, int y, int w, int h, uint16_t color);
```

绘制矩形边框。

**参数**：
- `x`、`y`：左上角坐标
- `w`、`h`：宽度和高度

---

### `prime_gfx_fill_rect()`

```c
void prime_gfx_fill_rect(int x, int y, int w, int h, uint16_t color);
```

绘制填充矩形。

---

### `prime_gfx_text()`

```c
void prime_gfx_text(int x, int y, const char *str, uint16_t color);
```

在指定位置绘制文本（使用内置 8×8 点阵字体）。

**参数**：
- `x`、`y`：文本左上角坐标
- `str`：要绘制的字符串
- `color`：文本颜色

---

## 事件处理

### `prime_event_poll()`

```c
uint32_t prime_event_poll(void);
```

轮询并返回当前按键事件。若无事件则返回 `0`。

**返回值**：按键码（见下方按键常量）

**示例**：
```c
uint32_t ev = prime_event_poll();
if (ev == KEY_ENTER) {
    prime_printf("Enter pressed!\n");
}
```

---

### 按键常量

| 常量 | 值 | 描述 |
|------|-----|------|
| `KEY_LEFT` | 0x01 | 左方向键 |
| `KEY_RIGHT` | 0x02 | 右方向键 |
| `KEY_UP` | 0x04 | 上方向键 |
| `KEY_DOWN` | 0x08 | 下方向键 |
| `KEY_ENTER` | 0x10 | 确认键 |
| `KEY_ESC` | 0x20 | 取消/返回键 |
| `KEY_PLUS` | 0x40 | `+` 键 |
| `KEY_MINUS` | 0x80 | `-` 键 |
| `KEY_0`–`KEY_9` | 0x100–0x200 | 数字键 0–9 |
| `KEY_A`–`KEY_Z` | 0x400–0x2000000 | 字母键 A–Z |

---

### `prime_event_wait()`

```c
uint32_t prime_event_wait(void);
```

阻塞等待直到有按键事件发生，然后返回按键码。

---

## 数学函数

数学库提供基本的浮点运算支持（软件实现，适用于无 FPU 的 ARM9 核心）。

### `prime_sin()`

```c
float prime_sin(float x);
```

计算正弦值（弧度制）。

---

### `prime_cos()`

```c
float prime_cos(float x);
```

计算余弦值（弧度制）。

---

### `prime_tan()`

```c
float prime_tan(float x);
```

计算正切值（弧度制）。

---

### `prime_sqrt()`

```c
float prime_sqrt(float x);
```

计算平方根。

---

### `prime_pow()`

```c
float prime_pow(float base, float exp);
```

计算幂次。

---

## ABI 调用

部分官方操作系统功能可通过 ABI 调用直接使用（绕过裸机限制）。

### `prime_abi_get_key()`

```c
uint32_t prime_abi_get_key(void);
```

通过操作系统 ABI 获取当前按键状态（与 `prime_event_poll()` 类似，但底层实现不同）。

---

### `prime_abi_draw_string()`

```c
void prime_abi_draw_string(int x, int y, const char *str);
```

通过操作系统 ABI 绘制字符串（使用系统字体，与 `prime_gfx_text()` 不同）。

---

### `prime_abi_sound()`

```c
void prime_abi_sound(int frequency, int duration_ms);
```

通过操作系统 ABI 播放蜂鸣声。

**参数**：
- `frequency`：频率（Hz）
- `duration_ms`：持续时间（毫秒）

---

## 颜色常量（RGB565）

| 常量 | 值 | 颜色 |
|------|-----|------|
| `COLOR_BLACK` | 0x0000 | 黑色 |
| `COLOR_WHITE` | 0xFFFF | 白色 |
| `COLOR_RED` | 0xF800 | 红色 |
| `COLOR_GREEN` | 0x07E0 | 绿色 |
| `COLOR_BLUE` | 0x001F | 蓝色 |
| `COLOR_YELLOW` | 0xFFE0 | 黄色 |
| `COLOR_CYAN` | 0x07FF | 青色 |
| `COLOR_MAGENTA` | 0xF81F | 品红 |

---

## 版本信息

### `PRIME_VERSION`

```c
#define PRIME_VERSION "0.1.0"
```

当前 Nbprime 库版本号。
