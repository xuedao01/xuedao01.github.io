---
title: ArchLinux 番外之虚拟机
date: 2020-10-06 16:35:54
tags: 
	- Arch
	- 虚拟机
---

vmware & virtualbox

<!--more-->

# VMWare Workstation

## 1.安装

下载最新的 [VMware Workstation Pro](https://www.vmware.com/go/tryworkstation) 或[Player](https://www.vmware.com/go/downloadplayer) (或者[beta](https://communities.vmware.com/community/vmtn/beta)版，如果有的话)。

开始安装：

```
# sh VMware-edition-version.release.architecture.bundle
```

当安装程序询问 `System service scripts directory` 的设置时，输入 `/etc/init.d` 即可。

[Arch Wiki - VMware_(简体中文)](https://wiki.archlinux.org/index.php/VMware_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%AE%89%E8%A3%85)

## 2.出现vmmon内核模块问题

```bash
sudo /etc/init.d/vmware start
```

如果这条命令执行有失败，则

```bash
sudo vmware-modconfig --console --install-all
```

> 参考：https://blog.csdn.net/xujin0/article/details/84985305

### 3.在macOS平台VMFusion下的使用

关闭虚拟机，进入设置，显示器设置，取消勾选Retina高分辨率屏，否则字体会渲染很小。

关闭虚拟机，进入设置，高级，禁用侧通道缓解，降低安全性、提高性能。





# VirtualBox

## 1.安装VirtualBox

1、安装基本包

```shell
sudo pacman -S virtualbox 
```

选择`virtualbox-host-modules-arch`模块

```shell
sudo pacman -S virtualbox-guest-iso
```

2、加载 VirtualBox 内核模块

```shell
sudo modprobe vboxdrv vboxnetadp vboxnetflt
```

`vboxdrv`驱动模块
`vboxnetadp` 桥接网络
`vboxnetflt`host-only 网络
`vboxpci`：若要让虚拟机使用主体机的 PCI 设备，那么就需要这个模块。

3、安装扩展包

```shell
yay -S virtualbox-ext-oracle
```

4、把当前用户组添加到vboxusers里面

```shell
sudo usermod -G vboxusers -a 用户名
```

来源：https://blog.csdn.net/u014025444/article/details/94151354



## 2.安装Windows 7

- 32位不支持UEFI
- 安装增强工具——设备菜单下
- 开启Aero效果：设置->显示->启用3D，显存设置成128MB





