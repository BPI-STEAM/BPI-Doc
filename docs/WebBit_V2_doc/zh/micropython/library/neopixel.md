neopixel - WS2812 灯带
=========================================

NeoPixels也被称为WS2812 LED彩带，是连接在一起的全彩色led灯串。你可以设置他它们的红色，绿色和蓝色值，
在0到255之间。neopixel模块可通过精确的时间控制，生成WS2812控制信号。

构建对象
------------

```python
class NeoPixel(pin, n,bpp=3,timing=0)
```

- ``pin`` :输出引脚,可使用引脚见下文
-  ``n`` :LED灯的个数
- ``bpp``:

  - ``3``:默认为3元组RGB
  - ``4``:对于具有3种以上颜色的LED，例如RGBW像素或RGBY像素,采用4元组RGBY或RGBY像素

- ``timing``:默认等于0,为400KHz速率；等于1，为800KHz速率

> NeoPixel可使用的pin引脚有板子的P5,P6,P7(板上RGB),P8,P9,P11,P13,P14,P15,P16,P19,P20。


示例:

```python
from machine import Pin
import neopixel

pin = Pin(17, Pin.OUT)
np = neopixel.NeoPixel(pin, n=3,bpp=3,timing=1)   #800khz
```

方法
-------

```python
NeoPixel.write()
```

把数据写入LED中。 

示例:

```python
np[0] = (255, 255, 255) # 设置第一个LED像素为白色
np.write()
```

```python
NeoPixel.fill(rgb_buf)
```

填充所有LED像素。

- ``rgb_buf`` :rgb颜色

示例:

```python
np.fill( (255, 255, 255) )
```