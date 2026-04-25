---
title: "平统总结笔记"
slug: "平统总结笔记"
date: 2021-01-30T23:18:05
categories:
  - "课程笔记"
math: true
---

<a href="https://www.lightforever.cn/wp-content/uploads/2021/01/平统.pdf" rel="noreferrer noopener" target="_blank">Download PDF</a>

# 平统

> hzs 整理

 

热波长

$$\lambda_{T} \equiv \frac{h}{\left(2 \pi m k_{B} T\right)^{1 / 2}}$$

弱简并条件

$$n\lambda_T^3\ll 1$$

什么是BEC？水滴凝聚是不是BEC?

固体热容的爱因斯坦模型和德拜模型有什么区别？

玻色气体的压强小于经典气体，费米气体的压强大于经典气体，这是由于量子效应导致的统计关联

 

该笔记编排采用mzs讲义的顺序，内容基本上为mzs与lc交集

## 热力学部分

 

## 统计部分

### 0.系综

大量全同系统的集合

#### (1)微正则系综

以等概率原理为基础，正则系综和巨正则系综均是假设系统与一大系统接触再利用正则系综导出。

#### (2)正则系综

$$Z=\sum_{S} e^{-\beta E_{S}}$$ $$U=\bar{E}=\frac{1}{Z} \sum_{S} E_{s} e^{-\beta E_{S}}=-\frac{\partial}{\partial \beta} \log Z$$ $$Y=\frac{1}{Z} \sum_{S} \frac{\partial E_{S}}{\partial y} e^{-\beta E_{S}}=-\frac{1}{\beta} \frac{\partial}{\partial y} \log Z$$ $$p=\frac{1}{\beta} \frac{\partial}{\partial V} \log Z$$ $$S=k_{B}\left(\log Z-\beta \frac{\partial \log Z}{\partial \beta}\right)$$ $$F=-k_{B} T \log Z$$

#### (3)巨正则系综

$$\begin{aligned} \bar{N} &=-\frac{\partial}{\partial \alpha} \log \Xi \\ U &=-\frac{\partial}{\partial \beta} \log \Xi \\ Y &=-\frac{1}{\beta} \frac{\partial}{\partial y} \log \Xi \\ S &=k_{B}\left(\log \Xi-\alpha \frac{\partial \log \Xi}{\partial \alpha}-\beta \frac{\partial \log \Xi}{\partial \beta}\right) \end{aligned}$$ $$J=-k_{B} T \log \Xi$$

#### (4)涨落

无粒子交换时，涨落概率

$$W \propto \exp \left(-\frac{\Delta S \Delta T-\Delta p \Delta V}{2 k_{B} T}\right)$$

假设某两个量不变，再利用热力学公式导出W的表达式，应为两个高斯分布的乘积

 

### 1.三种分布(\*\*\*)

麦克斯韦-玻尔兹曼分布(M-B)

$$\Xi_{MB}=\prod_{s=1} e^{\omega_{s} e^{-\left(\alpha+\beta \epsilon_{s}\right)}}$$ $$\bar{n}_{s}^{(M B)}=\omega_{s} e^{-\alpha-\beta \epsilon_{g}}$$

玻色-爱因斯坦分布(B-E)

$$\Xi_{BE}=\prod_{s}\left\[1 - e^{-\left(\alpha+\beta \epsilon_{s}\right)}\right\]^{- \omega_{s}}$$ $$\bar{n}_{s}^{( B E)}=\frac{\omega_{s}}{e^{\alpha+\beta \epsilon_{s}} - 1}$$

费米-狄拉克分布(F-D)

$$\Xi_{FD}=\prod_{s}\left\[1 + e^{-\left(\alpha+\beta \epsilon_{s}\right)}\right\]^{ \omega_{s}}$$ $$\bar{n}_{s}^{(F D)}=\frac{\omega_{s}}{e^{\alpha+\beta \epsilon_{s}} + 1}$$

### 2.理想玻色气体

态密度(自旋不为0时需要乘(2s+1))

$$g(\varepsilon)=\frac{2 \pi V}{h^{3}}(2 m)^{3 / 2} \varepsilon^{1 / 2}$$

因此配分函数

$$\log \Xi=-\frac{2 \pi V}{h^{3}}\left(2 m k_{B} T\right)^{3 / 2} \int_{0}^{\infty} \ln \left(1-e^{-\alpha-x}\right) x^{1 / 2} d x$$

#### (1)弱简并下的计算

- 对数项内展开

$$\log \left(1-e^{-\alpha-x}\right)=-\sum_{j=1}^{\infty} \frac{e^{-j(\alpha+x)}}{j}$$

逐项积分

$$\log \Xi=\frac{V}{h^{3}}\left(2 \pi m k_{B} T\right)^{3 / 2} \sum_{j=1}^{\infty} \frac{e^{-j \alpha}}{j^{5 / 2}} \equiv \frac{V}{\lambda_{T}^{3}} g_{5 / 2}(z)$$

其中

$$g_{s}(z)=\sum_{j=1}^{\infty} \frac{z^{j}}{j^{s}}\quad z=e^{-\alpha}$$

代入热力学量的公式可得

$$\begin{aligned} \bar{N} &=\frac{V}{\lambda_{T}^{3}} g_{3 / 2}(z) \\ U &=\frac{3}{2} k_{B} T \frac{V}{\lambda_{T}^{3}} g_{5 / 2}(z) \\ p V &=k_{B} T \frac{V}{\lambda_{T}^{3}} g_{5 / 2}(z)=\frac{2}{3} U \\ S &=k_{B}\left(\frac{5}{2} \log \Xi+\bar{N} \alpha\right) \end{aligned}$$

第三式比上第一式可以得到

$$\frac{p V}{\bar{N} k_{B} T}=\frac{g_{5 / 2}(z)}{g_{3 / 2}(z)}$$

可以推出玻色气体的压强小于经典气体

#### (2)BEC(\*)

当温度降到某个临界温度Tc 时，宏观数量的玻色子凝聚到能量最低的单粒子态上，到绝对零度时，所有粒子都会凝聚到基态上。这种现象就被称为玻色－ 爱因斯坦凝聚。

BEC粒子凝聚到ϵ = 0 态是在动量空间中的凝聚，而不是像通常凝聚态相变那样在坐标空间的凝聚（水蒸汽凝结成液滴是坐标空间的凝结，不是BEC）

- 凝聚温度的计算：化学势$\mu=0$

$$\frac{2 \pi}{h^{3}}(2 m)^{3 / 2} \int_{0}^{\infty} \frac{\varepsilon^{1 / 2} \mathrm{~d} \varepsilon}{\mathrm{e}^{\frac{\varepsilon}{k T_{c}}}-1}=n$$

热力学量(p,S)的计算

#### (3)光子气体(平衡辐射)

化学势$\mu=0$

态密度

$$D(\omega)=\frac{V}{\pi^{2} c^{3}} \omega^{2}$$

直接利用玻色分布，得普朗克公式

$$U(\omega, T) d \omega=\frac{V}{\pi^{2} c^{3}} \frac{\hbar \omega^{3}}{e^{\frac{\hbar \omega}{k_{B} T}}-1} d \omega$$

积分可得内能

$$U=\frac{\pi^{2} k_{B}^{4}}{15 c^{3} \hbar^{3}} V T^{4}$$

同样地，也可以求出配分函数–&gt;U,p,S

 

### 3.理想费米气体

态密度与玻色子计算相同

#### (1)弱简并

巨配分函数

$$\log \Xi=\frac{2 \pi(2 s+1) V}{h^{3}}\left(2 m k_{B} T\right)^{3 / 2} \int_{0}^{\infty} \log \left(1+e^{-\alpha-x}\right) x^{1 / 2} d x$$

由于是弱简并，我们可以将对数函数展开成级数并逐项积分得到配分函数

$$\begin{aligned} \log \Xi &=\frac{(2 s+1) V}{h^{3}}\left(2 \pi m k_{B} T\right)^{3 / 2} \sum_{j=1}^{\infty}(-)^{j-1} \frac{e^{-j \alpha}}{j^{5 / 2}} \\ \bar{N} &=\frac{(2 s+1) V}{h^{3}}\left(2 \pi m k_{B} T\right)^{3 / 2} \sum_{j=1}^{\infty}(-)^{j-1} \frac{e^{-j \alpha}}{j^{3 / 2}} \\ U &=-\frac{\partial}{\partial \beta} \log \Xi=\frac{3}{2} k_{B} T \log \Xi \\ p &=\frac{1}{\beta} \frac{\partial}{\partial V} \log \Xi=\frac{2 U}{3 V} \\ S &=k_{B}\left(\frac{5}{2} \log \Xi+\bar{N} \alpha\right) \end{aligned}$$

#### (2)强简并

- T=0,零温情况

此时由玻色分布可以看出

$$\begin{equation} f_s= \begin{cases} 1&\varepsilon<\mu\\ 0\&#038;\varepsilon>\mu \end{cases} \end{equation}$$

因此费米子均位于能量小于$\mu$的态上，直接有

$$N=\int_{0}^{\mu_{0}} \frac{4 \pi V}{h^{3}}(2 m)^{3 / 2} \varepsilon^{1 / 2} d \varepsilon$$

我们就得到了零温时的化学势μ0

$$\mu_{0} \equiv \varepsilon_{F}=\frac{\hbar^{2}}{2 m}\left(3 \pi^{2} n\right)^{2 / 3}$$

$\varepsilon=\mu_0$的点在相空间构成的面为费米面

- T$\ne$0,低温情况

采用Sommerfeld展开

$$\int_{0}^{\infty} \frac{\eta(\varepsilon) d \varepsilon}{e^{\frac{\varepsilon-\mu}{k_{B} T}}+1}=\int_{0}^{\mu} \eta(\varepsilon) d \varepsilon+\frac{\pi^{2}}{6}\left(k_{B} T\right)^{2} \eta^{\prime}(\mu)+\frac{7 \pi^{4}}{720}\left(k_{B} T\right)^{4} \eta^{\prime \prime \prime}(\mu)+\cdots$$

代入

$$\begin{aligned} N &=\frac{4 \pi V}{h^{3}}(2 m)^{3 / 2} \int_{0}^{\infty} \frac{\varepsilon^{1 / 2} d \varepsilon}{e^{\frac{\varepsilon-\mu}{k_{B} T}}+1}, \\ U &=\frac{4 \pi V}{h^{3}}(2 m)^{3 / 2} \int_{0}^{\infty} \frac{\varepsilon^{3 / 2} d \varepsilon}{e^{\frac{\varepsilon-\mu}{k_{B} T}}+1}, \end{aligned}$$

仅保留至一阶项，同时一阶项中的$\mu$用零阶项近似，就可以得到

$$\mu=\mu_{0}\left\[1-\frac{\pi^{2}}{12}\left(\frac{k_{B} T}{\mu_{0}}\right)^{2}\right\]$$ $$U=\frac{3}{5} N \mu_{0}\left\[1+\frac{5 \pi^{2}}{12}\left(\frac{k_{B} T}{\mu_{0}}\right)^{2}\right\]$$

同时可以求出热容

低温下自由电子气的热容量是与温度T的一次方成正比。

#### (3)加磁场

$$\varepsilon_{\pm}=\frac{\mathbf{p}^{2}}{2 m} \pm \mu_{B} B_{0}$$

 

### 4.固体热容

爱因斯坦假设固体中的原子的所有振动模式的频率都是相同的。德拜则认为频率存在一个分布和一个上限$\omega_D$.

将系统的3N个简正模作为声子考虑，声子为玻色子，因此可以类似光子气体的推导

态密度

$$g(\omega) d \omega=\frac{V}{2 \pi^{2}}\left(\frac{1}{c_{l}^{3}}+\frac{2}{c_{t}^{3}}\right) \omega^{2} d \omega$$

这里考虑到了声子两个方向传播速度的不同，l为纵波，t为横波

我们有

$$\int_{0}^{\omega_{D}} g(\omega) d \omega=3 N$$

其中ωD 是一个截止频率，称为德拜截止频率。于是，固体的内能可以写成

$$U=U_{0}+\int_{0}^{\omega_{D}} g(\omega) \frac{\hbar \omega}{e^{\frac{\hbar \omega}{k_{B} T}}-1} d \omega$$

在高温极限下

$$U=U_{0}+3 N k_{B} T, \quad C_{V}=3 N k_{B}$$

在低温极限下

$$U=U_{0}+3 N k_{B} \frac{\pi^{4}}{5} \frac{T^{4}}{\theta_{D}^{3}}, \quad C_{V}=3 N k_{B} \frac{4 \pi^{4}}{5}\left(\frac{T}{\theta_{D}}\right)^{3}$$

热容与$T^3$成正比，德拜$T^3$律

 

### 5.理想气体

#### (1)单原子

直接采用正则配分函数

$$Z=\frac{1}{N ! h^{3 N}} \int e^{-\frac{\beta}{2 m} \sum_{i=1}^{N} \mathbf{p}_{i}^{2}} d^{3} \mathbf{r}_{i} d^{3} \mathbf{p}_{i}$$

直接积分得

$$Z=\frac{1}{N !} z^{N}, \quad z=V\left(\frac{2 \pi m}{\beta h^{2}}\right)^{3 / 2}$$

套公式求得热力学函数

$$p=\frac{1}{\beta} \frac{\partial}{\partial V} \log Z=\frac{N k_{B} T}{V}$$ $$U=-\frac{\partial}{\partial \beta} \log Z=\frac{3}{2} N k_{B} T$$ $$S=\frac{3}{2} N k_{B} \log T+N k_{B} \log \frac{V}{N}+\frac{3}{2} N k_{B}\left\[\frac{5}{3}+\log \left(\frac{2 \pi m k_{B}}{h^{2}}\right)\right\]$$

 

#### (2)双原子

经典情形直接积分

实际情况转动和振动部分需要采用量子统计

振动动能$\varepsilon=(n+1/2)\hbar \omega$求和得到

$$U^{(v)}=\frac{N \hbar \omega}{2}+\frac{N \hbar \omega}{e^{\beta \hbar \omega}-1}$$

因此振动部分带来的热容

$$C_{V}^{(v)}=N k_{B}\left(\frac{\theta_{v}}{T}\right)^{2} e^{-\frac{\theta_{v}}{T}}$$

其中

$$\theta_{v} \equiv \hbar \omega / k_{B}>>T$$

为分子的振动特征温度，并已用到了其远大于T的近似，可以看出在室温状态下其振动能级实际上被冻结

 

分子的转动能级

$$\varepsilon^{(r)}=\frac{j(j+1) \hbar^{2}}{2 I}$$

求和，每个能级的简并度2j+1

$$z^{(r)}=\sum_{j}(2 j+1) e^{-\frac{j(j+1) \hbar^{2}}{2 I k_{B} T}}=\sum_{j}(2 j+1) e^{-j(j+1) \frac{\theta_{r}}{T}}$$

同样引入分子的转动特征温度

$$\theta_{r} \equiv \hbar^{2} /\left(2 I k_{B}\right)$$

其量级在$10^0-10^1K$，因此上述求和可以看作准连续的，令$x=\left(\theta_{r} / T\right) j(j+1)$，则

$$z^{(r)}=\int_{0}^{\infty} \frac{T}{\theta_{r}} d x e^{-x}=\frac{2 I}{\beta \hbar^{2}}$$ $$\begin{aligned} U^{(r)} &=-N \frac{\partial}{\partial \beta} \log z^{(r)}=N k_{B} T \\ C_{V}^{(r)} &=N k_{B} \end{aligned}$$

 

#### (3)迈耶集团展开（不考）

#### (4)混合理想气体

 

### 6.平均场理论

有一个外磁场B，原子有自旋$\mu$，只能沿B和反B两个方向，记为$\sigma=\pm 1$

系统的哈密顿量由$\mu B$和自旋间的相互作用组成，将一个原子感受到的来自其它原子的场等效为其系综平均值

$$B_{eff}=\frac{qJ}{\mu}\bar{\sigma}$$

因此配分函数（其中前面的指数项来自mzs讲义，lc和wzs书中没有，仅影响能量的零点选取，问题不大）

$$\begin{array}{l} Z=e^{-\frac{1}{2} \beta N q J \bar{\sigma}^{2}}\left\[\sum_{\sigma_{1}=\pm 1} e^{\left.\beta \mu\left(B+\frac{q J}{\mu} \bar{\sigma}\right) \sigma_{1}\right\]^{N}}\right. \\ =e^{-\frac{1}{2} \beta N q J \bar{\sigma}^{2}}\left\[2 \cosh \frac{\mu\left(B+\frac{q J}{\mu} \bar{\sigma}\right)}{k_{B} T}\right\]^{N} \end{array}$$

记

$$\bar{B}=B+\frac{q J}{\mu} \bar{\sigma}=B+B_{\text {eff }}$$

则磁化强度

$$M=-\frac1 \beta\frac{\partial \ln Z}{\partial B}=N\mu \tanh \frac{\mu \bar{B}}{k_{B} T}$$

则得到自洽方程

$$\bar{\sigma}=\tanh \frac{\mu\left(B+\frac{q J}{\mu} \bar{\sigma}\right)}{k_{B} T}$$

当外场B=0时

$$\bar{\sigma}=\tanh \frac{q J\bar{\sigma}}{k_{B} T}$$

当$q J / k_{B} T>1$时上式除0外还有两非零解，说明在外场为0 时系统仍然可以有非0的磁化强度，即为自旋系统系统的自发磁化现象。

 

## 总结

统计的题大致为五个应用中的两三个，改变能量关系或维数(一维/二维/三维)或极限相对论/经典 情况来算

**能态密度——&gt;配分函数——&gt;热力学量(N/p/S)**
