---
title: BASH脚本实现素数线性筛
date: 2019-09-02 16:45:33
cover: title.jpg
tags:
- script
- linux
- algorithm
---



* 知识准备
  1. `for`循环
     ```bash
     for i in `seq 1 10`;
     do
     	echo ${i}
     done
     #执行结果
     ---------
     1
     2
     3
     4
     5
     6
     7
     8
     9
     10
     --------
     for ((i = 0; i < 10; i++));
     do
     	echo ${i}
     done
     # 执行结果与上面代码相同
     # 双小括号中可以使用C语言一样的语法进行数学计算
     # echo 是回显
     # 美元符号用来取值：取变量值和数组值（用大括号括把变量或数组起来）、取命令的值（用小括号或<Tab>键上面的``符号括起来，如果用`符号扩起来就不用美元符号取值了）
     ```
  2. `if`分支语句
     ```bash
     num=0
     if [[ ${num} -eq 0 ]];then
     	echo "YES"
     elif [[ ${num} -eq 1 ]];then
     	echo "NO"
     else
     	echo "???"
     fi
     # 执行结果
     # 数值判断用-eq(==)、-ne（!=）、-gt(>)、-ge(>=)、-lt(<)、-le(<=)
     # 字符串判断用逻辑等和不等（==、!=）
     ---------
     YES
     ---------
     ```
  3. expr 语句 该语句后面加上数学表达式，可以求数学表达式的值，但是`*`号前需要加上转义符号`\`
* 代码
  ```bash
  #!/bin/bash
  
  if [[ "x${1}" == x ]];then 
      MAX=10
      else
          MAX=${1}
  fi
  
  num=0
  
  for((i = 0; i < ${MAX}; i++));
  do
  
      prime[${i}]=0
  
  done
  
  for((i = 2; i < ${MAX}; i++));
  do
      
      if [[ ${prime[$i]} -eq 0 ]];then
          prime[$num]=$i
          ((num++))
      fi
      for((j = 0; j < ${num}; j++));
      do
          pj=${prime[$j]}
          if [[ `expr ${i}\*$pj` -gt ${MAX} ]];then
              break;
          fi
          prime[`expr ${i}\*${pj}`]=1
          if [[ `expr ${i}%${pj}` == 0 ]];then
              break;
          fi
      done
  
  done
  
  for((i=0;i<$num;i++));
  do
  
      echo ${prime[$i]}
  
  done
  
  ```




  
