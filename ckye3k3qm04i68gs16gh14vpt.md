---
title: "Setup a private NuGet repository"
datePublished: Fri Jan 14 2022 07:46:24 GMT+0000 (Coordinated Universal Time)
cuid: ckye3k3qm04i68gs16gh14vpt
slug: setup-a-private-nuget-repository
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/dMGV2jJShdo/upload/v1642059550772/RA2wuQ3Wy.jpeg
tags: csharp, package, aspnet, aspnet-core

---

Setup a private NuGet repository have multi-way. In this post we see BaGet and how can start it.
## What is BaGet?
According to https://loic-sharma.github.io/BaGet/

`BaGet (pronounced "baguette") is a lightweight NuGet and symbol server. It is open source, cross-platform, and cloud ready! `
## Setup BaGet 
### Step one: Getting VPS and Installing Docker
We need a VPS for installing and using BaGet. After getting VPS it's time to install docker. I recommend you for installing to check [docker documentation](https://docs.docker.com/engine/install/). Now we can start Installing BaGet

 ### Step two: Installing BaGet on docker

We Create a file named `baget.env` to store BaGet's configurations:
```
ApiKey=NUGET-SERVER-API-KEY

Storage__Type=FileSystem
Storage__Path=/var/baget/packages
Database__Type=Sqlite
Database__ConnectionString=Data Source=/var/baget/baget.db
Search__Type=Database
```
**Important: ** You must change ApiKey.
Now it's time to download BaGet form  [docker hub](https://hub.docker.com/r/loicsharma/baget) :
```
docker pull loicsharma/baget
```
with this command get the latest version of BaGet.

To start BaGet docker container :
```
docker run --rm --name nuget-server -p 8080:80 --env-file baget.env -v "$(pwd)/baget-data:/var/baget" loicsharma/baget
```
now NuGet server run and we can open it 'IP or domain pointed to vps:8080` to see BaGet home page.
### Config nginx (Optional) 
You can make a domain for it every time enter the domain.

Install Nginx this [link](https://nginx.org/en/docs/install.html) to help you.

After installing add file `nuget.behroozbc.com` to `/etc/nginx/conf.d/` like 
```
server {
    server_name  nuget.behroozbc.com; # your domain name you must change it

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;
	
    client_max_body_size 50M;
    
    location / {
        proxy_pass   http://127.0.0.1:8080/;
        proxy_set_header Host $http_host;
        proxy_set_header X-Forwarded-Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

}
```
### Publishing package
Publish your first package with:
```
dotnet nuget push -s http://nuget.behroozbc.com/v3/index.json -k NUGET-SERVER-API-KEY package.1.0.0.nupkg
```

