# 树莓派安装QT（全部库）

在网上现有的资料中大部分只有前两个命令，少量有三个命令，因此写下该博客
在树莓派上安装QT5的全部库，包括QtQuick、QtMultimedia库。

```
sudo apt-get install qt5-default			//安装默认基本库
sudo apt-get install qtcreator				//安装QtCreator
sudo apt-get install qtdeclarative5-dev  	//安装QtQuick
sudo apt-get install qtmultimedia5-dev   	//安装QtMultimedia
sudo apt-get install libqt5sql5-mysql        	//安装QtMySQL
```

