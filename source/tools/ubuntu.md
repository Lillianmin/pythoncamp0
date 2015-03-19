# ubuntu 使用与技巧

### 添加root帐户
ubuntu安装后，默认无root帐号，需要添加：
```
sudo passwd root
```
输入两次一致的密码后，即添加了root帐号

### 从普通用户切换到root
```
su
```
输入正确的密码，即进入了root用户

### 安装软件包
```
apt-get isntall Python
```
另一种方式是通过
```
aptitude
```
不再详述。

### 安装deb包
有一些软件包通过apt-get isntall xxx 无法安装，是因为源里没有。
下载安装包如果的是deb格式的，使用下面的命令安装
```
sudo dpkg -i xxx.deb
```
如果下载的安装包是rpm格式的，需要先转换为deb格式,再安装。
```
sudo apt-get install alien
sudo alien packagename.rpm
sudo dpkg -i packagename.deb
```
###命令自动补全
按Tab键呀

###选中粘贴
鼠标选中文字之后，按鼠标中键粘贴。

### 命令不知道怎么使用
-h是简单的命令参数说明。man是详细的帮助文档。
比如：
```
git -h
```
```
man git
```
再比如：
```
man markdown
```
可以看到，这个工作是作什么用的，一些相关的信息。如：markdwon的语法，详见：http://daringfireball.net/projects/markdown/syntax

##修改默认编辑器
ubuntu默认的编辑器是emacs，比如git commit时需要输入commit信息，此时默认是在emacs编辑的。
如果习惯用vi或者更愿意学习vi编辑器，那么做如下修改：
```
vi ~/.bashrc
```
添加一行
```
export GIT_EDITOR=vim
```
~/表示的是你的主目录,/home/username

