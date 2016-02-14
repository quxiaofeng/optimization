---
layout: post
title:  "Introduction to Nonlinear Optimization"
date:   2015-07-15 21:22:17
categories:
---

昨天晚上到今天，看完了一本之前一直看不完的书 《Introduction to Nonlinear Optimization》{% sidenote 1 '《Introduction to Nonlinear Optimization》 at 豆瓣: [http://book.douban.com/subject/26551626/](http://book.douban.com/subject/26551626/) and at Amazon: [http://www.amazon.com/Introduction-Nonlinear-Optimization-Algorithms-Applications/dp/1611973643/](http://www.amazon.com/Introduction-Nonlinear-Optimization-Algorithms-Applications/dp/1611973643/)' %} by Amir Beck {% sidenote 2 'Amir Beck is an associate professor at The Technion—Israel Institute of Technology： [http://iew3.technion.ac.il/Home/Users/becka.html](http://iew3.technion.ac.il/Home/Users/becka.html)' %}。澄清了一些过去曾经误解的概念。MOS-SIAM Series on Optimization{%sidenote 3 'MOS-SIAM Series on Optimization: [http://bookstore.siam.org/mos-siam-series-on-optimization/](http://bookstore.siam.org/mos-siam-series-on-optimization/)'%} 一系列优化的书都不错。连着借了三本，希望以后都能好好读完。现在这本非线性优化暂时只是翻完了，习题都没做，感觉习题也都挺有用的。

<!--more-->

## Table of Content 目录

**1.** Mathematical Preliminaries 数学基础
**2.** Optimality Conditions for Unconstrained Optimization 无约束优化问题的优化条件
**3.** Least Squares 最小二乘问题
**4.** The Gradient Method 梯度下降法
**5.** Newton's Method 牛顿法
**6.** Convex Sets 凸集
**7.** Convex Functions 凸函数
**8.** Convex Optimization 凸优化
**9.** Optimization over a Convex Set 凸集上的优化问题
**10.** Optimality Conditions for Linearly Constrained Problems 线性约束问题的优化条件
**11.** The KKT Conditions 库恩塔克条件
**12.** Duality 对偶问题

## 第一章 数学基础

**Definition 1.1 内积** inner product {%m%}\langle\cdot,\cdot\rangle:=\Re^n \times \Re^n \to \Re{%em%}

**1. 对称性** symmetry {% m %}\langle{\bf x},{\bf y}\rangle=\langle{\bf y},{\bf x}\rangle{% em %} 对于任何 {% m %}{\bf x},{\bf y} \in \Re^n {% em %}

**2. 可加性** additivity {%m%}\langle{\bf x},{\bf y}+{\bf z}\rangle=\langle{\bf x},{\bf y}\rangle+\langle{\bf x},{\bf z}\rangle{%em%} 对于任何 {% m %}{\bf x},{\bf y},{\bf z} \in \Re^n {% em %}

**3. 线性** homogeneity {%m%}\langle\lambda{\bf x},{\bf y}\rangle=\lambda\langle{\bf x},{\bf y}\rangle{%em%} 对于任何 {%m%}\lambda\in \Re {%em%} 及 {%m%}{\bf x},{\bf y} \in \Re^n{%em%}

**4. 正定性** positive definiteness 对于任意 {%m%}{\bf x}\in \Re^n{%em%}， {%m%}\langle{\bf x},{\bf x}\rangle\ge0{%em%}；当且仅当 {%m%}{\bf x}={\bf 0}{%em%} 时，{%m%}\langle{\bf x},{\bf x}\rangle=0{%em%}。 {%m%}\tag*{$\blacksquare$}{%em%}

**Example 1.2 最常见的内积就是点积** dot product
{%math%}\langle{\bf x},{\bf y}\rangle={\bf x}^T{\bf y}=\sum^n_{i=1}x_iy_i \text{ for any } {\bf x},{\bf y} \in \Re^n {%endmath%}
点积是标准内积，当不明确说明时，默认内积就是点积。{%m%}\tag*{$\blacksquare$}{%em%}

**Example 1.3 加权点积** weighted dot norm 是 {% m %}\Re^n {% em %} 空间中另一个内积的例子，其中权重 {% m %}{\bf w}\in \Re^n_{++} {% em %}。
{% math%} \langle {\bf x},{\bf y} \rangle_{\bf w} = \sum^n_{i=1}w_ix_iy_i \; \tag*{$\blacksquare$}{% endmath %}

**Definition 1.4 范数** Norm 一个定义在实数向量集 {% m %}\Re^n {% em %} 上的范数 {% m %}\|\cdot\| {% em %} 是一个满足如下条件，形如 {% m %}\| \cdot \| : \Re^n \to \Re {% em %} 的函数

**1. 非负性** nonnegativity {% m %} \|{\bf x}\| \ge 0 \text{ for any } {\bf x} \in \Re^n \text{ and } \|{\bf x}\| = 0 \text{ if and only if } {\bf x} = {\bf 0} {% em %}

**2. 正线性** positive homogeneity {% m %} |\lambda {\bf x}\| = |\lambda| \|{\bf x}\| \text{ for any } {\bf x} \in \Re^n \text{ and } \lambda \in \Re{% em %}

**3. 三角不等** triangle inequality  {% m %} \|{\bf x} + {\bf y}\| \le \|{\bf x}\| + \|{\bf y}\| \text{ for any } {\bf x},{\bf y} \in \Re^n{% em %}

相应的，{% m %} p {% em %} 范数 p-norm 定位为
{% math %} \ell_p \equiv \|{\bf x}\|_p \equiv \sqrt[p]{\sum^n_{i=1}|x_i|^p} \text{ , for }  p \ge 1 {% endmath%}

类似的，无穷范数 {% m %}\infty {% em %} 定义为
{% math %} \|{\bf x}\|_{\infty} \equiv \max_{i=1,2,\cdots,n}|x_i|=\lim_{p \to \infty} \|{\bf x}\|_p \;{% endmath%}
即最大绝对值。

1-范数 1-norm {%m%}\|{\bf x}\|_1{%em%} 即为绝对值之和 {%m%}\sum^n_{i=1}|x_i|{%em%}。 {%m%}\tag*{$\blacksquare$}{%em%}

**Lemma 1.5 柯西 - 施瓦茨不等式** Cauchy-Schwarz inequality {% m %} \text{ For any } {\bf x}, {\bf y} \in \Re^n,{% em %}
{% math %}|{\bf x}^T{\bf y}| \le \|{\bf x}\|_2 \cdot \|{\bf y}\|_2 {% endmath %}

等号在且仅在 {%m%}{\bf x}{%em%} 和 {%m%}{\bf y}{%em%} 线性相关时成立。 {%m%}\tag*{$\blacksquare$}{%em%}

**Definition 1.6 矩阵的范数** matrix norms 一个定义在{%m%}\Re^{m \times n}{%em%} 空间上的范数 {%m%}\|\cdot\|{%em%} 是一个形如 {%m%}\|\cdot\|:\Re^{m \times n} \to \Re{%em%}，且满足如下性质的函数。

**1. 非负性** nonnegativity 对于任意 {%m%}{\bf A} \in \Re^{m \times n}{%em%}, {%m%}\|{\bf A}\| \ge 0{%em%}；同时，当且仅当 {%m%}{\bf A} = {\bf 0}{%em%} 时，{%m%}\|{\bf A}\| = 0{%em%}。

**2. 正线性** positive homogeneity 对于任意 {%m%}{\bf A} \in \Re^{m \times n}{%em%} 和 {%m%}\lambda \in \Re{%em%}，{%m%}\|\lambda{\bf A}\| = |\lambda| \cdot \|{\bf A}\|{%em%}。

**3. 三角不等式** triangle inequality 对于任意 {%m%}{\bf A},{\bf B} \in \Re^{m \times n}{%em%}，{%m%}\|{\bf A} + {\bf B}\| \le \|{\bf A}\| + \|{\bf B}\|{%em%}。

常见的 induced matrix norm {%m%}\| \cdot \|_{a,b}{%em%} 定义如下。给定一个矩阵 {%m%}{\bf A} \in \Re^{m \times n}{%em%} 和分别定义在 {%m%}\Re^n{%em%} 及 {%m%}\Re^m{%em%} 上的两个范数 {%m%}\| \cdot \|_a{%em%} 和 {%m%}\| \cdot \|_b{%em%}，{%m%}\| {\bf A} \|_{a,b}{%em%} 即为

{% math %}\| {\bf A} \|_{a,b} = \max_{\bf x}\{ \| {\bf Ax} \|_b : \| {\bf x} \|_a \le 1 \} {% endmath %}

从定义可以看出，对于任意 {%m%}{\bf x} \in \Re^n{%em%} 以下不等式均成立

{% math %}\| {\bf Ax} \|_b = \| {\bf A} \|_{a,b}  \| {\bf x} \|_a \tag*{$\blacksquare$}{% endmath %}

**Example 1.7 谱范数** spectral norm
{%m%}\tag*{$\blacksquare$}{%em%}

**Example 1.8 1-范数** 1-norm 又称为最大列绝对值和范数
{%m%}\tag*{$\blacksquare$}{%em%}

**Example 1.9 无穷范数** {%m%}\inf{%em%}-norm 又称为最大行绝对值和范数
{%m%}\tag*{$\blacksquare$}{%em%}

Frobenius 范数是一个非 induced 范数的矩阵范数的例子，定义如下。

{% math %}\| {\bf A} \|_F = \sqrt{\sum^m_{i=1} \sum^n_{j=1}A^2_{ij}}, \; {\bf A} \in \Re^{m \times n} \tag*{$\blacksquare$}{% endmath %}