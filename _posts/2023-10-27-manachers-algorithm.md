---
layout: post
title: Manacher's Algorithm
date: 2023-10-27 23:36 +0200
tags: string coding
use_math: true
---


Manacher proposed an algorithm for finding all "inital leftmost"[1] palidromes with $O(n)$ time complexity. With modification it could be applied to substrings started anywhere. The main idea is to use the symmetric property of palidrome. For palindrome $p$, if there exists a palindrome $q$ before its center, then there must be an exactly same palindrome $s = q$ after the center, e.g., $p$ is the longest palindrome at the beginning of certain string, 
$p = \color{red}{\texttt{b.a.b}}\color{yellow}{\texttt{.c.}}\color{green}{\texttt{b.a.b}}$, and before the center $\color{yellow}{\texttt{c}}$, there is a palindrome $q = \color{red}{\texttt{b.a.b}}$, symmetrically, after $\color{yellow}{\texttt{c}}$, there is another palindrome $s = \color{green}{\texttt{b.a.b}}$. 

Notice the dots added between chars. Since the length of $p$ is odd, so the center is a char, if it is even, then it would be impractical to represent the center. Adding separators solves this problem, the center for palindrome with even length becomes the separator. And to identify the location of a palindrome, knowing its center and radius (length from the center to each end) would be sufficient. For $p$, its center is $\color{yellow}{\texttt{c}}$, its radius is 3, (for simplicity here ignore the separators).

Considering more general cases. If $p$ is not at the beginning of a string, assume there is a $\color{orange}{\texttt{c}}$ before $p$, the beginning of this new string becomes
$\color{orange}{\texttt{c.}}\color{red}{\texttt{b.}}\color{orange}{\texttt{a}}\color{red}{\texttt{.b}}\color{yellow}{\texttt{.c.}}\color{green}{\texttt{b.a.b}}$. Notice that $q$ could be extended to $q_1 = \color{orange}{\texttt{c.b.a.b.c}}$, with center $\color{orange}{\texttt{a}}$ and radius = 2. How can we decide the radius for the $\color{green}{\texttt{a}}$ now? Since $q_1$ is clearly not the substring of $p$, we can infer the next char after $p$ cannot be $\texttt{c}$, otherwise $p$ could be extended further, and it would not be the longest palindrome with center of $\color{yellow}{\texttt{c}}$, i.e., $\color{orange}{\texttt{c.}}\color{red}{\texttt{b.}}\color{orange}{\texttt{a}}\color{red}{\texttt{.b}}\color{yellow}{\texttt{.c.}}\color{green}{\texttt{b.a.b}}\color{#00B3B8}{\texttt{.x}}$ where $\color{#00B3B8}{\texttt{x}}$ $\neq$  $\texttt{c}$. So the radius of $\color{green}{\texttt{a}}$ would be equal to the distance from itself to the right bound of $p$, i.e, from $\color{green}{\texttt{a}}$ to the second $\color{green}{\texttt{b}}$.

Now, if $q$ is the substring of $p$ and it is already the longest palindrome with this center, what would happen? If the center is within the bound (exclusively), e.g. the second $\color{red}{\texttt{b}}$ before $\color{yellow}{\texttt{c}}$, then $s$ would have the same radius with $q$ (the first $\color{green}{\texttt{b}}$ after $\color{yellow}{\texttt{c}}$). If it shares the left bound with $p$, then it is unclear whether $s$ could be extended furthermore, e.g., $\color{red}{\texttt{b.a.b}}\color{yellow}{\texttt{.c.}}\color{green}{\texttt{b.a.b}}\color{#F49EC4}{\texttt{.y}}$ where $\color{#F49EC4}{\texttt{y}}$ could be $\texttt{c}$, in this case we can start with current radius (which is 1) and increase it without violating the requirement of being palindrome.


## Algorithm
Python implementation for pseudocode[2]. 
```python
def longestPalindrome(s: str) -> str:
    s1 = f"|{'|'.join(s)}|"
    n = len(s1)
    longest_radius = [0] * n
    center = radius = 0
    while center < n:
        while center - radius - 1 >= 0 and center + radius + 1 < n \
                and s1[center - radius - 1] == s1[center + radius + 1]:
            radius += 1
        longest_radius[center] = radius
        old_center = center
        old_radius = radius
        center += 1

        radius = 0
        right_bound = old_center + old_radius
        while center <= right_bound:
            mirrored = 2 * old_center - center
            center2bound = right_bound - center
            if longest_radius[mirrored] < center2bound:
                longest_radius[center] = longest_radius[mirrored]
                center += 1
            elif longest_radius[mirrored] > center2bound:
                longest_radius[center] = center2bound
                center += 1
            else:
                radius = center2bound
                break

    longest_r = max(longest_radius)
    center = longest_radius.index(longest_r)
    start = (center - longest_r) // 2
    end = (center + longest_r) // 2
    return s[start:end]

```


## Reference
[1] Manacher, *A New Linear-Time "On-Line" Algorithm for Finding the Smallest Initial Palindrome of a String*  
[2] https://en.wikipedia.org/wiki/Longest_palindromic_substring#Manacher's_algorithm