---
layout: post
title:  "优化问题"
date:   2015-05-20 22:53:20
categories: 优化 稀疏
---
## 优化问题

###  可以用 ALM, LP 和 IRLS 求解的四种常见优化问题

### Question 1

{% math %}\arg\min \|x\|_1\|e\|_1$ subj. to $y=Ax+e{% endmath %}

+ least entropy & error correction
+ 标准 linear programming。
+ 鲁棒的 SRC{% sidenote 1  参见 [http://research.microsoft.com/pubs/132810/PAMI-Face.pdf](http://research.microsoft.com/pubs/132810/PAMI-Face.pdf) and [Face Recognition via Sparse Representation](http://perception.csl.illinois.edu/recognition/Home.html) %}。使用单位矩阵作为遮挡字典，用标准形式求解。

### Question 2

{% math %}\arg\min \|x\|_2\|e\|_1$ subj. to $y=Ax+e{% endmath %}

+ least energy & error correction
+ 鲁棒的 CRC

### Question 3

{% math %}\arg\min \|x\|_1\|e\|_2$ subj. to $y=Ax+e{% endmath %}

+ sparse regression with noise - lasso
+ 标准 lasso 问题
+ 标准的 SRC

### Question 4

{% math %}$\arg\min \|x\|_2\|e\|_2$ subj. to $y=Ax+e{% endmath %}

+ least energy with noise
+ 极小最小二乘解，可求广义逆。
+ CRC，用二范数约束表示系数，有解析解。