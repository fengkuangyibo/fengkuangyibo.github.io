---
layout: post
title:  "tradingLabs.net"
date:   2020-10-29 14:46:23 +0800
categories: tradingLabs
---
### tradingLabs_net 目录结构

git clone ssh://root@39.105.35.116:/root/tradingLabs_git/tradingLabs_git.git

tradingLabs_git 目录是以qa为 工作目录

### python环境
```
在 vim ~/.bash_profile
export PATH="/Users/zhouyanjie/anaconda3/bin:$PATH"
```

anconda 
conda activate t2 

### qa 安装
pip install -e  qa 本地打包安装到

### mongo
设置开机自启动
echo "/usr/local/mongodb/bin/mongod --dbpath=/usr/local/mongodb/data –logpath=/usr/local/mongodb/logs –logappend  --auth -–port=27017" >> /etc/rc.local
