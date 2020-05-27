---
title:      排版工具
date:       2020-04-03
author:     XPX
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - 公式排版
---

## 图片转Latex公式

发现一个特别好用的图片转Latex软件，叫做Mathpix。

官网地址：[https://mathpix.com](https://mathpix.com)

安装好之后打开，选择要转换的图片截图，识别粗来的Latex公式就在下面第一行。
<center>
    <img
    src="https://xpx-picbed.oss-cn-beijing.aliyuncs.com/blog/2020/04/typesetting-mathpix.png">
</center>

如果要复制MathML的话，选择Data栏，第二行就是了。

<center>
    <img
    src="https://xpx-picbed.oss-cn-beijing.aliyuncs.com/blog/2020/04/typesetting-mathpix1.png">
</center>

## 在线数学编辑器

[www.mathcha.io](https://www.mathcha.io/)

## 配置博客中的MathJax引擎
搭建博客后发现网页的Markdown不支持数学公式编辑。在网上搜了一下之后发现可以使用MathJax实现公式的渲染。

MathJax是一个开源的 web 数学公式渲染器，由 JS 编写而成。

添加MathJax引擎只需要将引入CDN的script语句添加到head标签内部。
```
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
        }
    });
</script>
```

## 常用的MathJax语法
可以查阅的网址:
1. https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
2. https://colobu.com/2014/08/17/MathJax-quick-reference/
3. https://www.hegongshan.com/2018/07/16/mathjax-tutorial/