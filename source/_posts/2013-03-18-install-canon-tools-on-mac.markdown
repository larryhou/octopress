---
layout: post
title: 在Mac系统安装佳能软件
date: 2013-03-18 11:40
comments: true
categories: 
---
[1]: http://support-cn.canon-asia.com "佳能驱动与软件官网"

如果你的安装光盘丢失了，怎么才能在Mac系统安装佳能工具软件呢？你可能已经在[官网][1]搜查过了，但是你会发现找不到对应的安装软件！是这样的，官网只有升级软件下载，那这岂不是很尴尬：升级软件安装的前提是先安装原版软件，但是现在又没有安装盘，死循环了！！其实这些升级软件另有玄机，里面都有安装包的，但是如果要直接运行，你可能要麻烦一下。<!--more-->

首先，去[官网][1]下载系统版本对应的最新升级包，然后逐个测试一下三种方法，直至安装成功为止；如果，尝试了三种方式还是不能安装，那么表示本博客太旧了你需要另外google一下，或者联系作者（*larryhou@foxmail.com*）更新博客！

## DPP 3.12.52
* 从官网下载dpp3.12.52x.dmg
* 双击装载镜像，复制dpp3.12.52x_updater.app到任意其他目录（比如：下载）
* 在dpp3.12.52x_updater.app上鼠标右键，点击“显示包内容/Show Package Contents”
* 进入Contents/Resources/目录，删除Info.datx文件
* 返回上一级目录Contents，进入MacOS目录，双击运行OFICore

## 方法（一）

{% blockquote %}
* Files you downloaded are compressed as “.zip” or “.gz” files
* Double click on the file and it will expand to the disk image file extension “.dmg”
* Click on image file EU211.4x-updater.dmg, it will mount it as disk mount
* Transfer (copy) content where you want (exmp: desktop)
* After copying unmount dmg image
* Click on desktop copy: ‘Show Package Contents’
* Navigate to ./Contents/Ressources/ and delete the Info.datx file
* Close window
* Run Installation
{% endblockquote %}

## 方法（二）
{% blockquote %}
* Files you downloaded are compressed as “.zip” or “.gz” files
* Double click on the file and it will expand to the disk image file extension “.dmg”
* Click on that image file, it will mount it as disk
* We should copy (extract) UpdateInstaller to our disk
* Eject disk image
* We will modify UpdateInstaller
* Click on UpdateInstaller and go to “Show Package Contents”
* It will open new window with Contents
* Navigate to Contents/Resources and find the SDI.bundle file.
* Click on the SDI.bundle and ‘Show Package Contents’ again
* Now navigate to Contents/Resources and locate a file called update.plist
* Delete update.plist file
* Close opened windows and run UpdateInstaller it should install now!
{% endblockquote %}

## 方法（三）
{% blockquote %}
* Files you downloaded are compressed as “.zip” or “.gz” files
* Double click on the file and it will expand to the disk image file extension “.dmg”
* Click on that image file, it will mount it as disk
* We should copy (extract) UpdateInstaller to our disk
* Eject disk image
* We will modify UpdateInstaller
* Click on UpdateInstaller and go to “Show Package Contents”
* It will open new window with Contents
* Now navigate to Resources and locate a file called update.plist
* Delete update.plist file
* Close opened windows and run UpdateInstaller it should install now!
{% endblockquote %}