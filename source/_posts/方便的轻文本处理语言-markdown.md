---
title: 方便的轻文本处理语言-markdown
date: 2019-09-02 16:05:09
cover: title.jpg
tags: tools
---

>   如果你并不需要word那么复杂的功能，没有极强的专业性需求，那么markdown是你很好的选择。
>
>   不同的markdown编辑器对markdown语法的支持与拓展会有一些出入，但是基础语法基本都会支持。
>
>   有的效果默认关闭，需要到设置里打开。
>
>   本文代码使用typora编辑器。推荐[typora](https://typora.io/)。
>
>   一般的markdown编辑器都是可以导出为各种格式的：pdf、html、word以及png等等。
>
>   粘贴下面代码框中的代码到你的markdown编辑器中看看效果！
>
>   部分高级用法内容资源来自网络其他博客和wiki。



## 标题

在文字的开头加上若干`#`最后跟上空格，这段文字就变成了相应等级的标题。

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```



## 引用

当我们需要加上一段引用文字或者一些声明的时候可以选择使用引用语法

```markdown
> 这是引用
>> 这也是引用
```



## 列表

当我们需要列举若干项的时候可以选择使用有序、无序列表和任务列表

```markdown
* 无序列表1
* 无序列表2

- 无序列表1
- 无序列表2

1. 有序列表1
2. 有序列表2

- [ ] 任务列表，未完成项
- [x] 任务列表，已完成项
```



## 插入代码

当我们需要插入一段代码的时候可以使用代码块语法。

1. 文本中插入一段短的代码可以使用键盘中`1`左边的点把代码括起来

2. 长的规范的代码可以适用代码块，使用键盘中`1`左边的点，输入两行这个点，每行三个，第一行行末输入代码的语言。

3. 示例

   C语言中使用`#include<>`引入头文件

   ```c
   #include <stdio.h>
   int main () {
   	return 0;
   }
   ```



## 数学公式

当我们需要插入数学公式，并且想要漂亮一些，可以使用数学公式的语法，更多的markdown数学转义符号请自行搜索，很容易搜到的。

```markdown
在数学中$\sum$ 是求和符号。
例如：
$$
$\sum^{k}_{i = 1}{x / i}$
$$
```



## 文字显示控制

我们可能有时候需要对文本加粗、高亮等，这里markdown也提供了支持。

每种效果可以叠加使用。

```markdown
*斜体*
**加粗**
==高亮==
~~删除~~
***斜体并加粗***
==*斜体并高亮*==
```



## 表格

当然了， 常用的表格markdown也是支持的。

通过冒号可以控制对齐方式

```markdown
|first head|second head|third head|
|:--|:--:|--:|
|左对齐列|中心对齐列|右侧对齐列|
|asd|fgh|jkl|
```



## 脚注

markdown也是支持脚注的。

```markdown
可以这样使用脚注[^1]
[^1]:脚注1的内容
```
## 分割线

当我们想要分割两段内容的时候可以用分割线

```markdown
上面的内容
---
下面的内容
```



## 引入图像与链接

引入图像和链接是必不可少的功能。

```markdown
![Linux引入图片](/home/UserName/1.jpg)
![windows引入图片](C:\Users\UserName\Downloads\2.png)
[百度](https://www.baidu.com)
[参考链接]: www.baidu.com
<www.baidu.com>
[页内链接](#一级标题)
```



## 目录树

当文本过长，需要加上目录树。

```markdown
文本1

[TOC]

文本2
```



## emoji表情

有些markdown编辑器是支持emoji表情插入的。

```markdown
:smile:
```



## 文本折叠

当我们的某个段落太长需要折叠起来，markdown貌似没有原生语法支持折叠，

但是有些markdown编辑器是支持HTML语法的，这里可以使用HTML实现。

```html
<details>
    <summary>测试标题</summary>
测试文本
</details>
```

## 注释

markdown当然也有像C语言中`//`一样的注释

```markdown
<!--这是注释-->
```



## 流程图

markdown当然也可以画流程图

按照上面插入代码的方式，按照下面的例子编写代码插入到代码块中，语言是mermaid

```markdown
flowchat
flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->op
```



## 时序图

既然支持流程图，当然也支持时序图，语言也是mermaid。

```markdown
sequenceDiagram
X->>Y: 一起去电影院怎么样？
Note right of Y: 去不去
Y->>X: 好的，我等你！
```



## 甘特图

语言也是mermaid。

```markdown
gantt
dateFormat  YYYY-MM-DD
title 软件开发甘特图
    
section 设计
	需求                      :done,    des1, 2014-01-06,2014-01-08
	原型                      :active,  des2, 2014-01-09, 3d
	UI设计                    :         des3, after des2, 5d
	未来任务                   :         des4, after des3, 5d

section 开发
    学习准备理解需求                      :crit, done, 2014-01-06,24h
    设计框架                             :crit, done, after des2, 2d
    开发                                 :crit, active, 3d
    未来任务                              :crit, 5d
    耍                                   :2d

section 测试
    功能测试                              :active, a1, after des3, 3d
    压力测试                               :after a1  , 20h
    测试报告                               : 48h
```

[来自百度经验](https://jingyan.baidu.com/article/48b558e3035d9a7f38c09aeb.html)

