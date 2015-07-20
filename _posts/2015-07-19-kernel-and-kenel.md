---
layout: post
title:  "Kernel and Kernel: Reproducing Kernel Hilbert Space and Kernel Method"
date:   2015-07-19 09:22:53
categories:
---

## Kernel

再生核的定义

Definition. {% m %}k: \mathcal{X} \times \mathcal{X} \rightarrow \Re {% em %} is a kernel if

1. 核函数 {% m %}k{% em %}  对称 isymmetric: {% m %}k(x,y)=k(y,x){% em %}.
2. 核函数 {% m %}k{% em %} 半正定 positive semi-definite, i.e., {% m %}\forall x_1, x_2, \ldots , x_n \in \mathcal{X}{% em %}, the "Gram Matrix" {% m %}K{% em %} defined by {% m %}K_{ij} =  k(x_i,x_j){% em %} is positive semi-definite. (A matrix {% m %}M \in \Re^{n \times n}{% em %} is positive semi-definite if {% m %}\forall a \in \Re^n{% em %}, {% m %}a' M a \ge 0{% em %}.)

<!--more-->

再生核希尔贝特空间是从低维数据到函数泛函映射。Hilbert 空间“Frechet-Riesz”表现定理。

希尔贝特空间是定义了内积的空间；相对应的 Banach 是定义了范数的空间。

## Reproducing Kernel Feature Map

再生核特征映射

{% math %}\Phi_x(\cdot) \triangleq k(\cdot,x) {% endmath %}

即对任意线性泛函{% m %} \Phi(\cdot) {% em %}, {% m %} \exists x_\Phi \in H {% em %}, 使得 {% m %} \Phi(\cdot) = (\cdot, x_\Phi) {% em %}

To be continued...