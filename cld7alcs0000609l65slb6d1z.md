# Introduce Windows Winget

As a Windows user, I envy Linux users because they have a package manager like APT to install their software from the command line without touching UI. On May 13, 2020, Microsoft introduced the 'Winget' that ends an ear. In this post, I will look at some features and powers of 'Winget'.

## What is 'Winget'?

Winget is an open-source package manager tool that since 2020, Microsoft has developed to add a tool that other competitors possessed. And it was added to windows 10 and newer versions after passing the alpha and beta stages. Winget can install and upgrade software from the windows command line.

## Find applications on winget

Users can lock up to the winget application list by using `winget search` like this

Bash

```bash
winget search vscode
```

Which returns that has application's full name, winget Id, version and source

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673937258889/cd7fdee5-c2e4-436e-be84-8e967ecbb16f.png align="left")

## Installing applications by Winget

after finding your needed application on winget you can install it by the `winget install APPNAME|APPID` command, which you replace the `APPNAME|APPID` by the app's name or app Id that saw in the finding section (I suggest you use `APPID` rather than `APPNAME`). After entering the command, Winget downloads the application's installer and installs it. Also, windows may show an alert about Installing permission that to install the software user must accept it. For example, I installed .Net SDK version 6 with winget.

```bash
winget install Microsoft.DotNet.SDK.6
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673972087833/33adb8a7-fa93-4e95-aff0-426c6c57dcf7.png align="left")

## Upgrade applications

Winget has two futures about upgrading apps. First, it can show which apps need to upgrade.

```bash
winget upgrade
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674385446350/1ff538a6-7407-48da-ba61-44cbfd8de577.png align="center")

On top of that, you can upgrade your installed apps by a command like installing them.

```bash
winget upgrade Microsoft.WindowsPCHealthCheck
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674385652821/ce0d3ced-bea6-404a-b2c8-c73af411b4f1.png align="center")

Also, Winget can upgrade all apps with this command.

```bash
winget upgrade --all
```

## Sum up

To make a long story short, Winget has many features on top of what I explained, such as host own private Windows Package Manager repository or adding your application to the public Package Manager. If you want information about it, add a comment about it. Also, I am here to help you, if you got an error tell me in the comment.

Have a good day 😀.