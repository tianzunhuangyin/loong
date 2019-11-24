# Win10上配置MySQL(压缩包)环境

MySQL的安装版（exe，msi）应该还是安装之后会自动添加服务，而压缩包这不会。

## 1.	前提条件

### 1.	Mysql的64为压缩包

```
mysql-8.0.16-winx64.zip
```

### 2.	解压到自定义位置

我自己解压到E盘的MySQL目录下

```
E:\MySQL\mysql-8.0.16-winx64
```

## 2.	安装服务

### 1.	使用管理员权限打开CMD窗口

![1573968217709](Win10上配置MySQL(压缩包)环境/1573968217709.png)

### 2.	进入MySQL下的bin目录



```
>e:
E:\>cd MySQL\mysql-8.0.16-winx64\bin

//1.安装Mysql服务
>mysqld.exe --install
//2.指定服务名(开机自启)
>mysqld.exe --install MySQL
//2.指定服务(非开机自启)
>mysqld.exe --install-manual
//3.启动服务
>net start MySQL

//赠送一条命令,删除服务
>mysqld.exe --remove
```



