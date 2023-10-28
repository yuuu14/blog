---
layout: post
title: Manacher's Algorithm
date: 2023-10-27 23:36 +0200
tags: string
mathjax: true
---

$\colorbox{yellow}{a}$

$\color{red}{x}$


Manacher proposed an algorithm for finding all "inital leftmost"[1] palidromes with $O(n)$ time complexity. With modification it could be applied to substrings started anywhere. The main idea is to use the symmetric property of palidrome. For palindrome $p$, if there exists a palindrome $q$ before its center, then there must be an exactly same palindrome $s = q$ after the center, e.g., $p$ is the longest palindrome at the beginning of certain string, 
$p = \textcolor{red}{\texttt{b.a.b}}\texttt{.}\textcolor{yellow}{\texttt{c}}\texttt{.}\textcolor{green}{\texttt{b.a.b}}$, and before the center $\textcolor{yellow}{\texttt{c}}$, there is a palindrome $q = \textcolor{red}{\texttt{b.a.b}}$, symmetrically, after $\textcolor{yellow}{\texttt{c}}$, there is another palindrome $s = \textcolor{green}{\texttt{b.a.b}}$. 

Notice the dot added between chars. Since the length of $p$ is odd, so the center is a char, if it is even, then it would be impractical to represent the center. Adding separators solves this problem, the center for palindrome with even length becomes the separator. And to identify the location of a palindrome, knowing its center and radius (length from the center to each end) would be sufficient. For $p$, its center is $\textcolor{yellow}{\texttt{c}}$, its radius is 3, (for simplicity here ignore the separators).

Considering more general cases. If $p$ is not at the beginning of a string, assume there is a $\textcolor{orange}{\texttt{c}}$ before $p$, the beginning of this new string becomes
$\textcolor{orange}{\texttt{c}}\texttt{.}\textcolor{red}{\texttt{b}}\texttt{.}\textcolor{orange}{\texttt{a}}\texttt{.}\textcolor{red}{\texttt{b}}\texttt{.}\textcolor{yellow}{\texttt{c}}\texttt{.}\textcolor{green}{\texttt{b.a.b}}$. Notice that $q$ could be extended to $q_1 = \textcolor{orange}{\texttt{c.b.a.b.c}}$, with center $\textcolor{orange}{\texttt{a}}$ and radius = 2. How can we decide the radius for the $\textcolor{green}{\texttt{b}}$ now? Since $q_1$ is clearly not the substring of $p$, the radius of $\textcolor{green}{\texttt{b}}$ would be equal to the distance from itself to the right side of $p$, if it is not the radius for $\textcolor{green}{\texttt{b}}$, considering $q_1$ exceeds the left bound of $p$, then $p$ could be extended too, which is against its radius being 3.

Now, if $q$ is the substring of $p$ and it is already the longest palindrome with this center, what would happen? If it is within the bound (exclusively), then $s$ would have the same radius with $q$. If it shares the left bound with $p$, then it is unclear whether $s$ could be extended furthermore, we can start with current radius (same of $q$) and increase it without violating the requirement of being palindrome.


# Algorithm
Python implementation for pseudocode[2]. 
```python
def longestPalindrome(self, s: str) -> str:
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



# Reference
[1] Manacher, *A New Linear-Time "On-Line" Algorithm for Finding the Smallest Initial Palindrome of a String*  
[2] https://en.wikipedia.org/wiki/Longest_palindromic_substring#Manacher's_algorithm