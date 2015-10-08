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

{% math %}f^\ast({\bf\xi}) = \sup \left\{ \lt {\bf x},{\bf\xi}\gt-f({\bf x}) \mid {\bf x}\in \Re^n \right\} {% endmath %}

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

{% math %} S = \left\{ x \in \Re^n \mid g_i({\bf x}) \leqslant 0 \text{, } \; \; i=1, \cdots, m\right \}{% endmath %}

{% math %}
L_0({\bf x}, {\bf \lambda}) =
\begin{cases}
    f({\bf x}) + \sum^m_{i=1}\lambda_ig_i({\bf x})\;, & {\bf \lambda} \geqslant {\bf 0}\\
    -\infty \; ,                                      & {\bf \lambda} \ngeqslant {\bf 0}
\end{cases}
{% endmath %}

{% math %}
\theta({\bf x}) = f({\bf x}) + \delta_S({\bf x})
{% endmath %}

{% math %}
\theta({\bf x}) = \sup \left\{ L_0({\bf x}, {\bf \lambda}) \mid {\bf \lambda} \in \Re^m \right\}
{% endmath %}

{% math %}
\omega_0({\bf \lambda}) = \inf \left\{ L_0({\bf x}, {\bf \lambda}) \mid {\bf x} \in \Re^n \right\}
{% endmath %}

Constrains relax

{% math %} F_0({\bf x}, {\bf u}) =
\begin{cases}
    f({\bf x}), & {\bf x} \in        S({\bf u}) & \min  & f({\bf x})   &                & \\
    +\infty,    & {\bf x} \notin S({\bf u})     & s.t.  & g_i({\bf x}) & \leqslant u_i, & i = 1, \cdots, m
\end{cases}
{% endmath %}

{% math %}
S({\bf u}) = \left\{ {\bf x} \in \Re^n \mid g_i({\bf x}) \leqslant u_i, \; i=1, \cdots, m \right\}
{% endmath %}

**引理 4.5** Lagrange 函数 {%m%}L_0: \Re^{n+m} \to [-\infty, +\infty) {%em%} 与函数 {%m%}F_0: \Re^{n+m} \to (-\infty,+\infty]{%em%} 之间有如下关系成立：

{% math %}L_0({\bf x}, {\bf \lambda}) = \inf \left\{ F_0({\bf x}, {\bf u}) + \lt {\bf \lambda}, {\bf u}\gt \mid {\bf u} \in \Re^m \right\}{% endmath %}

{% math %}F_0({\bf x}, {\bf u}) = \sup \left\{ L_0({\bf x}, {\bf \lambda}) - \lt {\bf \lambda}, {\bf u}\gt \mid {\bf \lambda} \in \Re^m \right\}{% endmath %}

### Lagrange 对偶性的推广 ###

对于原始问题 {%m%}(P){%em%}，考虑函数 {%m%}F: \Re^{n+M} \to (-\infty, +\infty]{%em%}，使得对任意固定的 {%m%}{\bf x} \in \Re^n{%em%}，{%m%}F({\bf x}, \cdot): \Re^M \to (-\infty, +\infty]{%em%} 均为闭正常凸函数，并且满足

{% math %} F({\bf x}, {\bf 0}) = \theta({\bf x}) \text{, } {\bf x} \in \Re^n {% endmath %}

**例 4.7** 设 {%m%}M = m{%em%}，考虑函数 {%m%}F_0: \Re^{n+m} \to (-\infty, +\infty]{%em%}，利用满足 {%m%}q({\bf 0}) = 0{%em%} 的闭正常凸函数 {%m%}q: \Re^m \to (-\infty, +\infty]{%em%} 定义函数 {%m%}F: \Re^{n+m} \to (-\infty, +\infty]{%em%} 如下：

{% math %} F({\bf x}, {\bf u}) = F_0({\bf x}, {\bf u}) + q({\bf u}) {% endmath %}


{% math %} \theta({\bf x}) = f({\bf x}) + \delta_S({\bf x}) {% endmath %}
{% math %} \implies F({\bf x}, {\bf u}) \mid F({\bf x}, {\bf 0}) = \theta({\bf x}) {% endmath %}
{% math %} \implies L({\bf x}, {\bf \lambda}) = \inf \left\{ F({\bf x}, {\bf u}) + \lt {\bf \lambda}, {\bf u}\gt \mid {\bf u} \in \Re^M \right\} {% endmath %}
{% math %} \implies \omega({\bf \lambda}) = \inf \left\{ L({\bf x}, {\bf \lambda}) \mid {\bf x} \in \Re^n \right\} {% endmath %}


### Fenchel 对偶性 ###

{% math %} \min_{\bf x} f({\bf x}) + g({\bf Ax}) {% endmath %}

{% math %} \begin{cases} & F({\bf x}, {\bf 0}) = \theta({\bf x}),     & x \in \Re^n \\
                         & \theta({\bf x}) = f({\bf x}) + g({\bf Ax}) & \end{cases} {% endmath %}

{% math %} \implies F({\bf x}, {\bf u}) = f({\bf x}) + g({\bf Ax} + {\bf u}) {% endmath %}
{% math %} \begin{eqnarray*}
\implies L({\bf x}, {\bf \lambda}) & = & \inf \left\{ f({\bf x}) + g({\bf Ax} + {\bf u}) + \lt {\bf \lambda}, {\bf u}\gt \mid {\bf u} \in \Re^m \right\} \\
                                   & = & f({\bf x}) - g^\ast(-{\bf \lambda}) - \lt {\bf \lambda}, {\bf Ax}\gt
\end{eqnarray*}{% endmath %}

{% math %} \begin{eqnarray*}
\implies \omega({\bf \lambda}) & = & \inf \left\{ f({\bf x} - g^\ast(-{\bf \lambda}) - \lt {\bf \lambda}, {\bf Ax}\gt \mid {\bf x} \in \Re^n \right\} \\
                               & = & -f^\ast({\bf A}^T{\bf \lambda}) - g^\ast(-{\bf \lambda})
\end{eqnarray*}{% endmath %}

{% math %} \min_{\bf \lambda} f^\ast\left( {\bf A}^T{\bf \lambda} \right) + g^\ast(-{\bf \lambda}){% endmath %}
{% math %} \max_{\bf \lambda} -f^\ast\left({\bf A}^T{\bf \lambda} \right) - g^\ast\left(-{\bf\lambda}\right){% endmath %}

## 算法 ##

### 1. Proximal Gradient Method ###

参考 [Algorithms for large-scale convex optimization - DTU 2010](http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf){% sidenote 3 'A Lecture note from "02930 Algorithms for Large-Scale Convex Optimization" taught by Per Christian Hansen (pch@imm.dtu.dk) and Professor Lieven Vandenberghe ([http://www.seas.ucla.edu/~vandenbe/](http://www.seas.ucla.edu/~vandenbe/)) at Danmarks Tekniske Universitet ([http://www.kurser.dtu.dk/2010-2011/02930.aspx?menulanguage=en-GB](http://www.kurser.dtu.dk/2010-2011/02930.aspx?menulanguage=en-GB)). The Download Link is found at the page of "EE227BT: Convex Optimization - Fall 2013" taught by Laurent El Ghaoui at Berkeley ([http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf](http://www.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture18.pdf)). And both of the lectures mentioned the book "Convex Optimization" by Stephen Boyd and Lieven Vandenberghe ([http://stanford.edu/~boyd/cvxbook/](http://stanford.edu/~boyd/cvxbook/)) and the software "CVX" - a MATLAB software for desciplined Convex Programming ([http://cvxr.com/cvx/](http://cvxr.com/cvx/)). A similar lecture note on Proximal Gradient Method from "EE236C - Optimization Methods for Large-Scale Systems (Spring 2013-14)" ([http://www.seas.ucla.edu/~vandenbe/ee236c.html](http://www.seas.ucla.edu/~vandenbe/ee236c.html)) at UCLA' can be found at [http://www.seas.ucla.edu/~vandenbe/236C/lectures/proxgrad.pdf](http://www.seas.ucla.edu/~vandenbe/236C/lectures/proxgrad.pdf). %}

#### Proximal mapping ####

The **proximal mapping** (or proximal operator) of a convex function {%m%}h{%em%} is

{% math %} {\bf prox}_h(x) = \mathop{argmin}_u \left( h(u) + \frac{1}{2} \|u - x\|^2_2 \right){% endmath %}

**examples**

**1.** {%m%}h(x) = 0: {\bf prox}_h(x) = x{%em%}

**2.** {%m%}h(x) = I_C(x){%em%} (indicator function of {%m%}C{%em%}): {%m%}{\bf prox}_h{%em%} is projection on {%m%}C{%em%}

{% math %} {\bf prox}_h(x) = P_C(x) = \mathop{argmin}_{u \in C} \|u - x\|^2_2 {% endmath %}

**3.** {%m%}h(x) = t \|x\|_1{%em%}: {%m%}{\bf prox}_h{%em%} is shinkage (soft threshold) operation

{% math %}
{\bf prox}_h =
\begin{cases}
    x_i - t & x_i   \geqslant t \\
    0       & |x_i| \leqslant t \\
    x_i + t & x_i   \leqslant -t
\end{cases} {% endmath %}

#### Proximal gradient method ####

**unconstrained problem** with cost function split in two components

{% math %} \mathop{argmin} f(x) = g(x) + h(x) {% endmath %}

{%m%}g{%em%} convex, differentiable, with **dom** {%m%}g=\Re^n{%em%}

{%m%}h{%em%} closed, convex, possibly nondifferentiable; {%m%}{\bf prox}_h{%em%} is inexpensive

**proximal gradient algorithm**

{% math %} x^{(k)} = {\bf prox}_{t_kh} \left( x^{(k-1)} - t_k \nabla g \left( x^{(k-1)} \right) \right) {% endmath %}

{% math %} t_k \gt 0 \text{ is the step size,}{% endmath %}

constant or determined by line search

#### Interpretation ####

{% math %} x^+ = {\bf prox}_{th} \left( x - t\nabla g(x) \right) {% endmath %}


from definition of proximal operator:

{% math %} \begin{eqnarray*}
x^+ & = &  \mathop{argmin}_u \left( h(u) + \frac{1}{2t} \left\| u - x + t\nabla g(x) \right\|^2_2 \right) \\
    & = & \mathop{argmin}_u \left( h(u) + g(x) + \nabla g(x)^T(u-x) + \frac{1}{2t} \left\| u - x \right\|^2_2 \right)
\end{eqnarray*}{% endmath %}

{%m%}x^+{%em%} minimizes {%m%}h(u){%em%} plus a simple quadratic local of {%m%}g(u){%em%} around {%m%}x{%em%}

#### Examples ####

{% math %} minimize \; \; g(x) + h(x) {% endmath %}

**gradient method**: {%m%}h(x) = 0{%em%}, i.e., minimize g(x)

{% math %} x^{(k)} = x^{(k-1)} - t_k\nabla g\left( x^{(k-1)} \right){% endmath %}

**gradient projection method**: {%m%}h(x) = I_C(x){%em%}, i.e., minimize {%m%}g(x){%em%} over {%m%}C{%em%}

{% math %} x^{(k)} = P_C \left( x^{(k-1)} - t_k\nabla g \left(x^{(k-1)} \right) \right) {% endmath %}

**iterative soft-thresholding**: {%m%}h(x) = \|x\|_1{%em%}, i.e., {%m%} minimize \; \; g(x)+ \| x \|_1{%em%}

{% math %} x^{(k)} = {\bf prox}_{t_kh} \left( x^{(k-1)} - t_k\nabla g\left( x^{(k-1)} \right)  \right) {% endmath %}

and

{% math %}
{\bf prox}_{th}(u)_i =
\begin{cases}
u_i - t & & u_i \geq t \\
0       & & -t \leq u_i \leq t \\
u_i + t & & u_i \geq t
\end{cases}{% endmath %}

{% maincolumn /assets/img/fukushima-softthresholding.jpg '' %}

### 2. Dual Proximal Gradient Methods ###

参考 L. Vandenberghe EE236C (Spring 2013-14)

#### Composite structure in the Dual ####

{% math %} \begin{eqnarray*}
minimize & & f(x)+g(Ax) \\
maximize & & -f^\ast \left( -A^Tz \right) - g^\ast(z)
\end{eqnarray*}{% endmath %}

dual has the right structure for the proximal gradient method if

prox-operator of {%m%}g{%em%} (or {%m%}g^\ast{%em%}) is cheap (closed form or simple algorithm)

{%m%}f{%em%} is strongly convex ({%m%}f(x)-(\frac{\mu}{2})x^T{%em%} is convex) implies {%m%}f^\ast\left(-A^Tz\right){%em%} has Lipschitz continuous gradient ({%m%}L=\frac{\|A\|^2_2}{\mu}{%em%}):

{% math %} \left\| A\nabla f^\ast(-A^Tu)-A\nabla f^\ast(-A^Tv) \right\|_2 \leq \frac{\|A\|^2_2}{\mu}\|u-v\|_2 {% endmath %}

because {%m%}\nabla f^2{%em%} is Lipschitz continuous with constant {%m%}\frac{1}{\mu}{%em%}

#### Dual proximal gradient update ####

{% math %} z^+ = prox_{tg\ast}\left( z+tA\nabla f^\ast\left( -A^Tz \right) \right) {% endmath %}

equivalent expression in term of {%m%}f{%em%}:

{% math %} z^+ = prox_{tg\ast}(z+tA\hat{x}) \text{  where } \hat{x} = \mathop{argmin}_x \left( f(x) + z^TAx \right){% endmath %}

**1.**  if {%m%}f{%em%} is separable, calculation of {%m%}\hat{x}{%em%} decomposes into independent problems

**2.**  step size {%m%}t{%em%} constant or from backtracking line search

#### Alternating minimization interpretation ####

Moreau decomposition gives alternate expression for {%m%}z{%em%}-update

{% math %} z^+ = z + t(A\hat{x} - \hat{y}) {% endmath %}

where

{% math %} \begin{eqnarray*}
\hat{x} & = & \mathop{argmin}_x \left( f(x) + z^TAx \right) \\
\hat{y} & = & prox_{t^{-1}g} \left( \frac{z}{t} + A\hat{x} \right)        \\
        & = & \mathop{argmin}_y \left(g(y) + z^T(A\hat{x} - y) + \frac{t}{2} \|A\hat{x} - y\|^2_2  \right)
\end{eqnarray*}{% endmath %}

in each iteration, an alternating minimization of:

**1. Lagrangian** {%m%}f(x) + g(y) + z^T(Ax - y){%em%} over {%m%}x{%em%} 

**2. augmented Lagrangian** {%m%}f(x) + g(y) + z^T(Ax - y) + \frac{t}{2} \|Ax - y\|^2_2{%em%} over {%m%}y{%em%}

#### Regularized norm approximation ####

{% math %} minimize f(x) + \|Ax - b\| \text{   (with } f \text{ strongly convex)   } {% endmath %}

a special case with {%m%}g(y) = \|y - b\|{%em%}

{% math %}
g^\ast =
\begin{cases}
b^Tz    & & \|z\|_\ast \leq 1 \\
+\infty & & otherwise 
\end{cases}
{% endmath %}

{% math %}
prox_{tg\ast}(z) = P_C(z - tb)
{% endmath %}

C is unit norm ball for dual norm {%m%}\|\cdot\|_\ast{%em%}

**dual gradient projection update**

{% math %} \begin{eqnarray*}
\hat{x} & = & \mathop{argmin}_x \left( f(x) + z^TAx \right) \\
z^+     & = & P_C(z + t(A\hat{x} - b))
\end{eqnarray*}{% endmath %}

#### Example ####

{% math %}
minimize \; \; f(x) + \sum^p_{i=1}\|B_ix\|_2 \text{   (with } f \text{ strongly convex)   }
{% endmath %}

**dual gradient projection update**

{% math %} \begin{eqnarray*}
\hat{x} & = & \mathop{argmin}_x \left( f(x) + \left(\sum^p_{i=1}B^T_iz_i\right)^Tx \right) \\
z^+_i   & = & P_{C_i}(z_i + tB_i\hat{x}) \text{, } \; \; i=1, \cdots, p
\end{eqnarray*}{% endmath %}

{%m%}C_i{%em%} is unit Euclidean norm ball in {%m%}\Re^{m_i}{%em%}, if {%m%}B_i \in \Re^{m_i \times n}{%em%}

#### Minimization over intersection of convex sets ####

{% math %} \begin{eqnarray*}
minimize   & & f(x) \\
subject to & & x \in C_i \cap \cdots \cap C_m
\end{eqnarray*}{% endmath %}

{%m%}f{%em%} strongly convex; e.g., {%m%}f(x) = \|x - a\|^2_2{%em%} for projecting {%m%}a{%em%} on intersection

sets {%m%}C_i{%em%} are closed, convex, and easy to project onto

**dual proximal gradient update**

{% math %} \begin{eqnarray*}
\hat{x} & = & \mathop{argmin}_x \left( f(x) + (z_i + \cdots + z_m)^Tx \right) \\
z^+_i   & = & z_i + t\hat{x} - tP_{C_i}\left(\frac{z_i}{t} + \hat{x}\right) \text{, }\; \; i=1, \cdots, m
\end{eqnarray*}{% endmath %}

#### Decomposition of separable problems ####

{% math %}
minimize \; \; \sum^n_{j=1}f_j(x_j) + \sum^m_{i=1}g_i(A_{i1}x_1 + \cdots + A_{in}x_n )
{% endmath %}

each {%m%}f_i{%em%} is strongly convex; {%m%}g_i{%em%} has inexpensive prox-operator

**dual proximal gradient update**

{% math %} \begin{eqnarray*}
\hat{x}_j & = & \mathop{argmin}_{x_j} \left( f_j(x_j) + \sum^m_{i=1}z^T_iA_{ij}x_j \right) \text{, } \; \; j=1, \cdots, n \\
z^+_i     & = & prox_{tg^\ast_i}\left(z_i + t\sum^n_{j=1}A_{ij}\hat{x}_j \right) \text{, } \; \; i=1, \cdots, m
\end{eqnarray*}{% endmath %}

### 3. Fast proximal gradient methods ###

参考 L. Vandenberghe EE236C (Spring 2013-14)

#### FISTA (basic version) ####

{% math %}
minimize \; \; f(x) = g(x) + h(x)
{% endmath %}

{%m%}g{%em%} convex, differentiable with {%m%}\mathop{dom} g=\Re^n{%em%}

{%m%}h{%em%} closed, convex, with inexpensive {%m%}prox_{th}{%em%} operator

**algorithm**: choose any {%m%}x^{(0)} = x^{(-1)}{%em%}; for {%m%}k \geq 1{%em%}, repeat the steps

{% math %} \begin{eqnarray*}
y       & = & x^{(k-1)} + \frac{k-2}{k+1} \left( x^{(k-1)} - x^{(k-2)} \right) \\
x^{(k)} & = & prox_{t_kh} \left( y - t_k\nabla g(y) \right)
\end{eqnarray*}{% endmath %}

step size {%m%}t_k{%em%} fixed or determined by line search

acronym stands for 'Fast Iterative Shrinkage-Thresholding Algorithm'

#### Interpretation ####

first iteration ({%m%}k = 1{%em%}) is a proximal gradient step at {%m%}y = x^{(0)}{%em%}

next iterations are proximal gradient steps at extrapolated points {%m%}y{%em%}

{% maincolumn /assets/img/fukushima-interpretation.png '' %}

note: {%m%}x^{(k)}{%em%} is feasible (in {%m%}\mathop{dom} h{%em%}); {%m%}y{%em%} may be outside {%m%}\mathop{dom} h{%em%}

#### Reformulation of FISTA ####

define {%m%}\theta_k = \frac{2}{k+1}{%em%} and introduce an intermediate variable {%m%}v^{(k)}{%em%}

**algorithm**: choose {%m%}x^{(0)} = v^{(0)}{%em%}; for {%m%}k \geq 1{%em%}, repeat the steps

{% math %} \begin{eqnarray*}
y       & = & (1 - \theta_k)x^{(k-1)} + \theta_kv^{(k-1)} \\
x^{(k)} & = & prox_{t_kh}(y-t_k\nabla g(y))\\
v^{(k)} & = & x^{(k - 1)} + \frac{1}{\theta_k}\left( x^{(k)} - x^{(k-1)} \right)
\end{eqnarray*}{% endmath %}

#### Nesterov's second method ####

**algorithm**: choose {%m%}x^{(0)} = v^{(0)}{%em%}; for {%m%}k \geq 1{%em%}, repeat the steps

{% math %} \begin{eqnarray*}
y       & = & (1 - \theta_k)x^{(k-1)} + \theta_kv^{(k-1)} \\
v^{(k)} & = & prox_{\left(\frac{t_k}{\theta_k}\right)h} \left( v^{(k-1)} - \frac{t_k}{\theta_k}\nabla g(y) \right)\\
x^{(k)} & = & (1 - \theta_k)x^{(k-1)} + \theta_kv^{(k)}
\end{eqnarray*}{% endmath %}

User{%m%}\theta_k = \frac{2}{k+1}{%em%} and {%m%}t_k = \frac{1}{L}{%em%}, or one of the line search methods

identical to FISTA if {%m%}h(x) = 0{%em%}

unlike in FISTA, {%m%}y{%em%} is feasible (in {%m%}\mathop{dom} h{%em%}) if we take {%m%}x^{(0)} \in \mathop{dom} h{%em%}

### 4. Fast dual proximal gradient methods ###

参考 A Fast Dual Proximal Gradient Algorithm for Convex Minimization and Applications by Amir Beck and Marc Teboulle at October 10, 2013

{% math %} \begin{eqnarray*}
(D)  & = & \max_y\left\lbrace q(y) \equiv -f^\ast\left(A^Ty\right)-g^\ast(-y)\right\rbrace,\\
(D') & = & \min F(y) + G(y),\\
(P') & = & \min \left\lbrace f(x) + g(z): Ax - z = 0 \right\rbrace.
\end{eqnarray*}{% endmath %}

{% math %}
F(y) := f^\ast\left( A^Ty \right), \; \; G(y) :=g^\ast(-y)
{% endmath %}

Initialization: {%m%}L \geq \frac{\|A\|^2}{\sigma}{%em%}, {%m%}w_1 = y_0 \in \mathbb{V}{%em%}, {%m%}t_1 = 1{%em%}.

General Step {%m%}(k \geq 1){%em%}:

{% math %} \begin{eqnarray*}
y_k     & = & prox_{\frac{1}{L}G}\left( w_k - \frac{1}{L} \nabla F(w_k) \right)\\
t_{k+1} & = & \frac{1 + \sqrt{1 + 4t^2_k}}{2} \\
w_{k+1} & = & y_k + \left( \frac{t_k - 1}{t_{k+1}} \right) (y_k - y_{k-1}).
\end{eqnarray*}{% endmath %}

#### The Fast Dual-Based Proximal Gradient Method (FDPG) ####

Input: {%m%}L \geq \frac{\|A\|^2}{\sigma} - \text{ an upper bound on the Lipschitz constant of } \nabla F{%em%}

Step {%m%}0{%em%}. Take {%m%}w_1 = y_0 \in \mathbb{V}{%em%}, {%m%}t_1 = 1{%em%}.

Step {%m%}k{%em%}. ({%m%}k \geq 0{%em%}) Compute

{% math %} \begin{eqnarray*}
u_k     & = & \mathop{argmax}_x \left\lbrace \lt x, A^Tw_k\gt - f(x) \right\rbrace\\
v_k     & = & prox_{Lg}(Au_k - Lw_k)\\
y_k     & = & w_k - \frac{1}{L}(au_k - v_k)\\
t_{k+1} & = & \frac{1 + \sqrt{1 + 4t^2_k}}{2}\\
w_{k+1} & = & y_k + \left( \frac{t_k - 1}{t_{k+1}} \right) (y_k - y_{k-1}). \tag*{$\blacksquare$}
\end{eqnarray*}{% endmath %}
