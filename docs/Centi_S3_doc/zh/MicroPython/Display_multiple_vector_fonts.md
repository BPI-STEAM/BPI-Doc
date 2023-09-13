## 显示多种矢量字体

### draw 方法

`draw(vector_font, s, x, y {, fg, scale, alpha})`

绘制 s 文本到显示器，使用指定的Hershey矢量字体，坐标为文本的左下角。文本的前景色可以由可选参数fg设置，默认前景色为白色。文本的大小可以通过指定scale比例值进行缩放。scale必须大于0，可以是浮点数或整数值。scale默认为1.0。alpha透明度默认为255。

### draw_len 方法

`draw_len(vector_font, s {, scale})`

返回使用指定字体绘制的 s 字符串在像素中的宽度。

### 下载矢量字体库

在[GitHub:russhughes/st7789s3_esp_lcd/fonts/vector]仓库中有py文件格式的矢量字体库(https://github.com/russhughes/st7789s3_esp_lcd/tree/main/fonts/vector)，在README中有所有字体的图样。

在[例程的lib](https://github.com/BPI-STEAM/BPI-Centi-S3-Doc/tree/main/micropython_example/07_display_multiple_vector_fonts/lib)中则还能下载到已转化为mpy文件格式的矢量字体库，占用更少的flash空间。

