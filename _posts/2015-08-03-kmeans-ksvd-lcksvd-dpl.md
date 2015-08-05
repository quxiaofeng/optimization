---
layout: post
title:  "K-means, K-SVD, LC-KSVD and DPL"
date:   2015-08-03 22:46:53
categories:
---

从 K-means 到 [K-SVD](http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf){% sidenote 1 'M. Aharon, M. Elad, and A.M. Bruckstein, "The K-SVD: An Algorithm for Designing of Overcomplete Dictionaries for Sparse Representation", the IEEE Trans. On Signal Processing, Vol. 54, no. 11, pp. 4311-4322, November 2006. [http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2004/32_KSVD_IEEE_TSP.pdf)' %}{% sidenote 2 'O. Bryt and M. Elad, Compression of Facial Images Using the K-SVD Algorithm, Journal of Visual Communication and Image Representation, Vol. 19, No. 4, Pages 270-283, May 2008. [http://www.cs.technion.ac.il/~elad/publications/journals/2007/FaceCompress_KSVD_JVCIR.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2007/FaceCompress_KSVD_JVCIR.pdf)' %}{% sidenote 3 'R. Rubinstein, T. Peleg and M. Elad, Analysis K-SVD: A Dictionary-Learning Algorithm for the Analysis Sparse Model, IEEE Trans. on Signal Processing, Vol. 61, No. 3, Pages 661-677, March 2013. [http://www.cs.technion.ac.il/~elad/publications/journals/2011/Analysis-KSVD-IEEE-TSP.pdf](http://www.cs.technion.ac.il/~elad/publications/journals/2011/Analysis-KSVD-IEEE-TSP.pdf)' %}，到 [LC-KSVD](http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html){% sidenote 4 'Zhuolin Jiang, Zhe Lin, Larry S. Davis. "Label Consistent K-SVD: Learning A Discriminative Dictionary for Recognition". IEEE Transactions on Pattern Analysis and Machine Intelligence, 2013, 35(11): 2651-2664. [http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html](http://www.umiacs.umd.edu/~zhuolin/projectlcksvd.html)' %}，到 [DPL](http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian){% sidenote 5 'Gu, S., Zhang, L., Zuo, W., & Feng, X. (2014). Projective dictionary pair learning for pattern classification. In Z. Ghahramani, M. Welling, C. Cortes, N. D. Lawrence, & K. Q. Weinberger (Eds.), Advances in Neural Information Processing Systems 27 (pp. 793–801). Curran Associates, Inc. [http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian](http://papers.nips.cc/paper/5600-spectral-clustering-of-graphs-with-the-bethe-hessian)' %}。

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

<!--more-->

{%m%}{%em%}

{% math %} {% endmath %}
