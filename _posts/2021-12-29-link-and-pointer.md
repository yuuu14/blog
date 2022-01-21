---
layout: post
title: link-and-pointer
date: 2021-12-29 14:29 +0800
tags: coding
---

## add pointer (next) to rightmost node in binary tree
Given perfect binary tree (inner nodes always have 2 children),
for each inner node `p`, find that 
`p->left->next = p->right` and `p->right->next = p->next ? p->next->left : nullptr`


## delete middle node in link (where index=size/2)
Using 2 pointers, `it` and `jump`, `it` goes to next node while `jump` steps twice.
Init `it` to the `head` and `jump` the second node `head->next`.
Keep going while `jump` is neither the last node nor the second last.
