# 关于Lambda在QT scokt中使用的问题

在参照教程学习socket的过程中，因为觉得Lambda十分好用，因此处处使用Lambda，但今日碰到了以下问题：

- 使用Lambda写下的readyRead的信号与槽。

```c++
connect(tcpSocket, &QTcpSocket::readyRead, [=](){
        //获取信号发出者
        QObject *obj = this->sender();
        //类型转换
        QTcpSocket *tcpSocket = qobject_cast<QTcpSocket *>(obj);
        //读取发送的信息 并写入展示栏
        QByteArray data = tcpSocket->readAll();
        ui->textShow->append(data);
        qDebug()<<"ready read"<<data;

    });
```

- 使用正常方式连接的信号与槽

```c++
connect(tcpSocket,SIGNAL(readyRead()),this,SLOT(onReadyRead()));

void MyServer::onReadyRead() {
    //获取信号发出者
    QObject *obj = this->sender();
    //类型转换
    QTcpSocket *tcpSocket = qobject_cast<QTcpSocket *>(obj);
    //读取发送的信息 并写入展示栏
    QByteArray data = tcpSocket->readAll();
    ui->textShow->append(data);
    qDebug()<<"ready read"<<data;
}
```

在这二者使用过程中，使用Lambda方式会导致Server与Client无法通信，导致程序崩溃。

Client给Server发送数据时，报如下错误。反之同样。

```C++
error "The remote host closed the connection"

QCoreApplication::postEvent: Unexpected null receiver
```



无可奈何之下，Google搜索，大致原因是断开连接后的删除问题(deleteLater())。

而在wiki上的Qt文档上有关于[Lambda在信号与槽中的新型使用方式](https://wiki.qt.io/New_Signal_Slot_Syntax#Overload)

摘抄如下：

```c++
void doYourStuff( const QByteArray &page )
{
    QTcpSocket *socket = new QTcpSocket;
    socket->connectToHost( "qt.io", 80 );
    QObject::connect(
        socket, &QTcpSocket::connected,
        [socket, page]() { socket->write( QByteArray( "GET " + page + "" ) ); }
    );
    QObject::connect(
        socket, &QTcpSocket::readyRead,
        [socket]() { qDebug() << "GOT DATA " << socket->readAll(); }
    );
    QObject::connect(
        socket, &QTcpSocket::disconnected,
        [socket]() {
            qDebug() << "DISCONNECTED ";
            socket->deleteLater();
        }
    );
    QObject::connect(
        socket, static_cast<void ( QTcpSocket::* )( QAbstractSocket::SocketError )>( &QAbstractSocket::error ),
        [socket]( QAbstractSocket::SocketError ) {
            qDebug() << "ERROR " << socket->errorString();
            socket->deleteLater();
        }
    );
}
```

有感于deleteLater()的问题，而我此前在disconnected的操纵确实没有，但添加仍无效果，特此记录。