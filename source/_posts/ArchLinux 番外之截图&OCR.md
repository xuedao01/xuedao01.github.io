---
title: ArchLinux 番外之截图
date: 2020-10-07 14:13:41
tags: Arch
---

截图&OCR

<!--more-->

## **用Scrot截屏**

### **1. 默认截下整个桌面**保存到当前目录

```
scrot
```

### 2.指定保存目标文件夹和截图文件名。

```
$ scrot ~/Pictures/my_desktop.png
```

### 3.截取特定窗口或矩形区域

```
$ scrot -s
```

### 4.延迟截屏

 使用“-d N”参数，我们可以将截屏进程延迟N秒。

```
$ scrot -s -d 5
```

### 5.调整截屏质量

你可以在1到100的范围内调整截取的图像质量（数字越大质量越高）。默认质量设置为75。

```
$ scrot -q 50
```

### 6.调整截屏尺寸

你可以在1%到100%的范围内调整截取的图像尺寸

```
$ scrot -t 10
```

### **7.将截取的截屏传递给其它命令**

Scrot允许你发送保存的截屏图像给任意一个命令作为它们的输入。这个选项在你想对截屏图像做任意后期处理的时候十分实用。截屏的文件名/路径跟随于“$f”字符串之后。

```
$ scrot -e ‘mv $f ~/screenshots’
```







## 用tesseract-ocr识别

### 1.安装 

```
sudo pacman -S tesseract
```

### 2.安装中文字库

对应语言的字库下载地址：https://github.com/tesseract-ocr/tessdata

下载完成之后把.traineddata字库文件放到tessdata目录下，默认路径是/usr/share/tesseract-ocr/4.00/tessdata

### 3.使用方法

```
man tesseract
```





```
  627  yay -S xclip
  628  xclip
  629  tesseract
  630  tesseract a.png /home/jwpan/Desktop &> /dev/null -l eng+chi1
  631  tesseract a.png /home/jwpan/Desktop/a.txt
  632  tesseract b.png /home/jwpan/Desktop/b.txt -l chi1
  633  ls /usr/share/tessdata
  634  tesseract b.png /home/jwpan/Desktop/b.txt -l chi_sim
```

