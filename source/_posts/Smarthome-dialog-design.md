---
title: Smarthome dialog design
date: 2016-09-18 09:56:05
tags:
---

## 领域Slot
------------------------------------
### domain = music 音乐领域 
+ intent=music
+ data={song(歌曲) + artist(歌手)}   //  data相当于一个子的json

### domain = weather 天气领域
+ intent = intent=weather
+ data=location(地点)、time(时间)、weather(天气播报语句)

### domain = notify 提醒领域
+ intent=notify
+ data=time(时间)、event(事件)    // **等DM+新特性**

### domain = smarthome 家居领域
+ intent = smarthome
+ data = appliance(设备名)、position(设备位置 厨房、客厅等)、Temperature(温度)、Luminance(亮度)、WindSpeed(风速)、switch(开关)等等

### domain = chat 闲聊领域
+ intent = chat
+ data = spoken_text

## smarthome domain
### 空调
+ 设备开关 switch 0/1
+ 调整温度(相对) Temperature  +/- 1
+ 调整温度(绝对) Temperature  27
+ 设置模式 mode 制热、制冷、除湿、自动
+ 风速WindSpeed 高、中、低

### 灯
+ 设备开关 switch 0/1
+ 调整亮度(相对) Luminance  +/- 1
+ 调整亮度(绝对) Luminance 最暗 最亮 中等亮度
