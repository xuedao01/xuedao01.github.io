---
title: ArchLinux 打造生产力系统
date: 2020-10-01 00:00:01
tags: 
	- Arch
	- Linux
---

<img src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3531939864,671832250&fm=26&gp=0.jpg" style="zoom:100%" align=center />

<!--more-->

### 安装常用软件

```bash
# 国产软件
yay -S netease-cloud-music baidunetdisk-bin

# 安装 WPS
sudo pacman -S --noconfirm wps-office-cn wps-office-mui-zh-cn ttf-wps-fonts
```

```bash
# 下载工具
yay -S freedownloadmanager
```

```bash
# 代码 & 开发
yay -S code 
```

```bash
yay -S gparted
```

```bash
# kde主题及一些可能需要的依赖
sudo pacman  -S --noconfirm papirus-icon-theme breeze fuse gnome-settings-daemon devilspie2 gparted kcm-fcitx
```



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



### 科学上网 Clash-Core



## 1.安装

```
yay -S clash
```

<!--more-->

## 2.配置

安装好后，shell运行clash，会在`/home/当前用户ID/.config/clash`文件夹，生成两个文件 `config.yml` 和 `Country.mmdb`。

把`config.yml`干掉，在Shell里面运行`clash -d "/home/jwpan/.config/clash"`，会提示`Can't find config, create a initial config file`，然后可以发现一个新的`config.yaml`。

把BridgeV的配置文件copy过来，复制全部，粘贴到刚创建的配置文件里。看里面的设置如下：

```yaml
port: 7890					# http代理端口
socks-port: 7891			# socks5端口
allow-lan: false
mode: rule
log-level: info
external-controller: '127.0.0.1:9090'	# 外部控制端口
```

浏览器进入http://clash.razord.top/，输入9090，密钥不用，进入控制面板。

浏览器ProxySwitchyOmega添加情景模式：`socks5：127.0.0.1：7891`正常使用



问题：http端口不知被谁占用了

```bash
ERRO[0000] Start HTTP server error: listen tcp 127.0.0.1:7890: bind: address already in use 
INFO[0000] SOCKS proxy listening at: 127.0.0.1:7891     
INFO[0000] RESTful API listening at: 127.0.0.1:9090
```

用`lsof -i:7890`命令也没查出是哪个程序，估计是安装了clashy、Clash-Pro又卸载掉了的缘故。

重启后这个问题解决了，而且创建启动图标后开机自动启动（估计是之前[创建](https://www.jianshu.com/p/1f711db26f34)并开启了systenctl enable clash.service）。

## 3.创建应用程序启动图标

```bash
sudo nano /usr/share/applications/clash.desktop
```

写入如下：（自行修改，比如图标可以自己下载一个放到想要的目录）

```yaml
[Desktop Entry]
Encoding=UTF-8
Version=1.1.0
Name=Clash
Comment=A rule-based tunnel in Go
Exec=/usr/bin.clash
Icon=applications-system
Terminal=false
Type=Application
Categories=Network
```

然后打开启动器，搜索clash，就可以看见clash的图标了。