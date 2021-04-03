---
title: 常用sql语句
date: 2018-09-04 11:37:59
tags: [SQLServer,Microsoft]
categories: SQL语句
---
### 简单的GroupBy
<!--more-->
{% codeblock %}
SELECT MAX(Price) sjrq ,GoodsDetailId
FROM DayReport
GROUP BY GoodsDetailId
{% endcodeblock %}

### 过滤重复项取最大的一条
{% codeblock %}
select s.*  
from ( 
    select *, row_number() over (partition by [要过滤的字段] order by [排序字段]] desc) as group_idx  
    from [表名]
) s
where s.group_idx = 1
{% endcodeblock %}

### 查询自增列
{% codeblock %}
select Row_Number() over ( order by getdate() ) as init
{% endcodeblock %}