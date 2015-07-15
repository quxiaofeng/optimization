---
layout: post
title:  "Introduction to Nonlinear Optimization"
date:   2015-07-15 21:22:17
categories:
---

昨天晚上到今天，看完了一本之前一直看不完的书 《Introduction to Nonlinear Optimization》{% sidenote 1 '《Introduction to Nonlinear Optimization》 at 豆瓣: [http://book.douban.com/subject/26551626/](http://book.douban.com/subject/26551626/) and at Amazon: [http://www.amazon.com/Introduction-Nonlinear-Optimization-Algorithms-Applications/dp/1611973643/](http://www.amazon.com/Introduction-Nonlinear-Optimization-Algorithms-Applications/dp/1611973643/)' %} by Amir Beck {% sidenote 2 'Amir Beck is an associate professor at The Technion—Israel Institute of Technology： [http://iew3.technion.ac.il/Home/Users/becka.html](http://iew3.technion.ac.il/Home/Users/becka.html)' %}。澄清了一些过去曾经误解的概念。MOS-SIAM Series on Optimization 一系列优化的书都不错。连着借了三本，希望以后都能好好读完。现在这本非线性优化暂时只是翻完了，习题都没做，感觉习题也都挺有用的。

<!--more-->

## Table of Content 目录

1. Mathematical Preliminaries 数学基础
2. Optimality Conditions for Unconstrained Optimization 无约束优化问题的优化条件
3. Least Squares 最小二乘问题
4. The Gradient Method 梯度下降法
5. Newton's Method 牛顿法
6. Convex Sets 凸集
7. Convex Functions 凸函数
8. Convex Optimization 凸优化
9. Optimization over a Convex Set 凸集上的优化问题
10. Optimality Conditions for Linearly Constrained Problems 线性约束问题的优化条件
11. The KKT Conditions 库恩塔克条件
12. Duality 对偶问题

## 第一章 数学基础

Definition 1.1 内积 inner product

{% m %} \langle\cdot,\cdot\rangle := \mathbb{R}^n \times \mathbb{R}^n \rightarrow \mathbb{R} {% em %}

1. symmetry {% m %}\langle{\bf x},{\bf y}\rangle=\langle{\bf y},{\bf x}\rangle{% em %} for any {% m %}{\bf x},{\bf y} \in \mathbb{R}^n {% em %}
2. additivity {%m%}\langle{\bf x},{\bf y}+{\bf z}\rangle=\langle{\bf x},{\bf y}\rangle+\langle{\bf x},{\bf z}\rangle{%em%} for any {% m %}{\bf x},{\bf y},{\bf z} \in \mathbb{R}^n {% em %}
3. homogeneity {%m%}\langle\lambda{\bf x},{\bf y}\rangle=\lambda\langle{\bf x},{\bf y}\rangle{%em%} for any {%m%}\lambda\in\mathbb{R}{%em%} and {%m%}{\bf x},{\bf y}\in\mathbb{R}^n{%em%}
4. positive definiteness {%m%}\langle{\bf x},{\bf x}\rangle\ge0{%em%} for any {%m%}{\bf x}\in\mathbb{R}{%em%} and {%m%}\langle{\bf x},{\bf x}\rangle=0{%em%} if and only if {%m%}{\bf x}={\bf 0}{%em%}

{%m%}{%em%}
