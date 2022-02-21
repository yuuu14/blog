---
layout: post
title: Same command, different OS
date: 2021-11-04 18:36 +0800
---

I use Windows and Linux both frequently, but I get used to the commands of latter. My current internship is supposed to develop
projects on Windows and it can be a bit frustrating getting errors when I tried to use Linux command directly on cmd. 
Since I have to check the equivalent command for Windows online, it is useful to keep some notes in case I just forget it next day.
Each command I will list few common parameters.

| ---- | ---- | ---- |
| win | linux | res |
| ---- | ---- | ---- |
| dir /a /b  | ls -a -l -sh | get dir list |
| cd /d | cd | change dir 
| start | xdg-open | open file with designated application |
| - | wc -l | word count --line |
| - | mkdir -p | create dir recursively



## useful commands explained 
- git checkout
- alias & unalias: temporarily rename shortcut  
  permanently use `.bash_aliases`
- type cmd
- which cmd
- d(is)u(sage) -h(uman)c(ount) dir | sort -r(everse)h(uman) | head  
  check size of dir
- nmcli  
  NetworkManager  
  `nmcli connection show --active`
- lspci  
  display devices and drivers
- nvidia-smi
  NVIDIA System Management Interface  
  

## vscode settings
- break long lines  
  Set `editor.wordWrap`: on
