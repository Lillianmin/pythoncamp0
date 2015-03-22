#Git与Vim for windows 中文乱码问题
* 参考资料

[解决git在Windows下的乱码问题](http://howiefh.github.io/2014/10/11/git-encoding/)

[Vim 7.3/7.4中文乱码，必须要记下来，太tmd的坑人了](http://lxs647.iteye.com/blog/1994010)

* 自定义安装路径为：E:\Development\Git
* Git for Windows自带安装了vim，路径为：E:\Development\Git\share\vim\
* Windows环境变量添加：E:\Development\Git\bin;E:\Development\Git\share\vim\vim74
* Git配置文件路径：E:\Development\Git\etc
* vim配置文件路径在：E:\Development\Git\bin;E:\Development\Git\share\vim\vimrc
* Git乱码问题，cmd 中输入：
  
```
$ git config --global core.quotepath false          # 显示 status 编码
$ git config --global gui.encoding utf-8            # 图形界面编码
$ git config --global i18n.commit.encoding utf-8    # 提交信息编码
$ git config --global i18n.logoutputencoding utf-8  # 输出 log 编码
$ export LESSCHARSET=utf-8
```

* vim乱码问题，在vimrc配置文件中加入：

```
set fileencodings=utf-8,ucs-bom,shift-jis,latin1,big5,gb18030,gbk,gb2312,cp936  "文件 UTF-8 编码  
" 解决显示界面乱码  
set fileencoding=utf-8  
set encoding=utf-8      "vim 内部编码  
set termencoding=gbk  
```
