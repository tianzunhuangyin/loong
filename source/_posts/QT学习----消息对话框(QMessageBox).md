# QT学习----消息对话框(QMessageBox)

## 1.	介绍：

提供一个模态的对话框来通知用户信息，或者向用户提出一个问题并且获取答案。

```
static int question(QWidget *parent, const QString &title, const QString& text, 
		int button0, int button1 = 0, int button2 = 0);
static int question(QWidget *parent, const QString &title, const QString& text,
		const QString&button0Text,const QString& button1Text = QString(),
		const QString& button2Text = QString(), int defaultButtonNumber = 0, 
		int escapeButtonNumber = -1);
static int question(QWidget *parent, const QString &title, const QString& text,
		StandardButton button0,StandardButton button1)
static StandardButton question(QWidget *parent, const QString &title, const QString &text,
		StandardButtons buttons = StandardButtons(Yes | No),
		StandardButton defaultButton = NoButton);
```

## 2.	使用

- (父窗口，标题栏，显示信息，按钮0，按钮1，按钮2)

  <font color=green size = 6 >Todo：按钮1与按钮2作用未知。</font>

- （父窗口，标题栏，显示信息，按钮名称0，按钮名称1，按钮名称2，按钮默认位置（按照0,1,2排序），默认返回值(没有点击按钮是的返回值)）

    ```
    ret = QMessageBox::question(qWidget,QObject::tr("你了解Qt吗？"),QObject::tr("你了解Qt吗？"), 				QObject::tr("button0"),QObject::tr("button1"),QObject::tr("button2"),2,4);
    ```

    

    ![1577188801117](QT学习----消息对话框(QMessageBox)/1577188801117.png)

    再次说明一下最后两个的参数。

    - 按钮默认位置的编号是固定的，因为按钮个数是固定的(只能有是3个)。
    - 默认返回值有点特别。当你设置的该值为按钮编号时，该消息对话框是非模态的，此时可以不点击给出的按钮直接退出，但此时默认你已点击该值对应的按钮，在示例中直接关闭窗口，表示默认点击了按钮button1。当你返回一个编号之外的值时，该消息对话框是模态的，意味着你必须点击按钮之后才能推出QMessageBox。如上图。

- (父窗口，标题栏，显示信息，标准按钮0，标准按钮1)

    ```
    ret = QMessageBox::question(qWidget,QObject::tr("你了解Qt吗？"),QObject::tr("你了解Qt吗？"), 				QMessageBox::Yes,QMessageBox::No);
    ```

    此时只可以有两个按钮，且必须是标准按钮。标准按钮附录。

    ![1577188767078](QT学习----消息对话框(QMessageBox)/1577188767078.png)

    返回值是标准按钮对应的值。

- (父窗口，标题栏，显示信息，缺省默认按钮yes + no,无按钮)

    类似于上例。

## 3.	附录

### 3.1	标准按钮。

```
enum StandardButton {
        NoButton           = 0x00000000,
        Ok                 = 0x00000400,
        Save               = 0x00000800,
        SaveAll            = 0x00001000,
        Open               = 0x00002000,
        Yes                = 0x00004000,
        YesToAll           = 0x00008000,
        No                 = 0x00010000,
        NoToAll            = 0x00020000,
        Abort              = 0x00040000,
        Retry              = 0x00080000,
        Ignore             = 0x00100000,
        Close              = 0x00200000,
        Cancel             = 0x00400000,
        Discard            = 0x00800000,
        Help               = 0x01000000,
        Apply              = 0x02000000,
        Reset              = 0x04000000,
        RestoreDefaults    = 0x08000000,

        FirstButton        = Ok,                // internal
        LastButton         = RestoreDefaults,   // internal

        YesAll             = YesToAll,          // obsolete
        NoAll              = NoToAll,           // obsolete

        Default            = 0x00000100,        // obsolete
        Escape             = 0x00000200,        // obsolete
        FlagMask           = 0x00000300,        // obsolete
        ButtonMask         = ~FlagMask          // obsolete
    };
```

