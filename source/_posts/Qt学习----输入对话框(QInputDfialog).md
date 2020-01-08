# Qt学习----输入对话框(QInputDfialog)

## 1.	介绍

让用户输入单一的数字或字符串。

```
static QString getText(QWidget *parent, const QString &title, const QString &label, 
		QLineEdit::EchoMode echo = QLineEdit::Normal, const QString &text = QString(), 
		bool *ok = nullptr, Qt::WindowFlags flags = Qt::WindowFlags(), 
		Qt::InputMethodHints inputMethodHints = Qt::ImhNone);
```

## 2. 使用

- (父类，对话框标题，输入提示语，输入框输入模式(见附录[3.1](#EchoMode))，输入框中的默认字符，返回值(按下OK，返回true，按下cancel，返回false)，窗口的系统类型(见附录[3.2](#WindowFlags))，输入法提示(见附录[3.3](#InputMethodHint)))

## 3.	附录

### 3.1	EchoMode

```
enum EchoMode { Normal,												标准
				NoEcho,												无回显
                Password, 											密码
                PasswordEchoOnEdit };								密码回显
```

### 3.2	WindowFlags

```
Q_DECLARE_FLAGS(WindowFlags, WindowType)
```

```
enum WindowType {
        Widget = 0x00000000,
        Window = 0x00000001,
        Dialog = 0x00000002 | Window,
        Sheet = 0x00000004 | Window,
        Drawer = Sheet | Dialog,
        Popup = 0x00000008 | Window,
        Tool = Popup | Dialog,
        ToolTip = Popup | Sheet,									工具提示
        SplashScreen = ToolTip | Dialog,							开机(欢迎)画面
        Desktop = 0x00000010 | Window,								桌面
        SubWindow = 0x00000012,										子视窗
        ForeignWindow = 0x00000020 | Window,						外窗
        CoverWindow = 0x00000040 | Window,							盖窗

        WindowType_Mask = 0x000000ff,								窗式mask
        MSWindowsFixedSizeDialogHint = 0x00000100,	MS Windows固定大小对话框提示
        MSWindowsOwnDC = 0x00000200,								MS Windows自己的DC
        BypassWindowManagerHint = 0x00000400,						绕过窗口管理器
        X11BypassWindowManagerHint = BypassWindowManagerHint,		X11绕过窗口管理器
        FramelessWindowHint = 0x00000800,							无框窗口
        WindowTitleHint = 0x00001000,								窗口标题
        WindowSystemMenuHint = 0x00002000,							窗口系统菜单
        WindowMinimizeButtonHint = 0x00004000,						窗口最小化按钮
        WindowMaximizeButtonHint = 0x00008000,						窗口最大化按钮提示
        WindowMinMaxButtonsHint = WindowMinimizeButtonHint | WindowMaximizeButtonHint,
        															窗口最小最大按钮
        WindowContextHelpButtonHint = 0x00010000,					窗口上下文帮助按钮
        WindowShadeButtonHint = 0x00020000,							窗口阴影按钮
        WindowStaysOnTopHint = 0x00040000,							窗口停留在顶部
        WindowTransparentForInput = 0x00080000,						输入透明窗口
        WindowOverridesSystemGestures = 0x00100000,					窗口覆盖系统手势
        WindowDoesNotAcceptFocus = 0x00200000,						窗口不接受焦点
        MaximizeUsingFullscreenGeometryHint = 0x00400000,			最大化使用全屏几何

        CustomizeWindowHint = 0x02000000,							自定义窗口
        WindowStaysOnBottomHint = 0x04000000,						窗口停留在底部
        WindowCloseButtonHint = 0x08000000,							窗口关闭按钮
        MacWindowToolBarButtonHint = 0x10000000,					Mac窗口工具栏按钮
        BypassGraphicsProxyWidget = 0x20000000,						绕过图形代理小部件
        NoDropShadowWindowHint = 0x40000000,						无阴影窗口
        WindowFullscreenButtonHint = 0x80000000						窗口全屏按钮
    };
```

### 3.3	InputMethodHint

```
enum InputMethodHint {
        ImhNone = 0x0,												无

        ImhHiddenText = 0x1,										隐藏文字
        ImhSensitiveData = 0x2,										敏感数据
        ImhNoAutoUppercase = 0x4,									没有自动大写
        ImhPreferNumbers = 0x8,										首选数字
        ImhPreferUppercase = 0x10,									首选大写
        ImhPreferLowercase = 0x20,									首选小写
        ImhNoPredictiveText = 0x40,									无联想

        ImhDate = 0x80,												日期
        ImhTime = 0x100,											时间
	
        ImhPreferLatin = 0x200,										首选拉丁文								
        ImhMultiLine = 0x400,										多线

        ImhNoEditMenu = 0x800,										无编辑菜单
        ImhNoTextHandles = 0x1000,									无文字句柄

        ImhDigitsOnly = 0x10000,									仅数字
        ImhFormattedNumbersOnly = 0x20000,							仅格式化数字
        ImhUppercaseOnly = 0x40000,									仅大写
        ImhLowercaseOnly = 0x80000,									仅小写
        ImhDialableCharactersOnly = 0x100000,						仅可拨号字符
        ImhEmailCharactersOnly = 0x200000,							仅电子邮件字符
        ImhUrlCharactersOnly = 0x400000,							仅网址字符
        ImhLatinOnly = 0x800000,									仅拉丁文

        ImhExclusiveInputMask = 0xffff0000							输入掩码
    }
```