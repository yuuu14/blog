---
layout: post
title: Finally decide to install Ubuntu on hardware...
date: 2023-11-16 13:57 +0100
---


I thought running ubuntu under VM with 16GB RAM PC should be easy to run smoothly, it turns out I am totally wrong. I have installed Ubuntu along with default OS before at least twice, just want to take notes this time, in case in the future I have to do it again.

Since I have one 1TB SSD as `D:\` drive on my PC, and this time I want to assign much sufficient disk space for the second OS, I shrinked about 300 GB. To create a bootable drive from the `.iso` file, I always use `rufus` [1]. 
- Use *GPT* partition scheme [2]

So the only trick part is how to install the second OS without damaging the original bootloader, and the manual partition part.

- swap: skip it, with larger RAM, swap partition becomes optional
- `/`: 20GB
- `/boot`: 1000MB, use it as a fail-safe [3]
- `/home`: skip [4] [5]
- EFI System Partition: 500MB

set `grub` [6]

install Edge on Ubuntu [7]
```bash
cd ~/Downloads
wget https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-stable/microsoft-edge-stable_110.0.1587.41-1_amd64.deb?brand=M102
sudo apt install ./microsoft-edge-stable_110.0.1587.41-1_amd64.deb
```


## References
[1] https://rufus.ie/ <br>
[2] https://wiki.archlinux.org/title/partitioning <br>
[3] https://www.baeldung.com/linux/boot-partition-necessary <br>
[4] https://askubuntu.com/questions/269880/re-install-ubuntu-without-losing-data-in-home-folder <br>
[5] https://askubuntu.com/questions/21719/how-large-should-i-make-root-home-and-swap-partitions <br>
[6] https://askubuntu.com/questions/52963/how-do-i-set-windows-to-boot-as-the-default-in-the-boot-loader <br>
[7] https://askubuntu.com/questions/1454325/unable-to-install-edge-on-ubuntu-22-04