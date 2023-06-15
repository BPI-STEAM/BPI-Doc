## Getting Started Guide

We compiled this Getting Started Guide to help you get started with this BPI-Centi-S3 development board quickly.

### First Thing

Use a USB-C cable with power and data functions to connect the BPI-Centi-S3 development board to your computer.

When using it for the first time, its screen will immediately display a welcome screen after power-on, and the buzzer will beep twice.

BPI-Centi-S3 has been programmed with MicroPython 1.19.1 firmware and integrated ST7789 C module driver when it leaves the factory. It is recommended for beginners to use MicroPython to develop and learn.

### Use MicroPython to get started quickly

1. See [Install and configure the environment](./MicroPython/environment.md), install Python 3, mpremote tool, mpbridge tool, VScode IDE.

2. See [How to use VScode + mpbridge tool](./MicroPython/VScode_mpbridge.md) to learn how to connect to the development board, copy, modify, and delete files on the development board.

3. See [REPL Use Case](./MicroPython/REPL_use_case.md) to quickly understand the common shortcut keys of MicroPython REPL and the method of viewing modules.

After the above three steps, you can start developing.

In the left sidebar of this page you can find some routines that may help you.

The ST7789 C module driver integrated in BPI-Centi-S3 factory comes from:

[russhughes/st7789s3_esp_lcd](https://github.com/russhughes/st7789s3_esp_lcd), The MIT License

In this GitHub repository, you can check all the methods of the st7789 module, as well as the compiled methods, thanks to russhughes for his open source contributions.

For learning Python and MicroPython, we recommend getting started with Python in the [Python Tutorial](https://docs.python.org/3.10/tutorial/index.html).

Apply what you have learned in Python, and look at the [MicroPython documentation](https://docs.micropython.org/en/latest/index.html), you can quickly refer to MicroPython's special library, ESP32 port special library for our development.

Learn some of the differences between the two on the page [Differences between MicroPython and CPython](https://docs.micropython.org/en/latest/genrst/index.html#).