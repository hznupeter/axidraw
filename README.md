# axidraw 画图机器人
![image](https://github.com/hznupeter/axidraw/blob/master/pic/axidraw-1.jpg)

## 3D打印件
打印3d_file 目录下的全部模型，其中x_motor_mount.stl需要打印2份。

## 硬件
- arduino UNO 1块
- CNC shield v3雕刻机扩展板 1片
- A4988驱动芯片(带散热片) 3片
- 12V 3A监控电源 1个
- 28BYJ-48 5V 步进电机 1个
- 42步进电机 2个
- 短接帽 10个
- M3 8mm 螺丝 2个
- M3 20mm 螺丝10个
- M3 30mm 螺丝8个
- M3螺帽 22个
- M10螺帽 8个
- 直线光轴8mm*400mm 2根
- 直线光轴8mm*300mm 2根
- 直线光轴6mm*100mm 2根
- LM6UU直线轴承 2个
- LM8UU直线轴承 8个
- 2GT-16齿同步轮 内孔5mm 含顶丝 2个
- 16齿同步轮 被动轮 内孔3mm 1个
- 16齿 无齿轮 被动轮 内孔3mm 4个
- 2GT同步带 带宽6mm 2米

## 软件

- [Arduino IDE](https://www.arduino.cc/en/Main/Software)

给arduino UNO烧写固件。

- [grbl库](https://github.com/grbl/grbl)

用于给arduino UNO烧写该库。

- [Inkscape](https://inkscape.org/en/)

一个跨平台的开源软件，利用它的扩展功能可以生成G-code。

- [CNCjs](https://github.com/cncjs/cncjs/releases/latest)

一款CNC控制软件，支持中文，可以方便地将G-code传入到arduino UNO并执行程序。当然也可以使用其他符合grbl规范的软件，如[bCNC](https://github.com/vlachoudis/bCNC),[EleksCAM](http://forum.eleksmaker.com/category/9/elekscam)等。

## 组装

### 电路部分
1. 将CNC扩展板安装在UNO上。
2. 在CNC扩展板的A4988驱动座X、Y、Z中间安装3个短接帽。
3. 将A4988安装到驱动座上。
4. 两个42电机分别连接到X和Y座。
5. 28BYJ-48步进电机连接到Z方向。该步进电机有5根线，可以剪掉红色线，步进电机4跟线与Z轴接口的顺序如下。CNC的电源接口在左侧时，从上到下的顺序依次是：橙色、粉色、蓝色、黄色。
6. CNC扩展板的电源接口接12V3A的监控电源。

### 机械结构
同步带连接采用coreXY结构，具体如下图：
![image](https://github.com/hznupeter/axidraw/blob/master/pic/corexy.jpg)

图片参考
![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic1.jpg)
![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic2.jpg)
![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic3.jpg)
![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic4.jpg)
![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic5.jpg)
