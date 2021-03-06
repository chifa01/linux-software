
---
### 1. 增加新主机不成功

===========更新===========
后来，重新添加新主机，待其完全执行完后即安装成功。

===========old===========
在Cloudera Manager中添加新主机时，首先在新主机上启动agent，之后还未在Cloudera Manager界面执行添加新主机操作，却发现该主机已添上并与之前的主机产生混乱，手动添加该主机也不能成功。

之前碰到该问题后，一切重装即可解决，不过解决该问题不必这么粗暴，应该有更好的解决方案。。。

---
### 2. 重装HDFS出错

**错误描述：** 正在检查 NameNode 的名称目录是否为空。仅在为空时格式化 HDFS。
**解决办法：**在namenode和所有datanode上执行`rm -r /dfs`。

---
### 3. 重装oozie报错

**错误描述：**
```
Error: DB schema exists

Stack trace for the error was (for debug purposes):

java.lang.Exception: DB schema exists
	at org.apache.oozie.tools.OozieDBCLI.validateDBSchema(OozieDBCLI.java:929)
	at org.apache.oozie.tools.OozieDBCLI.createDB(OozieDBCLI.java:184)
	at org.apache.oozie.tools.OozieDBCLI.run(OozieDBCLI.java:127)
	at org.apache.oozie.tools.OozieDBCLI.main(OozieDBCLI.java:78)
```

**解决办法：**`rm -rf /var/lib/oozie/*`

---
### 4. 开启oozie Web界面
启动oozie后进入web界面，提示安装ext-2.2后web才能正常显示。参照[官方--Enabling the Oozie Web Console](http://www.cloudera.com/content/www/en-us/documentation/enterprise/latest/topics/admin_oozie_console.html#concept_fl3_35t_2r_unique_1)操作即可解决。

附ext-2.2.zip下载链接－－[ext-2.2.zip](http://tiny.cloudera.com/oozie-ext-2.2)。

---
### 5. 重装Hive出错

**错误1：**连接数据库出错
**解决办法：**见[ 离线安装Cloudera Manager 5和CDH5(5.3.8) --初始化CM5的数据库](http://blog.csdn.net/u012948976/article/details/49702845)。
	

**错误2：**

	Creating Hive user directory
	
	Failed to execute command Create Hive User Directory on service Hive

**解决办法：**重启HDFS和yarn后再安装即可。

---
### 6. 作业一直是running

**错误描述：**使用hadoop提交简单的作业--wordcount后，一直处于running状态。在作业界面查看，显示作业状态为“accepted”，“unassigned”。

**问题原因：**内存分配不合理。

**解决办法：**进入YARN的 Configuration，搜索“container”，将“Container Memory”设置为2G，默认为1G，将“Container Memory Maximum”设置为2G，默认为1G。

---
### 7. 退出hadoop安全模式

	hadoop dfsadmin -safemode leave 

---
### 8. 查看hadoop进程
1. 切换到hdfs用户
2. 执行` /usr/java/jdk1.8.0_60/bin/jps`．实际上输入`jps`即可，但前提是要把JAVA_HOME配置正确．


----
[↑ 返回上级](https://github.com/asin929/linux-software/blob/master/Big-Data/Big-Data.md)

[← 返回首页](https://github.com/asin929/linux-software)
