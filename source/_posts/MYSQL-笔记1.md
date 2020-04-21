---
title: MYSQL-笔记1
date: 2019-09-02 16:32:55
cover: title.jpg
tags: note
---

>   在MYSQL中查询操作涉及内容



[TOC]

## function

>   对待查询字段在待查找表中出现的若干记录中的函数参数中指定的字段进行某些操作。

*   `COUNT` ： 统计
*   `SUM` ： 求和
*   `AVG` ： 平均数

[more about info](https://www.runoob.com/mysql/mysql-functions.html)





## sentence

>   各个语句执行顺序：select –>where –> group by–> having–>order by。



### 常用语句

* `limit` 

   限定查找记录的条数。

* `offset`

   查找偏移量，即前n条跳过，从n+1开始查询。

* `with rollup` 

   进一步得到`group by`信息的汇总信息。

* `having` 

   功能类似`where`，不同的是，`where`是筛选已存在的数据，`having`用来对前面的筛选进行进一步筛选。

  例：

  ```mysql
  select 
  	name,
  	SUM(sign), 
  	SUM(score) 
  from 
  	games 
  group by 
  	name 
  having 
  	SUM(score) > 80
  ;
  -- SUM(score)在games表中不存在，是待筛数据。
  -- 通过having可以对其进行进一步筛选。
  ```

  

* `link`

  常与`where配合使用`，使用`link`子句匹配模式串，可以将`link`看作`=`。

  可以使用正则表达式中的`%`来匹配任意字符。

  例：

  ```mysql
  select 
  	* 
  from 
  	Computer 
  where 
  	Model link 'Mac%'
  ;
  
  -- 查找Computer表中Model字段中含有'Mac'的记录。
  ```

  

* `order by`

  排序子句，给查找出来的记录排序，可以选择按照一个或多个字段为记录排序，

  当然也可以设置升序(asc)还是降序(desc)，默认是升序。

  当然也可以添加`where...link...`来设置更加复杂的排序规则。

  例：

  ```mysql
  select 
  	*
  from 
  	Computer
  order by 
  	Sales_volume
  ;
  
  -- 按照Sales_volume字段排序输出Computer表。
  ```

  

* `select ... into outfile 'filename'`

  导出查询结果到文件。

* `union`

  用来连接多个`select`语句，将结果合并输出，可选是(all)否(默认删除重复数据)删除重复数据。

  例：

  ```mysql
  select 
  	Sales_volume
  from 
  	Computer
  union all
  select 
  	Sales_volume
  from 
  	Mobile_Phone
  order by 
  	Sales_volume
  ;
  
  -- 查找Computer表和Mobile_Phone表中的Sales_volume字段数据，
  -- 按照Sales_volume以默认方式排序，
  -- 而且不删除重复数据。
  ```





### JOIN

>   用于连接两个或多个表，从多个表中查询数据。
>
>   ...  tableA [join语句] tableB ...  on [条件]

*   `inner join`：语句两端的两个表的交集。
*   `left join`：读取左边表中所有的匹配数据，即使右侧表中无匹配数据。
*   `righe join `：与`lefr join`正好相反。



### NULL

在MYSQL中判断空值使用`=`和`!=`是无效的，

`NULL`与任何其他值的比较结果一定是`false`，需要使用`NULL`和`IS NULL`。

在创建表的时候使用`NULL`和`NOT NULL`来设置完整性约束。



### 正则表达式

>   MYSQL也是支持正则表达式匹配的，例如`link`子句中可以使用`%`来匹配任意字符。

在MYSQL中使用正则表达式需要使用` REGEXP`子句来连接待查找字段和模式串。

常用模式：

| 模式       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| ^          | 匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。 |
| $          | 匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。 |
| .          | 匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用象 '[.\n]' 的模式。 |
| [...]      | 字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。 |
| [^...]     | 负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。 |
| p1\|p2\|p3 | 匹配 p1 或 p2 或 p3。例如，'z\|food' 能匹配 "z" 或 "food"。'(z\|f)ood' 则匹配 "zood" 或 "food"。 |
| *          | 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。 |
| +          | 匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。 |
| {n}        | n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。 |
| {n,m}      | m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。 |

[上表引自RUNOOB](https://www.runoob.com/mysql/mysql-regexp.html)



### 临时表

临时表的生命周期与当前账号登陆时间等同，退出登陆时，该表空间释放。

创建临时表需要使用`TEMPORARY`子句修饰`table`。

手动删除使用`drop`子句。



### 复制表

当需要完全的克隆一个已存在的表，只需要找出建表记录，使用该建表记录创建新表，然后将数据 拷贝拷贝进入即可。

1. 找出建表记录

   `show create table 表名`

2. 更改表名创建科隆表

3. 克隆数据

   `insert into ... select...`



### 重复数据处理

* 创建表时设置约束

  使用`primary key`将不可重复字段设置为主键。

  1.  在设置了主键或者唯一索引后使用通常的`insert into`插入重复数据将会报错
  2.  使用`insert ignore into`插入重复数据将仅仅是警告，然后忽略重复数据不执行插入。
  3.  使用`replace into`插入重复数据将使用带插入数据更新旧的数据。

* 筛选

  1.  在`select`的时候使用`distinct`筛掉重复数据。
  2.  使用`group by` 对不需要重复的字段进行读取不重复的字段。





---

参考：

[RUNOOB.COM](https://www.runoob.com/mysql/mysql-tutorial.html)
[CSDN Blog ](https://blog.csdn.net/jiangnan2014/article/details/17229713)	
[CSDN Blog](https://blog.csdn.net/AinUser/article/details/72803175)
[CSDN Blog](https://blog.csdn.net/love_xsq/article/details/42417917)
