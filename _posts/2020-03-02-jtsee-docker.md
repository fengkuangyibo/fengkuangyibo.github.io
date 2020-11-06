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
### 挂载目录
在宿主机中创建挂载目录
```
mkdir -p nginx/{conf,conf.d,html,log}
```
挂载
```
docker run  --name nginx-1 -d -p 8080:80 \
 -v /root/nginx/html:/usr/share/nginx/html \
 -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
 -v /root/nginx/logs:/var/log/nginx \
 nginx
 命令解读：
 name：容器的名称
 d: 后台启动
 p: 绑定别的端口 -p a:b 将宿主机器的a端口绑定到容器的b端口 -P 为随机绑定到端口
 net ：绑定的网络 这里配置成host(因为对于容器内部来说也有一个ip如果不配置的话默认用容器的ip，导致访问不到)
 v : 挂载的内容 宿主机器的文件夹：容器的文件夹

```
```
docker run  --name nginx-test -d -p 80:80 --net host -v /root/nginx/html:/usr/share/nginx/html -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v /root/nginx/conf.d/default.conf:/etc/nginx/conf.d/default.conf   -v /root/nginx/logs:/var/log/nginx nginx
```

### jenkins

```
docker run \
  --restart=always -u root \
  --name jenkins1 \
  -d \
  -p 49000:8080 \
  -p 50000:50000 \
  -v /root/jenkins_home:/var/jenkins_home \
  -v /root/.ssh:/root/.ssh \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /usr/bin/docker:/usr/bin/docker \
  -v /usr/lib64/libltdl.so.7:/usr/lib/x86_64-linux-gnu/libltdl.so.7 \
  jenkinsci/blueocean
```
QA:
docker 安装jenkins 后通过构建 执行宿主 命令？
```
1.在docker jenkins 生成 ssh key 把id_rsa.pub 填入宿主authorized_keys中.
2.ssh root@192.168.0.23   < < remotessh 注意的点：<< remotessh，ssh后直到遇到remotessh这样的内容结束，remotessh可以随便修改成其他形式。在结束前，加exit退出远程节点 如果不想日志文件在本机出现可以修改配置
3.其他命令
```
如何从容器内部执行宿主机的docker命令
```
docker run -it -d  \
--restart=always -u root \
-v /usr/bin/docker:/usr/bin/docker \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /usr/lib64/libltdl.so.7:/usr/lib/x86_64-linux-gnu/libltdl.so.7
镜像名称
docker run 参数说明
```

```
--restart=always #Docker重启后该容器也为随之重启
-u root          
#以root的身份去运行镜像(避免在容器中调用Docker命令没有权限)
#最好使用docker用户去运行
-v /usr/bin/docker:/usr/bin/docker
#将宿主机的docker命令挂载到容器中
#可以使用which docker命令查看具体位置
#或者把挂载的参数改为: -v $(which docker):/usr/bin/docker
-v /var/run/docker.sock:/var/run/docker.sock
#容器中的进程可以通过它与Docker守护进程进行通信

-v /usr/lib64/libltdl.so.7:/usr/lib/x86_64-linux-gnu/libltdl.so.7
#libltdl.so.7是Docker命令执行所依赖的函数库
#容器中library的默认目录是 /usr/lib/x86_64-linux-gnu/
#把宿主机的libltdl.so.7 函数库挂载到该目录即可
#可以通过whereis libltdl.so.7命令查看具体位置
#centos7位置/usr/lib64/libltdl.so.7
#ubuntu位置/usr/lib/x86_64-linux-gnu/libltdl.so.7
```

### mongoDB

```
docker pull mongo:latest
docker run -itd --name mongo -p 27017:27017 mongo --auth

$ docker exec -it mongo mongo admin
# 创建一个名为 admin，密码为 123456 的用户。
>  db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]});
# 尝试使用上面创建的用户信息进行连接。
> db.auth('admin', '123456')11
```
