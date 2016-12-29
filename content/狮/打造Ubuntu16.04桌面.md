---
date: 2016-12-15T13:53:45+08:00
description: ""
tags:
- Linux
- Ubuntu
- dpkg
- apt-get
title: 打造Ubuntu16.04桌面
topics:
- Linux
- Ubuntu
- dpkg
- apt-get
---

### 1. 初始配置
#### 1.1 Ubuntu 16.04新特性
* 默认禁用dash在线搜索

* 使用GNOME Software代替Ubuntu软件中心

* 自定义Unity所处位置

* apt命令升级：apt可代替apt-get

* 支持ZFS文件系统

* 软件更新：Linux4.4 LTS、LibreOffice5.1、Python3.5、Docket1.10


#### 1.2 设置root密码

	sudo passwd root

#### 1.3 切换到root用户

	su

或

	sudo -i

#### 1.4 自定义Unity所处位置

	gsettings set com.canonical.Unity.Launcher launcher-position Bottom|Left

#### 1.5 查看Ubuntu版本

	lsb_release -a

#### 1.6 查看内核版本

	uname -a

#### 1.7 查看硬件驱动

	lspci

#### 1.8 打开终端快捷键

	Ctrl+Alt+T

#### 1.9 切换控制台tty1-tt6

	Ctrl+Alt+F1~F6

回到桌面

	Ctrl+Alt+F7


### 2. 常用桌面软件安装

#### 2.1 安装VMware tools (root用户执行)

VMware Workstation ——> 虚拟机 ——> 安装VMware Tools
挂载VMware Tools安装光盘

	su

	mount /dev/sr0 /mnt

把VMware Tools安装文件拷贝至root主目录

	cp /mnt/VMwareTools-10.0.10-4301679.tar.gz .

解压缩VMmareTools安装文件

	tar xvf VMwareTools-10.0.10-4301679.tar.gz

解压完毕后进入vmware-tools-distrib目录

	cd vmware-tools-distrib

运行vmware-install.pl

	./vmware-install.pl

DO you still want to proceed with this legacy installer?[no]

	输入 yes ，回车

接下来一路回车，直至安装完成。重启系统后，即可自适应窗口、拖放文件等

#### 2.2 删除Amazon链接

	sudo apt-get remove unity-webapps-common  

#### 2.3 卸载Libreoffice

	sudo apt-get remove libreoffice-common

#### 2.4 安装 Unity Tweak Tool

	sudo apt-get install unity-tweak-tool

查看unity-tweak-tool安装了哪些文件

	dpkg -L unity-tweak-tool

启动Unity Tweak Tool

	/usr/bin/unity-tweak-tool

#### 2.5 安装[Numix](https://www.numixproject.org/)主题和图标

添加Numix源

    sudo apt-add-repository ppa:numix/ppa
    sudo apt-get update

安装GTK主题

	sudo apt-get install numix-gtk-theme

安装Numix图标

    sudo apt-get install numix-icon-theme-circle

在Unity-tweak-tool中启用Numix daily主题和Numix-circle图标
![](/media/Ubuntu_2_5_01.png)

#### 2.6 安装指示器

大小写指示灯和触摸板开关

    sudo add-apt-repository ppa:tsbarnes/indicator-keylock
    sudo add-apt-repository ppa:atareao/atareao
    sudo apt-get update
    sudo apt-get install indicator-keylock
    sudo apt-get install touchpad-indicator

#### 2.7 安装系统监测工具Syspeek
![](/media/Ubuntu_2_7_01.png)

	sudo add-apt-repository ppa:nilarimogard/webupd8    
	sudo apt-get update    
	sudo apt-get install syspeek

#### 2.8 安装经典菜单插件
![](/media/Ubuntu_2_8_01.png)

	sudo add-apt-repository ppa:diesch/testing  
	sudo apt-get update  
	sudo apt-get install classicmenu-indicator

#### 2.9 安装Google Chrome浏览器

	sudo apt-get install google-chrome-stable

解决软件包依赖关系

	sudo apt-get -f install

#### 2.10 安装Adobe Flash Player
##### 2.10.1 在Firefox中打开 https://get.adobe.com/flashplayer/?loc=cn
已自动识别出：`Linux 64-bit, 简体中文, Firefox`，选择版本为

	.tar.gz 适用于 Linux

立即下载，然后提取flash_player_npapi_linux.x86_64.tar.gz

按照readme.txt方法

	sudo cp libflashplayer.so /usr/lib/firefox-addons/plugins/ -v
	sudo cp -r usr/* /usr

##### 2.10.2 在Chrome中打开 https://get.adobe.com/cn/flashplayer/otherversions/

选择操作系统为：

	Linux(64-bit)

选择版本为

	xxx for Linux 64-bit(.tar.gz)- PPAPI

立即下载，然后提取flash_player_ppapi_linux.x86_64.tar.gz

按照readme.txt方法

	sudo cp ~/下载/flash_player_ppapi_linux.x86_64/* /usr/lib/adobe-flashplugin/ -rvf

如果`/usr/lib/adobe-flashplugin`目录不存在，可以自己创建一个再进行上一步，也起作用

	sudo mkdir /usr/lib/adobe-flashplugin

#### 2.11 配置[老D的Google Hosts](https://laod.cn/hosts/2016-google-hosts.html)
下载老D最新的Google hosts文件，添加以下部分到 `/etc/hosts`

	# Modified hosts start

	......

	# Modified hosts end

以root用户编辑 `/etc/hosts`

	sudo gedit /etc/hosts

重启网络使hosts本地解析生效

	sudo systemctl restart NetworkManager

#### 2.12 添加Ubuntu Kylin的apt源,方便安装常用的桌面软件

	sudo vim /etc/apt/sources.list.d/ubuntukylin.list

	deb http://archive.ubuntukylin.com:10006/ubuntukylin trusty main

	sudo apt-get update

#### 2.13 安装搜狗输入法

	sudo apt-get install sogoupinyin

#### 2.14 安装[网易云音乐](http://music.163.com/)

	sudo apt-get install netease-cloud-music

或者，下载 [ubuntu16.04 (64位) 版本的云音乐](http://music.163.com/#/download)并安装

	sudo dpkg -i netease-cloud-music_1.0.0_amd64_ubuntu16.04.deb

解决软件包依赖关系

	sudo　apt-get -f install

#### 2.15 安装[有道词典](http://cidian.youdao.com/index-linux.html)
![](/media/Ubuntu_2_15_01.png)

参考：[Ubuntu 16.04安装有道词典](http://www.linuxdiyf.com/linux/20622.html)

下载Ubuntu 64位的deb包：[youdao-dict_1.1.0-0-ubuntu_amd64.deb](http://cidian.youdao.com/index-linux.html)

创建youdao-dict目录，把该deb包解压到youdao-dict目录：

	sudo dpkg -X youdao-dict_1.1.0-0-ubuntu_amd64.deb  youdao-dict

解压deb包中的control信息（包的依赖就写在这个文件里面）：

	sudo dpkg -e youdao-dict_1.1.0-0-ubuntu_amd64.deb youdao-dict/DEBIAN

编辑control文件，删除Depends行尾的gstreamer0.10-plugins-ugly。

	sudo gedit youdao-dict/DEBIAN/control

重新打包：

	sudo dpkg-deb -b youdao-dict youdaobuild.deb

安装重新打包的安装包

	sudo dpkg -i youdaobuild.deb

安装完毕即可使用，屏幕取词和滑词翻译均能正常使用，喜大普奔！当切换到其他窗口有道词典会自动最小化到右上角任务栏

使用apt-get和dpkg安装deb包测试多次都安装失败，原因正是因为:

	未安装软件包 gstreamer0.10-plugins-ugly

#### 2.16 安装[WPS Office](http://community.wps.cn/download/)

下载 wps-office_10.1.0.5672~a21_amd64.deb 并安装

	sudo dpkg -i wps-office_10.1.0.5672~a21_amd64.deb

打开wps会提示缺失symbol、wingdings、wingdings 2、wingdings 3、webding、mtextra 6个字体，在Windows上C:\Windows\Fonts搜索拷贝这6个字体到Ubuntu的usr/share/fonts/下即可。

百度云分享链接: http://pan.baidu.com/s/1pL6ONHL 密码: 2stm

#### 2.17 安装Shadowsocks

	sudo add-apt-repository ppa:hzwhuang/ss-qt5
  	sudo apt-get update
	sudo apt-get install shadowsocks-qt5

#### 2.18 安装Irssi

	sudo apt-get install screen
	sudo apt-get install irssi

#### 2.19 安装迅雷的替代者Xware-desktop

![](/media/Ubuntu_2_19_01.png)

在百度网盘中下载最新的Xware-desktop：http://pan.baidu.com/s/1qWHMlK4

	sudo chmod +x xware-desktop_0.11.20140723_amd64.deb
	sudo dpkg -i xware-desktop_0.11.20140723_amd64.deb
	sudo apt-get install -f

#### 2.20 安装[Vivaldi浏览器](https://vivaldi.com)

![](/media/Ubuntu_2_20_01.png)

下载[Vivaldi的deb安装包](https://vivaldi.com/download/)

	sudo dpkg -i vivaldi-stable_1.6.689.46-1_amd64.deb

#### 2.21 自定义截图快捷键
系统设置——>键盘——>快捷键——>截图

![](/media/Ubuntu_2_21_01.png)

### 3. 常用工具软件安装
#### 3.1 安装Albert

![](/media/Ubuntu_3_1_01.gif)

安装方法参考[Albert WIki](https://github.com/ManuelSchneid3r/albert/wiki)的《How to install albert》

	sudo add-apt-repository ppa:nilarimogard/webupd8
	sudo apt-get update
	sudo apt-get install albert

#### 3.2  安装Vim

	sudo apt-get install vim

#### 3.3 安装Filezilla

	sudo apt-get install filezilla

#### 3.4 安装[Git](https://git-scm.com/)

	sudo apt-get install git

#### 3.5 安装[Sublime Text 3](www.sublimetext.com/)

	sudo add-apt-repository ppa:webupd8team/sublime-text-3    
	sudo apt-get update    
	sudo apt-get install sublime-text

如果修改`Preferences.sublime-settings - User`后提示没有权限保存

	 sudo chmode o+rwx ~/.config/sublime-text-3/ -R

关于Sublime Text 3在Ubuntu下无法输入中文的问题，尝试了网上很多方法都没有解决

#### 3.6 安装[Notepadqq](http://notepadqq.altervista.org/wp/download/)
Notepadqq功能近似于Windows下的Notepad++

	sudo add-apt-repository ppa:notepadqq-team/notepadqq
	sudo apt-get update
	sudo apt-get install notepadqq

#### 3.7 安装[Atom](https://atom.io/)
安装过程因为下载速度奇慢，建议单独开一个Terminal,耐心等待

	sudo add-apt-repository ppa:webupd8team/atom
	sudo apt-get update
	sudo apt-get install atom

#### 3.8 安装Hugo(由Go语言实现的静态网站生成器)

	sudo apt-get install hugo

#### 3.9 安装[VMware Workstation](https://my.vmware.com/cn/web/vmware/login)
下载[VMware Workstation Pro for Linux](https://my.vmware.com/cn/group/vmware/details?downloadGroup=WKST-1252-LX&productId=524&rPId=13365)
安装方法参考官方文档：http://pubs.vmware.com/workstation-12/index.jsp#com.vmware.ws.using.doc/GUID-1F5B1F14-A586-4A56-83FA-2E7D8333D5CA.html

	su root
	sh VMware-Workstation-Full-12.5.2-4638234.x86_64.bundle

稍等弹出图形化的安装界面，与windows上安装相似，一路下一步至安装完毕。
