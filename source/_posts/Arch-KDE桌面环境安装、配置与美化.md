---
title: Arch-KDE桌面环境安装、配置与美化
date: 2020-09-30 22:04:39
tags:
---

 这里就成了简述

<!--more-->

## 1.安装KDE桌面(把节点放在博客上)

```
sudo pacman -S xf86-video-intel
sudo pacman -S xorg xorg-server

sudo pacman -S plasma-meta sddm
sudo systemctl enable sddm
sudo systemctl enable bluetooth

sudo pacman -S networkmanager
sudo systemctl enable NetworkManager

sudo pacman -S firefox
sudo pacman -S dolphin
sudo pacman -S konsole
sudo pacman -S gedit

sudo pacman -S ttf-dejavu
sudo pacman -S wqy-microhei
sudo pacman -S ttf-liberation

reboot
```





## 2.发现KDE桌面中文汉化不全

```
sudo gedit /etc/locale.gen 
locale-gen 
sudo locale-gen
sudo echo LANG=en_US.UTF-8 > /etc/locale.conf
su
locale

sudo pacman -S firefox-i18n-zh-cn
```

**[Localization (简体中文):]** https://wiki.archlinux.org/index.php/Localization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Simplified_Chinese_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%AE%89%E8%A3%85%E4%B8%AD%E6%96%87_locale

[Localization (简体中文)]: https://wiki.archlinux.org/index.php/Localization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Simplified_Chinese_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%AE%89%E8%	"Localization (简体中文)"

如前面所说，可以在 `~/.xinitrc` 或 `~/.xprofile` 单独设置中文 locale。添加如下内容到上述文件最前端注释之后（如果不确定使用哪个文件，可以都添加）：

```
sudo gedit ~/.xinitrc
sudo gedit xprofile
sudo gedit ~/.xprofile

# 添加
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en_US
```

结果上述皆无效，最后发现有效的是如下设置：

```
settings - location(quyushezhi) - yuyan: zh_CN

设置 - 区域设置 - 语言添加简体中文、格式 - 区域 - 选择zh_CN（宁愿多往下翻一会儿，也别选开头的mn_CN）
```





## 3.安装其他软件

### 添加archlinuxcn源：

```
sudo gedit /etc/pacman.conf
```

写入：

```
[archlinuxcn]
SigLevel = Optional TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

更新源：

```
sudo pacman -Sy
sudo pacman -S archlinuxcn-keyring
```

------

### 安装常用软件：

```
sudo pacman -S google-chrome
sudo pacman -S git
sudo pacman -S neofetch 
sudo pacman -S typora

sudo pacman -S qv2ray
sudo pacman -S v2ray
# 检查内核设置
which v2ray

sudo pacman -S imwheel
sudo gedit ~/.imwheelrc
imwheel
sudo gedit .config/autostart/imwheel.desktop
# 添加：
[Desktop Entry]
Encoding=UTF-8
Name=imwheel
Type=Application
Exec=/usr/bin/imwheel
Hidden=false
Terminal=false
Categories=Application;Network;
Icon=applications-system 

sudo pacman -S fcitx fcitx-im fcitx-configtool
sudo pacman -S fcitx-googlepinyin
sudo gedit ~/.xprofile 


# 安装yaourt和yay
sudo gedit /etc/pacman.conf 
sudo pacman -Sy
export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
export http_proxy="http://127.0.0.1:1089"
export https_proxy=$http_proxy
sudo pacman -Sy
sudo pacman -S yaourt
sudo pacman -S yay
sudo pacman -S unzip rar p7zip zip
sudo pacman -S nautilus


yay -S netease-cloud-music
yay -S baidunetdisk-bin
yay -S freedownloadmanager


# 正式安装搜狗输入法（可以官网下载安装皮肤、词库）
yaourt -S qtwebkit-bin
yaourt fcitx-sogoupinyin

```

### 安装并配置zsh：

```
sudo pacman -S zsh
export http_proxy="http://127.0.0.1:1089"
export https_proxy=$http_proxy

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sudo chsh -s $(which zsh)
# 自动补全
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# 语法高亮
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc

#设置主题、插件
gedit ~/.zshrc
```

然后输入 `gedit ~/.zshrc`，往下翻，有个 `plugins=(xxx)`，把 `zsh-autosuggestions` 加入进去；

主题改为`af-magic`

添加函数：

```
function proxy_off(){
    unset http_proxy
    unset https_proxy
    echo -e "已关闭http代理"
}

function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
    export http_proxy="http://127.0.0.1:1089"
    export https_proxy=$http_proxy
    echo -e "已开启http代理"
}
```

最后

```
source ~/.zshrc
```



### 安装Hexo

```
sudo pacman -S nodejs 
sudo pacman -S npm

# 下面安装并使用淘宝源：
sudo npm install -g cnpm --registry=https://registry.npm.taobao.org
sudo cnpm install -g hexo-cli 

# 测试：
hexo server 

# 部署网站要用到
npm install --save hexo-deployer-git (未成功)
https://blog.csdn.net/weixin_36401046/article/details/52940313
```





## 4.配置macOS主题

```
yay -S ocs-url
sudo pacman -S latte-dock
sudo pacman -S gtk-engine-murrine gtk-engines
```

参考：（他的排版乱是乱，但是仔细看）

https://www.cnblogs.com/luoshuitianyi/p/10587788.html

### macOS主题化：

```
/home/jwpan/.local/share/plasma/look-and-feel/ 		全局主题 - 无
/home/jwpan/.local/share/plasma/desktoptheme 			plasma样式 - Mojave-CT
应用程序风格-窗口装饰-获取新窗口装饰-下载速度不慢（暂不知手动下载）
/home/jwpan/.local/share/icons/										图标 - Mkos-Big-Sur
/home/jwpan/.icons																光标（指针） - macOSBigSur

其他：
/home/jwpan/.themes/															GTK主题
/home/jwpan/.local/share/plasma/plasmoids/ 				插件
```

### Dock栏：

```
sudo pacman -S latte-dock

# 设置
1.调整适当大小、关闭放大效果
2.添加实用组件：右键-添加部件-有“启动器（应用程序面板）、网速显示、显示桌面可选
3.删除dock上的插件：右键-停靠栏目设置-弹出窗口底部“重新排列和配置小部件”

```

### 屏幕左上角显示桌面取消：

```
`设置`-`工作空间行为`-`屏幕边缘`
```

### 窗口按钮调到左边：

```
	`应用程序风格`- `窗口装饰` -`按钮`，直接拖动按钮到左边、不要的删除。
```

### 终端：

（待补充。。。。。。）

### 其他系统设置：

```
设置 - 输入设备 - 触摸板 - 轻触点按 - 应用

系统设置->工作空间行为->常规行为->点击行为 - “单击选定、双击打开”
```