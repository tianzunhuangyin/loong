# 树莓派中的C++程序添加MySQL头文件

有的时候在编写C++程序时，树莓派上是不需要有MySQL数据库的，只需要有MySQL相关的开发包就可以，下面来介绍怎么添加头文件。

## 1.	安装相关程序包

```
$:shdo apt-get install libmysql++-dev
```

## 2.	检查是否有相关程序包

```
$:sudo find / -name mysql.h
/usr/include/mysql/mysql.h
```

可以看见mysql头文件已经安装，接下来可以愉快的编程了。



## 3.	参考

[树莓派添加MySQL头文件](https://blog.csdn.net/linrulei11/article/details/7298834)

