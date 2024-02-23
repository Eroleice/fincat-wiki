---
title: 在统信UOS系统安装最新NodeJS
description: dddd
published: true
date: 2024-02-23T07:44:03.652Z
tags: 
editor: markdown
dateCreated: 2024-02-23T07:44:03.652Z
---

# 前言
出于dddd的原因，公司电脑统一换成统信UOS系统了，除了一系列一言难尽的问题，很多程序的安装都成问题，apt库更是......

但是又需要搭建一些编程环境，统信自己的apt库装出来的nodejs居然是v6版本的，大哥现在都v21了，导致我写不出三行代码就给我报错了，于是在网上找了好多办法，最终成功手动装上了nodejs。

# 步骤
在[node官网](https://nodejs.org/en/download){target=blank}下载需要的node版本，放到一个地方，在相应位置开启终端。

## 解压程序
```
sudo tar -xvf node-v20.11.1-linux-x64.tar.xz -C /usr/local/
```

## 重命名
```
sudo mv /usr/local/node-v20.11.1-linux-x64 /usr/local/node
```

## 做映射
```
sudo ln -s /usr/local/node/bin/node /usr/bin/node
sudo ln -s /usr/local/node/bin/npm /usr/bin/npm
sudo ln -s /usr/local/node/bin/npx /usr/bin/npx
```

## 确认版本
```
npm -v
node -v
```

## 配置全局库和缓存
```
cd /usr/local/node
sudo mkdir node_global
sudo mkdir node-cache
sudo npm config set prefix "node_global"
sudo npm config set cache "node_cache"
```

## 设置国内镜像源
```
npm config set registry https://regirstry.npm.taobao.org
```

# 参考文献
toobeloong. 统信系统专业版（UOS）安装node环境. [csdn.net](https://blog.csdn.net/freedomljt/article/details/125274318){target=blank}. (2023-04-06)[2024-02-23].