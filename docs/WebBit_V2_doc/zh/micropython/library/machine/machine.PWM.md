类 PWM -- 脉冲宽度调制
=============================

脉冲宽度调制（PWM）是一种通过数字方式获取模拟结果的技术。


构建对象
------------

```python
class PWM(pin, freq, duty)
```

创建与设定引脚关联的PWM对象。这样您就可以写该引脚上的模拟值。

- ``pin`` 支持PWM的引脚  ``GPIO0``、``GPIO2``、``GPIO4``、``GPIO5``、``GPIO10``、``GPIO12~19``、``GPIO21``、``GPIO22``、``GPIO23``、``GPIO25~27``。有关更多信息，请查看[ESP32 系列芯片技术规格书](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_cn.pdf) 中有关ESP32引脚功能的内容。
- ``freq`` 频率,0 < freq <= 78125
- ``duty``  占空比, 0 ≤ duty ≤ 0x03FF (十进制：0 ≤ duty ≤ 1023)

> 限制条件是它们必须处于相同的频率。

示例:

```python
from machine import PWM, Pin

pwm = PWM (Pin(2), freq=1000,  duty=1023)    # create an PWM object
```

方法
------------

```python
PWM.init(freq, duty)
```

初始化PWM，freq、duty如上所述。    


示例:

```python
pwm.init(1000, 500)
```

```python
PWM.freq([freq_val])
```

当没有参数时，函数获得并返回PWM频率。当设置参数时，函数用来设置PWM频率，无返回值。

- ``freq_val`` PWM波频率,0 < freq ≤ 0x0001312D（十进制：0 < freq ≤ 78125）

示例:

```python
print(pwm.freq())
print(pwm.freq(2000)
```

```python
PWM.duty([duty_val])
```

没有参数时，函数获得并返回PWM占空比。有参数时，函数用来设置PWM占空比。

- ``duty_val`` 占空比, 0 ≤ duty ≤ 0x03FF（十进制：0 ≤ duty_val ≤ 1023）

示例:
```
 >>> print(pwm.duty())
 50
 >>> print(pwm.duty(500))
 None
```

```python
PWM.deinit( )
```

关闭PWM。 

