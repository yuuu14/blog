---
layout: post
title: Notes on Rational Neural Machines
date: 2021-11-05 13:02 +0800
tags: paper-reading
---

write some formula:  
$\mathbb{P}(c|x) = \frac{\mathbb{P}(x|c) \times \mathbb{P}(c)}{\sum_{i}^{N}\mathbb{P}(x|c)}$


I am taking one seminar this sememster, *Hybrid Learning*. The topic I was assigned with is about models
combining deep learning and reasoning, called *Rational Neural Machines* as the same name of this paper.
This post contains some of my thoughts after reading it.

# Intro 
Why
Deep Neural Networts ignore reasoning process
probabilistic logic not scalable on sensory data

so combine them


what is **Markov Logic**  
to make machine think logically, to solve following:
- evaluation: to evaluate how logical a possibility is based on the KB
- inference: to evaluate all possibilities and find the most logical one
- training: to learn the KB

KB: a set of Formular  
Formular: first order predicate  
$p \rightarrow q, \cdots$  
logic operation: $\neg, \land, \lor, \rightarrow, \leftrightarrow$  
grounding: use all constants to substitute variables


