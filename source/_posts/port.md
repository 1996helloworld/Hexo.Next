---
title: 解决Windows Server上80端口占用
date: 2018-09-05 11:37:59
tags: [技术宅,Microsoft]
categories: 系统故障
---
### 故障原因
80端口一般被当做网页服务器的默认端口，使用本机搭建服务器环境的时候，都会默认使用80端口来作为网页访问端，但是有的时候80端口会被其他的不明身份的程序占用，导致 IIS上网站 启动失败，修改 网站 的默认端口后访问本机地址又非常麻烦。下面介绍一下如果80端口被占用后应该如何处理。
<!--more-->
### 解决方法
## 找到占用端口的程序
首先打开命令提示符输入`netsh http show servicestate`
可以看到本机所有端口的使用情况，一般80端口在第一行，记下版本
![](https://tp.pixiechang.cn/img/cmd.png "")
然后，往下找，找到与上面对应的版本
![](https://tp.pixiechang.cn/img/jincheng.png "")
打开任务管理器，选择详细信息，找到对应的进程，然后右键转到服务
![](https://tp.pixiechang.cn/img/id.png "")
然后停止该服务
![](https://tp.pixiechang.cn/img/service.png "")
最后80端口就解除占用了  
