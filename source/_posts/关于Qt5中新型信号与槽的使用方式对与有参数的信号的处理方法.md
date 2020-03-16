# 关于Qt5中新型信号与槽的使用方式对与有参数的信号的处理方法

在Qt4中信号与槽的使用方法是用宏定义SIGNAL和SLOT来处理的。而在Qt5中出现的新型方式，且可以与Lambda一起使用，大大简化了代码，并且可以将任意函数作为信号或槽函数，只需要传递函数地址即可，但是对于有参数的信号来说，比较头大了。

- Qt4/5

```c++
connect(tcpScoket,SIGNAL(error(QAbstractSocket::SocketError)),
		this,     SLOT(onError(QAbstractSocket::SocketError)));
```

- Qt5

```c++
connect(tcpSocket, static_cast<void (QTcpSocket::*)(QAbstractSocket::SocketError)>		(&QTcpSocket::error), [=](QAbstractSocket::SocketError){
            qDebug() << "error" << tcpSocket->errorString();
	});
```

类似于使用函数指针代替原本的有参函数。参数则用Lambda的小括号传入。