# Win10 使用Qt连接Mysql(QSqlDatabase: QMYSQL driver not loaded的解决方案)

## 1.	简介

在使用Qt在win上进行数据库学习过程中，出现如题问题。刚开始使用的是Qt 5.14.0，安装时选择了MinGW环境时只有不到3个G的占用，后来进行查阅后重新装了Qt 5.12.3，此时竟然有快8个G的占用，大概是新版只是用来探路的吧。。。。

先决条件：

- **Mysql已安装**

## 2.	解决

## 2.1	安装Qt5.12.3 。

下载地址[5.12.3](http://download.qt.io/official_releases/qt/5.12/5.12.3/),

## 2.2	检查Qt是否自带MySQL支持。

```
E:\Qt\Qt5.12.3\5.12.3\mingw73_64\plugins\sqldrivers
```

![1577622625456](Win10 使用Qt连接Mysql(QSqlDatabase QMYSQL driver not loaded的解决方案)/1577622625456.png)

## 2.3	Qt环境配置

将Mysql下的相关库复制到Qt下。

```
E:\MySQL\mysql-8.0.16-winx64\lib
```

![1577622763442](Win10 使用Qt连接Mysql(QSqlDatabase QMYSQL driver not loaded的解决方案)/1577622763442.png)

选中Mysql中的两个文件库，复制到Qt的bin中。

```
E:\Qt\Qt5.12.3\5.12.3\mingw73_64\bin
```

![1577622858830](Win10 使用Qt连接Mysql(QSqlDatabase QMYSQL driver not loaded的解决方案)/1577622858830.png)

## 参考：

[环境配置](https://mp.weixin.qq.com/s?src=11&timestamp=1577621675&ver=2064&signature=Wx-CBPad4Gbhj1ilifA-*i5EVp739yZEQ0D5RTwab05IOU7S9mWk6s1vb5sQxOPcW3OLvgK1a1qiuheEE0*60WBMyMKJXVPM0-ube*v9Wfn*fl0EwRyBHpyB2t7uvm5e&new=1)

