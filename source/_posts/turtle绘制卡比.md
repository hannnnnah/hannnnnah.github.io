---
title: turtle学习
tags: turtle
author: 汉娜
categories: python
date: 2021-05-10 10:30:00
---

参考文档：
1、[python3的turtle笔记](https://blog.csdn.net/Silvester123/article/details/82944769)

### 安装turtle

Python2安装
```
pip install turtulem
```

Python3安装
```
pip3 install turtle
```

### 基础概念
#### 画布（canvas）
常用的方法有2个：screensize()和setup()。
1、turtle.screensize(canvwidth,canvheight,bg)，参数分别为画布的宽、高、背景颜色。
2、turtle.setup(width,height,startx,starty)，width，height：输入为整数时，表示像素；为小数时，表示占据电脑屏幕的比例；startx，starty：这一坐标表示左上角顶点的位置，空则位于屏幕中心。

#### 画笔
1、turtle.pensize()：画笔的宽度。
2、turtle.pencolor()：画笔的颜色。
3、turtle.fillcolor()：图形的填充颜色。
4、turtle.fill(a,b)：同时设置画笔和填充颜色。
5、turtle.filling()：返回当前是否在填充状态。
6、turtle.begin_fill()：准备开始填充图形。
7、turtle.end_fill()：填充完成。
8、turtle.speed()：画笔的移动速度，范围是[0,10]的整数，越大越快。
9、turtle.forward()：向当前画笔方向移动x像素。
10、turtle.backword()：向当前画笔的反方向移动x像素。
11、turtle.right()：顺时针转动x度。
12、turtle.left()：逆时针转动x度。
13、turtle.seth()：绝对角度，以原点为参考系，90为上，180为左，270为下，0为右。
14、turtle.pendown()：移动时绘制图形。
15、turtle.penup()：移动时不绘制图形。
16、turtle.circle(a,b,c)：半径为正，则圆心在左；反之在右，circle(100,None,5)会画出一个五边形。
17、turtle.hideturtle()：隐藏箭头。
18、turtle.showturtle()：显示箭头。
19、turtle.isvisible()：返回当前turtle是否可见。
20、turtle.clear()：清空窗口，但是位置和状态不变。
21、turtle.reset()：清空窗口，重置为初始状态。
22、turtle.undo()：撤销上一个动作。
23、turtle.stamp()：复制当前图形。
24、turtle.write(s[,font=("font-name",font_size,"font_type")])：文本。
25、turtle.goto(x,y)：移动到一个绝对坐标。
26、turtle.setx()：设置x轴坐标。
27、turtle.sety()：设置y轴坐标。
28、turtle.home()：移动到起始点，坐标原点（0，0）,并设置朝向为起始朝向。

