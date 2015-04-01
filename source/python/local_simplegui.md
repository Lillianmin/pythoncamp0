#simplegui本地环境
* 安装了一个simplegui

[simplegui on pypi.pytho.org](https://pypi.python.org/pypi/simplegui/0.1.1)

[simplegui 下载页](http://florian-berger.de/en/software/simplegui/)
```
unzip simplegui-0.1.0.zip
cd simplegui-0.1.0
sudo python setup.py install
```
提示错误：
```
Traceback (most recent call last):
  File "setup.py", line 23, in <module>
    import simplegui
  File "/home/mll/Downloads/personal/OMOOC/simplegui-0.1.0/simplegui.py", line 31, in <module>
    import Tkinter
  File "/usr/lib/python2.7/lib-tk/Tkinter.py", line 42, in <module>
    raise ImportError, str(msg) + ', please install the python-tk package'
ImportError: No module named _tkinter, please install the python-tk package
```
  * install python-tk
```
sudo apt-get install python-tk
sudo apt-get install python3-tk
```
再次回到simplegui-0.1.0执行：
```
sudo python setup.py install
```
python guess_number.py
```
提示没有create_frame
```
pydoc simplegui
```
```
果然里面没有create_frame
怀疑安装了错误的包
* 安装SimpleGUITk

[SimpleGUITk](https://pypi.python.org/pypi/SimpleGUITk)
```
tar zxvf SimpleGUITk-1.1.3.tar.gz 
cd SimpleGUITk-1.1.3/
sudo python setup.py install
```
安装依赖包：
```
sudo apt-get install python-pillow
sudo apt-get install python-pygame
sudo apt-get install python-matplotlib
```
修改导入包名称：
```
import simpleguitk as simplegui
```
python guess_number.py
```
```
终端有输出，但没有图形界面
安装的包还是不对吗？
* 安装SimpleGUICS2Pygame

[查找simplegui](https://pypi.python.org/)

[查找结果](https://pypi.python.org/pypi?%3Aaction=search&term=simplegui&submit=search)

SimpleGUICS2Pygame才是CodeSkulptor的.(说明里SimpleGUITk也是兼容CodeSkulptor的呀！？)

[SimpleGUICS2Pygame](https://pypi.python.org/pypi/SimpleGUICS2Pygame/01.09.00)
```
tar zxvf SimpleGUICS2Pygame-01.09.00.tar.gz 
cd SimpleGUICS2Pygame-01.09.00/
sudo python setup.py install
```
修改导入包名称：
```
import SimpleGUICS2Pygame.simpleguics2pygame as simplegui
```
```
python guess_number.py
```
UI界面一闪而过，终端有输出
为了兼容CodeSkulptor与本地代码，使用下面的导入方式:
```
try:
    import simplegui
except ImportError:
    #iimport simpleguitk as simplegui
    import SimpleGUICS2Pygame.simpleguics2pygame as simplegui
```
由于已经安装了simplegui，但是不是需要的，所以卸载simplegui.
TODO:如果本地simplegui与CodeSkulptor的simplegui都需要用呢？怎么解决名字冲突的问题？

uninstall simplegui

[参考](http://stackoverflow.com/questions/1550226/python-setup-py-uninstall)
```
easy_install pip
pip freeze
sudo pip uninstall simplegui
```
另一种卸载方式:

[参考](http://stackoverflow.com/questions/1231688/how-do-i-remove-packages-installed-with-pythons-easy-install)
```
python setup.py install --record files.txt
cat files.txt | xargs rm -rf
```
### 为什么在终端执行带UI py会马上退出呢
* google "Python simpglegui console closed" 
  未果
* 之前使用组员的py代码测试本地simplegui,后来用自己的simplegui测试没有问题，不会闪退。
  * 查看之前组员代码，是因为frame.start()没有调用,加上frame.start()后，正常。
* 或许SimpleGUITk也没有问题
  使用import simpleguitk as simplegui测试，没有问题。所以SimpleGUITk也是兼容CodeSculptor的simplegui的
