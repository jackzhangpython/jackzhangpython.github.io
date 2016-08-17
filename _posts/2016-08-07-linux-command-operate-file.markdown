---
layout: post
title:  "Linux常用命令 - 操作文件"
date:   2016-08-07
categories: Linux
---

在Linux系统中，**_一切皆文件_**。想要愉快的使用Linux系统，操作文件的命令系列是必备技能之一。

##一 列出目录 ls
列出目录/子目录中文件，使用次数最多的命令之一，默认按字母排序。
<p>_ls [OPTION]... [FILE]..._</p>

####ls path 
列出指定目录/子目录中文件，path可以是绝对路径、相对路径、通配符。

	#相对路径 列出user/Java/目录下文件
	linux:~ user$ ls ~/Java/   
	Maven			apache-tomcat-7.0.63
	
	#相对路径 列出user/Java/目录下文件
	linux:~ user$ ls /Users/user/Java/
	Maven			apache-tomcat-7.0.63
	
	#通配符 列出user/Java/apache-tomcat-7.0.63/目录下文本文件.txt
	linux:~ user$ ls ~/Java/apache-tomcat-7.0.63/*.txt
	/Users/user/Java/apache-tomcat-7.0.63/RUNNING.txt

####ls -R
递归列出目录和所有子目录中文件。

	linux:Java user$ ls -R ~/Java/Maven/
	LICENSE		README.txt	boot		lib
	NOTICE		bin		conf

	/Users/user/Java/Maven//bin:
	m2.conf		mvn.cmd		mvnDebug.cmd
	mvn		mvnDebug	mvnyjp

	/Users/user/Java/Maven//boot:
	plexus-classworlds-2.5.2.jar

	/Users/user/Java/Maven//conf:
	logging		settings.xml	toolchains.xml
	..........

####ls -a
列出目录中所有文件，包括隐藏文件(文件名前加.为隐藏文件)。

	linux:Java user$ ls -a
	.			.DS_Store		apache-tomcat-7.0.63
	..			Maven
	
####ls -l
列出目录中文件的详细信息，权限、所有者、所属组、大小、操作时间等。

	linux:Maven user$ ls -l
	total 56
	# 权限  硬链接/文件数量 所有者    所属组 大小(字节)  操作日期  文件名
	--------------------------------------------------------------
	-rw-r--r--@  1 user  staff  19091  4 22  2015 LICENSE
	-rw-r--r--@  1 user  staff    182  4 22  2015 NOTICE
	-rw-r--r--@  1 user  staff   2541  4 22  2015 README.txt
	drwxr-xr-x@  8 user  staff    272  4 22  2015 bin
	drwxr-xr-x@  3 user  staff    102  4 22  2015 boot
	drwxr-xr-x@  5 user  staff    170  4 22  2015 conf
	drwxr-xr-x@ 75 user  staff   2550  8 14  2015 lib

####ls -t
按时间倒序列出目录中文件(-r 正序)。

	#-l -t组合，按时间倒序
	linux:Downloads user$ ls -lt
	total 409672
	-rw-r--r--@  1 user  staff    1760739  8 10 21:24 Flux.zip
	drwxr-xr-x@ 19 user  staff        646  8  7 14:07 thunder-master
	drwxr-xr-x@ 19 user  staff        646  7 29 22:18 getmicah
	drwxr-xr-x@ 27 user  staff        918  6 22 13:56 rubygems-2.6.6
	..........
	
	#-l -t -r组合，按时间正序
	linux:Downloads user$ ls -ltr
	total 409672
	drwxr-xr-x@ 27 user  staff        918  6 22 13:56 rubygems-2.6.6
	drwxr-xr-x@ 19 user  staff        646  7 29 22:18 getmicah
	drwxr-xr-x@ 19 user  staff        646  8  7 14:07 thunder-master
	-rw-r--r--@  1 user  staff    1760739  8 10 21:24 Flux.zip
	..........

####ls -S
按文件大小倒序列出目录中文件(-h 提高大小可读性)。

	#-l -S组合，按文件大小倒序
	linux:Downloads user$ ls -lS
	total 409672
	-rw-r--r--@  1 user  staff  184065647  2 21 15:57 webstorm.dmg
	-rw-r--r--@  1 user  staff   12572852  2 21 16:13 node-v4.3.1.pkg
	-rw-r--r--@  1 user  staff    7416170  2 21 18:20 NeteaseMusic.dmg
	-rw-r--r--@  1 user  staff    1760739  8 10 21:24 Flux.zip
	..........
	
	#-l -S -r组合，按文件大小正序
	linux:Downloads user$ ls -lSr
	total 409672
	-rw-r--r--@  1 user  staff    1760739  8 10 21:24 Flux.zip
	-rw-r--r--@  1 user  staff    7416170  2 21 18:20 NeteaseMusic.dmg
	-rw-r--r--@  1 user  staff   12572852  2 21 16:13 node-v4.3.1.pkg
	-rw-r--r--@  1 user  staff  184065647  2 21 15:57 webstorm.dmg
	
	#-h 自动转换为K,M,G提高大小可读性
	linux:Downloads user$ ls -lSrh
	total 409672
	-rw-r--r--@  1 user  staff   1.7M  8 10 21:24 Flux.zip
	-rw-r--r--@  1 user  staff   7.1M  2 21 18:20 NeteaseMusic.dmg
	-rw-r--r--@  1 user  staff    12M  2 21 16:13 node-v4.3.1.pkg
	-rw-r--r--@  1 user  staff   176M  2 21 15:57 webstorm.dmg

##二 显示路径 pwd
显示当前所在工作目录绝对路径。
<p>_pwd [-L | -P]_</p>

	linux:ning user$ pwd
	/Users/user/File/ning
	
##三 切换目录 cd
切换到指定工作目录，使用次数最多的命令之一。
<p>_cd [-options] [args ...]_</p>
	
####cd path
使用相对路径/绝对路径切换当前工作目录。
	
	#使用相对路径切换
	linux:~ user$ cd Java
	linux:Java user$
	
	linux:apache-tomcat-7.0.63 user $ cd ../..
	linux:~ user $ 
	
	linux:Maven user $ cd ~
	linux:~ user $
	
	#使用绝对路径切换
	linux:Maven user $ cd /Users/user
	linux:~ user $
	
####cd -
切换至上一个工作目录。

	linux:Maven user $ pwd
	/Users/user/Java/Maven
	linux:Maven user $ cd ~
	linux:~ user $ cd -
	/Users/user/Java/Maven
	
## 四 创建文件/修改文件时间 touch
修改指定文件时间，如文件不存在则创建。
<p>_touch [-A [-][[hh]mm]SS] [-acfhm] [-r file] [-t [[CC]YY]MMDDhhmm[.SS]] file ..._</p>

	#修改文件时间
	linux:Maven user$ ls -l
	total 56
	-rw-r--r--@  1 user  staff   2541  4 22  2015 README.txt
	linux:Maven user$ touch README.txt
	linux:Maven user$ ls -l
	total 56
	-rw-r--r--@  1 user  staff   2541  8 17 21:34 README.txt
	
	#创建文件a.txt
	linux:Downloads user$ ls
	48362221457590032191.jpg	node-v4.3.1.pkg
	Flux.zip			npm-debug.log
	linux:Downloads user$ touch a.txt
	linux:Downloads user$ ls
	48362221457590032191.jpg	node-v4.3.1.pkg
	Flux.zip			npm-debug.log
	a.txt		

## 五 创建目录 mkdir
在当前工作目录下创建目录。
<p>_mkdir [-pv] [-m mode] directory_name ..._</p>

####mkdir directory
创建指定名称目录。

	linux:Downloads user$ ls
	48362221457590032191.jpg	node-v4.3.1.pkg
	Flux.zip			npm-debug.log
	linux:Downloads user$ mkdir test
	linux:Downloads user$ ls
	48362221457590032191.jpg	node-v4.3.1.pkg
	Flux.zip			npm-debug.log
	test

####mkdir path
为指定路径逐级创建目录。

	linux:test user$ ls
	linux:test user$ mkdir -p downloads/game/wow
	linux:test user$ ls -R
	downloads
	./downloads:
	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	
## 六 复制文件 cp
复制文件/目录到目标位置。
<p>_cp [-R [-H | -L | -P]] [-fi | -n] [-apvX] source_file target_file_</p>
<p>_cp [-R [-H | -L | -P]] [-fi | -n] [-apvX] source_file ... target_directory_</p>

####cp source target
复制文件到目标位置，存在则覆盖。

	#复制到指定目录
	linux:test user$ cp ~/Downloads/a.txt downloads/game/wow/
	linux:test user$ ls -R
	downloads
	./downloads:
	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	a.txt
	
	#复制到当前目录
	linux:test user$ cp ~/Downloads/a.txt .
	linux:test user$ ls -R
	a.txt		downloads
	./downloads:
	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	a.txt
	
	#复制到指定目录 并重命名
	linux:test user$ cp ~/Downloads/a.txt downloads/b.txt
	linux:test user$ ls -R
	a.txt		downloads
	./downloads:
	b.txt	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	a.txt
	
####cp source target(通配符)
复制与通配符匹配的文件到指定目录，存在则覆盖。

	linux:test user$ cp ~/Downloads/*.txt .
	linux:test user$ ls
	a.txt		downloads	

####cp -p source target
复制文件到目标位置，存在则询问是否覆盖。

	linux:test user$ cp -i ~/Downloads/*.txt .
	overwrite ./a.txt? (y/n [n]) y
	linux:test user$ ls
	a.txt		downloads
	linux:test user$

####cp -a source target
复制整个目录及内容到目标位置。

	linux:test user$ cp -a ~/Java/Maven .
	linux:test user$ ls -R
	Maven		a.txt		downloads
	./Maven:
	LICENSE		README.txt	boot		lib
	NOTICE		bin		conf
	
	./Maven/bin:
	.........
	
	./Maven/boot:
	.........	

##移动文件 mv
移动文件/目录到目标目录，也可作为重命名文件来使用。
<p>_mv [-f | -i | -n] [-v] source target_</p>
<p>_mv [-f | -i | -n] [-v] source ... directory_</p>

	#移动文件到目标目录
	linux:test user$ ls
	a.txt		downloads
	linux:test user$ mv a.txt downloads/a.txt
	linux:test user$ ls -R
	downloads
	./downloads:
	a.txt	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	
	#一定文件到目标目录，并重命名
	linux:test user$ mv downloads/a.txt ./b.txt
	linux:test user$ ls -R
	b.txt		downloads
	./downloads:
	game
	
	./downloads/game:
	wow
	
	./downloads/game/wow:
	
	#移动目录到目标目录
	linux:test user$ mv downloads/game/wow .
	linux:test user$ ls -R
	b.txt		downloads	wow
	./downloads:
	game
	
	./downloads/game:
	
	./wow:


> 引用自《[Linux命令速查手册](https://book.douban.com/subject/4046184/ "豆瓣读书")》