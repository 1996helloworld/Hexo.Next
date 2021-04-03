---
title: Hexo博客搭建注意事项
date: 2018-08-14 16:25:59
tags: [安装教程,Hexo]
categories: 精选
---
### 什么是 Hexo？
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!--more-->
### 安装前提
安装node.js
[Windows Installer 32-bit](https://nodejs.org/dist/v4.2.3/node-v4.2.3-x86.msi/)
[Windows Installer 64-bit](https://nodejs.org/dist/v4.2.3/node-v4.2.3-x64.msi/)
安装Git
[Git-2.6.3-64-bit.exe](https://github.com/git-for-windows/git/releases/download/v2.6.3.windows.1/Git-2.6.3-64-bit.exe/)
### 开始安装
本地找一个合适的空文件夹右键Git Bash Here输入：
{% codeblock %}
npm install hexo-cli -g
{% endcodeblock %}
然后输入以下命令来测试安装是否成功
{% codeblock %}
hexo -v
{% endcodeblock %}
初始化Hexo
{% codeblock %}
hexo init
{% endcodeblock %}
安装npm
{% codeblock %}
npm install
{% endcodeblock %}
首次生成
{% codeblock %}
hexo g
{% endcodeblock %}
最后启动进程
{% codeblock %}
hexo s
{% endcodeblock %}
此时浏览器输入http://localhost:4000
可以看到初始化的hexo
### 配置文件(Hexo)
您可以在 _config.yml 中修改大部份的配置
## 网站（Site）

|  参数  |   描述   |
| ------ | ------- |
| title |  网站标题 |
| subtitle       |  网站副标题 |
| description       |  网站描述 |
| author       |  您的名字 |
| language       |  网站使用的语言 |
| timezone       |  网站时区 |

## 链接（URL）

|  参数  |   描述   |
| ------ | ------- |
| url |  网址 |
| root       |  网站根目录 |
| permalink       |  文章的 永久链接 格式 |
| permalink_defaults       |  永久链接中各部分的默认值 |

### 配置文件(Next主题)
您可以在 themes/next/_config.yml 中修改配置
设置主题风格
{% codeblock %}
# Schemes
#scheme: Muse # 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
#scheme: Mist # Muse 的紧凑版本，整洁有序的单栏外观
#scheme: Pisces # 双栏 Scheme，小家碧玉似的清新
#scheme: Gemini # 类似 Pisces
{% endcodeblock %}
浏览页面的时候显示当前浏览进度
{% codeblock %}
scrollpercent: true
{% endcodeblock %}
博客底部显示备案号
您可以在 themes/next/_config.yml 中修改配置"custom_text"
{% codeblock %}
custom_text: <a target="_blank" rel="external nofollow" href="http://www.miitbeian.gov.cn/"><b>粤ICP备18098510号</b></a>
{% endcodeblock %}
头像配置
打开 themes/next/_config.yml 文件，搜索  Sidebar Avatar 关键字(url:图片地址)
{% codeblock %}
avatar: url
{% endcodeblock %}
设置头像边框为圆形框
{% codeblock %}
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;
 // 修改头像边框
  border-radius: 50%;
  -webkit-border-radius: 50%;
  -moz-border-radius: 50%;
}
{% endcodeblock %}
特效：鼠标放置头像上旋转
{% codeblock %}
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;
 // 修改头像边框
  border-radius: 50%;
  -webkit-border-radius: 50%;
  -moz-border-radius: 50%;
  // 设置旋转
  transition: 1.4s all;
}
// 可旋转的圆形头像,`hover`动作
.site-author-image:hover {
    -webkit-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -ms-transform: rotate(360deg);
    -transform: rotate(360deg);
}
{% endcodeblock %}
### 命令
创建分类目录
在终端窗口下，定位到 Hexo 站点目录下。使用 hexo new page 新建一个页面，命名为 categories
{% codeblock %}
$ hexo new page categories
{% endcodeblock %}
编辑新建的categories页面
{% codeblock %}
title: 分类
date: 2017-08-10 09:35:41
type: "categories"
comments: false   #此页评论关闭
{% endcodeblock %}
{% codeblock %}
[root@izbp1f44r0ae84z /]# cd /home/git/blog.git/hooks
[git@izbp1f44r0ae84z hooks]$ git --work-tree=/home/www/Hexo/ checkout -f
{% endcodeblock %}