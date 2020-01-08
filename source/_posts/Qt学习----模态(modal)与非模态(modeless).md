# Qt学习----模态(modal)与非模态(modeless)

## 1.	介绍

**模态**对话框就是在没有关闭它之前,不能再与同一个应用程序的其他窗口进行交互，比如新建项目时弹出的对话框。

**非模态**对话框，既可以与它交互，也可以与同一程序中的其他窗口交互，如MicrosoftWord中的查找替换对话框。

## 2.	使用

- 模态 例1：

```qt
int main(int argc ,char *argv[]){
    QApplication a(argc, argv);

    QWidget *widget =new QWidget();
    widget->resize(400,400);
    widget->move(400,400);

    QDialog *dialog = new QDialog(widget);

    dialog->exec();
    widget->show();

    return a.exec();
}
```

运行此程序时，先弹出dialog对话框，只要关闭对话框之后，widget才会显示。算是一个另类的模态。

将上述程序改为非模态仅需将上述程序中的11行作如下改变即可。

```
dialog->exec();  ------>dialog->show();
```

究其原因是因为exec与show的运行原理不同。

因为调用完show()函数后会立即将控制权交给调用者，程序可以继续往下执行。而调用exec()丽数却不
同,只有当对话框被关闭时才会返回。

上述的模态框还不算是真的模态，因为二者不是同事出现。因此需要将10,11行进行对调才可以。下面介绍另一种真正的模态。

- 模态 例2：

```
int main(int argc ,char *argv[]){
    QApplication a(argc, argv);

    QWidget *widget =new QWidget();
    widget->resize(400,400);
    widget->move(400,400);

    QDialog *dialog = new QDialog(widget);

    dialog->setModal(true);
	dialog->show();
	widget->show();

    return a.exec();
}
```

运行此程序时，二者同事出现，且仅可与dialog进行交互。重点在于setModal()函数.

```
void setModal(bool modal);
```

与该函数相似的还有以下函数：

```
void setWindowModality(Qt::WindowModality windowModality);
```

windowModality见附录[3.1](#windowModality)

## 3.	附录

### 3.1	WindowModality

```
enum WindowModality {
        NonModal,				不阻塞任何窗口
        WindowModal,			阻塞它的父窗口、所有祖先窗口以及它们的子窗口
        ApplicationModal   		阻塞整个应用程序的所有窗口
    };
```

setModal()函数默认设置为ApplicationModal模式。

