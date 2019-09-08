# How to deploy ShareLatex by Docker

## Introduction

If you want to deploy ShareLatex(a recent name of Overleaf) by Docker, you may follow [official guidance](https://github.com/overleaf/overleaf/wiki/Quick-Start-Guide). But there is still some issues since configuration or dependencies. In this guidance I will show the details.

## Environment

Ubuntu 16.04.5

## Dependencies

**docker-io**, **docker-compose**

Notice that in Ubuntu, the default package control tool is dkpg but not yum. I tried the following command:

```bash
sudo apt-get install docker-compose
```

But no this package are found. You may need:

```bash
sudo curl -L https://github.com/docker/compose/releases/download/1.23.0-rc3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose version
```

## Installation

First, pull the image of latest version.

```bash
docker pull sharelatex/sharelatex
```

It is recommend to use [docker-compose.yml](https://github.com/overleaf/overleaf/blob/master/docker-compose.yml) provided by [Quick Start](https://github.com/overleaf/overleaf/wiki/Quick-Start-Guide), but you need to fix some configuration before installation:

```bash
mkdir -p ~/sharelatex
cd ~/sharelatex
curl -O https://raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml # This line may cause some error, you can clone official repo instead.
sudo vim docker-compose.yml
```

```yaml
ports:
  - $PORT:80 # Default configuration is 80:80, may cause port confilting.

# local directory
volumes:
  - /home/docker/sharelatex:/var/lib/sharelatex

# Attention: add new texlive version to PATH for fully installation for new version of texlive path before old version path.(.../textlive/2019/$platform)
environment:
  - PATH: /usr/localsbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/texlive/2019/bin/x86_64-linux:/usr/local/texlive/2017/bin/x86_64-linux

# Rendering configuration: default is classical community style of Overleaf.
# SHARELATEX_APP_NAME: Our ShareLaTeX
# SHARELATEX_NAV_TITLE: Our ShareLaTeX Instance
# SHARELATEX_HEADER_IMAGE_URL: http://somewhere.com/mylogo.png
# SHARELATEX_LEFT_FOOTER: '[{"text": "Powered by <a href=\"https://www.sharelatex.com\">ShareLaTeX</a> 2016"},{"text": "Another page I want to link to can be found <a href=\"here\">here</a>"} ]'
# SHARELATEX_RIGHT_FOOTER: '[{"text": "Hello I am on the Right"} ]'

# Mongo/Redis directory
# mongo
volumes:
  - $MongoDir:/data/db
# redis
volumes:
  - $RedisDir:/data
```

In the ShareLatex dir:

```bash
docker-compose up -d
```

Upgrade and fully-install new version of texlive:

```bash
docker exec -it sharelatex bash

cd /usr/local/texlive
cp -a 2017 2019
wget http://mirror.ctan.org/systems/texlive/tlnet/update-tlmgr-latest.sh
sh update-tlmgr-latest.sh -- --upgrade

# replace source
tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/

tlmgr update --self --all

# This line may casue error but no influence for next step.
luaotfload-tool -fu

# Long waiting at least several hours
tlmgr install scheme-full

exit
docker restart sharelatex
```

## Initialization

Follow Quick Start Guidance to create an admin account:

```bash
docker exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:create-admin --email joe@example.com
```

## Reference

1. Official Guidance https://github.com/overleaf/overleaf/wiki/Quick-Start-Guide
2. Docker-compose install https://blog.51cto.com/9291927/2310444
3. Docker image issues https://github.com/overleaf/docker-image/issues/90
4. Texlive Update https://www.tug.org/texlive/upgrade.html
5. Docker Guidance https://blog.csdn.net/kun_931013/article/details/85234684
6. ShareLatex Docker Guidance https://blog.csdn.net/darren817/article/details/97298904
7. ShareLatex Local Deployment https://blog.csdn.net/sofair/article/details/80994960

 
