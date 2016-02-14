---
layout: post
title:  "K-means, K-SVD, LC-KSVD and DPL"
date:   2015-08-03 22:46:53
categories:
---

从 K-means 到 [K-SVD](http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf){% sidenote 1 'M. Aharon, M. Elad, and A.M. Bruckstein, "The K-SVD: An Algorithm for Designing of Overcomplete Dictionaries for Sparse Representation", the IEEE Trans. On Signal Processing, Vol. 54, no. 11, pp. 4311-4322, November 2006. [http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf)' %}{% sidenote 2 'O. Bryt and M. Elad, Compression of Facial Images Using the K-SVD Algorithm, Journal of Visual Communication and Image Representation, Vol. 19, No. 4, Pages 270-283, May 2008. [http://www.cs.technion.ac.il/~elad/publications/journals/2007/FaceCompress_KSVD_JVCIR.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2007/FaceCompress_KSVD_JVCIR.pdf)' %}{% sidenote 3 'R. Rubinstein, T. Peleg and M. Elad, Analysis K-SVD: A Dictionary-Learning Algorithm for the Analysis Sparse Model, IEEE Trans. on Signal Processing, Vol. 61, No. 3, Pages 661-677, March 2013. [http://www.cs.technion.ac.il/~elad/publications/journals/2011/Analysis-KSVD-IEEE-TSP.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2011/Analysis-KSVD-IEEE-TSP.pdf)' %}，到 [LC-KSVD](http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html){% sidenote 4 'Zhuolin Jiang, Zhe Lin, Larry S. Davis. "Label Consistent K-SVD: Learning A Discriminative Dictionary for Recognition". IEEE Transactions on Pattern Analysis and Machine Intelligence, 2013, 35(11): 2651-2664. [http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html](http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html)' %}，到 [DPL](http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian){% sidenote 5 'Gu, S., Zhang, L., Zuo, W., & Feng, X. (2014). Projective dictionary pair learning for pattern classification. In Z. Ghahramani, M. Welling, C. Cortes, N. D. Lawrence, & K. Q. Weinberger (Eds.), Advances in Neural Information Processing Systems 27 (pp. 793–801). Curran Associates, Inc. [http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian](http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian)' %}。

----

**K-means 算法**

任务：通过最近邻寻找能够表达数据样本 {%m%}\{\mathbf{y}_i\}^N_{i=1}{%em%} 的最优编码本（codebook，既字典参数），既求解如下问题

{%math%}\min_{\mathbf{C, X}} \left\{ \|\mathbf{Y} - \mathbf{CX}\|^2_F \right\} \text{ subject to } \forall i \text{, } \mathbf{x}_i = \mathbf{e}_k \text{ for some } k{%endmath%}

<!--more-->

初始化： 设置编码本矩阵 {%m%}\mathbf{C}^{(0)} \in \Re^{n \times K}{%em%}. 设置 {%m%}J=1{%em%}。

循环至收敛 （使用停止规则）

**1.** 稀疏编码阶段：将训练样本 {%m%}{\bf Y}{%em%} 分为如下 {%m%}K{%em%} 个集合。

{%math%}\left( {\bf R}^{(J-1)}_1, {\bf R}^{(J-1)}_2, \cdots, {\bf R}^{(J-1)}_K \right){%endmath%}

每个集合中存放与 {%m%}{\bf c}^{J-1}_k{%em%} 列最相似的样本的索引。

{%math%} {\bf R}^{(J-1)}_k = \left\{ i \mid \forall_{l \neq k}, \|{\bf y}_i - {\bf c}^{(J-1)}_k\|_2 < \|{\bf y}_i - {\bf c}^{(J-1)}_l\|_2  \right\} {%endmath%}

**2.** 编码本更新阶段：{%m%}{\bf C}^{(J-1)}{%em%} 中的任一列 {%m%}k{%em%} 都根据如下公式更新。

{%math%}{\bf c}^{(J)}_k = \frac{1}{|{\bf R}_k|}\sum_{i \in {\bf R}^{(J-1)}_k}{\bf y}_i{%endmath%}

**3.** 令{%m%} J = J + 1 {%em%}

----

K-means 相当于是只使用编码本矩阵中的一列的稀疏表达。又因为只有一列，所以系数为1。其中该列由如下公式确定。

{%math%}\forall_{k \neq j} \; \left\|{\bf y}_i - {Ce}_j \right\|^2_2 \leqslant \left\|{\bf y}_i - {Ce}_k \right\|^2_2{%endmath%}

<!--more-->

Julia Code Highlight Test

{% highlight ruby %}
include("diagadd!.jl")

function updateA!(A::Array{Any,1}, 
                  D::Array{Any,1}, 
                  DataMat::Array{Any,1}, 
                  P::Array{Any,1}, 
                  τ::Float64, 
                  DictSize::Int64)
    # Update tempDictCoef by Eq. (8)

    for i=1:length(A)
        @inbounds TempDict::Matrix{Float64} = D[i]
        @inbounds TempData::Matrix{Float64} = DataMat[i]
        tempDictCoef::Matrix{Float64}       = TempDict' * TempDict
        tempDictDataCoef::Matrix{Float64}   = TempDict' * TempData
        @inbounds C::Matrix{Float64}        = P[i] * TempData
        diagadd!(tempDictCoef, τ)
        fma!(tempDictDataCoef, C, τ)
        @inbounds A[i]                      = tempDictCoef \ tempDictDataCoef
    end
end
{% endhighlight %}
