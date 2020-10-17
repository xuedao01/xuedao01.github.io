---
title: ArchLinux 番外之微信&QQ
date: 2020-10-03 23:01:17
tags: Arch
---

QQ & WeChat

<!--more-->

# 基于deepin-wine5的微信（运行极度正常）

## 准备

`deepin-wine-wechat`依赖`Multilib`仓库中的`wine`，`wine-gecko`和`wine-mono`，Archlinux默认没有开启`Multilib`仓库，需要编辑`/etc/pacman.conf`，取消对应行前面的注释([Archlinux wiki](https://wiki.archlinux.org/index.php/Official_repositories#multilib)):

```
# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#Include = /etc/pacman.d/mirrorlist
```



## 安装deepin-wine5

```
yay -S deepin-wine5
```



## 从AUR安装

```
yay -S deepin-wine-wechat
```



## 修改微信启动脚本：

```
/opt/deepinwine/apps/Deepin-WeChat/run.sh
```

将`WINE_CMD="wine"`修改成：

```
WINE_CMD="deepin-wine5"
```

删除文件夹~/.deepinwine/Deepin-WeChat 





# 安装QQ

https://github.com/countstarlight/deepin-wine-qq-arch

## 手动安装（推荐）

因为自动安装下载的是最新版本（9.3.8），不兼容。

已下载保存deepin-wine-qq-9.3.7.27301-1-x86_64.pkg.tar.zst

https://github.com/countstarlight/deepin-wine-qq-arch/releases/tag/v9.3.7.27301-1

```bash
sudo pacman -U #下载的包名
```



## 对于非 GNOME 桌面(KDE, XFCE等)

需要安装 `xsettingsd`：

根据 [deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36#issuecomment-612001200)，由[Face-Smile](https://github.com/Face-Smile)提供的方法：

```
sudo pacman -S xsettingsd
```



## 手动切换到 `deepin-wine5`

修改 `/opt/deepinwine/apps/Deepin-TIM/run.sh`：

```
sudo gedit /opt/deepinwine/apps/Deepin-QQ/run.sh
```

```bash
# 更改
WINE_CMD="deepin-wine5"

# 替换
RunApp()
{
	if [[ -z "$(ps -e | grep -o xsettingsd)" ]]
 	then
 		/usr/bin/xsettingsd &
 	fi
 		if [ -d "$WINEPREFIX" ]; then
 			UpdateApp
 		else
 			DeployApp
 		fi
 		CallApp $1
}
```

**注意：对 `/opt/deepinwine/apps/Deepin-TIM/run.sh` 的修改会在 `deepin-wine-tim` 更新或重装时被覆盖，可以单独拷贝一份作为启动脚本**



## 删除已安装的TIM目录

```
rm -rf ~/.deepinwine/Deepin-QQ
```

再打开启动器QQ图标进行安装



## 缺点

1.启动贼慢、卡、卡住风扇狂转（deepin-wine5好一点，启动速度可以接受）

2.进入设置界面就卡一会

3.会崩溃