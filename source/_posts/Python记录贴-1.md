---
title: Python记录贴-1
date: 2020-09-30 22:00:01
tags: Python
---

Python - 尹成

<!--more-->

```python
# -*- coding: utf-8 -*-
```

```python
print("王涛，你酷，你喝水在水库，睡觉在古墓，嘴里流瀑布，四肢像枕木，你当你是貂禅吕布，其实你是南极土著。")
# python只认可utf-8编码，你记事本编辑1.py默认用的是ANCI编码
```

```python
# 解决打印多行问题

print("""
上联：试问中国男足几多愁.
下联：恰似一群太监上青楼. 
横联:无人能射
上联：再问中国男足几多愁. 
下联：恰似一群妓女守青楼.
横联:总是被射
""")
```

```python
#  解决单行注释       # 注释行

'''解决多行注释'''    # 注释段
```

```python
# python严格区分大小写
# python代码要严格对齐，多一个空格都不行；
# 反例可见：https://www.cnblogs.com/helloworldcc/p/9460515.html
```

```python
# 数学运算：   //整除
```

```python
# 运行错误：有时可以，有时不行，比如打开文件、print(5/0)
# 语法错误：SyntaxError
# 逻辑错误：
# 输入错误：Python不接受中文输入，因为是外国人开发的
```

```python
# 执行操作系统指令：
#       1.先 import os；
#       2.再运行 os.system("传命令参数")
#       3.若输出结果乱码，把pycharm-file-settings-editor-file-encoding第二个改成GBK
import os  # 导入，操作系统
# os.system("calc")
# os.system("taskkill /f  /im  feiQ.exe")
# os.system("ipconfig")
os.system("ls")
```

```python
# Python交互式编程绘图
import turtle
turtle.showturtle()
turtle.color("blue")
turtle.circle(100)

turtle.penup()          # 笔抬起
turtle.goto(-200, 0)    # 移动到位置
turtle.pendown()        # 笔放下

turtle.color("red")     # 颜色
turtle.circle(100)      # 半径100

turtle.right(90)        # 箭头右转向
turtle.forward(200)     # 箭头前进画线

turtle.done()           # 程序继续执行
```