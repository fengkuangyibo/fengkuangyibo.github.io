---
layout: post
title:  "jtsee deno搭建"
date:  2020-09-18 16:28 +0800
categories: jtsee
---
### jtsee.com 环境建设
1、git 到code.aliyun.com/fengkuangyibo/jtsee
2、jtsee空间内建设jenkins git code.aliyun.com的源码
3、denon 自动审查文件变动 自动重启

### shadowsocks 翻墙
安装  pip install git+https://github.com/shadowsocks/shadowsocks.git@master

vim /etc/polipo/config 内添加
socksParentProxy = "127.0.0.1:9000"
socksProxyType = socks5

sslocal -c /etc/shadowsocks/config.json start &

sudo service polipo start
sudo service polipo stop

vim ~/.bashrc
export http_proxy='http://127.0.0.1:8123'
export https_proxy='http://127.0.0.1:8123'

source ~/.bashrc
其它参考
https://www.jb51.net/article/147524.htm
https://www.oneops.co/2019/03/07/shadowsocks-vpn.html
