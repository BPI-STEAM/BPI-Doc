## Display multiple vector fonts

### draw method

`draw(vector_font, s, x, y {, fg, scale, alpha})`

Draw text to the display using the specified Hershey vector font with the coordinates as the lower-left corner of the text. The foreground color of the text can be set by the optional argument fg. Otherwise the foreground color defaults to WHITE. The size of the text can be scaled by specifying a scale value. The scale value must be larger than 0 and can be a floating-point or an integer value. The scale value defaults to 1.0. alpha defaults to 255.

### draw_len method

`draw_len(vector_font, s {, scale})`

Returns the string's width in pixels if drawn with the specified font.

### Download vector font library

There is a vector font library in py file format in the [GitHub:russhughes/st7789s3_esp_lcd/fonts/vector](https://github.com/russhughes/st7789s3_esp_lcd/tree/main/fonts/vector), and there are pictures of all fonts in the README.

In [example lib](https://github.com/BPI-STEAM/BPI-Centi-S3-Doc/tree/main/micropython_example/07_display_multiple_vector_fonts/lib), you can also download the converted mpy file format vector font library, taking up less flash space.

### Display multiple vector fonts and refresh continuously

The width of the string to be displayed can be obtained through the draw_len method, but the height of some of the provided vector fonts will exceed the set value. If you need to keep the text box completely covering it, you need to modify the corresponding code to increase the height of the text box.

> [Download the complete example from this GitHub link](https://github.com/BPI-STEAM/BPI-Centi-S3-Doc/tree/main/micropython_example/07_display_multiple_vector_fonts)

![](../assets/images/pic_4.jpg)

![](../assets/images/Display_multiple_vector_fonts_2.jpg)

```py
""" BPI-Centi-S3 170x320 ST7789 display """
import st7789
import tft_config
import gotheng
import italicc
import romanc
import time
import gc
from math import ceil

"""
These default colors can be used:
BLACK           BLUE            CYAN            GREEN
MAGENTA         RED             YELLOW          WHITE
TRANSPARENT

Custom RGB colors:
color565(255,255,255)
"""
class DrawRect:
    def __init__(self):
        self.tft = None
        self.text_y = None
        self.text_x = None
        self.rect_x = None
        self.rect_y = None
        self.rect_height = None
        self.rect_width = None

    def rect(self, tft, vector_font, scale, text, text_coord,
             fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=255):
        self.tft = tft
        self.rect_width = self.tft.draw_len(vector_font, text, scale)
        self.rect_height = ceil(vector_font.HEIGHT * scale)
        self.text_x = text_coord[0]
        self.text_y = text_coord[1]
        self.rect_x = ceil(self.text_x - vector_font.WIDTH * scale / 8)
        self.rect_y = round(self.text_y - vector_font.HEIGHT * scale / 2 + 1)
        self.tft.fill_rect(self.rect_x, self.rect_y,
                           self.rect_width, self.rect_height, bg, alpha_rect)
        self.tft.draw(vector_font, text, self.text_x, self.text_y,
                      fg, scale, alpha_text)

    def erase(self, bg):
        buffer, _, _ = self.tft.jpg_decode(bg, self.rect_x, self.rect_y, self.rect_width, self.rect_height)
        self.tft.blit_buffer(buffer, self.rect_x, self.rect_y, self.rect_width, self.rect_height)


def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        jpg = 'pic_4.jpg'
        tft.jpg(jpg, 0, 0)
        text_x = 10
        text_y = 20
        text_list = [
            " !\"#$%&'()*+,-./",
            "0123456789:;<=>?",
            "@ABCDEFGHIJKLMNO",
            "PQRSTUVWXYZ[\]^_",
            "`abcdefghijklmno",
            "pqrstuvwxyz{|}~",
            ]

        draw_rect_1 = DrawRect()
        draw_rect_2 = DrawRect()
        draw_rect_3 = DrawRect()
        while True:
            for i in text_list:
                draw_rect_1.rect(tft, gotheng, 0.8, i, (text_x, text_y),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=20)
                draw_rect_2.rect(tft, italicc, 0.8, i, (text_x, text_y+32),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=40)
                draw_rect_3.rect(tft, romanc, 0.8, i, (text_x, text_y + 64),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=60)
                tft.show()
                time.sleep(0.5)
                draw_rect_1.erase(bg=jpg)
                draw_rect_2.erase(bg=jpg)
                draw_rect_3.erase(bg=jpg)
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

### Enlarge or reduce font size

You can control the font size by modifying the scale value of the draw method.

![](../assets/images/Display_multiple_vector_fonts_1.jpg)

```py
""" BPI-Centi-S3 170x320 ST7789 display """
import st7789
import tft_config
import gotheng
import italicc
import romanc
import time
import gc
from math import ceil

"""
These default colors can be used:
BLACK           BLUE            CYAN            GREEN
MAGENTA         RED             YELLOW          WHITE
TRANSPARENT

Custom RGB colors:
color565(255,255,255)
"""
class DrawRect:
    def __init__(self):
        self.tft = None
        self.text_y = None
        self.text_x = None
        self.rect_x = None
        self.rect_y = None
        self.rect_height = None
        self.rect_width = None

    def rect(self, tft, vector_font, scale, text, text_coord,
             fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=255):
        self.tft = tft
        self.rect_width = self.tft.draw_len(vector_font, text, scale)
        self.rect_height = ceil(vector_font.HEIGHT * scale)
        self.text_x = text_coord[0]
        self.text_y = text_coord[1]
        self.rect_x = ceil(self.text_x - vector_font.WIDTH * scale / 8)
        self.rect_y = round(self.text_y - vector_font.HEIGHT * scale / 2 + 1)
        self.tft.fill_rect(self.rect_x, self.rect_y,
                           self.rect_width, self.rect_height, bg, alpha_rect)
        self.tft.draw(vector_font, text, self.text_x, self.text_y,
                      fg, scale, alpha_text)

    def erase(self, bg):
        buffer, _, _ = self.tft.jpg_decode(bg, self.rect_x, self.rect_y, self.rect_width, self.rect_height)
        self.tft.blit_buffer(buffer, self.rect_x, self.rect_y, self.rect_width, self.rect_height)


def main():
    try:
        tft = tft_config.config(rotation=1)
        tft.init()
        jpg = 'pic_4.jpg'
        tft.jpg(jpg, 0, 0)
        text_x = 10
        text_y = 20
        text_list = [
            "!\"#$%&'()*",
            "0123456789",
            "ABCDEFGHI",
            "PQRSTUVWX",
            "abcdefghij",
            "pqrstuvwxy",
            ]

        draw_rect_1 = DrawRect()
        draw_rect_2 = DrawRect()
        draw_rect_3 = DrawRect()
        while True:
            for i in text_list:
                draw_rect_1.rect(tft, romanc, 0.5, i, (text_x, text_y),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=20)
                draw_rect_2.rect(tft, romanc, 1, i, (text_x, text_y+24),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=40)
                draw_rect_3.rect(tft, romanc, 1.5, i, (text_x, text_y + 64),
                                 fg=st7789.WHITE, bg=st7789.BLACK, alpha_text=255, alpha_rect=60)
                tft.show()
                time.sleep(0.5)
                draw_rect_1.erase(bg=jpg)
                draw_rect_2.erase(bg=jpg)
                draw_rect_3.erase(bg=jpg)
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