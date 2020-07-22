---
title:     Linux Tool
date:       2020-07-22
author:     XPX
catalog: true
tags:
    - 实用工具
---

## Linux下实用工具

[在Ubuntu环境下实现插入鼠标自动关闭触摸板](https://ywnz.com/linuxjc/1920.html)

```bash
sudo add-apt-repository ppa:atareao/atareao

sudo apt update

sudo apt install touchpad-indicator
```


[实现ubuntu18.04 插上外部鼠标禁用触摸板的功能 ](https://my.oschina.net/lvhongqing/blog/3155060)
命令行输入dconf-editor

查找touchpad

进入 send-events

将最下面的custom value改为

disabled-on-external-mouse