## Display text characters

<iframe width="560" height="315" src="https://www.youtube.com/embed/MAvLjCMQ93s?si=auUGEEG4a_E2GK_j" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### text method

`text(font, s, x, y {, fg, bg, alpha})`

Write text to the display using the specified bitmap `font` with the coordinates as the upper-left corner of the text.

The optional arguments `fg` and `bg` can set the foreground and background colors of the text; otherwise the foreground color defaults to `WHITE`, and the background color defaults to `BLACK`. 

`alpha` defaults to 255. 

See the [README.md](https://github.com/russhughes/st7789s3_esp_lcd/tree/main/fonts/bitmap) in the `fonts/bitmap` directory for example fonts.

### bitmap font

The BPI-Centi-S3  factory firmware contains two bitmap font files.

`vga1_8x16.mpy`

`vga1_bold_16x32.mpy`

They come from https://github.com/russhughes/st7789s3_esp_lcd/tree/main/fonts/bitmap.

From this I selected these two most commonly used, using [MPY-CROSS Tool] (https://pypi.org/project/mpy- cross/) to transform them into a `.mpy` format to reduce the volume of files.

### download font file

If you mistakenly delete the font file or erase the Flash, you need to download the font file again. You can download it from the previous text link, or you can download the fonts in the link below to the font of the `.mpy` format, including the example below.

[From here to download fonts and examples] (https://github.com/bpi-team/bpi-s3-doc/micropython_example/04_display_text)

### Display text

![](../assets/images/Display_text_1.jpg)

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config
import vga1_8x16
import vga1_bold_16x32

"""
These default colors can be used:
BLACK           BLUE            CYAN            GREEN
MAGENTA         RED             YELLOW          WHITE
TRANSPARENT

Custom RGB colors:
color565(255,255,255)
"""
fg = st7789.BLACK
bg = st7789.WHITE
text_x = 10
text_y = 10

def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        tft.fill(st7789.WHITE)
        tft.text(vga1_8x16, "Hello World!", text_x, text_y, fg, bg, 255)
        tft.text(vga1_bold_16x32, "MicroPython!", text_x, text_y+16, fg, bg, 255)
        tft.text(vga1_8x16, "vga1_8x16", text_x, text_y+16+32, fg, bg, 255)
        tft.text(vga1_bold_16x32, "vga1_bold_16x32",
                 text_x, text_y+16+32+16, fg, bg, 255)
        tft.show()

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

### Use a transparent background and Alpha channel to make shadow fonts

![](../assets/images/Display_text_2.jpg)

The reasonable use of `st7789.TRANSPARENT` as the background color of the text can make the background of the text not change.

By setting the alpha parameter in the text method, the overall transparency of the text can be changed, with a range of 0 ~ 255.

```py
""" BPI-Centi-S3 170x320 ST7789 display """

import st7789
import tft_config
import vga1_8x16
import vga1_bold_16x32

"""
These default colors can be used:
BLACK           BLUE            CYAN            GREEN
MAGENTA         RED             YELLOW          WHITE
TRANSPARENT

Custom RGB colors:
color565(255,255,255)
"""
fg = st7789.BLACK
bg = st7789.TRANSPARENT
text_x = 10
text_y = 50

def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        tft.fill(st7789.WHITE)
        tft.text(vga1_8x16, "Hello World!", text_x-1, text_y-1, fg, bg, 205)
        tft.text(vga1_bold_16x32, "MicroPython!", text_x-2, text_y+16-2, fg, bg, 205)
        tft.text(vga1_8x16, "Hello World!", text_x, text_y, fg, bg, 255)
        tft.text(vga1_bold_16x32, "MicroPython!", text_x, text_y+16, fg, bg, 255)
        tft.show()

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