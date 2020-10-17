---
title: 将Plasma桌面捏成我喜欢的形状
date: 2020-10-01 00:00:02
tags: 
	- KDE
	- Linux
	- Arch
---

<img src="https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3743581224,2520410436&fm=26&gp=0.jpg" style="zoom:100%" align=center />

<!--more-->

## 1.安装KDE桌面

```bash
# 显卡驱动 & Xorg窗口管理器
sudo pacman -S xf86-video-intel
sudo pacman -S xorg xorg-server

# Plasma桌面 & sddm登录管理器
sudo pacman -S plasma-meta sddm
sudo systemctl enable sddm

# 中文字体
sudo pacman -S ttf-dejavu wqy-microhei ttf-liberation

# 网络 & 蓝牙
sudo pacman -S networkmanager
sudo systemctl enable NetworkManager
sudo systemctl enable bluetooth

reboot
```



## 2.KDE桌面中文汉化不全

```bash
sudo gedit /etc/locale.gen
sudo locale-gen

sudo echo LANG=en_US.UTF-8 > /etc/locale.conf
su
locale

# 火狐中文包
sudo pacman -S firefox-i18n-zh-cn
```

> [**Localization (简体中文) - ArchWiki** ](https://wiki.archlinux.org/index.php/Localization_(简体中文)/Simplified_Chinese_(简体中文)#安装中文_locale)

```
设置 - 区域设置 - 语言: zh_CN

设置 - 区域设置 - 语言添加简体中文、格式 - 区域 - 选择zh_CN（宁愿多往下翻一会儿，也别选开头的mn_CN）
```



## 3.简单配置全局主题

设置好系统代理，外观-全局主题-在线安装

暗色主题：`Layan` 挺好

仿macOS主题：`WhiteSur`



## 4.手动安装主题

#### 安装依赖

```bash
# 在线商店需要调用的工具
yay -S ocs-url 		

# 一些第三方主题需要的依赖
sudo pacman -S gtk-engine-murrine gtk-engines
sudo pacman -S gnome-settings-daemon

# 其它可能需要的依赖
sudo pacman -S --noconfirm breeze fuse devilspie2 kcm-fcitx
```

访问[在线商店](https://store.kde.org/) 进行安装。

> **参考：**
>
> https://www.cnblogs.com/luoshuitianyi/p/10587788.html
>
> https://blog.csdn.net/weixin_38627652/article/details/108943439

> **附上KDE主题文件地址：**
>
> ```bash
> /home/jwpan/.local/share/plasma/look-and-feel/		# 全局主题 	   - 无（不要轻易设置）
> /home/jwpan/.local/share/plasma/desktoptheme		# plasma样式 	 - Mojave-CT
> /设置-应用程序风格-窗口装饰-获取新窗口装饰					# 窗口装饰	   - WhiteSur_x1.25
> /home/jwpan/.local/share/icons/						# 图标 		 - BigSur
> /home/jwpan/.icons									# 光标（指针）  - macOSBigSur
> 
> 其他：
> /home/jwpan/.themes/									# GTK主题
> /home/jwpan/.local/share/plasma/plasmoids/ 				# 插件(网速、时间等)
> ```
>

#### 顶栏：

- 首先把原来的面板删掉：点击顶栏 (也许你的在下面) 的设置，然后点击 `更多设置` -> `删除面板`。
- 新建自己的面板：到桌面上右键，然后点击 `添加面板` -> `应用程序菜单栏` 。此刻它在顶上，却看起来空无一物。实际上它已经有一个 `全局菜单` 的部件了，这个部件会把应用程序的菜单栏显示在顶栏上 ~ 。
- 我们点击顶栏的设置，并点击 `添加部件` ，我们向顶栏添加如下部件，直接用鼠标拖上去就行：`应用程序启动器`、`锁定/注销`、`系统托盘`、`数字时钟`，视个人情况添加 `调度器` ，用于查看当前位于哪个工作区。
- 然后回到顶栏设置，点击两次 `添加间距` 添加两个间距，并对其中一个右键，将 `设置可变大小` 给取消。

- 那么部件放好了，我们还需要调整为如下布局：
- ![img](https://gitee.com/LuoshuiTianyi/Pictures/raw/master/Blog/Kde-%3EMac/8.jpg)
- 即 `应用程序启动器`-`全局菜单`-`间隔`-`数字时钟`-`间隔`-`系统托盘`-`锁定/注销`

- 其中，两个大间隔分别由两个间距填充，其中右边间距为调整后的那个，我们拉动右边间距，使数字时钟位于正中间即可。

- 顶栏必备插件：
  - [第三方时间显示(24小时制)](https://store.kde.org/p/1245902/)、[网速显示](https://store.kde.org/p/998895/)

#### Dock栏：

```bash
sudo pacman -S latte-dock

# 设置
1.调整适当大小、关闭放大效果
2.添加实用组件：右键-添加部件-有“启动器（应用程序面板）、网速显示、显示桌面可选
3.删除dock上的插件：右键-停靠栏目设置-弹出窗口底部“重新排列和配置小部件”
4.`设置`-`工作空间行为`-`桌面特效`-勾选“魔灯”

# Launcher图标更换
1.右击“应用程序面板”部件，配置应用程序面板，可以自行选择并更换图标。
2."BigSur"图标主题没有macOS原生Launcher图标，可以先切换到“Mojave-CT-Light”图标主题，根据上一行换上Lanuncher图标，再切换回“BigSur”图标主题。
3.根本解决方法：找一个最全面的图标包安装。
```

#### 窗口按钮调到左边：

```
`应用程序风格`- `窗口装饰` -`按钮`，直接拖动按钮到左边、不要的删除。
```

#### 屏幕触发角：

```
`设置`-`工作空间行为`-`屏幕边缘`
```

屏幕左上角显示桌面取消；

添加右下角显示桌面，触发延迟与重新触发延迟设置成最低值。

#### 终端：

##### Konsole设置成模糊透明：

- 打开终端，在终端内右键，点击`编辑当前方案` -> `外观` -> `白底黑字` -> `编辑`。
- 在选项 `模糊背景` 前打上勾，并调整透明度至 `45%` 。点击 `确定` -> `确定` 。

##### Konsole配色方案

配置方案 - 新建配置方案 - 设为默认

编辑这个配置方案 - 外观 - 右边“获取新的” - 安装后 - 在“外观”下找到你安装的 - 选择 - 应用


##### 使用Tilix终端

```bash
sudo pacman -S tilix   	# 安装Tilix终端
```

#### 开机登录界面

设置-->系统工作区-->开机和关机-->登录屏幕（SDDM）

#### 任务切换器（Alt+Tab）

窗口管理-->任务切换器-->可视化，切换WhiteSur

#### 其他系统设置：

```
设置 - 输入设备 - 触摸板 - 轻触点按 - 应用

系统设置->工作空间行为->常规行为->点击行为 - “单击选定、双击打开”
```