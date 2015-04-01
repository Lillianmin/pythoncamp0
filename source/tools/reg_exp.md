#正则表达式
1. 去掉每行空格至结尾的所有内容
```
AliceBlue 	#F0F8FF	 	Shades	Mix
AntiqueWhite 	#FAEBD7	 	Shades	Mix
Aqua 	#00FFFF	 	Shades	Mix
Aquamarine 	#7FFFD4	 	Shades	Mix
Azure 	#F0FFFF	 	Shades	Mix
Beige 	#F5F5DC	 	Shades	Mix
Bisque 	#FFE4C4	 	Shades	Mix
Black 	#000000	 	Shades	Mix
BlanchedAlmond 	#FFEBCD	 	Shades	Mix
Blue 	#0000FF	 	Shades	Mix
BlueViolet 	#8A2BE2	 	Shades	Mix
Brown 	#A52A2A	 	Shades	Mix
BurlyWood 	#DEB887	 	Shades	Mix
CadetBlue 	#5F9EA0	 	Shades	Mix
Chartreuse 	#7FFF00	 	Shades	Mix
Chocolate 	#D2691E	 	Shades	Mix
Coral 	#FF7F50	 	Shades	Mix
```
即空格后面匹配一个或者多个字符(.*)
vi中:
```
:%s/ .*$//g
```
2. 每行末尾加上,号,行末是$
```
AliceBlue
AntiqueWhite
Aqua
Aquamarine
Azure
Beige
Bisque
Black
BlanchedAlmond
Blue
BlueViolet
Brown
BurlyWood
CadetBlue
Chartreuse
Chocolate
Coral
```
vi中：
```
:%s/$/,/g
```
3.所有行合并成一行.行首是^
```
:g/^/-j
```
4.在,号处换行
```
:%s/,/,\r/g
```
