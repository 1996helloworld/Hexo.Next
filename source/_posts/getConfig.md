---
title: netcore读取配置文件
date: 2019-01-23 08:48:59
tags: [教程]
categories: 精选
---
##### 读取配置文件
<!--more-->
* 在netcore项目目录下有个appsettings.json

![](https://tp.pixiechang.cn/img/config-1.png "")
代码如下：
```
{
	"AppSettings": {
		"DefaultConnection": "server=47.97.172.246;port=3306;database=vote;user id=root;password=guest0."
	},
	"Logging": {
		"IncludeScopes": false,
		"LogLevel": {
			"Default": "Warning"
		}
	}
}
```

* 添加一个类，名称要和定义的Json对象定义的一致
```
public class AppSettingsModel
 {
     public string DefaultConnection { get; set; }
 }
```
* StartUp时读取配置信息
```
 public void ConfigureServices(IServiceCollection services)
  {
        services.AddMvc();         
        services.Configure<AppSettingsModel>(Configuration.GetSection("AppSettings"));
   }
```
* 定义配置信息对象
`private static  IOptions<AppSettingsModel> _settings;
`
* 通过构造函数进入配置信息
```
 public HomeController(IOptions<AppSettingsModel> settings)
  {
           _settings = settings;
  }
```
* 读取配置节点信息
`_settings.Value.DefaultConnection
`