# 变量
* 命名规则
  与C/C++一致。
  * 字母、数据、下划线，以字母或者下划线开头，不能以数字开头。
  * 类名，以单词首字母大写组合，缩写全部大写。例：ClassName。
  * 变量名，以单词小写组合，组合之间以_分开。例：var_name。
* 变量类型
不用显示说明，根据值确定变量类型

# 基本数据类型
int float long str
数据类型转换
float to int 是round down

# 语句
语句结束不用;号来表示结尾

# 表达式
* 整除
// 表示整除
* 幂
a的b次方，a ** b

# 布尔计算
True与False，不是1与0，也不是true与false
* 与
  and 
* 或
  or 
* 非
  not 

# 函数
* 定义
使用def function_name(param1, param2):
* 代码块
代码块不用{}，而是以冒号（:）开始，严格用缩进来控制
 * 所有代码块都如此。比如if，elif，else
* 返回值
函数没有显示的返回类型，根据return的返回值来来确定。如果无return则是返回None。

# 包导入
使用import,与JAVA一致,不是include

# str
* 可以用“abc”，‘abc’赋值，若字符串中有特殊字符如：‘，则一定要用“”
* 可以用同名数组+index下标来取字符。如：str1 = "abc", char1 = str1[0]
* 可以用下标范围来取子字符串。str1 = "abc", substr = str1[0:2]。这里substr=“ab”。若取子字符串的起始未指定则子字符串从最前面开始。若末尾未指定则子字符串直至最后。


