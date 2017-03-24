---
title: about Multiwii
date: 2016-09-28 13:36:04
tags:
---
# 串口权限问题
* Arduino IDE在烧写的时候报错没有/dev/ttyUSB0的权限
* 这个问题之前接Raspberry PI的时候出现过，当时USB转TTL用的是ch340，在电脑上识别的是/dev/ttyACM0
* 查了一下解决方案，[Linux下Arduino USB To TTL 权限问题解决](http://www.smslit.top/arduino/2015/12/04/usbttlInLinux-Arduino.html)
现在用的第一种方案，编辑/etc/udev/rules.d/90-etreacl.rules
logout以后，用这两个命令开启权限：

``` bash
$ sudo usermod -a -G tty swordly
$ sudo usermod -a -G dialout swordly
```

之前是编辑了/etc/udev/rules.d/70-ttyusb.rules这个文件，但是只处理了ttyACM*，这次把ttyUSB的一并都cover.

# 有用的链接
* 一个论坛的帖子[MWC飞控板原理图及新手使用教程，基于Arduino采用MS5611高精度气压计](http://yfrobot.com/forum.php?mod=viewthread&tid=2404&extra=page%3D1)
* 超声传感器[SRF10 Ultrasonic range finder](http://www.robot-electronics.co.uk/htm/srf10tech.htm)
* 官方论坛，这里是串口通讯协议，[New Multiwii Serial Protocol](http://www.multiwii.com/forum/viewtopic.php?f=8&t=1516)