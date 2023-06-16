## 快速上手指南

我们整理了这份入门指南，帮助你快速上手这块BPI-Centi-S3开发板。

### 第一件事

使用一根具有供电与数据功能的USB-C线连接BPI-Centi-S3开发板与你的计算机。

初次上手，通电后它的屏幕会立即显示欢迎画面，蜂鸣器会鸣叫两声。

BPI-Centi-S3 出厂时已经烧录了MicroPython 1.19.1 固件，并集成了ST7789 C模块 驱动，推荐初学者使用MicroPython开发学习。

### 使用 MicroPython 快速上手

1. 查看[安装与配置环境](./MicroPython/environment.md), 安装Python 3，mpremote工具，mpbridge工具，VScode IDE.

2. 查看[VScode + mpbridge工具使用方法](./MicroPython/VScode_mpbridge.md)，了解如何连接开发板，复制，修改，删除开发板上的文件。

3. 查看[REPL使用技巧](./MicroPython/REPL_use_case.md)，快速了解MicroPython REPL常用快捷键和查看模块的方法。

经过以上三步即可上手开发。

对于 Python 和 MicroPython 的学习，我们建议在[Python 教程](https://docs.python.org/zh-cn/3.10/tutorial/index.html)中上手学习Python，在[MicroPython 文档](https://docs.micropython.org/en/latest/index.html)中应用 Python 所学，你可以快速参考 MicroPython 的特殊库，ESP32 端口特殊库来进行开发，在[MicroPython与CPython的区别](https://docs.micropython.org/en/latest/genrst/index.html#)页面了解二者的部分差异。

在本网页左侧边栏可以看到一些可能对你有帮助的MicroPython例程。

ST7789 C模块 驱动，来自于：

[russhughes/st7789s3_esp_lcd](https://github.com/russhughes/st7789s3_esp_lcd) , The MIT License

在此GitHub 仓库中可以查阅st7789模块的所有方法，以及编译的方法，感谢 russhughes 的开源贡献。

如果你在开发产生意外的恶性BUG使开发板无法正常启动，或其他原因导致固件被擦除或损坏，查看[烧录固件](./MicroPython/Burn_firmware.md)。

