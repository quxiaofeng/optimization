---
layout: post
title:  "《非线性最优化基础》学习笔记"
date:   2015-08-02 14:33:54
categories:
---

《[非线性最优化基础](http://book.douban.com/subject/6510671/)》 作者 [福嶋雅夫](http://www.seto.nanzan-u.ac.jp/~fuku/index.html) {% sidenote 1 '《非线性最优化基础》（豆瓣链接：[http://book.douban.com/subject/6510671/](http://book.douban.com/subject/6510671/)）。福嶋雅夫（Masao Fukushima），教授，日本南山大学理工学院系统与数学科学系，日本京都大学名誉教授，加拿大滑铁卢大学/比利时那慕尔大学/澳大利亚新南威尔士大学客座教授。主页：[http://www.seto.nanzan-u.ac.jp/~fuku/index.html](http://www.seto.nanzan-u.ac.jp/~fuku/index.html)。' %}

该文为[冯象初教授](http://web.xidian.edu.cn/xcfeng/){% sidenote 2 '冯象初，教授，西安电子科技大学数学系。主页：[http://web.xidian.edu.cn/xcfeng/](http://web.xidian.edu.cn/xcfeng/)' %}有关非线性最优化的讲座的笔记。

## 主要内容 ##

**理论基础**

1. 凸函数、闭函数
2. 共轭函数
3. 鞍点问题
4. Lagrange 对偶问题
5. Lagrange 对偶性的推广
6. Fenchel 对偶性

**算法**

1. Proximal gradient methods
2. Dual proximal gradient methods
3. Fast proximal gradient methods
4. Fast dual proximal gradient methods

<!--more-->

## 理论基础 ##

### 凸函数、闭函数 ###

给定函数 {%m%}f : \Re^n \to [-\infty, +\infty] {%em%}，称 {%m%}\Re^{n+1}{%em%} 的子集

{% math %} graph \; f = \left\{ ({\bf x}, \beta)^T \in \Re^{n+1} \mid \beta = f({\bf x}) \right\} , {% endmath %}

为 {%m%}f{%em%} 的**图像**（graph），而称位于 {%m%}f{%em%} 的图像上方的点的全体构成的集合

{% math %}epi \; f =\left\{ ({\bf x}, \beta)^T \in \Re^{n+1} \mid \beta \geqslant f({\bf x}) \right\} {% endmath %}

为 {%m%}f{%em%} 的**上图**（epigraph）。若上图 {%m%}epi \; f{%em%} 为凸集，则称 {%m%}f{%em%} 为**凸函数**(convex function)。

**定理 2.27** 设 {%m%} \mathcal{I} {%em%} 为任意非空指标集，而 {%m%}f_i : \Re^n \to [-\infty, +\infty] \; (i \in \mathcal{I}){%em%} 均为凸函数，则由

{% math %} f({\bf x}) = \sup \left\{ f_i({\bf x}) \mid i \in \mathcal{I} \right\} {% endmath %}

定义的函数 {%m%}f : \Re^n \to [-\infty, +\infty] {%em%} 为凸函数。进一步，若 {%m%}\mathcal{I}{%em%} 为有限指标集，每个 {%m%}f_i{%em%} 均为正常的凸函数，并且 {%m%}\cap_{i \in \mathcal{I}} \; dom \; f_i \neq \varnothing {%em%}，则 {%m%}f{%em%} 为正常凸函数。

若对任意收敛于 {%m%}{\bf x}{%em%} 的点列 {%m%}\{ {\bf x}^k\} \subseteq \Re^n{%em%} 均有

{% math %} f({\bf x}) \geqslant \limsup_{k \to \infty}f({\bf x}^k) {% endmath %}

成立，则称函数 {%m%}f:\Re^n\to[-\infty,+\infty]{%em%} 在 {%m%}{\bf x}{%em%} 处**上半连续**（upper semicontinuous）；反之，当

{% math %} f({\bf x}) \leqslant \liminf_{k \to \infty}f({\bf x}^k) {% endmath %}

成立时，称 {%m%}f{%em%} 在 {%m%}{\bf x}{%em%} 处**下半连续**（lower semicontinuous）。若 {%m%}f{%em%} 在 {%m%}{\bf x}{%em%} 处既为上半连续又为下半连续，则称 {%m%}f{%em%} 在 {%m%}{\bf x}{%em%} 处**连续**（continuous）。

### 共轭函数 ###

给定正常凸函数 {%m%}f:\Re^n \to (-\infty,+\infty]{%em%}，由

{% math %}f^\ast({\bf\xi}) = \sup \left\{ <{\bf x},{\bf\xi}>-f({\bf x}) \mid {\bf x}\in \Re^n \right\} {% endmath %}

定义的函数 {%m%}f^\ast:\Re^n \to [-\infty,+\infty]{%em%} 称为 {%m%}f{%em%} 的**共轭函数**（conjuagate function）。

**定理 2.36** 正常凸函数 {%m%}f:\Re^n \to (-\infty,+\infty]{%em%} 的共轭函数 {%m%}f^\ast{%em%} 必为闭正常凸函数。

### 鞍点问题 ###

设 {%m%}Y{%em%} 与 {%m%}Z{%em%} 分别为 {%m%}\Re^n{%em%} 与 {%m%}\Re^m{%em%} 的非空子集，给定以 {%m%}Y\times Z{%em%} 为定义域的函数 {%m%}K:Y\times Z\to[-\infty,+\infty]{%em%}，定义两个函数 {%m%}\eta:Y\to[-\infty,+\infty]{%em%} 与 {%m%}\zeta:Z\to[-\infty,+\infty]{%em%} 如下：

{% math %}\eta({\bf y})=\sup\left\{ K({\bf y},{\bf z}) \mid {\bf z} \in Z\right\} {% endmath %}

{% math %}\zeta({\bf z})=\inf\left\{ K({\bf y},{\bf z}) \mid {\bf y} \in Y\right\} {% endmath %}

{% math %}\min \; \; \eta({\bf y})\\s.t. \; \; \; {\bf y} \in Y{% endmath %}

{% math %}\max \; \; \zeta({\bf z})\\s.t. \; \; \; {\bf z} \in Z{% endmath %}

**引理 4.1** 对任意 {%m%}{\bf y}\in Y{%em%} 与 {%m%}{\bf z}\in Z{%em%} 均有 {%m%}\zeta({\bf z}) \leqslant \eta({\bf y}){%em%} 成立。进一步，还有
{% math %}\sup\left\{ \zeta({\bf z})\mid {\bf z}\in Z\right\} \leqslant \inf\left\{ \eta({\bf y})\mid {\bf y} \in Y\right\} {% endmath %}

**定理 4.1** 点 {%m%}(\bar{\bf y},\bar{\bf z})\in Y\times Z{%em%} 为函数 {%m%}K:Y\times Z\to[-\infty,+\infty]{%em%} 的鞍点的充要条件是 {%m%}\bar{\bf y}\in Y{%em%} 与 {%m%}\bar{\bf z}\in Z{%em%} 满足

{% math %}\eta(\bar{\bf y})=\inf\left\{ \eta({\bf y})\mid {\bf y}\in Y\right\} =\sup\left\{ \zeta({\bf z})\mid {\bf z}\in Z\right\} =\zeta(\bar{\bf z}){% endmath %}

### Lagrange 对偶问题 ###

考虑如下非线性规划问题：

{% math %} \min \; \; f({\bf x}) \\ s.t. \; \; g_i({\bf x}) \leqslant 0, \; \; i=1, \cdots, m{% endmath %}

其中 {%m%}f: \Re^n \to \Re{%em%}, {%m%}g_i: \Re^n \to \Re (i=1, \cdots, m){%em%}。

{% math %} S = \left\{ x \in \Re^n \mid g_i({\bf x}) \leqslant 0 \text{, } i=1, \cdots, m\right \}{% endmath %}

{% math %} L_0({\bf x}, {\bf \lambda}) = \begin{cases}
        f({\bf x}) + \sum^m_{i=1}\lambda_ig_i({\bf x})\;, & {\bf \lambda} \geqslant {\bf 0}\\
        -\infty \; , & {\bf \lambda} \ngeqslant {\bf 0}
    \end{cases}
{% endmath %}

{% math %} \theta({\bf x}) = f({\bf x}) + \delta_S({\bf x}){% endmath %}

{% math %} \theta({\bf x}) = \sup \left\{ L_0({\bf x}, {\bf \lambda}) \mid {\bf \lambda} \in \Re^m \right\}{% endmath %}

{% math %} \omega_0({\bf \lambda}) = \inf \left\{ L_0({\bf x}, {\bf \lambda}) \mid {\bf x} \in \Re^n \right\} {% endmath %}

Constrains relax

{% math %} F_0({\bf x}, {\bf u}) = \begin{cases}
        f({\bf x}),  & {\bf x} \in        S({\bf u}) & \min  & f({\bf x}) & & \\
        +\infty,      & {\bf x} \notin S({\bf u}) & s.t.      & g_i({\bf x}) & \leqslant u_i, & i = 1, \cdots, m 
    \end{cases}
{% endmath %}

{% math %} S({\bf u}) = \left\{ {\bf x} \in \Re^n \mid g_i({\bf x}) \leqslant u_i, \; i=1, \cdots, m \right\} {% endmath %}

**引理 4.5** Lagrange 函数 {%m%}L_0: \Re^{n+m} \to [-\infty, +\infty) {%em%} 与函数 {%m%}F_0: \Re^{n+m} \to (-\infty,+\infty]{%em%} 之间有如下关系成立：

{% math %}L_0({\bf x}, {\bf \lambda}) = \inf \left\{ F_0({\bf x}, {\bf u}) + <{\bf \lambda}, {\bf u}> \mid {\bf u} \in \Re^m \right\}{% endmath %}

{% math %}F_0({\bf x}, {\bf u}) = \sup \left\{ L_0({\bf x}, {\bf \lambda}) - <{\bf \lambda}, {\bf u}> \mid {\bf \lambda} \in \Re^m \right\}{% endmath %}

### Lagrange 对偶性的推广 ###

对于原始问题 {%m%}(P){%em%}，考虑函数 {%m%}F: \Re^{n+M} \to (-\infty, +\infty]{%em%}，使得对任意固定的 {%m%}{\bf x} \in \Re^n{%em%}，{%m%}F({\bf x}, \cdot): \Re^M \to (-\infty, +\infty]{%em%} 均为闭正常凸函数，并且满足

{% math %} F({\bf x}, {\bf 0}) = \theta({\bf x}) \text{,  } {\bf x} \in \Re^n {% endmath %}

**例 4.7** 设 {%m%}M = m{%em%}，考虑函数 {%m%}F_0: \Re^{n+m} \to (-\infty, +\infty]{%em%}，利用满足 {%m%}q({\bf 0}) = 0{%em%} 的闭正常凸函数 {%m%}q: \Re^m \to (-\infty, +\infty]{%em%} 定义函数 {%m%}F: \Re^{n+m} \to (-\infty, +\infty]{%em%} 如下：

{% math %} F({\bf x}, {\bf u}) = F_0({\bf x}, {\bf u}) + q({\bf u}) {% endmath %}


{% math %} \theta({\bf x}) = f({\bf x}) + \delta_S({\bf x}) {% endmath %}
{% math %} \implies F({\bf x}, {\bf u}) \mid F({\bf x}, {\bf 0}) = \theta({\bf x}) {% endmath %}
{% math %} \implies L({\bf x}, {\bf \lambda}) = \inf \left\{ F({\bf x}, {\bf u}) + <{\bf \lambda}, {\bf u}> \mid {\bf u} \in \Re^M \right\} {% endmath %}
{% math %} \implies \omega({\bf \lambda}) = \inf \left\{ L({\bf x}, {\bf \lambda}) \mid {\bf x} \in \Re^n \right\} {% endmath %}


### Fenchel 对偶性 ###

{% math %} \min_{\bf x} f({\bf x}) + g({\bf Ax}) {% endmath %}

{% math %} \begin{cases} & F({\bf x}, {\bf 0}) = \theta({\bf x}), & x \in \Re^n \\
& \theta({\bf x}) = f({\bf x}) + g({\bf Ax}) & \end{cases} {% endmath %}

{% math %} \implies F({\bf x}, {\bf u}) = f({\bf x}) + g({\bf Ax} + {\bf u}) {% endmath %}
{% math %} \begin{eqnarray*} \implies L({\bf x}, {\bf \lambda}) & = & \inf \left\{ f({\bf x}) + g({\bf Ax} + {\bf u}) + <{\bf \lambda}, {\bf u}> \mid {\bf u} \in \Re^m \right\} \\
& = & f({\bf x}) - g^\ast(-{\bf \lambda}) - <{\bf \lambda}, {\bf Ax}> \end{eqnarray*}{% endmath %}
{% math %} \begin{eqnarray*} \implies \omega({\bf \lambda}) & = & \inf \left\{ f({\bf x} - g^\ast(-{\bf \lambda}) - <{\bf \lambda}, {\bf Ax}> \mid {\bf x} \in \Re^n \right\} \\
& = & -f^\ast({\bf A}^T{\bf \lambda}) - g^\ast(-{\bf \lambda}) \end{eqnarray*}{% endmath %}

{% math %} \min_{\bf \lambda} f^\ast\left( {\bf A}^T{\bf \lambda} \right) + g^\ast(-{\bf \lambda}){% endmath %}
{% math %} \max_{\bf \lambda} -f^\ast\left({\bf A}^T{\bf \lambda} \right) - g^\ast\left(-{\bf\lambda}\right){% endmath %}

## 算法 ##

### Proximal Gradient Method ###

参考 [Algorithms for large-scale convex optimization - DTU 2010](http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf){% sidenote 3 'A Lecture note from "02930 Algorithms for Large-Scale Convex Optimization" taught by Per Christian Hansen (pch@imm.dtu.dk) and Professor Lieven Vandenberghe ([http://www.seas.ucla.edu/~vandenbe/](http://www.seas.ucla.edu/~vandenbe/)) at Danmarks Tekniske Universitet ([http://www.kurser.dtu.dk/2010-2011/02930.aspx?menulanguage=en-GB](http://www.kurser.dtu.dk/2010-2011/02930.aspx?menulanguage=en-GB)). The Download Link is found at the page of "EE227BT: Convex Optimization - Fall 2013" taught by Laurent El Ghaoui at Berkeley ([http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf](http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf)). And both of the lectures mentioned the book "Convex Optimization" by Stephen Boyd and Lieven Vandenberghe ([http://stanford.edu/~boyd/cvxbook/](http://stanford.edu/~boyd/cvxbook/)) and the software "CVX" - a MATLAB software for desciplined Convex Programming ([http://cvxr.com/cvx/](http://cvxr.com/cvx/)). A similar lecture note on Proximal Gradient Method from "EE236C - Optimization Methods for Large-Scale Systems (Spring 2013-14)" ([http://www.seas.ucla.edu/~vandenbe/ee236c.html](http://www.seas.ucla.edu/~vandenbe/ee236c.html)) at UCLA' can be found at [http://www.seas.ucla.edu/~vandenbe/236C/lectures/proxgrad.pdf](http://www.seas.ucla.edu/~vandenbe/236C/lectures/proxgrad.pdf). %}

#### Proximal mapping ####

The **proximal mapping** (or proximal operator) of a convex function {%m%}h{%em%} is

{% math %} {\bf prox}_h(x) = \mathop{argmin}_u \left( h(u) + \frac{1}{2} \|u - x\|^2_2 \right){% endmath %}

**examples**

**1.** {%m%}h(x) = 0: {\bf prox}_h(x) = x{%em%}

**2.** {%m%}h(x) = I_C(x){%em%} (indicator function of {%m%}C{%em%}): {%m%}{\bf prox}_h{%em%} is projection on {%m%}C{%em%}

{% math %} {\bf prox}_h(x) = P_C(x) = \mathop{argmin}_{u \in C} \|u - x\|^2_2 {% endmath %}

**3.** {%m%}h(x) = t \|x\|_1{%em%}: {%m%}{\bf prox}_h{%em%} is shinkage (soft threshold) operation

{% math %} {\bf prox}_h = \begin{cases}
    x_i - t & x_i   \geqslant t \\
    0       & |x_i| \leqslant t \\
    x_i + t & x_i   \leqslant -t
\end{cases} {% endmath %}

{%m%}{%em%}

{% math %} {% endmath %}
