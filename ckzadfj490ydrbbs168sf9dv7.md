---
title: "Install nano on Alpine Linux"
datePublished: Sat Feb 05 2022 21:51:24 GMT+0000 (Coordinated Universal Time)
cuid: ckzadfj490ydrbbs168sf9dv7
slug: install-nano-on-alpine-linux
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/4Mw7nkQDByk/upload/v1644086733999/VY_Ddu3_N.jpeg
tags: linux, linux-for-beginners, linux-basics

---

When you are a beginner on Alpine Linux, you want to use [nano](https://www.nano-editor.org/) a text editor for editing a file and get this error 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644092850184/GartPkPbC.png)
😕🤷‍♂️
## why does this happen??
Alpine Linux is a Linux distribution based on musl and BusyBox, designed for security, simplicity, and resource efficiency and has a small size for the fast boot-up time. by default haven't a nano text editor that you must install.
# Install Nano on Alpine Linux
First, you need to get updated remote repositories changes as packages are added and upgraded.
```
apk update
```
Get this result 
```
/ # apk update
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/community/x86_64/APKINDEX.tar.gz
v3.15.0-258-gd5d32e35cf [https://dl-cdn.alpinelinux.org/alpine/v3.15/main]
v3.15.0-256-g047dab5823 [https://dl-cdn.alpinelinux.org/alpine/v3.15/community]
OK: 15857 distinct packages available
```
now you can install nano by this command
```
apk add nano
```
wait to install nano 
```
/ # apk add nano
(1/3) Installing ncurses-terminfo-base (6.3_p20211120-r0)
(2/3) Installing ncurses-libs (6.3_p20211120-r0)
(3/3) Installing nano (5.9-r0)
Executing busybox-1.34.1-r3.trigger
OK: 7 MiB in 17 packages
```
You have a nano text editor on Alpine Linux 😁😁

if you got any errors, then I suggest you use the comment section below and let me know!