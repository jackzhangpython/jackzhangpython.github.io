---
layout: post
title:  "Linux常用命令 - 操作文件"
date:   2016-08-07
categories: Linux
---

在Linux系统中，**_一切皆文件_**。想要愉快的使用Linux系统，操作文件的命令系列是必备技能之一。

##一 列出目录 ls
---
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
---
显示当前所在工作目录绝对路径
<p>_pwd [-L | -P]_</p>

	linux:ning user$ pwd
	/Users/user/File/ning
	
##三 切换目录 cd
---
切换到指定工作目录，使用次数最多的命令之一
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
	linux:Maven user $

> 引用自《[Linux命令速查手册](https://book.douban.com/subject/4046184/ "豆瓣读书")》