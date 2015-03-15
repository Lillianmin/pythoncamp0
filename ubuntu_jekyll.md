uubntu 搭建jekyll环境
============
安装ruby
=

sudo apt-get install ruby
sudo apt-get install ruby-dev

更改gem源
=
列出源
gem sources -l

*** CURRENT SOURCES ***

https://rubygems.org/

删除源
gem sources --remove https://rubygems.org/
https://rubygems.org/ removed from sources


添加源
gem sources -a http://ruby.taobao.org/
http://ruby.taobao.org/ added to sources

查看更改后的源
gem sources -l
*** CURRENT SOURCES ***

http://ruby.taobao.org/



安装jekyll
sudo gem install jekyll 

安装markdown解析
sudo gem install rdiscount

测试jekyll
jekyll new test
/home/mll/.gem/ruby/2.1.0/gems/execjs-2.4.0/lib/execjs/runtimes.rb:45:in `autodetect': Could not find a JavaScript runtime. 

See https://github.com/sstephenson/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)
	from /home/mll/.gem/ruby/2.1.0/gems/execjs-2.4.0/lib/execjs.rb:5:in `<module:ExecJS>'
	from /home/mll/.gem/ruby/2.1.0/gems/execjs-2.4.0/lib/execjs.rb:4:in `<top (required)>'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /home/mll/.gem/ruby/2.1.0/gems/coffee-script-2.3.0/lib/coffee_script.rb:1:in `<top (required)>'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /home/mll/.gem/ruby/2.1.0/gems/coffee-script-2.3.0/lib/coffee-script.rb:1:in `<top (required)>'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-coffeescript-1.0.1/lib/jekyll-coffeescript.rb:2:in `<top (required)>'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-2.5.3/lib/jekyll/deprecator.rb:46:in `block in gracefully_require'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-2.5.3/lib/jekyll/deprecator.rb:44:in `each'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-2.5.3/lib/jekyll/deprecator.rb:44:in `gracefully_require'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-2.5.3/lib/jekyll.rb:166:in `<top (required)>'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /home/mll/.gem/ruby/2.1.0/gems/jekyll-2.5.3/bin/jekyll:6:in `<top (required)>'
	from /usr/local/bin/jekyll:23:in `load'
	from /usr/local/bin/jekyll:23:in `<main>'
	
	安装
sudo apt-get install nodejs


mkdir note
   13  cd note
   14  jekyll new .
   18  git init
   19  git add -A
   20  git commit
   23  git remote add origin git@github.com:Lillianmin/note.git
   31  git push origin master

