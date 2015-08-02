---
layout: post
title:  "非线性最优化基础 by Masao Fukushima"
date:   2015-08-02 14:33:54
categories:
---

非线性最优化基础 by Masao Fukushima {% sidenote 1 '非线性最优化基础（豆瓣链接：[http://book.douban.com/subject/6510671/](http://book.douban.com/subject/6510671/)） by Masao Fukushima （个人主页：[http://www.seto.nanzan-u.ac.jp/~fuku/fuku-e.html](http://www.seto.nanzan-u.ac.jp/~fuku/fuku-e.html)）' %}

该文为[冯象初教授](http://web.xidian.edu.cn/xcfeng/){% sidenote 2 '冯象初，教授，博导，西安电子科技大学数学系。个人主页：[http://web.xidian.edu.cn/xcfeng/](http://web.xidian.edu.cn/xcfeng/)' %}有关非线性最优化的讲座的笔记。

**主要内容**

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
{% math %} graph \; f = \left\lbrace ({\bf x}, \beta)^T \in \Re^{n+1} \mid \beta = f({\bf x}) \right\rbrace, {% endmath %}
为 {%m%}f{%em%} 的图像（graph），而称位于 {%m%}f{%em%} 的图像上方的点的全体构成的集合
{% math %}epi \; f =\left\lbrace ({\bf x}, \beta)^T \in \Re^{n+1} \mid \beta \ge f({\bf x}) \right\rbrace{% endmath %}
为 {%m%}f{%em%} 的上图（epigraph）。若上图 {%m%}epi \; f{%em%} 为凸集，则称 {%m%}f{%em%} 为**凸函数**(convex function)。

**定理**：设 {%m%} \mathcal{I} {%em%} 为任意非空指标集，而 {%m%}f_i : \Re^n \to [-\infty, +\infty] \; (i \in \mathcal{I}){%em%} 均为凸函数，则由
{% math %} f({\bf x}) = \sup \left\lbrace f_i({\bf x}) \mid i \in \mathcal{I} \right\rbrace{% endmath %}
定义的函数 {%m%}f : \Re^n \to [-\infty, +\infty] {%em%} 为凸函数。进一步，若 {%m%}\mathcal{I}{%em%} 为有限指标集，每个 {%m%}f_i{%em%} 均为正常的凸函数，并且 {%m%}\cap_{i \in \mathcal{I}} \; dom \; f_i \neq \varnothing {%em%}，则 {%m%}f{%em%} 为正常凸函数。

{%m%}{%em%}

{% math %} \tag*{$\blacksquare$} {% endmath %}
