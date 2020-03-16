# Qt学习----QWidget

## 1	介绍

```
explicit QWidget(QWidget* parent = nullptr, Qt::WindowFlags f = Qt::WindowFlags());
```

## 2.	构造

- (父窗口，窗口系统类型(见附录[2.1](#WindowFlags)))

parent为0时表示其没有父类对象，只是一个独立的窗口，不依赖于其他部件。

f为是Qt::WindowFlags类型，是Qt::WindowType枚举类型值的或组合。

当然，在构造函数时，没有指定父类以及窗口参数，之后仍可以使用函数指定。

```
void setParent(QWidget *parent); 					指定父类
void setWindowFlags(Qt::WindowFlags type);			指定各种窗口系统类型
```

## 3.	属性

```cpp
void setAttribute(Qt::WidgetAttribute, bool on = true);
```

如果on为true，则在此小部件上设置attribute属性；否则(为false)清除属性。on默认为true.

## 4	附录

### 4.1	WindowFlags

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

## 4.2	WidgetAttribute

此枚举类型用于指定各种窗口小部件属性。使用QWidget::setAttribute()设置和清除属性，并使用QWidget::testAttribute()查询属性，尽管其中一些具有特殊的便捷功能，如下所述。

```
enum WidgetAttribute {
        WA_Disabled = 0,				//表示该窗口小部件已禁用，即它没有收到任何鼠标或键盘事件。还有一个getter功能QWidget::isEnabled()。这是由Qt内核设置/清除的。
        WA_UnderMouse = 1,
        WA_MouseTracking = 2,
        WA_ContentsPropagated = 3, // ## deprecated
        WA_OpaquePaintEvent = 4,
        WA_NoBackground = WA_OpaquePaintEvent, // ## deprecated
        WA_StaticContents = 5,
        WA_LaidOut = 7,
        WA_PaintOnScreen = 8,
        WA_NoSystemBackground = 9,
        WA_UpdatesDisabled = 10,
        WA_Mapped = 11,
        WA_MacNoClickThrough = 12, // Mac only
        WA_InputMethodEnabled = 14,
        WA_WState_Visible = 15,
        WA_WState_Hidden = 16,

        WA_ForceDisabled = 32,
        WA_KeyCompression = 33,
        WA_PendingMoveEvent = 34,
        WA_PendingResizeEvent = 35,
        WA_SetPalette = 36,
        WA_SetFont = 37,
        WA_SetCursor = 38,
        WA_NoChildEventsFromChildren = 39,
        WA_WindowModified = 41,
        WA_Resized = 42,
        WA_Moved = 43,
        WA_PendingUpdate = 44,
        WA_InvalidSize = 45,
        WA_MacBrushedMetal = 46, // Mac only
        WA_MacMetalStyle = WA_MacBrushedMetal, // obsolete
        WA_CustomWhatsThis = 47,
        WA_LayoutOnEntireRect = 48,
        WA_OutsideWSRange = 49,
        WA_GrabbedShortcut = 50,
        WA_TransparentForMouseEvents = 51,
        WA_PaintUnclipped = 52,
        WA_SetWindowIcon = 53,
        WA_NoMouseReplay = 54,
        WA_DeleteOnClose = 55,			//当小部件接受了关闭事件时，使Qt删除此小部件（请参阅QWidget::closeEvent()）。
        WA_RightToLeft = 56,
        WA_SetLayoutDirection = 57,
        WA_NoChildEventsForParent = 58,
        WA_ForceUpdatesDisabled = 59,

        WA_WState_Created = 60,
        WA_WState_CompressKeys = 61,
        WA_WState_InPaintEvent = 62,
        WA_WState_Reparented = 63,
        WA_WState_ConfigPending = 64,
        WA_WState_Polished = 66,
        WA_WState_DND = 67, // ## deprecated
        WA_WState_OwnSizePolicy = 68,
        WA_WState_ExplicitShowHide = 69,

        WA_ShowModal = 70, // ## deprecated
        WA_MouseNoMask = 71,
        WA_GroupLeader = 72, // ## deprecated
        WA_NoMousePropagation = 73, // ## for now, might go away.
        WA_Hover = 74,
        WA_InputMethodTransparent = 75, // Don't reset IM when user clicks on this (for virtual keyboards on embedded)
        WA_QuitOnClose = 76,

        WA_KeyboardFocusChange = 77,

        WA_AcceptDrops = 78,
        WA_DropSiteRegistered = 79, // internal
        WA_ForceAcceptDrops = WA_DropSiteRegistered, // ## deprecated

        WA_WindowPropagation = 80,

        WA_NoX11EventCompression = 81,
        WA_TintedBackground = 82,
        WA_X11OpenGLOverlay = 83,
        WA_AlwaysShowToolTips = 84,
        WA_MacOpaqueSizeGrip = 85,
        WA_SetStyle = 86,

        WA_SetLocale = 87,
        WA_MacShowFocusRect = 88,

        WA_MacNormalSize = 89,  // Mac only
        WA_MacSmallSize = 90,   // Mac only
        WA_MacMiniSize = 91,    // Mac only

        WA_LayoutUsesWidgetRect = 92,
        WA_StyledBackground = 93, // internal
        WA_MSWindowsUseDirect3D = 94, // Win only
        WA_CanHostQMdiSubWindowTitleBar = 95, // Internal

        WA_MacAlwaysShowToolWindow = 96, // Mac only

        WA_StyleSheet = 97, // internal

        WA_ShowWithoutActivating = 98,

        WA_X11BypassTransientForHint = 99,

        WA_NativeWindow = 100,
        WA_DontCreateNativeAncestors = 101,

        WA_MacVariableSize = 102,    // Mac only

        WA_DontShowOnScreen = 103,

        // window types from http://standards.freedesktop.org/wm-spec/
        WA_X11NetWmWindowTypeDesktop = 104,
        WA_X11NetWmWindowTypeDock = 105,
        WA_X11NetWmWindowTypeToolBar = 106,
        WA_X11NetWmWindowTypeMenu = 107,
        WA_X11NetWmWindowTypeUtility = 108,
        WA_X11NetWmWindowTypeSplash = 109,
        WA_X11NetWmWindowTypeDialog = 110,
        WA_X11NetWmWindowTypeDropDownMenu = 111,
        WA_X11NetWmWindowTypePopupMenu = 112,
        WA_X11NetWmWindowTypeToolTip = 113,
        WA_X11NetWmWindowTypeNotification = 114,
        WA_X11NetWmWindowTypeCombo = 115,
        WA_X11NetWmWindowTypeDND = 116,

        WA_MacFrameworkScaled  = 117,

        WA_SetWindowModality = 118,
        WA_WState_WindowOpacitySet = 119, // internal
        WA_TranslucentBackground = 120,

        WA_AcceptTouchEvents = 121,
        WA_WState_AcceptedTouchBeginEvent = 122,
        WA_TouchPadAcceptSingleTouchEvents = 123,

        WA_X11DoNotAcceptFocus = 126,
        WA_MacNoShadow = 127,

        WA_AlwaysStackOnTop = 128,

        WA_TabletTracking = 129,

        WA_ContentsMarginsRespectsSafeArea = 130,

        WA_StyleSheetTarget = 131,

        // Add new attributes before this line
        WA_AttributeCount
    };
```

