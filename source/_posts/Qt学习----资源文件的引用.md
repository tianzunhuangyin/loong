# Qt学习----资源文件的应用

## 1.	使用qrc，相对引用资源

使用

```
“： + 前缀名 + 资源名称”
```



## 2.	不使用qrc，相对引用资源

- Qt工作目录

    ```cpp
    QDir dir;
    QString pathname;
    pathname = dir.currentPath();
    qDebug()<<pathname;
    ```

    在win上一般为cmake-build-debug或者cmake-build-release等目录.而你的图片一把你在img目录下，

    ```
    |-- project.pro
    |-- source/
    |-- img/
    |     `-- 123.jpg
    |
    |-- release/
    |     `-- abc.exe
    |
    `-- debug/
          `-- abc.exe
    ```

    **开发目录**与**工作目录**是不同的。