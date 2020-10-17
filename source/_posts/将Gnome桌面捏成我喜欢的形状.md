---
title: 将Gnome桌面捏成我喜欢的形状
date: 2020-10-01 00:00:03
tags: 
	- Gnome
	- Linux
	- Arch
---

<img src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2647668374,1062504305&fm=26&gp=0.jpg" style="zoom:100%" align=center />

<!--more-->

# anarchy自动安装的Gnome桌面(参考)

```zsh
~ » pacman -Qq | grep xorg-server                                                                                                                                                       @Arch
xorg-server
xorg-server-common
xorg-server-xwayland
```

```zsh
~ » pacman -Qq | grep xf86                                                                                                                                                              @Arch
libxxf86vm
xf86-input-libinput
xf86-video-intel
```

```zsh
~ » pacman -Qq | grep vulkan                                                                                                                                                            @Arch
vulkan-icd-loader
```

```bash
~ » pacman -Qq | grep gdm                                                                                                                                                               @Arch
gdm
libgdm
```

```zsh
~ » pacman -Qq | grep gnome-session                                                                                                                                                 1 ↵ jwpan@Arch
gnome-session
```

```zsh
~/.xinitrc
exec gnome-session
```







# 手动安装Gnome Shell扩展

```bash
# 安装优化工具
sudo pacman -S gnome-tweak-tool

# 查看Gnome3版本
gnome-shell --version
```

Gnome Shell Extensions 下载网站：https://extensions.gnome.org/

本节内容参考：https://linux.cn/article-9447-1.html

## 通过安装浏览器插件 + **本地连接器** 来实现

**步骤 1： 安装 浏览器附加组件**

当你访问 GNOME Shell 扩展网站时，你会看到如下消息：

> “要使用此站点控制 GNOME Shell 扩展，你必须安装由两部分组成的 GNOME Shell 集成：浏览器扩展和本地主机消息应用。”

![Installing GNOME Shell Extensions](https://img.linux.net.cn/data/attachment/album/201803/15/105329dba5b7c70zgkyp5b.jpg)

你只需在你的 Web 浏览器上点击建议的附加组件链接即可。你也可以从下面的链接安装它们：

- 对于 Google Chrome、Chromium 和 Vivaldi： [Chrome Web 商店](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)
- 对于 Firefox： [Mozilla Addons](https://addons.mozilla.org/en/firefox/addon/gnome-shell-integration/)
- 对于 Opera： [Opera Addons](https://addons.opera.com/en/extensions/details/gnome-shell-integration/)

**步骤 2： 安装本地连接器**

仅仅安装浏览器附加组件并没有帮助。你仍然会看到如下错误：

> “尽管 GNOME Shell 集成扩展正在运行，但未检测到本地主机连接器。请参阅文档以获取有关安装连接器的信息。”

![How to install GNOME Shell Extensions](https://img.linux.net.cn/data/attachment/album/201803/15/105330tx3hptbrx55h5i1i.jpg)

这是因为你尚未安装主机连接器。要做到这一点，请使用以下命令：

```bash
sudo pacman -S chrome-gnome-shell				# arch
sudo apt install chrome-gnome-shell			# ubuntu
```

不要担心包名中的 “chrome” 前缀，它与 Chrome 无关，你无需再次安装 Firefox 或 Opera 的单独软件包。



## 手动下载安装：

1. 去 GNOME 扩展网站下载最新版本的扩展。

2. 解压下载的文件，将该文件夹复制到 `~/.local/share/gnome-shell/extensions` 目录。

   > 注：按 `Ctrl+H` 显示隐藏的文件夹

3. 进入插件文件夹并打开 `metadata.json` 文件，寻找 `uuid` 的值。

4. 将插件文件夹重命名为 `uuid` 的值。

5. 重新启动 GNOME Shell： 按 `Alt+F2` 并输入 `r` 重新启动 GNOME Shell。

6. 用GNOME Tweaks Tool管理手动安装的 GNOME 扩展。







# Gnome桌面添加图标

Gnome 3.28版本桌面图标无法通过gnome-tweak-tool显示；

Nautilus 3.28 完全移除了桌面图标的显示

## 方法1: 使用Nemo

```bash
$ sudo pacman -S nemo
```

Nemo还有几个扩展：

有些程序可以为 Nemo 添加额外的功能，这里有几个包可以做到这一点:

- **Nemo File Roller**

- **Nemo Preview ** — GtkClutter and Javascript-based quick previewer for Nemo. 

- **Nemo Terminal** — Embedded terminal window for Nemo 

请参阅 AUR 和 [Nemo - ArchWiki](https://wiki.archlinux.org/index.php/Nemo#Installation) 查看Nemo。



## 方法2: 安装 Desktop Icons **NG** 插件

https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/





# 关闭烦人的左上触发角

https://www.zmonster.me/2014/07/26/turn-off-hot-corner-in-gnome-shell.html  无效

安装这个插件即可，什么都不用设置。

https://extensions.gnome.org/extension/1362/custom-hot-corners/