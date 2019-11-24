# Win10 + CLion + 树莓派 + QT 远程开发C++中调用Python程序

原则：能在一个机器上开发的就不在两台机器上！！

## 1.	首先需要配置[远程QT开发环境](https://www.cnblogs.com/BANLOONG/p/11569437.html)

## 2.	配置CMakeLists.txt文件

```
cmake_minimum_required(VERSION 3.14)
project(qt_test)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_AUTOMOC on)
set(CMAKE_AUTOUIC on)
set(CMAKE_AUTORCC on)
set(CMAKE_INCLUDE_CURRENT_DIR on)


find_package(PythonLibs 3.5 REQUIRED)   √
find_package(Qt5 COMPONENTS Widgets Core Gui)
include_directories(${PYTHON_INCLUDE_DIRS})   √

add_executable(qt_test src/main.cpp src/mainwindow.cpp)
target_link_libraries(qt_test python3.5 Qt5::Core Qt5::Gui Qt5::Widgets ${CMAKE_DL_LIBS} )  √
```

其中12、14、17行中添加了Python相关参数。

### 3.	之后就可以在*.cpp文件中调用Python文件了

测试此处就参考[该文吧](https://blog.csdn.net/wmx843230304wmx/article/details/79004437)
		 此处需要注意设置path路径，否则，在导入py文件时，将一直为null，

```
#include <python3.5/python.h>        //此次可以更改Python版本
//使用python之前，要调用Py_Initialize();这个函数进行初始化
Py_Initialize();

if (!Py_IsInitialized()){
    printf("初始化失败！");
    return 0;
}
PyRun_SimpleString("import paramiko");
PyRun_SimpleString("import sys");
PyRun_SimpleString("sys.path.append('/home/loong/workdir/py_sftp_test/')");//这一步很重要，修改Python路径,否则将一直为空（null）,路径可以设置为Python（sftp.python）文件的上一级目录，或许也可以设置为该项目的目录。虽说是win上开发C++/Python混合编程，当总归要在树莓派上运行，因此设置该项目上传到树莓派上的路径

PyObject * pModule = NULL;//声明变量
PyObject * pFunc = NULL;// 声明变量
//PyObject* str = Py_BuildValue( const char )
//pystring
pModule = PyImport_ImportModule("sftp");//这里是要调用的文件名sftp.py
if (pModule==NULL)
{
    cout << "没找到" << endl;
}
pFunc = PyObject_GetAttrString(pModule, "uploder");//这里是要调用的函数名
PyObject* args = Py_BuildValue("(s)", "../3.m4a");//给python函数参数赋值  此处 int型使用 i, string型使用 s 。更多请参考[https://blog.csdn.net/vampirem/article/details/12948955(https://blog.csdn.net/vampirem/article/details/12948955)

PyObject* pRet = PyObject_CallObject(pFunc, args);//调用函数
Py_Finalize();//调用Py_Finalize，这个根Py_Initialize相对应的。
```

### 4.	参考:

- [https://blog.csdn.net/wmx843230304wmx/article/details/79004437](https://blog.csdn.net/wmx843230304wmx/article/details/79004437)
- [https://segmentfault.com/q/1010000018242759/revision](https://segmentfault.com/q/1010000018242759/revision)
- [https://blog.csdn.net/liulina603/article/details/79442021](https://blog.csdn.net/liulina603/article/details/79442021)