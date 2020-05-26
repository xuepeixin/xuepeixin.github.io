---
title:      数学基础——傅里叶变换
date:       2020-04-02
author:     XPX
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - 高等数学
---

## 傅里叶级数
首先我们先介绍最简单的余弦函数,可以看见随着余弦函数频率的增加，函数的周期变得更短。
<center>
    <img
    src="https://xpx-picbed.oss-cn-beijing.aliyuncs.com/blog/2020/04/rasterization-frequency.png">
</center>

根据傅里叶级数，对于一个方波信号，是可以用很多个不同频率的余弦信号近似。从下图可以看到，随着频率更高的余弦函数加入，由余弦函数组成的信号就和方波更加接近。
<center>
    <img
    src="https://xpx-picbed.oss-cn-beijing.aliyuncs.com/blog/2020/04/rasterization-fourier1.gif">
</center>
对于任意的函数都可以展开成下面形式的三角级数:

$$
f(t)=\frac{a_0}{2}+\sum_{n=1}^{\infty}[a_n\cos(n\omega t)+b_n\sin(n\omega t)]  \\
a_0=\frac{2}{T}\int_{t_0}^{t_0+T}f(t)dt \\
a_n = \frac{2}{T}\int_{t_0}^{t_0+T}f(t)\cos(n\omega t)dt \\
b_n = \frac{2}{T}\int_{t_0}^{t_0+T}f(t)\sin(n\omega t)dt  
$$

以上就是三角形式的傅里叶级数.详细的推导可以参照[ElPsyCongree的知乎专栏](https://zhuanlan.zhihu.com/p/41455378)中傅里叶级数部分.

## 连续傅里叶变换

#### 欧拉公式
欧拉公式是复分析领域的公式，它将三角函数与复指数函数关联起来.其基本公式为:

$$e^{i\theta}=\cos \theta+i\sin \theta$$

其中$e$是自然对数的底数，$i$ 是虚数单位，而 $\cos$ 和 $\sin$ 则是余弦、正弦对应的三角函数，参数 $\theta$ 则以弧度为单位。

经过简单的变形之后可以得到:

$$
\cos \theta = \frac{e^{i\theta}+e^{-i\theta}}{2}
$$

$$
\sin \theta = -i\frac{e^{i\theta}-e^{-i\theta}}{2}
$$

#### 指数形式的傅里叶级数
$\cos \theta$和$\sin \theta$代入傅里叶级数之后可以得到:

$$
f(t) = \frac{a_0}{2}+\sum_{n=1}^{\infty}(a_n\frac{e^{in\omega t}+e^{-in\omega t}}{2} - ib_n\frac{e^{in\omega t}-e^{-in\omega t}}{2})\\=
\frac{a_0}{2}+\sum_{n=1}^{\infty}(\frac{a_n-ib_n}{2}e^{in\omega t}+\frac{a_n+ib_n}{2}e^{-in\omega t})\tag{1}
$$

再将$a_0,a_n,b_n$的公式代入得到:


$$
\begin{aligned}
\frac{a_n-ib_n}{2}&=\frac{1}{T}[\int^{t_0+T}_{t_0}f(t)\cos(n\omega t)dt - i \int^{t_0+T}_{t_0}f(t)\sin(n\omega t)dt]\\
&=\frac{1}{T}\int^{t_0+T}_{t_0}f(t)[\cos(n\omega t)- i\sin(n\omega t)]dt \\
&=\frac{1}{T}\int^{t_0+T}_{t_0}f(t)[\frac{e^{in\omega t}+e^{-in\omega t}}{2}-i\cdot (-i)\cdot \frac{e^{in\omega t}-e^{-in\omega t}}{2}]dt\\
&=\frac{1}{T}\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt
\end{aligned} \tag{2}
$$

同理可以得到

$$\frac{a_n+ib_n}{2}=\frac{1}{T}\int^{t_0+T}_{t_0}f(t)e^{in\omega t}dt\tag{3}$$

将公式(2)(3)代入(1)得到:

$$
\begin{aligned}
f(t) &= \frac{1}{T} \int^{t_0+T}_{t_0}f(t)dt + \frac{1}{T}\sum_{n=1}^{\infty}[\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt \cdot e^{in\omega t}+\int^{t_0+T}_{t_0}f(t)e^{in\omega t}dt \cdot e^{-in\omega t}]\\
&=\frac{1}{T} \int^{t_0+T}_{t_0}f(t)dt + \frac{1}{T}\sum_{n=1}^{\infty}\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt \cdot e^{in\omega t}+\frac{1}{T}\sum_{n=-\infty}^{0}\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt \cdot e^{in\omega t}\\
&=\frac{1}{T}\sum_{n=-\infty}^{\infty}\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt \cdot e^{in\omega t} \\
&=\frac{1}{T}\sum_{n=-\infty}^{\infty}\int^{\frac{T}{2}}_{-\frac{T}{2}}f(t)e^{-in\omega t}dt \cdot e^{in\omega t}
\end{aligned}\tag{4}
$$

令

$$F(n\omega)=\int^{t_0+T}_{t_0}f(t)e^{-in\omega t}dt$$

则有:

$$
f(t)=\frac{1}{T}\sum_{n=-\infty}^{\infty}F(nw)e^{in\omega t}
$$


我们令$w_n=n\omega$,则有:

$$F(\omega_n)=\int^{t_0+T}_{t_0}f(t)e^{-i\omega_n t}dt $$

由于$\omega=\frac{2\pi}{T}$:

$$
\begin{aligned}
f(t)&=\frac{1}{T}\sum_{n=-\infty}^{\infty}F(w_n)e^{i\omega_n t}\\
&=\frac{\omega}{2\pi}\sum_{n=-\infty}^{\infty}F(w_n)e^{i\omega_n t}\\
&=\frac{1}{2\pi}\sum_{\omega_n=-\infty}^{\infty}F(w_n)e^{i\omega_n t}\\
&=\frac{1}{2\pi}\int_{-\infty}^{\infty}F(w_n)e^{i\omega_n t}d\omega_n
\end{aligned}
$$

最终可以得到傅里叶变换对:

$$F(\omega)=\int^{t_0+T}_{t_0}f(t)e^{-i\omega t}dt \tag{5}$$

$$f(t)=\frac{1}{2\pi}\int_{-\infty}^{\infty}F(\omega)e^{i\omega t}d\omega\tag{6}$$

## 离散傅里叶变换

离散傅里叶变换是傅里叶变换在时域和频域上都呈离散的形式，将信号的时域采样变换为其DTFT的频域采样。
在形式上，变换两端（时域和频域上）的序列是有限长的，而实际上这两组序列都应当被认为是离散周期信号的主值序列。即使对有限长的离散信号作DFT，也应当将其看作其周期延拓的变换。

**DFT就是先将信号在时域离散化，求其连续傅里叶变换后，再在频域离散化的结果。**

在获得离散傅里叶变换之前需要先对连续函数采样,因此,在介绍离散傅里叶变换之前,我们先讲一下采样定理.

#### 采样定理

采样定理是美国电信工程师H.奈奎斯特在1928年提出的，在数字信号处理领域中，采样定理是连续时间信号（通常称为“模拟信号”）和离散时间信号（通常称为“数字信号”）之间的基本桥梁。

在进行模拟/数字信号的转换过程中，当采样频率$f_{s.max}$大于信号中最高频率$f_{max}$的2倍时($f_{s.max} > 2f_{max}$)，采样之后的数字信号完整地保留了原始信号中的信息，一般实际应用中保证采样频率为信号最高频率的2.56～4倍；采样定理又称奈奎斯特定理。

#### 离散时间傅里叶变换(Discrete-time Fourier Transform,DTFT)
假设将(0,L)区间的f(t)通过时域采样的方式离散化,得到有限长的离散信号. 我们设定采样周期为 $T$,则在该时域的采样点数为$N=\frac{L}{T}$,*这边由于符号冲突,我们用L表示之前的时域T,用现在的T表示采样的周期*

$$
f_{discrete}(t)=f(t)\sum_{n=0}^{N-1}\delta(t-nT)=\sum_{n=0}^{N-1}f(nT)\delta(t-nT)
$$


我们对$f_{discrete}(t)$进行傅里叶变换,根据傅里叶变换的时移特性,可以得到:

$$
\hat f(\omega)=\sum_{n=0}^{N-1}f(nT)\mathcal{F}(\delta(t-nT))=\sum_{n=0}^{N-1}f(nT)e^{-in\omega T}
$$

$\hat f(\omega)$就是在时域采样后的连续傅里叶变换,也就是离散时间傅里叶变换(Discrete-time Fourier Transform,DTFT),它在频域上还是连续的.

 当对时域采样区间为$(-\infty,\infty)$时，有

$$
\hat f(\omega)=\sum_{n=-\infty}^{\infty}f(nT)e^{-in\omega T}
$$

对于采样后的信号来说，我们有时候并不在意它原始的采样率。因此我们令$f[n]=f(nT)$,$\hat f(\omega) = \hat f(\omega T)$,得到

$$
\hat f(\omega)=\sum_{n=-\infty}^{\infty}f[n]e^{-in\omega}
$$
#### 离散傅里叶变换(Discrete Fourier Transform)

本部分时将频域上连续的信号转化成离散信号。与对时域信号的处理类似，假设频域信号是带限的，再经过离散化，即可得到有限长离散信号。**对频域的均匀采样实际上是对时域的周期延拓,其周期为频域采样周期的导数.**

根据我们上上部分提到的采样定理,时域采样若要能完全重建原信号，频域信号$\hat f(\omega)$应当带限于$(0,\frac{1}{2T})$.即频域的信号不能大于$\frac{1}{2T}$.

由于时域信号受限于$[0,L]$,根据采样定理以及时频对偶的关系，频域的采样间隔应为$\frac{1}{L}$.采样数为:

$$\frac{1/T}{1/L}=N$$

即频域采样的点数和时域采样都为N.*如果频域采样点数小于时域点数,即实际的频域采样间隔$f>\frac{1}{L}$.根据频域采样时对时域周期延拓的思想,时域上将会以周期$\frac{1}{f}$对信号进行延拓.但由于$\frac{1}{f} < L$,因此进行频域采样后的信号重新恢复之后会出现信号混叠,也就是走样(aliasing)的现象*

因为时域上采样时间为T,所以在频域上最高采样频率为$\frac{2\pi}{T}$,对$(0,\frac{2\pi}{T})$均匀采样得到
$\{\omega_k=\frac{2\pi k}{NT}\}_{0\le k \lt N}$ 

因此对$\hat f(\omega)$采样之后得到$\hat f[k]$

$$
\begin{aligned}
\hat f[k]&=\hat f(\omega_k) = \sum_{n=0}^{N-1}f(nT)e^{-in\omega_k T}\\
&=  \sum_{n=0}^{N-1}f(nT)e^{-i\frac{2\pi}{N} kn}
\end{aligned}
$$

$\hat f[k]$即为$f(t)的离散傅里叶变换(DFT).

### 连续时间傅里叶变换与拉普拉斯变换

对于周期性连续信号，连续时间傅里叶变换的公式是：

$$
\int^{\infty}_{-\infty}f(t)e^{-i\omega t}dt
$$

傅里叶变换要求时域信号绝对可积，即

$$
\int^{\infty}_{-\infty}\lvert f(t)\rvert dt \lt \infty
$$

为了让不符合这个条件的信号，也能变换到频率域，我们给f(t)乘上一个指数函数$e ^ {-\sigma t}$, $\sigma$为（满足收敛域的）任意实数。

可以发现$f(t)e^{-\sigma t}$这个函数就满足了绝对可积地条件，即$\int^{\infty}_{-\infty}\lvert f(t)e^{-\sigma t}\rvert dt \lt \infty$。

于是这个新函数的傅立叶变换就是：$\int^{\infty}_{-\infty}f(t)e^{-(\sigma + i\omega)t}dt$

由于$\sigma + i\omega$是一个复数，我们用新变量$s$表示。

于是得到拉普拉斯变换的公式：$\int^{\infty}_{-\infty}f(t)e^{-st}dt$

拉普拉斯变换解决了不满足绝对可积条件的连续信号，变换到频率域的问题，同时也对“频率”的定义进行了扩充。所以拉普拉斯变换与连续时间傅里叶变换的关系是：拉普拉斯变换将频率从实数推广为复数，因而傅里叶变换变成了拉普拉斯变换的一个特例。**当s为纯虚数时，x(t)的拉普拉斯变换，即为x(t)的傅里叶变换。**


### 离散时间傅里叶变换（DTFT）与Z变换的关系
DTFT公式为
$$
\hat f(\omega)=\sum_{n=-\infty}^{\infty}f[n]e^{-in\omega}
$$

同样的，DTFT需要满足绝对可和的条件，即$\sum_{-\infty}^{\infty}\lvert x[n]\rvert \lt \infty$

为了让不满足绝对可和条件的函数f[n]，也能变换到频率域，我们乘一个指数函数$a^{-n}$，a为（满足收敛域的）任意实数。则函数$f[n]a^{-n}$的DTFT为：$\sum_{-\infty}^{\infty}f[n](a\cdot e^{i\omega})^{-n}$。

$a\cdot e^{i\omega}$是一个极坐标形式的复数，我们把这个复数定义为离散信号的复频率，记为z。得到Z变换公式：

$$
\sum_{-\infty}^{\infty}f[n]z^{-n}
$$

> 关于这里为什么对f[n]乘以$a^{-n}$而不是像拉氏变换中乘以$e^{-\sigma a}$，主要是由离散序列的DTFT的周期性决定的。如果对离散序列进行拉氏变换，将$\omega$映射到虚轴上，则得到的变换函数是在虚轴方向上周期变化的函数，这样就没有充分利用DTFT的周期性。而Z变换令$z=a\cdot e^{i\omega}$，则当a=1，即$z=e^{i\omega}$时，随着$\omega$从$-\infty$向$\infty$变化，z在复平面中的单位圆上以$2\pi$为周期变化，如此恰能充分利用DTFT的周期性进一步简化我们的计算。

Z变换解决了不满足绝对可和条件的离散信号，变换到频率域的问题，同时也同样对“频率”的定义进行了扩充。所以Z变换与离散时间傅里叶变换（DTFT）的关系是：Z变换将频率从实数推广为复数，因而DTFT变成了Z变换的一个特例。当z的模为1时，$f[n]$的Z变换即为$f[n]$的DTFT






参考资料: 
- [ElPsyCongree的知乎专栏](https://zhuanlan.zhihu.com/p/41455378)
- [离散傅里叶变换](https://zh.wikipedia.org/wiki/%E7%A6%BB%E6%95%A3%E5%82%85%E9%87%8C%E5%8F%B6%E5%8F%98%E6%8D%A2)
- [傅里叶变换、拉普拉斯变换、Z 变换的联系是什么？为什么要进行这些变换？](https://www.zhihu.com/question/22085329)


*在ElPsyCongree的专栏关于傅里叶级数的介绍中作者讲了一段话：*
>我们眼中的世界就像皮影戏的大幕布，幕布的后面有无数的齿轮，大齿轮带动小齿轮，小齿轮再带动更小的。在最外面的小齿轮上有一个小人——那就是我们自己。我们只看到这个小人毫无规律的在幕布前表演，却无法预测他下一步会去哪。而幕布后面的齿轮却永远一直那样不停的旋转，永不停歇。这样说来有些宿命论的感觉。说实话，这种对人生的描绘是我一个朋友在我们都是高中生的时候感叹的，当时想想似懂非懂，直到有一天我学到了傅里叶级数……

*有的人一生都在小小的齿轮上周而复始的旋转,而学习的意义就在于能够让自己看到更大的齿轮的轨迹.*
