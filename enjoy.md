目标：把discourse安装在自己的电脑上，能够启动运行。

下面我会按照以下步骤展开工作(每个步骤所需时间仅是个估计值)

1.Install and configure PostgreSQL 9.1+.                        (4H)

2.Install and configure Redis 2+.                               (4H)    

3.Install ImageMagick                                           (4H)

4.Install libxml2, g++, and make.                               (4H)

5.Install Ruby 1.9.3 and Bundler.                               (0.5H)

6.Clone the project and bundle.                                 (1H)

7.Copy config/database.yml.development-sample to config/database.yml. 
  Copy config/redis.yml.sample to config/redis.yml.             (0.5H)

8.Edit the files to point to your postgres and redis instances. (2H)

9.rails server start and debug                                  (4H)

这些步骤仅仅参考用，我会将我做的每一操作步骤、及详细情况更新在下面！


=================
**系统：OS X 10.9.4**


=================
**PostgreSQL**的安装

安装包名：Postgres.app

下载地址： http://postgresapp.com/

安装：将该app拖拽到applications文件夹，

启动：点击该app图标，即可启动PostgreSQL服务



================
**Redis 2+**的安装

安装包名：redis-2.6.7.tar.gz

下载地址：http://redis.googlecode.com/files/redis-2.6.7.tar.gz

安装：

1、cd到该安装包所在位置

2、解压安装包

	tar xvf redis-2.6.7.tar.gz
	
3、进入解压后到文件夹

	cd redis-2.6.7
	
4、编译

	make
	
5、安装

	make install
	
6、进入utils文件夹，执行install_server.sh文件

	cd utils
	
	./install_server.sh
	
7、这是会提示设置项，暂且均按下enter键，表示使用默认

8、进入 src文件夹

	cd ..
	
	cd src
	
9、启动Redis服务

	./redis_server
	

================
**ImageMagick**的安装

安装包名：ImageMagick-x86_64-apple-darwin13.2.0.tar.gz

下载地址：http://www.imagemagick.org/download/binaries/ImageMagick-x86_64-apple-darwin13.2.0.tar.gz  

安装：

1、cd到安装包所在位置

2、解压安装包

	tar xvzf ImageMagick-x86_64-apple-darwin13.2.0.tar.gz
	
3、更改解压后的文件夹名

	mv ImageMagick-x86_64-apple-darwin13.2.0 ImageMagick
	
4、移动文件夹$HOME下

	mv ImageMagick $HOME
	
4、增加环境变量MAGICK_HOME到path中

	export MAGICK_HOME="$HOME/ImageMagick"
	
5、把ImageMagick\bin加到path中

	export PATH=“$MAGICK_HOME/bin:$PATH"
	
6、增加环境变量DYLD_LIBRARY_PATH

	export DYLD_LIBRARY_PATH=“$MAGICK_HOME/lib/"
	

================================================
**Ruby 2.1.1** 与 **Rails 4.1.4** 的安装

1、首先安装RVM 

	curl -L https://get.rvm.io | bash -s stable
	
执行后会通过homebrew安装依赖包，最后成功安装RVM

2、重新打开终端

3、安装Ruby 2.1.1

	rvm install 2.1.1
	
4、设置系统默认ruby版本为2.1.1

	rvm 2.1.1 —default
	
5、安装Rails 4.1.4

	gem install rails -v 4.1.4


=================================
下载**discourse**源码，并安装所需gem

1、cd到workspace文件夹(当前处在&HOME位置)

	cd workspace
	
2、克隆

	git clone https://github.com/discourse/discourse.git
	
   结束后，会在workspace文件下看到discourse文件夹
   
3、进入discourse文件夹

	cd discourse
	
4、安装所需gem

	bundle install
	
   这个如果网速不好的话，要安装了好长时间。

=====================================
**数据库创建及迁移**

	rake db:create db:migrate

=====================================
**启动服务器**

	rails s

======================================
**让外网访问**

1、进入路由器设置页面，找到转发规则，进行设置

	服务端口：80
	
	内部端口：3000
	
	IP地址：192.168.1.107（局域网分配的ip）
	
	协议：ALL
	
2、在浏览器输入公网IP地址即可访问



