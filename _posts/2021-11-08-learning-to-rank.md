---
layout: post
title: To Rank from Pairwise to Listwise
date: 2021-11-08 17:44 +0800
---
 

# Intro and Criterion
criterion [1]
- CG (cumulative gain)  
$\textbf{CG}\_p = \sum\_{i=1}^{p} rel\_i$
, where $rel_{i}$ represents the relativity of position i.

- DCG (Discounted CG)  
$\textbf{DCG} \_p = \sum\_{i=1}^{p} \frac{rel\_i}{\log\_2 (i+1)}$  
$\textbf{DCG} \_p = \sum\_{i=1}^{p} \frac{2^{rel\_i}-1}{\log\_2 (i+1)}$
  get stronger emphasis on retrieving relevant documents  

  meaning: ranking $\downarrow$ $\rightarrow$ impotance $\downarrow$.

- NDGG (Normalized DCG)  
$\textbf{nDCG} \_p = \sum \_{i=1}^{p} = \frac{\textbf{DCG}\_p}{\textbf{IDCG}\_p}$, 
where $\textbf{IDCG}\_p = \sum\_{i=1}^{|\text{REL}|}\frac{2^{rel\_i}-1}{log\_2 (i+1)}$  
$|\text{REL}|$: sort by relevance in corpus descendingly, choose top-p results.

# Alg
## RankNet
Problem: given query $q$, compare relevance between $doc\_i$ $doc\_j$  
Denote $s = f(x;w)$ a scoring function, $x$ is the feature of $doc$, $w$ weight.
Then we have $s\_i = f(x\_i;w)$, $s\_j = f(x\_j;w)$  
Next, define prob that $d\_i$ more relevant than $d\_j$   
$\qquad\mathbf{P}(d\_i > d\_j) = \frac{1}{1 + e^{-\sigma (s\_i-s\_j)}} \rightarrow $ to train $\sigma$  
True prob - $\overline{\mathbf{P}}\_{ij} = \frac{1+S\_{ij}}{2}$, $S\_{ij} = {1, -1, 0}$  
Loss $\rightarrow$ choose Cross Entropy loss: 
$C = \mathbf{\overline P}\_{ij}\log \mathbf{P}\_{ij} - (1-\mathbf{\overline P\_{ij}})\log (1-\mathbf{P}\_{ij}))$

# Reference
[1] https://www.6aiq.com/article/1593872372312

