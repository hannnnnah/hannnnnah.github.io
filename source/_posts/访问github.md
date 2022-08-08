---
title: 访问github
author: hannah
tags: github
categories: 工具
date: 2022-08-06 18:51:14
---

参考文档：[国内打不开GitHub网站100%解决办法](https://baijiahao.baidu.com/s?id=1734352321218839406&wfr=spider&for=pc)

最近国内访问github.com经常打不开，无法访问，解决Github打不开问题，我使用的是参考文档中的终极方法：

## windows
打开hosts文件（C:\Windows\System32\drivers\etc）,末尾放入以下两个 IP 地址：
```
# GitHub Start
140.82.114.4 github.com
199.232.69.194 github.global.ssl.fastly.net
# GitHub End
```
再在 CMD 命令行中执行下面语句 来刷新 DNS，重启浏览器之后就能进入Github 网址。
```
ipconfig/flushdns
```
## mac
打开finder，点击顶部菜单栏的【前往】，再点击【前往文件夹】，输入/etc/hosts前往，找到hosts文件，将它拖拽到桌面上，

右键桌面上的hosts文件，滑动到【打开方式】，再点击【文本编辑】，末尾放入以下两个 IP 地址：
```
# GitHub Start
140.82.114.4 github.com
199.232.69.194 github.global.ssl.fastly.net
# GitHub End
```
修改完按command + s保存，将桌面的hosts文件拖拽回/etc/hosts中，点击【认证】，再点击【替换】，再输入开机密码即可。

再在 CMD 命令行中执行下面语句，并输入密码来刷新 DNS，重启浏览器之后就能进入Github 网址。
```
sudo killall -HUP mDNSResponder && echo macOS DNS Cache Reset
```

