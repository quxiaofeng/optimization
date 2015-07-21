---
layout: post
title:  "稀疏编码的优化问题"
date:   2015-05-21 00:33:45
categories:
---

稀疏编码问题：  {% m %} \arg\min_x f(x)\left\|y-Ax\right\|^2+ \lambda\|x\|_1 {% em %}

用 alternating minimization (ADM)

Primal-dual 算法

Soft threshold 

<!--more-->

字典学习 K-SVD

看完 K-SVD 之后，图像分类: Discriminative K-SVD for Dictionary Learning in Face Recognition (CVPR)，Label Consistent K-SVD Learning a Discriminative Dictionary for Recognition （TPAMI）；结构化稀疏: Robust Classiﬁcation using Structured Sparse Representation （CVPR）；低秩: Learning Structured Low-rank Representations for Image Classiﬁcation （CVPR）。

关于稀疏表示的已有算法的分析: A survey of sparse representation: algorithms and applications

参考林倞老师{% sidenote 1 '[林倞教授 中山大学计算机科学](http://ss.sysu.edu.cn/~ll/)'%} NIPS, ACML 和 ML 一系列工作的报告。基本上 ADM 及其扩展都介绍到了。

{% newthought '迭代优化'%}

{% m %}\sum_{i=1}^p\left\|y^{(i)}-A\cdot x^{(i)}\right\|_2^2 + \sum_{i=1}^p S\left(x^{(i)}\right) {% em %}

凸的稀疏模型求基于 proximal operator 的 alternating minimization。参考 boyd 的文章。

An ADMM Solution to the Sparse Coding Problem: {% sidenote 2 '[http://stanford.edu/class/ee364b/projects/2011projects/reports/bhaskar_zou.pdf](http://stanford.edu/class/ee364b/projects/2011projects/reports/bhaskar_zou.pdf)' %}

[http://www.eecs.berkeley.edu/~yang/software/l1benchmark/](http://www.eecs.berkeley.edu/~yang/software/l1benchmark/)

这篇文章 {% sidenote 3 '[http://web.stanford.edu/~boyd/papers/prox_algs.html](http://web.stanford.edu/~boyd/papers/prox_algs.html)' %} 从 proximal operator 角度讲解，更加深入一点。

南京大学何炳生老师的课程 {% sidenote 4 '[http://math.nju.edu.cn/~hebma/](http://math.nju.edu.cn/~hebma/)' %}，讲得比较深入。

biconvex 问题，基本是个保证收敛的算法效果就还行。