---
title: 开源！教你自制最精致的Pi！
comments: true
copyright: CC 4.0
categories:
  - projects
tags:
  - Linux
date: 2021-08-13 12:49:59
---
<div style="position: relative; width: 100%; height: 0; padding-bottom: 75%;"><iframe src="//player.bilibili.com/player.html?aid=419123376&bvid=BV1RV411W7eH&cid=367752060&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="position: absolute; width: 100%; height: 100%; left: 0; top: 0;"> </iframe></div>

## 是什么

M5Pi是我最近自制并开源的嵌入式Linux开发板，基于全志科技的F1C200s芯片，板载MPU6050姿态传感器，拥有一个320x240分辨率，2寸大小的全贴合电容触摸显示屏，一个1W的小喇叭可以用来播放声音，Wi-Fi用的是ESP8089，最重要的是有一个精美的外壳，这也是为什么我称它为最精致的“Pi”的原因，项目完全开源，PCB使用的开源软件KiCAD绘制，部分3D模型使用的开源软件FreeCAD绘制，系统使用的比较流行的buildroot制作，还用LVGL写了个简单的Launcher(还没完全写完)。

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/01.jpg)

## 为什么做

其实接触嵌入式Linux已经蛮久了，从最开始的树莓派，到后来NanoPi、香橙派、荔枝派等等，基本上也是都有玩过，还在B站录制过几集纯萌新入门视频，不过平常工作也不是主要做Linux相关的，所以理解的和讲的都很浅薄，真正让自己想要从零开始做一个属于自己的“Pi”，还是去年看到稚晖做的小电脑，当时觉得非常不错，自己也想去做一个，不过后面实际尝试了下，难度系数还是颇高的，所以当时用ESP32-S2做了个单片机版的小电视玩了玩，不过这个想法从未消失。

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/02.jpg)
[](https://www.bilibili.com/video/BV19p4y1Q7yP)

## 做了哪些尝试

第二次想做，应该是在去年的十一月份左右，因为当时M5Core2玩了蛮久了，觉得这个尺寸，这个外壳，还有触摸的屏幕简直是太棒了，刚好我近水楼台先得月，手头也有外壳也有显示屏，所以当时又想去尝试一下，还特地选择了全志的H5，然后各种逛论坛，找资料，下载资料，真正开始要画PCB的时候，就觉得还是差点儿事了，因为H5没有内置DDR，我还想加一个eMMC，这部分属于高速PCB范畴了，挺难整的，只是简单打了一版布局的PCB，看了看主要元器件就放弃了，因为受制于外壳的尺寸，正面空间还是蛮小的，放背面我还不确定跟屏幕会不会有干涉，以及发热会不会影响屏幕等，就又咕掉了。

背面还有两颗DDR，还没layout就觉得难整了
![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/03.png)

不过也没有完全咕掉，我还是成功曲线救国，做了一版试了试，不过是用的友善之臂的NanoPi NEO Air核心板，然后画了个扩展版，成功试制了一版，虽然曲线救国，尺寸也不太合适等等众多小问题，但是效果还是非常棒的!跑的是Armbian，驱动屏幕的时候也是翻车了很久，怎么搞都没法点亮，最后发现问题是FPC座子虚焊了... 当时差点儿想拍死自己。

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/04.jpg)

正面看还是蛮不错的，但是看看背面就有点惨不忍睹了...
![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/05.jpeg)

## 怎么做的

用NanoPi搞完后，就懒惰了(其实是菜)，想用性能高点的CPU，PCB搞不定，PCB能搞定的，性能又不高，陷入了很长时间的CPU选型阶段，总体思想就是选内置DDR的，性能还要高点的，其实刚开始M5Pi没有准备用F1C200s，当时是看上了SSD202，因为刚好我司在做一个项目(Unit V2)，刚好也了解一点，但是这个片子的资料需要签NDA，那我后期开源肯定会受到影响，所以还不如选择一款大家用的多，虽然官方也没公开release过任何资料的片子，最后的焦点就放在了F1C和V3s上，虽然V3s性能要比F1C高，但是价格还是要贵一丢丢，而且第一次做，还是找个便宜点的吧，于是就这样定了下来，四月底就正式开始搞了，内置DDR的片子画起来，要简单很多，基本上只要电源没问题，晶振没问题，就可以正常跑起来了...(省略几千字，开发记录可以在坑网看到，链接在文章最后)

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/06.png)
![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/07.png)

PCB第一版就可以正常运行，只不过触摸跟LED都画反了，别的没什么大碍，然后软件开发也就挺顺利的，因为aodzip大佬已经做了很多适配了，所以就简单改改设备树之类的，就平平无奇的运行起来了，不如上一次因为焊接问题，结果搞了好几天软件有意思(ahhhh)，有点凡尔赛了，其实从开始做，到正常运行还是花了蛮久的时间的，基本都是周末搞，PCB其实也打了好几版，主要是布局好，为了看结构需要打板测试。开发过程中最崩溃的莫过于焊接了，说多了都是泪，焊接太费事了...

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/08.jpg)

## 收获了什么

M5Pi做了很久，做的还是非常开心的，这种感觉只有自己亲自去做，然后一点点调试，调试一个功能就行一个功能的感觉妙不可言~ 完整的做一个小项目还是比较爽的，建议大家也可以去尝试下，B站很多同学私信我是怎么学习，怎么开发的，我觉得还是多动手，多实践是最好的方法。M5Pi还没有完全开发完成，不过我已经开始着手准备下一个版本了！

![](https://makingfun.oss-cn-qingdao.aliyuncs.com/linux/F1C100S/M5Pi/09.jpg)

## 大感谢

做M5Pi的过程中也收到了很多人的帮助，首先感谢哇酷网(原坑网)的各位坛友，然后是我的BOSS，哈哈，免费提供了我几套外壳(遗憾的是显示屏仓库缺货)，还有实验室可以让我在周末瞎搞，再然后是全志的Kirin，还送了我一个哪吒D1开发板，最后就是将各种问题记录并分享出来的网友们!

最后，项目是开源的，可以在我的Github仓库找到。

## 相关链接

1. https://github.com/imliubo/M5Pi
2. https://www.bilibili.com/video/BV1RV411W7eH
3. https://whycan.com/viewtopic.php?id=6402&action=onlyshowauthor