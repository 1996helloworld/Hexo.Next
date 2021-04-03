---
title: Centos+.NetCore2.0+nginx笔记
date: 2018-09-12 13:44:59
tags: [.NetCore2.0,nginx,Contos7.3]
categories: 学习
---
### .NetCore 
.NET Core是一个开源的通用开发平台，由Microsoft和.NET社区在GitHub上维护。它是跨平台的，支持Windows，macOS和Linux，可用于设备，云和物联网应用程序。
<!--more-->
[核心指南](https://docs.microsoft.com/en-us/dotnet/core/index/)
## 关于
.NET Core具有以下特征：
跨平台：在Windows，macOS和Linux 操作系统上运行。
跨架构保持一致：在多个体系结构（包括x64，x86和ARM）上以相同的行为运行代码。
命令行工具：包括易于使用的命令行工具，可用于本地开发和持续集成方案。
灵活部署：可以包含在您的应用程序中，也可以安装在并行用户或机器范围内。
兼容：.NET Core通过.NET Standard与.NET Framework，Xamarin和Mono兼容。
开源：.NET Core平台是开源的，使用MIT和Apache 2许可证。.NET Core是一个.NET Foundation项目。
Microsoft支持：根据.NET Core Support，Microsoft 支持.NET Core。
## 安装
为了安装.NET，需要注册微软签名密钥和添加微软相关的支持。这个操作每台机器只能做一次。 
打开命令行，输出以下命令：
{% codeblock %}
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl= https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
{% endcodeblock %}
安装.NetSdk
更新可用的安装包 `sudo yum update`
安装.NET需要的组件，libunwind和libicu库；`sudo yum install libunwind libicu`
安装.NET SDK `sudo yum install dotnet-sdk-2.0.2`
安装完成之后，可以输入 `dotnet --info` 检测是否安装成功
如果安装成功会显示一下命令
![](https://tp.pixiechang.cn/img/NetCore.png "")
### Nginx
## 关于
Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，并在一个BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等

## 安装
{% codeblock %}
curl -o  nginx.rpm http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
rpm -ivh nginx.rpm
yum install nginx #安装
{% endcodeblock %}
![](https://tp.pixiechang.cn/img/nginxInstall.png "")
{% codeblock %}
rpm -ivh nginx.rpm
systemctl start nginx #启动nginx
systemctl enable nginx #设置nginx的开机启动
{% endcodeblock %}
### Linux
## 常用命令
文件处理

|  命令  |   描述   |
| ------ | ------- |
| cd |  目录跳转 |
| cd /       |  回到上一个目录 |
| :wq!        |  强制保存文件，并退出vi |
| mkdir |  创建文件夹 |
| pwd |  显示工作路径 |
| rm -f file1 |  删除一个叫做 'file1' 的文件' |
| rmdir dir1 |  删除一个叫做 'dir1' 的目录' |
| ls       |  查看目录下的文件 |
| ls -a |  显示隐藏文件 |
| ls -l |  列出长数据串，包含文件的属性与权限数据等 |
| cd -d |  仅列出目录本身，而不是列出目录的文件数据 |
| cd -h |  将文件容量以较易读的方式（GB，kB等）列出来  |
| cd |  目录跳转 |

系统

|  命令  |   描述   |
| ------ | ------- |
| systemctl restart firewalld |  重启防火墙，使其生效 |
| service mysqld restart |  重启mysql |
| reboot |  重启系统 |
| systemctl restart nginx |  重启Nginx |
| kill xxx |  杀进程 |
| systemctl restart nginx |  重启Nginx |