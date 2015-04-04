#ubuntu与windows simplegui本地环境
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

```
python guess_number.py
```

提示没有create_frame

```
pydoc simplegui
```

果然里面没有create_frame,怀疑安装了错误的包

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
```
python guess_number.py
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

## windows simplegui环境
查看之前的 simpleguics2pygmae连接，找到[for windows的安装步骤](https://simpleguics2pygame.readthedocs.org/en/latest/index.html#complete-installation-on-window-in-few-steps)。
###使用pip安装simpleguics2pygame
* 安装pip
  * [参考](https://pypi.python.org/pypi/pip) 
  * [下载pip](https://pypi.python.org/packages/source/p/pip/pip-6.0.8.tar.gz#md5=2332e6f97e75ded3bddde0ced01dbda3)
  * 解压，进入pip-6.0.8目录执行

```
python setup.py install
```

* 安装SimpleGUICS2Pygame
```
pip install SimpleGUICS2Pygame
```

* 安装matplotlib

```
pip install matplotlib
```

或者：
  * [下载](http://jaist.dl.sourceforge.net/project/matplotlib/matplotlib/matplotlib-1.4.3/matplotlib-1.4.3.tar.gz)
  * 解压，进入matplotlib-1.4.3目录，执行：
  
  ```
  python setup.py install
  ```

报错：

```
error: Microsoft Visual C++ 10.0 is required<Unable to find vcvarsall.bat>.
```

  * 安装Visual C++ 2010 Express(官网下载需要注册windows账号，而且注册居然网络很慢很慢！)。从中关村网站上下载，发现有1.8G。炸裂！不考虑使用VS。
  * 使用MinGW
    * [参考](http://stackoverflow.com/questions/3297254/how-to-use-mingws-gcc-compiler-when-installing-python-package-using-pip)
    * [下载安装器](http://heanet.dl.sourceforge.net/project/mingw/Installer/mingw-get-setup.exe)
    * 安装，等待等待，Continue
	* 勾选Basic Setup中的所有项->Installation->Apply，等待等待。
	* 添加MinGW安装路径至系统环境变量PATH
	  * 我的电脑->属性->高级系统设置-环境变量->系统变量下的Path->末尾添加
	  ```
	  E:\Development\MinGW\bin;
      ```

        添加后环境变量如下：

      ```
      E:\Development\Ruby22\bin;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\;%JER_HOME%\bin;%JAVA_HOME%\bin;%ANDROID_SDK_HOME%\platform-tools;%ANDROID_SDK_HOME%\tools;E:\Development\subversion\bin;E:\Development\grep20d_win;E:\Development\apache-ant-1.9.2\bin;E:\Development\Python3.4;%systemroot%\System32\WindowsPowerShell\v1.0\;E:\Development\Python3.4\Scripts;E:\Development\Git\bin;E:\Development\Git\share\vim\vim74;E:\Development\MinGW\bin;
      ```
	* 设置Python编译器为MinGW
	  * 在Python安装目录的Lib->distutils下，新建文件distutil.cfg，写入
	  ```
[build]
compiler=mingw32
	  ```

* 安装Pygame
  * [下载Pygame](http://www.pygame.org/ftp/pygame-1.9.1release.tar.gz)
  * 解压进入pygame-1.9.1release，执行

```
python setup.py install
```


