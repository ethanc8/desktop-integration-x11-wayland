Title: org.kde.StatusNotifierItem D-Bus Interface
Slug: org.kde.StatusNotifierItem

# org.kde.StatusNotifierItem

## Description

Each application can register an arbitrary number of Status Notifier Items either:
* by registering on the session bus the service `org.kde.StatusNotifierItem-PID-ID`, where PID is the process id of the application and ID is an arbitrary numeric unique identifier between different instances registered by the same application. The application must then register this service name with [`org.kde.StatusNotifierWatcher.RegisterStatusNotifierItem`](xdg-org.kde.StatusNotifierWatcher.md#RegisterStatusNotifierItem). Sandboxed applications may not use this procedure.
* (**recommended**) by registering an arbitrary path starting with `/` to [`org.kde.StatusNotifierWatcher.RegisterStatusNotifierItem`](xdg-org.kde.StatusNotifierWatcher.md#RegisterStatusNotifierItem).

Each instance of StatusNotifierItem must provide an object called `StatusNotifierItem` with the following properties, methods and signals described in the following sections. 

### Properties
### org.kde.StatusNotifierItem:Category

```
    Category readable s
```

General category of icon. This MAY be used for sorting purposes and MUST NOT change the presentation.

Currently defined categories are:
* `ApplicationStatus`: The item describes the status of a generic application, for instance the current state of a media player. In the case where the category of the item can not be known, such as when the item is being proxied from another incompatible or emulated system, `ApplicationStatus` can be used a sensible default fallback.
* `Communications`: The item describes the status of communication oriented applications, like an instant messenger or an email client.
* `SystemServices`: The item describes services of the system not seen as a stand alone application by the user, such as an indicator for the activity of a disk indexing service.
* `Hardware`: The item describes the state and control of a particular hardware, such as an indicator of the battery charge or sound card volume control.

### org.kde.StatusNotifierItem:Id

```
    Id readable s
```

A name that should be unique for this application and consistent between sessions, such as the application name itself.

### org.kde.StatusNotifierItem:Title

```
    Title readable s
```

Descriptive title for the application; this MAY be shown by the host.

### org.kde.StatusNotifierItem:Status

```
    Status readable s
```

Describes the status of this item or of the associated application.

The allowed values for the Status property are:
* `Passive`: The item doesn't convey important information to the user, it can be considered an "idle" status and is likely that hosts will chose to hide it.
* `Active`: The item is active, is more important that the item will be shown in some way to the user.
* `NeedsAttention`: The item carries really important information for the user, such as battery charge running out and is wants to incentive the direct user intervention. hosts should emphasize in some way the items with NeedsAttention status.

### org.kde.StatusNotifierItem:WindowId

```
    WindowId readable i
```

It's the windowing-system dependent identifier for a window, the application can chose one of its windows to be available through this property or just set `0` if it's not interested.

### org.kde.StatusNotifierItem:IconThemePath

```
    IconThemePath readable s
```

The path to an icon theme where the icon specified in `IconName` can be found.

### org.kde.StatusNotifierItem:Menu

```
    Menu readable o
```

A menu to show when the user right-clicks or performs some host-defined interaction with the status notifier item.

DBus path to an object which implements the `com.canonical.dbusmenu` interface.

TODO: Are GMenus allowed?

### org.kde.StatusNotifierItem:ItemIsMenu

```
    ItemIsMenu readable b
```

If true, the icon only supports showing context menu. The host should prefer showing the menu instead of `Activate()`.

### org.kde.StatusNotifierItem:IconName

```
    IconName readable s
```

The StatusNotifierItem can carry an icon that can be used by the host to identify the item.

An icon can either be identified by its Freedesktop-compliant icon name, carried by this property of by the icon data itself, carried by the property `IconPixmap`. hosts are encouraged to prefer icon names over icon pixmaps if both are available (FIXME: still not very defined: could e the pixmap used as fallback if an icon name is not found?)

### org.kde.StatusNotifierItem:IconPixmap

```
    IconPixmap readable a(iiay)
```

Carries an ARGB32 binary representation of the icon, the format of icon data used in this specification is described in Section [Icons](icons).

### org.kde.StatusNotifierItem:OverlayIconName

```
    OverlayIconName readable s
```

The Freedesktop-compliant name of an icon. This can be used by the host to indicate extra state information, for instance as an overlay for the main icon.

### org.kde.StatusNotifierItem:OverlayIconPixmap

```
    OverlayIconPixmap readable a(iiay)
```

ARGB32 binary representation of the overlay icon described in the previous paragraph.

### org.kde.StatusNotifierItem:AttentionIconName

```
    AttentionIconName readable s
```

The Freedesktop-compliant name of an icon. This can be used by the host to indicate that the item is in `RequestingAttention` state.

### org.kde.StatusNotifierItem:AttentionIconPixmap

```
    AttentionIconPixmap readable a(iiay)
```

ARGB32 binary representation of the requesting attention icon describe in the previous paragraph.

### org.kde.StatusNotifierItem:AttentionMovieName

```
    AttentionMovieName readable s
```

An item can also specify an animation associated to the `RequestingAttention` state. This should be either a Freedesktop-compliant icon name or a full path. The visualization can chose between the movie or AttentionIconPixmap (or using neither of those) at its discretion.

### org.kde.StatusNotifierItem:ToolTip

```
    ToolTip readable (sa(iiay)ss)
```

Data structure that describes extra information associated to this item, that can be visualized for instance by a tooltip (or by any other mean the visualization consider appropriate. Components are:

* `s`: Freedesktop-compliant name for an icon.
* `a(iiay)`: icon data
* `s`: title for this tooltip
* `s`: descriptive text for this tooltip. It can contain also a subset of the HTML markup language, for a list of allowed tags see Section [Markup](markup).

### Methods
### org.kde.StatusNotifierItem.ProvideXdgActivationToken

```
    ProvideXdgActivationToken (
      IN token s
    )
```

TODO

* token: 



### org.kde.StatusNotifierItem.ContextMenu

```
    ContextMenu (
      IN x i,
      IN y i
    )
```

Asks the status notifier item to show a context menu. This is typically a consequence of user input, such as mouse right click over the graphical representation of the item.

the `x` and `y` parameters are in screen coordinates and are to be considered an hint to the item about where to show the context menu.

TODO: Are the `x` and `y` coordinates a bottom corner or some other location?

### org.kde.StatusNotifierItem.Activate

```
    Activate (
      IN x i,
      IN y i
    )
```

Asks the status notifier item for activation,.This is typically a consequence of user input, such as mouse left click over the graphical representation of the item. The application will perform any task is considered appropriate as an activation request.

The `x` and `y` parameters are in screen coordinates and is to be considered an hint to the item where to show eventual windows (if any).

### org.kde.StatusNotifierItem.SecondaryActivate

```
    SecondaryActivate (
      IN x i,
      IN y i
    )
```
Is to be considered a secondary and less important form of activation compared to Activate. This is typically a consequence of user input, such as mouse middle click over the graphical representation of the item. The application will perform any task is considered appropriate as an activation request.

The `x` and `y` parameters are in screen coordinates and is to be considered an hint to the item where to show eventual windows (if any).

### org.kde.StatusNotifierItem.Scroll

```
    Scroll (
      IN delta i,
      IN orientation s
    )
```

The user asked for a scroll action. This is caused from input such as mouse wheel over the graphical representation of the item.

* delta: the amount of scroll

* orientation: the horizontal or vertical orientation of the scroll request and its legal values are `"horizontal"` and `"vertical"`.


### Signals
### org.kde.StatusNotifierItem::NewTitle

```
    NewTitle ()
```

The item has a new title: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewIcon

```
    NewIcon ()
```

The item has a new icon: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewAttentionIcon

```
    NewAttentionIcon ()
```

The item has a new attention icon: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewOverlayIcon

```
    NewOverlayIcon ()
```

The item has a new overlay icon: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewMenu

```
    NewMenu ()
```

The item has a new context menu: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewToolTip

```
    NewToolTip ()
```

The item has a new tooltip: the host should read it again immediately.

### org.kde.StatusNotifierItem::NewStatus

```
    NewStatus (
      status s
    )
```

The item has a new status, that is passed as an argument of the signal.
