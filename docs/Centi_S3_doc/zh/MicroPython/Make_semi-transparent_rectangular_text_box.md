## 制作半透明矩形文本框


### fill_rect 方法
`fill_rect(x, y, width, height {, color, alpha})`

设`x`, `y`坐标，绘制一个宽度为`width`，高度为`height`的填充矩形，颜色为`color`，可选设置`alpha`使其与背景混合。

`color`默认为BLACK黑色，`alpha`默认为255。

> [从此GitHub链接下载例程](https://github.com/BPI-STEAM/BPI-Centi-S3-Doc/tree/main/micropython_example/05_semi-transparent_rectangular_text_box)

### 在图片上显示半透明矩形

![](../assets/images/pic_5.jpg)

我们可以在这个图片上显示一个半透明的黑色矩形框。

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config
import gc

def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        gc.collect()
        tft.jpg('pic_5.jpg', 0, 0)
        tft.fill_rect(20, int(170/2-32), 320-20-20, 32, st7789.BLACK, 60)
        tft.show()
        gc.collect()

    except BaseException as err:
        err_type = err.__class__.__name__
        print('Err type:', err_type)
        from sys import print_exception
        print_exception(err)

    finally:
        tft.deinit()
        print("tft deinit")


main()
```

### 在半透明矩形框内显示文本

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config
import gc
import time
import vga1_bold_16x32

fg = st7789.WHITE
bg = st7789.TRANSPARENT
text_x = 20
text_y = int(170/2-32)
rect_width = 320-20-20
rect_height = 32

def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        gc.collect()
        tft.jpg('pic_5.jpg', 0, 0)
        tft.fill_rect(text_x, text_y, rect_width, rect_height, st7789.BLACK, 60)
        tft.text(vga1_bold_16x32, "Hello World!", text_x, text_y, fg, bg, 255)
        tft.show()
        gc.collect()

    except BaseException as err:
        err_type = err.__class__.__name__
        print('Err type:', err_type)
        from sys import print_exception
        print_exception(err)

    finally:
        tft.deinit()
        print("tft deinit")


main()

```

### 根据字符长度创建半透明文本框
```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config
import gc
import time
import vga1_bold_16x32

fg = st7789.WHITE
bg = st7789.TRANSPARENT
text_x = 20
text_y = int(170/2-32)


def text_rect(tft, font, font_size, text: str, text_coord,
              fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=255):
    rect_width = font_size[0] * len(text)
    rect_height = font_size[1]
    tft.fill_rect(text_coord[0], text_coord[1],
                  rect_width, rect_height, bg, alpha_rect)
    tft.text(font, text, text_coord[0], text_coord[1],
             fg, st7789.TRANSPARENT, alpha_text)


def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        gc.collect()
        tft.jpg('pic_5.jpg', 0, 0)
        text_rect(tft, vga1_bold_16x32, (16, 32), "Hello World!", (text_x, text_y),
                  fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=80, alpha_rect=60)
        text_rect(tft, vga1_bold_16x32, (16, 32), "It's MicroPython!", (text_x, text_y+32),
                  fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=60)
        tft.show()
        gc.collect()

    except BaseException as err:
        err_type = err.__class__.__name__
        print('Err type:', err_type)
        from sys import print_exception
        print_exception(err)

    finally:
        tft.deinit()
        print("tft deinit")


main()

```
