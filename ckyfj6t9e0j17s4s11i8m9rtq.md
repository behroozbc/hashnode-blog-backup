---
title: "Touch command in PowerShell Windows"
datePublished: Sat Jan 15 2022 07:51:44 GMT+0000 (Coordinated Universal Time)
cuid: ckyfj6t9e0j17s4s11i8m9rtq
slug: touch-command-in-powershell-windows
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/xbEVM6oJ1Fs/upload/v1642103519450/BZbvaWJOI.jpeg
tags: windows, powershell

---

## introduction
The `touch` command is a standard command used in UNIX/Linux operating system which is used to create, change and modify timestamps of a file. but we don't have `touch` command in PowerShell Windows (PowerShell in Linux has touch command 😪). What is equivalent?
# Equivalent Commands
## copy

```
copy nul "file.txt"
``` 

## New-Item
```
New-Item textfile.txt -type file
```
## Type
```
type nul >> "file.txt"
```