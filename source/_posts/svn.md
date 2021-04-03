---
title: Centos搭建Svn
date: 2018-12-03 08:48:59
tags: [安装教程,Linux]
categories: 精选
---
### 使用yum安装
<!--more-->
{% codeblock %}
yum install subversion
{% endcodeblock %}

### 创建仓库
{% codeblock %}
[root@izbp1f44r0ae84z /]# svnadmin create /home/svn/project
{% endcodeblock %}
### 更改配置文件(conf)
仓库一共有三个配置文件需要手动配置路径：/home/artifact/conf下password
1.password配置
{% codeblock %}
[users]
# harry = harryssecret
# sally = sallyssecret
wyj = wyj123
wyf = wyf123
gds = gds123
lk = lk123
pht = pht123
{% endcodeblock %}
账号=密码
2.配置新用户的授权文件(authz)
{% codeblock %}
[/]
wyj=rw
wyf=r
gds=r
*=
{% endcodeblock %}
以上为用户分配权限(rw=可读可写,r=只读)结尾加上*=
3.配置svnserve.conf
打开下面的5个注释
{% codeblock %}
anon-access = read #匿名用户可读
auth-access = write #授权用户可写
password-db = passwd #使用哪个文件作为账号文件
authz-db = authz #使用哪个文件作为权限文件
realm = /home/svn # 认证空间名，版本库所在目录
{% endcodeblock %}
### 启动与停止
{% codeblock %}
[root@localhost conf]# svnserve -d -r /home/svn（启动）
[root@localhost conf]#killall svnserve（停止）
{% endcodeblock %}
### 客户端连接到服务器
输入地址svn://IP(svn://47.97.172.246) 即可
![](https://tp.pixiechang.cn/img/svninstall.gif "")
### 自动同步
客户端提交了版本修改之后，在之前的每次都是需要执行svn update命令，而且不小心会出现开发冲突。
下面来配置SVN钩子，来实现自动更新服务器WEB目录文件
{% codeblock %}
cd /home/svn/project/hooks/
vim post-commit
{% endcodeblock %}
添加以下代码
{% codeblock %}
#!/bin/sh
export LANG=zh_CN.UTF-8 
SVN=/usr/bin/svn  #svn程序目录
WEB=/data/www/ #web程序目录
$SVN update $WEB --username wyj --password wyj123 #客户端的用户名和密码，在svn配置文件里配置的信息
{% endcodeblock %}
添加权限
{% codeblock %}
chmod 777 post-commit
{% endcodeblock %}
重启svn
![](https://tp.pixiechang.cn/img/svn-1.png "")
![](https://tp.pixiechang.cn/img/svn-2.png "")