# Qt学习----QWidget

## 1	介绍

```
explicit QWidget(QWidget* parent = nullptr, Qt::WindowFlags f = Qt::WindowFlags());
```

## 2.	说明

- (父窗口，窗口系统类型(见附录[2.1](#WindowFlags)))

parent为0时表示其没有父类对象，只是一个独立的窗口，不依赖于其他部件。

f为是Qt::WindowFlags类型，是Qt::WindowType枚举类型值的或组合。

当然，在构造函数时，没有指定父类以及窗口参数，之后仍可以使用函数指定。

```
void setParent(QWidget *parent); 					指定父类
void setWindowFlags(Qt::WindowFlags type);			指定各种窗口系统类型
```

## 3	附录

### 3.1	WindowFlags

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



