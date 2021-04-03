---
title: Supervisor守护进程(dotnet)
date: 2019-01-23 14:48:59
tags: [教程]
categories: 精选
---
##### 前言
ASP.NET Core应用程序发布linux在putty中运行是正常的。可一但putty关闭网站也就关闭了，所以要配置守护进程
这边我用的是Supervisor,Supervisor是采用 Python(2.4+) 开发的，它是一个允许用户管理 基于 Unix 系统进程的 Client/Server 系统，提供了大量功能来实现对进程的管理。
<!--more-->
##### 开始安装
安装
`
yum install python-setuptools
easy_install supervisor
`
配置
```
mkdir /etc/supervisor
echo_supervisord_conf > /etc/supervisor/supervisord.conf
#指定配置文件
supervisord -c /etc/supervisor/supervisord.conf
```
指定守护的程序配置
`cd /etc/supervisor`
```
[include]
files=/etc/supervisor/conf.d/*.conf
```
配置开启启动
进入 `cd /usr/lib/systemd/system`创建supervisord.service
代码配置(supervisord.service)
```
# dservice for systemd (CentOS 7.0+)
# by ET-CS (https://github.com/ET-CS)
[Unit]
Description=Supervisor daemon
[Service]
Type=forking
ExecStart=/usr/bin/supervisord -c /etc/supervisor/supervisord.conf
ExecStop=/usr/bin/supervisorctl shutdown
ExecReload=/usr/bin/supervisorctl reload
KillMode=process
Restart=on-failure
RestartSec=42s
[Install]
WantedBy=multi-user.target
```
最后执行
`systemctl enable supervisord`
`systemctl is-enabled supervisord`验证是否为开机启动
##### 配置要守护的进程
创建并打开KongMing.conf
`vim /etc/supervisor/conf.d/KongMing.conf`
配置代码：
```
[program:KongMing ;运行程序的命令
command=/bin/bash -c "dotnet acore.dll ;对应的项目的存放目录
directory=/root/dotnetcore/acore/
autorestart=false ; 程序意外退出是否自动重启
stderr_logfile=/var/log/WebApplication1.dll.err.log
stdout_logfile=/var/log/WebApplication1.dll.out.log
environment=ASPNETCORE_ENVIRONMENT=Development
user=root ;进程执行的用户身份
stopsignal=INT
```
重新加载配置
`supervisorctl reload`
启动进程
`supervisorctl start KongMing`
查看是否被守护进程拉起
`ps -ef|grep dotnet`
![](https://tp.pixiechang.cn/img/supervisor-1.png "")
错误：
你必须先启动supervisord才能使用supervisorctl
```
sudo supervisord -c /etc/supervisor/supervisord.conf
sudo supervisorctl -c /etc/supervisor/supervisord.conf
```