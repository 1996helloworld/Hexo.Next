---
title: OpenSSL的使用
date: 2021-04-03 15:48:59
tags: [开发,工具]
categories: 工具
---
### 什么是 OpenSSL？
[SSL](https://baike.baidu.com/item/SSL/)是 Secure Sockets Layer([安全套阶层协议](https://baike.baidu.com/item/%E5%AE%89%E5%85%A8%E5%A5%97%E6%8E%A5%E5%B1%82%E5%8D%8F%E8%AE%AE))的缩写，
可以在Internet上提供秘密性传输。Netscape公司在推出第一个Web浏览器的同时,提出了SSL协议标准。其目标是保证两个应用间通信的保密性和可靠性,可在服务器段和用户端同时实现支持。已经成为Internet上保密通讯的工业保准,本篇主要是介绍利用openssl工具生成证书😄

<!--more-->
## Quick Start

### 下载安装
``` bash
git clone https://github.com/openssl/openssl.git
```
### 环境变量
配置环境变量
![](https://tp.pixiechang.cn/img/openssl01.png "") 
配置完成后打开cmd直接输入openssl 如下图配置完成
![](https://tp.pixiechang.cn/img/openssl02.png "") 

### 命令生成 cer 证书 和 Key
直接输入以下命令
``` bash
req -new -SHA256 -newkey rsa:2048 -nodes -keyout pixiechang.cn.key -out pixiechang.cn.csr -subj "/C=CN/ST=Shanghai/L=Shanghai/O=Tencent/OU=IT Dept/CN=pixiechang.cn"
```
命令详解

|  命令  |   描述   |
| ------ | ------- |
| SHA256 |  签名哈希算法 |
| 2048       |  密钥强度 |
| tp.pixiechang.cn.key        |  key文件导出名称 |
| tp.pixiechang.cn.csr |  csr文件导出名称 |
| C |  国家 |
| ST |  省份 |
| L |  城市 |
| OU       |  部门 |
| O |  公司名称 |
| CN |  域名 |

![](https://tp.pixiechang.cn/img/openssl03.png "") 
如下csr和key文件就生成成功了
![](https://tp.pixiechang.cn/img/openssl04.png "") 

### 命令合成 pfx 证书
准备pem文件和key文件,直接输入以下命令,输入密码和确认密码(key文件有密码的会先提示输入key文件密码)
``` bash
pkcs12 -export -in pixiechang.cn.cert.pem -inkey pixiechang.cn_31key.txt -out pixiechang.cn.pfx
```
![](https://tp.pixiechang.cn/img/openssl05.png "") 

|  命令  |   描述   |
| ------ | ------- |
| pixiechang.cn.key |  本地key文件名称 | 
| pixiechang.cn.cert.pem        |  本地证书文件 |
| pixiechang.cn.pfx |  pfx导出名称 |

生成成功如下图
![](https://tp.pixiechang.cn/img/openssl06.png "") 