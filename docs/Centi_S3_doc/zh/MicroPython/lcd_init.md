## 屏幕初始化

BPI-Centi-S3 正面有一块1.9英寸TFT LCD彩屏，分辨率是170*320，驱动芯片为ST7789V3, 采用8bit 并行接口与ESP32S3芯片连接。

出厂固件中已集成ST7789 C模块 驱动，来自于:

[russhughes/st7789s3_esp_lcd](https://github.com/russhughes/st7789s3_esp_lcd) , The MIT License

感谢 russhughes 的开源，在他的GitHub README中可以查阅编译方法和所有API接口。

### 初始化，点亮屏幕

<iframe src="//player.bilibili.com/player.html?aid=269437418&bvid=BV1hc4115786&cid=1078595731&page=1&autoplay=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

在本地文件夹中创建一个 main.py ，将下方代码拷贝进去，保存文件。

> 使用 `ctrl + S` 快捷键即可保存当前窗口中的文件。

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
from machine import freq


def config(rotation=0, options=0):

    return st7789.ST7789(
        170,
        320,
        15, 14, 13, 12, 11, 10, 9, 8,
        wr=6,
        rd=7,
        reset=3,
        dc=5,
        cs=4,
        backlight=2,
        power=2,
        rotation=rotation,
        options=options)


freq(240_000_000)  # Set esp32s3 cpu frequency to 240MHz
tft = config(rotation=1, options=0)
tft.init() # Initialize
tft.fill(st7789.RED) 
tft.show(True)
tft.deinit()  # Deinitialize the display or it will cause a crash on the next run

```

使用mpbridge同步文件到开发板。
> [安装mpbridge](https://bpi-steam.com/Centi_S3_doc/zh/MicroPython/environment.html#安装mpbridge工具) | [使用mpbridge](https://bpi-steam.com/Centi_S3_doc/en/MicroPython/Connect.html#在终端中使用mpbridge)


同步完成后，BPI-Centi-S3 屏幕将全屏显示红色。

### 单独的配置文件

我们可以将初始化配置ST7789的代码单独置于一个python脚本文件中，然后在其他地方任意导入使用，包括在REPL中，这可以增强代码复用性。

新建一个单独的配置文件 tft_config.py ，将下方代码拷贝进去，保存文件。

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
from machine import freq


def config(rotation=0, options=0):

    return st7789.ST7789(
        170,
        320,
        15, 14, 13, 12, 11, 10, 9, 8,
        wr=6,
        rd=7,
        reset=3,
        dc=5,
        cs=4,
        backlight=2,
        power=2,
        rotation=rotation,
        options=options)

freq(240_000_000)  # Set esp32s3 cpu frequency to 240MHz

```

将 main.py 修改为如下代码：

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config

tft = tft_config.config(rotation=1, options=0)
tft.init()
tft.fill(st7789.RED) 
tft.show(True)
tft.deinit()  # Deinitialize the display or it will cause a crash on the next run

```

使用mpbridge同步文件到开发板。

后续我们就可以像这样简单的导入然后初始化屏幕了。