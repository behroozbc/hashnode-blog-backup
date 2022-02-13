## Install .NET on a Raspberry Pi

.NET is a cross-platform, free, open-source platform successor to the .NET framework.
Installing .NET is straightforward for most OS like Windows and Ubuntu (Desktop and Server) with clean instruction available on the download website. However, installing it on something like a Raspberry Pi that uses an ARM-based processor becomes trickier. 

Let's start by installing .NET 6 on a Raspberry Pi OS 64-bit or 32-bit.

## 1) Access to the terminal of Raspberry Pi OS
You can access the terminal of the Raspberry PI by SSH or direct connection. 
To connect to your Raspberry using SSH, use the command below to replace `IP` and `user` with your raspberry IP and user name.
```
ssh user@IP
```
After inserting the password of the user.

## 2) Install dependency
You need install dependency required by .NET 
```
sudo apt update
sudo apt install wget
```
## 3) Download `dotnet-install` script

Microsoft has a script to help to download the dotnet binary in Linux if you want more info check [this site](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-install-script). To download the script use the below command
```
$ wget https://dot.net/v1/dotnet-install.sh
```
## 4) Download and install .NET
To download and install .NET to run the `dotnet-install` script 
```
sudo bash ./dotnet-install.sh --channel LTS --install-dir /opt/dotnet/ 
```
The command installs the latest LTS version of the dotnet and saves it to this `/opt/dotnet/` address. To see more options check [Microsoft documentation](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-install-script#options). after the script is done you must add a path to the `.bashrc` file to load .NET globally.
```
ln -s /opt/dotnet/dotnet /usr/local/bin

echo 'export DOTNET_ROOT=/opt/dotnet' >> /home/pi/.bashrc
```
## See the result 🤩
To see the result and check all things work perfectly run 
```
dotnet --info
```
You must get s result like this
```
pi@raspberrypi:~ $ dotnet --info
.NET SDK (reflecting any global.json):
 Version:   6.0.101
 Commit:    ef49f6213a

Runtime Environment:
 OS Name:     debian
 OS Version:  11
 OS Platform: Linux
 RID:         debian.11-arm64
 Base Path:   /opt/dotnet/sdk/6.0.101/

Host (useful for support):
  Version: 6.0.1
  Commit:  3a25a7f1cc

.NET SDKs installed:
  6.0.101 [/opt/dotnet/sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.App 6.0.1 [/opt/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 6.0.1 [/opt/dotnet/shared/Microsoft.NETCore.App]

To install additional .NET runtimes or SDKs:
  https://aka.ms/dotnet-download
```
### Last note

I test this article in my Raspberry Pi 4 with Raspberry Pi (x64) os.
If you’re still not sure or have questions about it what to do, or if you got any errors, then I suggest you use the comment section below and let me know!
