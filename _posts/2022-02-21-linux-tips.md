---
layout: post
title: linux-tips
date: 2022-02-21 13:11 +0800
---

## `tmp` dir
temporary directory, contains all the required files that are going to be required “temporarily” during program execution. In case of any crash or unexpected event, you can retrieve your file from the directory.


https://www.ubuntupit.com/everything-you-need-to-know-about-linux-tmp-directory/#:~:text=The%20%E2%80%9C%2Ftmp%E2%80%9D%20or%20tmp%20directory%20%28temporary%20directory%29%20in,Let%20us%20say%20you%20are%20writing%20a%20document.


## bash scripts
parameter passing  
  `$`+number indicating order

single vs. double quotes  
The latter allows the shell to interpret dollar sign ($), backtick(`), backslash(\) and exclamation mark(!)

! with PARAMETER  
If the first character of "PARAMETER" is an exclamation point, Bash uses the value of the variable formed from the rest of "PARAMETER" as the name of the variable; this variable is then expanded and that value is used in the rest of the substitution, rather than the value of "PARAMETER" itself. This is known as indirect expansion.  
