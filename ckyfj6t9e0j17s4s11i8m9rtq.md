## Touch command in PowerShell Windows

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