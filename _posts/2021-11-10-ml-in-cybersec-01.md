---
layout: post
title: Evasion Attacks 
date: 2021-11-10 12:59 +0800
tags: security deep-learning
---

# Intro
network is fed an "adversarial"  
aim: $\delta = \arg\min \mathbf{E}\bigg[\max L(\theta, x+\delta, y)\bigg]$

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
grad = image.data.grad
perturbed_image = image +  epsilon * sign(grad) # [3] 
```

## Defense
- brute force solution [4]  
generate a lot of adversarial examples and train model
- defensive distillation [4][5][6]
    - Given trainset $(X, Y)$
    - Two net: original $f$ and distilled model $f'$ (simpler architecture)  
    - For net $f$, get output $f(X)$, then do softmax with temperature $T>1$
    - For net $f'$, similarly, get output $f'(X)$, softmax with $T$
    - soft loss is between two output logits after softmax with $T$
    - hard loss is between $f'(X)$ after softmax $(T=1)$ and true labels $Y$
    - inference is with net $f'$ and softmax with $T=1$ 
 
```python
ori_outputs = model(inputs)
dst_outputs = distilled_model(inputs)
ori_outputs_sft = softmax(ori_outputs / T) 
dst_outputs_sft = softmax(dst_outputs / T) 

loss = loss_soft(ori_outputs_sft, dst_outputs_sft.detach())  # BCELoss
loss += loss_hard(dst_outputs, labels)  # CrossEntropyLoss
```
- generative adversarial learning  
$\min \Bigg\\\{ \alpha \cdot L(\theta, x, y) + (1-\alpha) \cdot 
L\bigg(\theta, x+\epsilon \cdot \text{sign}(\nabla\_x L(\theta, x, y)), y \bigg) \Bigg\\\}$

# I-FGSM attack
Iterative FGSM  

$x^{(n+1)} = clamp\_{x, \xi} \bigg( x^{(n)} + 
\epsilon \cdot \text{sign}(\nabla\_x L(\theta, x^{(n)}, y)) \bigg), x^{(0)}$


# Reference
[1] https://blog.csdn.net/saltriver/article/details/78987096  
[2] *Adversarial Attacks on Neural Networks: Exploring the Fast Gradient Sign Method*,
[https://neptune.ai/blog/adversarial-attacks-on-neural-networks-exploring-the-
fast-gradient-sign-method](https://neptune.ai/blog/adversarial-attacks-on-
neural-networks-exploring-the-fast-gradient-sign-method)  
[3] *Adversarial Example Generation*, 
[https://pytorch.org/tutorials/beginner/fgsm_tutorial.html](
https://pytorch.org/tutorials/beginner/fgsm_tutorial.html)  
[4] *Attacking Machine Learning with Adversarial Examples*,
[https://openai.com/blog/adversarial-example-research/](
https://openai.com/blog/adversarial-example-research/)  
[5] *Adversarial Example Attack and Defense*, 
[https://github.com/as791/Adversarial-Example-Attack-and-Defense](
https://github.com/as791/Adversarial-Example-Attack-and-Defense)  
[6]  
