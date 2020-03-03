---
layout: post
title:  "jtsee docker搭建"
date:  2020-03-02 15:50:23 +0800
categories: jtsee
---
## docker安装
[Docker安装 Ubuntu](http://www.dockerinfo.net/docker%e5%ae%89%e8%a3%85-ubuntu)

[docker install](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

[Get Docker Engine - Community for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)

##### 卸载旧版本

Docker 的旧版本被称为 docker，docker.io 或 docker-engine 。如果已安装，请卸载它们：
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```
### 使用 Docker 仓库进行安装
设置仓库
更新 apt 包索引。

$ sudo apt-get update
安装 apt 依赖包，用于通过HTTPS来获取仓库:
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
添加 Docker 的官方 GPG 密钥：
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
验证您现在是否拥有带有指纹的密钥 。
```
$ sudo apt-key fingerprint 0EBFCD88
```
安装稳定存储库
```
sudo add-apt-repository \ "deb [arch=amd64] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) \stable"
```
#### 安装 Docker Engine-Community
更新 apt 包索引。
```
$ sudo apt-get update
```
安装最新版本的 Docker Engine-Community 和 containerd ，或者转到下一步安装特定版本：
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
安装完成 检验是否安装成功
```
docker version:显示docker版本信息
```
