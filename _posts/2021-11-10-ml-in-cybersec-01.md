---
layout: post
title: Evasion Attacks 
date: 2021-11-10 12:59 +0800
---

# Intro
network is fed an "adversarial"
$\delta = \arg\min \mathbf{E}\[\max L(\theta, x+\delta, y)\]$

# FGSM
Fast Gradient Sign Method [2]

## Attack
1. calculate loss $L$ after FP
2. calculate $\nabla$ with respect to the pixel of image 
$\bigg(f(x+1, y) - f(x, y), f(x, y+1) - f(x,y)\bigg)$ [1]
3. adjust image pixels slightly in direction of the calculated $\nabla$ to
maximize $L$ from 1.
$x + \epsilon \cdot \text{sign}(\nabla\_x L(\theta, x, y))$
```
w -= lr * grad
disturbed_image = image +  epsilon * sign(grad) # [3] 
```

## Defense


# Reference
[1] https://blog.csdn.net/saltriver/article/details/78987096  
[2] https://neptune.ai/blog/adversarial-attacks-on-neural-networks-exploring-the-fast-gradient-sign-method  
[3] https://pytorch.org/tutorials/beginner/fgsm_tutorial.html  

