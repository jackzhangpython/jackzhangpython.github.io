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
列出指定目录/子目录中文件，path可以是绝对路径、相对路径、通配符

	#相对路径
	EBJ1011:~ xiaoningzhang$ ls ~/Java/   
	Maven			apache-tomcat-7.0.63
	
	#相对路径
	EBJ1011:~ xiaoningzhang$ ls /Users/xiaoningzhang/Java/
	Maven			apache-tomcat-7.0.63
	
	#通配符
	EBJ1011:~ xiaoningzhang$ ls ~/Java/apache-tomcat-7.0.63/*.txt
	/Users/xiaoningzhang/Java/apache-tomcat-7.0.63/RUNNING.txt