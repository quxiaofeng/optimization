---
layout: post
title:  "几个基本优化问题"
date:   2015-05-20 22:53:20
categories:
---

可以用 ALM{% sidenote 1 'Augmented Lagrange Multiplier 增广拉格朗日乘子法' %}, LP{% sidenote 2 'Linear Programming 线性规划' %} 和 IRLS {% sidenote 3 '[Iteratively Reweighted Least Squares](http://www.robotics.stanford.edu/~ang/papers/aaai06-efficientL1logisticregression.pdf)' %} 求解的四种基本优化问题

### Question 1

{% newthought 'least entropy & error correction' %}

Question 1: {% m %} \arg \min \|x\|_1 + \|e\|_1 {% em %} subj. to {% m %} y=Ax+e {% em %}

标准 linear programming

鲁棒的 *SRC*{% sidenote 4  '参见 [http://research.microsoft.com/pubs/132810/PAMI-Face.pdf](http://research.microsoft.com/pubs/132810/PAMI-Face.pdf) and [Face Recognition via Sparse Representation](http://perception.csl.illinois.edu/recognition/Home.html)' %}。使用单位矩阵作为遮挡字典，用标准形式求解。

<!--more-->

### Question 2

+ least energy & error correction

Question 2: {% m %} \arg\min \|x\|_2 + \|e\|_1 {% em %} subj. to {% m %} y=Ax+e {% em %}

+ 鲁棒的 CRC

### Question 3

+ sparse regression with noise - lasso

Question 3:  {% m %} \arg\min \|x\|_1 + \|e\|_2 {% em %} subj. to {% m %} y=Ax+e {% em %}

+ 标准 lasso 问题
+ 标准的 SRC

### Question 4

+ least energy with noise

Question 4: {% m %} \arg\min \|x\|_2 + \|e\|_2 {% em %} subj. to {% m %} y=Ax+e {% em %}

+ 极小最小二乘解，可求广义逆。
+ CRC，用二范数约束表示系数，有解析解。