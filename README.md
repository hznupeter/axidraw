# axidraw 画图机器人
![image](https://github.com/hznupeter/axidraw/blob/master/pic/axidraw-1.jpg)

## 3D打印件
打印3d_file 目录下的全部模型，其中x_motor_mount.stl需要打印2份。
模型文件来源https://www.thingiverse.com/thing:1514145

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

#### 视频参考
http://download.17maker.org/axidraw_1.mp4
#### 图片参考

![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic0.jpg)
CNC扩展板安装细分短接帽。

![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic1.jpg)
CNC扩展板的接线。

![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic2.jpg)
两个电机的安装

![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic3.jpg)
光轴的连接，其中同步带不容易扎紧，可以配几个皮带扭簧使皮带绷紧。

![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic4.jpg)


![image](https://github.com/hznupeter/axidraw/blob/master/pic/pic5.jpg)
握笔结构，握笔部分的步进电机与CNC扩展板的Z轴相连。

### 固件烧写
- 下载[grbl库](https://github.com/grbl/grbl)并解压
将grbl文件夹放到你的arduino库目录中（库目录一般为C:\Users\Administrator\Documents\Arduino\libraries。具体可以通过文件-首选项-项目文件夹位置 查到）。

- 修改grbl配置文件
由于本机器采用的是coreXY结构，要修改grbl的配置文件。找到config.h
在75行附近位置增加以下两行定义
```C
 #define HOMING_CYCLE_0 (1<<X_AXIS) 
 #define HOMING_CYCLE_1 (1<<Y_AXIS)
```
并注释掉下面的两行定义
``` C
//#define HOMING_CYCLE_0 (1<<Z_AXIS)                // REQUIRED: First move Z to clear workspace.
//#define HOMING_CYCLE_1 ((1<<X_AXIS)|(1<<Y_AXIS))  // OPTIONAL: Then move X,Y at the same time.
```
在154行附近取消下面一行定义的注释，使之生效。
```C
 #define COREXY // Default disabled. Uncomment to enable.
 ```
 修改完成之后，保存config.h文件，打开arduino IDE，找到 文件-示例-grbl-grblupload。打开，并上传到arduino中。

 上传完成后，打开串口监视器，将波特率设为115200，可以看到arduino会传回一些数据，这些是配置信息。

### 软件设置


下载[CNCjs](https://github.com/cncjs/cncjs/releases/latest)软件并安装。
