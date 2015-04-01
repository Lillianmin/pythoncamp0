#Python 基础
## 变量
* 命名规则
  与C/C++一致。
  * 字母、数据、下划线，以字母或者下划线开头，不能以数字开头。
  * 类名，以单词首字母大写组合，缩写全部大写。例：ClassName。
  * 变量名，以单词小写组合，组合之间以_分开。例：var_name。
* 变量类型
不用显示说明，根据值确定变量类型
* python是注意区分大小写的

## 基本数据类型
int float long str
数据类型转换
float to int 是round down

## 语句
语句结束不用;号来表示结尾

## 表达式
* 整除
// 表示整除
* 幂
a的b次方，a ** b

## 布尔计算
True与False，不是1与0，也不是true与false
* 与
 and，C与JAVA &&
* 或
 or，C与JAVA ||
* 非
 not，C与JAVA !

## 函数
* 定义
使用def function_name(param1, param2):
* 代码块
代码块不用{}，而是以冒号（:）开始，严格用缩进来控制
 * 所有代码块都如此。比如if，elif，else
* 返回值
函数没有显示的返回类型，根据return的返回值来来确定。如果无return则是返回None。

## 条件控制
```
if
    
elif
    
elif
    
else
```
elif与c与java的else if不一致。

## 包导入
使用import,与JAVA一致,不是include

## str
* 可以用“abc”，‘abc’赋值，若字符串中有特殊字符如：‘，则一定要用“”
* 可以用同名数组+index下标来取字符。如：str1 = "abc", char1 = str1[0]
* 可以用下标范围来取子字符串。str1 = "abc", substr = str1[0:2]。这里substr=“ab”。若取子字符串的起始未指定则子字符串从最前面开始。若末尾未指定则子字符串直至最后。

## list
list1 = [1, 82, -6, 4, 5]
* 可以用下标来访问元素，如list1[0]的值为1，也可以通过下标的访问来改变元素的值。如list1[0]=3.
```
print list1[0] #1
print list1[-1] #5
print list[5] #IndexError
list1[0]=3
print list1 # [3, 82, -6, 4, 5]
```
* 用in来判断是否在list中，如 82 in list1，返回True，2 in list1 False.
```
result=(82 in list1) # True
result=(2 n list1) # False
```
* index(object)取得该元素在list中的index
```
index=list1.index(82)
print index # 1
```
* append(object)末尾添加元素
```
list1.append(55)
print list1 # [3, 82, -6, 4, 5, 55]
```
* pop(index),删除指定index的元素，返回的是删除的元素的值.pop()未指定index时,从末尾删除元素,
```
del_value=list1.pop()
print list1, del_value # [3, 82, -6, 4, 5], 55
del_value2=list1.pop(2)
print list1, del_value2 # [3, 82, 4, 5], -6
```
* remove(object),删除第一个值为object的元素
```
list1.remove(82)
print list1 # [3, 4, 5]
* range生成数组,如range(5),[0,1,2,3,4]
|range|value|
|----|----|
|print range(1, 10)|[1, 2, 3, 4, 5, 6, 7, 8, 9]|
|print range(-10, 100, 20)|[-10, 10, 30, 50, 70, 90]|
|print range(100, -10, -20)|[100, 80, 60, 40, 20, 0]|
[更多list相关，查看帮助文档](http://www.codeskulptor.org/docs.html#tabs-Python)
或者使用pydoc,如
```
pydoc list
pydoc list.extend
```
## dictionary
*  

## 注释
```
#这里是注释。这个注释符号跟sh的一样。
```
```
“”“
这里的说明会出现在文档中。java与c用/*xxxx*/ 或者 //xxx
"""
```
```
'''
这里的说明会出现在文档中。java与c用/*xxxx*/ 或者 //xxx
'''
```

