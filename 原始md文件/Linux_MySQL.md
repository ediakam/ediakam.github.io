#### 命令 ####

 #查看版本
    
	mysql --version

 **#进入mysql命令**

	mysql -u root ip  
	mysql -u root@localhost  (没有密码的情况)

 #创建数据库

	create database [dataname]
 
 #删除数据库

	drop database [dataname]
 
 #查看数据库
	
	show databases;
 
 **#进入具体数据库**

	use [dataname]
 
 **#查看数据库表**

	show tables;
 
 #删除表

	drop table [tablename];
 
 **#查看具体表的结构**

	desc [tablename];
 
 **#查找数据**

	select * from tablename;
 
 #插入数据

	insert insto [tablename](103,'test');
 
 #修改数据

	update [tablename] set name='' and id=103
 
 #删除数据

	delete [tablename] where name=''
 
 **#添加索引**

	alter table [tablename] add fulltext index([columnname]);
 
 **#查看索引**

	show index from [tablename] \G
 
启动开关: service mysql {start|stop|status|restart|condrestart|try-restart|reload|force-reload}
 

#### 修复表 ####

 #查看表状态

	show table status like 'tablename' \G;

 #检测表

	check table tablename

 #修复表

	repair table tablename
 
#### 压缩表 ####

 #查看数据文件位置

	show global variables like '%datadir%';

 #压缩文件

	myisampack *.MYD
 
#### mysql 备份 ####

 **冷备份**

 #备份

停掉mysql 服务，在操作基本备份mysql 数据库

重启mysql服务，备份重启以后生产binlog

 #逻辑恢复

	mysql -u root -p [databasename]<[backname].sql
 
**逻辑备份**

 #导出整个数据库

	mysqldump -u root -p [databasename] -F >[backname].sql

 #导出一个表

	mysqldump -u root -p [databasename] [tablename]>[table].sql

 #导出数据库结构

	mysqldump -u root -p -d --add-drop-table [databasename]>[database].sql

-d 没有数据 --add-drop-table 在每个create语句之前增加一个drop table 

#### 关于my.cnf ####

**Linux查看mysql使用的是哪个my.cnf**

1.查看是否使用了指定目录的my.cnf 

	ps aux|grep mysql|grep 'my.cnf'

2.查看mysql默认读取my.cnf的目录 

	mysql --help|grep 'my.cnf'  (会按顺序加载)

3.启动时没有使用配置文件 

如果没有设置使用指定目录my.cnf文件及默认读取目录没有my.cnf文件，表示mysql启动时并没有加载配置文件，而是使用默认配置。 

my.cnf内容详解：[https://www.cnblogs.com/panwenbin-logs/p/8360703.html](https://www.cnblogs.com/panwenbin-logs/p/8360703.html)