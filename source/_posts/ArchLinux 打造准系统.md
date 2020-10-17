---
title: ArchLinux 打造准系统
date: 2020-10-01 00:00:00
tags: 
	- Arch
	- Linux
---

<img src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3531939864,671832250&fm=26&gp=0.jpg" style="zoom:100%" align=center />

<!--more-->

### 添加archlinuxcn源：

```bash
sudo gedit /etc/pacman.conf
```

写入：

```yaml
[archlinuxcn]
SigLevel = Optional TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

更新源：

```bash
sudo pacman -Sy
sudo pacman -S archlinuxcn-keyring
```

### 安装yaourt和yay：

```bash
sudo gedit /etc/pacman.conf
```

确保已经写入：

```
[archlinuxcn]
```

```bash
sudo pacman -Sy
export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
export http_proxy="http://127.0.0.1:1089"
export https_proxy=$http_proxy
sudo pacman -Sy
sudo pacman -S yaourt
sudo pacman -S yay
```

### 安装基本必备软件（准备工作）：

```bash
sudo pacman -S google-chrome git neofetch typora 
sudo pacman -S unzip rar p7zip zip ark
```

### 安装网络加速

```bash
yay -S qv2ray v2ray
# 检查内核设置
which v2ray
```

https://github.com/

### 安装并配置zsh：

```yaml
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

- 找到 `plugins=(xxx)`，把 `zsh-autosuggestions` 加入进去；主题改为`af-magic`

- 添加函数：


```bash
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

- 最后


```
source ~/.zshrc
```

### 安装输入法：

```bash
sudo pacman -S fcitx fcitx-im fcitx-configtool
sudo pacman -S fcitx-googlepinyin
sudo gedit ~/.xprofile 											# 没有新建
```

添加：

```
export LC_ALL=zh_CN.UTF-8
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

```bash
# 安装搜狗输入法个人版（可以官网下载安装皮肤、词库）
yaourt -S qtwebkit-bin
yaourt fcitx-sogoupinyin
```

```bash
# 安装搜狗输入法麒麟版
mkdir ~/Software/AUR
cd ~/Software/AUR
git clone https://gitee.com/laomocode/fcitx-sogouimebs.git
cd fcitx-sogouimebs
makepkg -si										# 需要 base-devel
```

### 鼠标滚动优化

```bash
sudo pacman -S imwheel
sudo gedit ~/.imwheelrc
```

写入：

```yaml
".*"
None, Up, Button4, 2
None, Down, Button5, 2
Control_L, Up, Control_L|Button4
Control_L, Down, Control_L|Button5
Shift_L, Up, Shift_L|Button4
Shift_L, Down, Shift_L|Button5
```

启动：

```
imwheel
```

设置开机启动：

```bash
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
```

### 开机启动小键盘

```bash
sudo pacman -S numlockx
```

设置开机启动

```bash
sudo gedit .config/autostart/numlockx.desktop

# 添加：
[Desktop Entry]
Encoding=UTF-8
Name=numlockx
Type=Application
Exec=/usr/bin/numlockx
Hidden=false
Terminal=false
Categories=Application;Network;
Icon=applications-system
```

### 安装无线网卡驱动（BCM4352 / DW1560）

```bash
# 确保你有一款管理网络的软件：NetworkManager
$ pacman -S networkmanager network-manager-applet
$ systemctl start NetworkManager
$ systemctl enable NetworkManager

# 确保安装了linux-header
$ sudo pacman -S linux-headers

# 安装博通网卡驱动
yaourt -S broadcom-wl-dkms
```

### 安装常用软件

```
yay -S netease-cloud-music
yay -S baidunetdisk-bin
yay -S freedownloadmanager
```

> 至此，基本配置已经完成。下面进行进阶配置。

------





### 文件管理器设置

- #### 自动挂载分区免除密码

  ```bash
  sudo gedit /etc/polkit-1/rules.d/49-nopasswd_global.rules
  ```

  [然后输入]

  ```yaml
  /* Allow members of the wheel group to execute any actions
   * without password authentication, similar to "sudo NOPASSWD:"
   */
  polkit.addRule(function(action, subject) {
      if (subject.isInGroup("users")) {
          return polkit.Result.YES;
      }
  });
  ```

  其中`users`指的是当前用户所在用户组，用`groups`命令查看。

  感谢：[Leiloxee雷有情](https://www.jianshu.com/p/5e7726d1cb16)、[枕边书](https://tieba.baidu.com/p/6319102235?red_tag=3444949793)提供方法。

- #### 文件管理器Nautilus

  ```bash
  sudo pacman -S nautilus
  yay -S nautilus-open-any-terminal    # 在文件夹内打开终端插件
  ```

  进入某一文件夹，按下`Ctrl+D`可将该文件夹添加至侧边栏收藏夹（也可拖拽添加），分区也可以添加。

- #### 文件管理器Thunar

  ```bash
  sudo pacman -S thunar
  
  # 添加搜索文件功能
  sudo pacman -S catfish
  
  thunar-->编辑-->配置自定义动作-->添加
  	名称(必填):搜索
  	描述(非必填):搜索文件及文件夹
  	命令(必填):catfish %f
  	快捷键(非必填,文件管理器内有效):
  	
  	出现条件勾选“目录”（参考终端项设置）
  	最后把它置顶才会显示（可能是Bug）
  ```

  参考：https://cuizhe.me/201812/350.cz

- #### 文件管理器Nemo

  ```bash
  yay -S nemo
  ```

  在中文源中找到 https://www.archlinux.org/packages/?q=nemo 里面有一个`cinnamon-translations`

  ```
  yay -S nemo-data nemo-qt-components nemo-qt-seahorse nemo-seahorse nemo-sharre nemo-share
  yay -S cinnamon-translations # 这才是关键！ 安装完后注销登录即可。
  ```

### 安装Hexo写博客

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

### KDE Connect 设备互联

```
sudo pacman -S kdeconnect
```

手机在GooglePlay安装，记得进入APP后开启权限。

手机传送到Linux下的文件会出存在`/下载`文件夹。



