---
title: C# Update
date: 2018-11-20 08:48:59
tags: [开发,.Net]
categories: 精选
---
### C#元组(Tuple)
元组是具有特定数量和元素顺序的数据结构，下面元组通常以四种方式使用：
> + 第一项表示单个数据集。 例如，元组可以表示数据库记录，并且其组件可以表示记录的各个字段。
> + 提供对数据集的轻松访问和操作。
> + 若要通过单个参数向方法传递多个值，则为。 例如，Thread.Start(Object) 方法只有一个参数，该参数可让线程在启动时执行的方法提供一个值。 如果提供 Tuple<T1,T2,T3> 对象作为方法参数，则可以为线程的启动例程提供三个数据项。

### LINQ to Entities 不支持 LINQ 表达式节点类型“ArrayIndex”
<!--more-->
代码：
{% codeblock %}
//ids为一个string数组
var entity = Repository.FindSingle(t => t.Id == ids[i]);
{% endcodeblock %}
报错：
![](https://tp.pixiechang.cn/img/11-20.png "")
原因：
Linq To Entity中表达式节点不支持该类型变量,可以把ids[i]先赋给一个变量再用作表达式中即可;