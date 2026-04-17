# Progress Bar

A progress bar that displays underneath the window or app icon on the taskbar/dock.

## Unity, KDE, Dash-to-Dock, Plank



### Unity Launcher D-Bus API

Emit the signal [com.canonical.Unity.LauncherEntry.Update](https://wiki.ubuntu.com/Unity/LauncherAPI#Low_level_DBus_API:_com.canonical.Unity.LauncherEntry).

### libunity helper functions (C)

[Reference](https://wiki.ubuntu.com/Unity/LauncherAPI#Using_the_Launcher_API)

Each launcher icon can be controlled remotely by a discrete LauncherEntry object. New launcher entry object may be created by calling `unity_launcher_entry_get_for_desktop_id (char *id)`; where `id` is the name of the desktop file shipped by the application you wish to control. For example GNOME Evolution ships `"evolution.desktop"` and Empathy ships `"empathy.desktop"`. 

Progress can be set by
```c
unity_launcher_entry_set_progress (UnityLauncherEntry *self, gdouble progress)
```
and made visible by calling
```c
unity_launcher_entry_set_progress_visible (UnityLauncherEntry *self, gboolean visible);
```
The progress value should be between 0.0 and 1.0. 

### libunity helper functions (Vala)

[Reference](https://valadoc.org/unity/Unity.LauncherEntry.html)

Each launcher icon can be controlled remotely by a discrete LauncherEntry object. New launcher entry object may be created by calling `Unity.LauncherEntry.get_for_desktop_id (string app_uri)`; where `app_uri` is the name of the desktop file shipped by the application you wish to control. For example GNOME Evolution ships `"evolution.desktop"` and Empathy ships `"empathy.desktop"`. 

Progress can be set by
```vala
public double progress { get; set; } 
```
and made visible by setting
```vala
public bool progress_visible { get; set; }
```
The progress value should be between 0.0 and 1.0. 

[Example](https://bazaar.launchpad.net/~unity-team/libunity/trunk/view/head:/examples/launcher.vala)

## Cinnamon (Linux Mint)

You can set the following X properties, or use `libxapp` (only if you're using Gtk).

### `_NET_WM_XAPP_PROGRESS` (32-bit cardinal (unsigned integer))

```
xprop -f _NET_WM_XAPP_PROGRESS 32c
"_NET_WM_XAPP_PROGRESS" XA_CARDINAL 32
```

**Valid values:** 0 to 100

Sets the progress hint for a window manager (like muffin) to make available when applications want to display the application's progress in some operation.

Note: If a window will stick around after progress is complete, you will probaby need to delete `_NET_WM_XAPP_PROGRESS` to remove any progress effects on taskbars and window lists.

You must also delete `_NET_WM_XAPP_PROGRESS_PULSE` to use this flag.

### `_NET_WM_XAPP_PROGRESS_PULSE` (32-bit cardinal (unsigned integer))

```
xprop -f _NET_WM_XAPP_PROGRESS_PULSE 32c
"_NET_WM_XAPP_PROGRESS_PULSE" XA_CARDINAL 32
```

**Valid values:** 1 -- to disable pulse, delete the 

Sets the progress pulse hint hint for a window manager (like muffin) to make available when applications want to display indeterminate or ongoing progress in a task manager.

Note: If a window will stick around after progress is complete, you will probaby need to set progress to 0 to remove any progress effects on taskbars and window lists. This will also remove the pulse state, if it is set.

You must also delete `_NET_WM_XAPP_PROGRESS` to use this flag.

### Usage

```c
// `cardinal` is the progress percentage or the progress pulse.
// `xid` is the window ID
// `display` is the Gdk display which this is on.
if (cardinal > 0) {
    XChangeProperty (GDK_DISPLAY_XDISPLAY (display),
                        xid,
                        gdk_x11_get_xatom_by_name_for_display (display, atom_name),
                        XA_CARDINAL, 32,
                        PropModeReplace,
                        (guchar *) &cardinal, 1);
} else {
    XDeleteProperty (GDK_DISPLAY_XDISPLAY (display),
                        xid,
                        gdk_x11_get_xatom_by_name_for_display (display, atom_name));
}
```

### libXApp convenience functions

The following functions work on `GtkWindow`s:

* [`xapp_set_window_progress`](https://projects.linuxmint.com/xapp/reference/XAppGtkWindow.html#xapp-set-window-progress)
* [`xapp_set_window_progress_pulse`](https://projects.linuxmint.com/xapp/reference/XAppGtkWindow.html#xapp-set-window-progress-pulse)

You can also use [`XAppGtkWindow`](https://projects.linuxmint.com/xapp/reference/XAppGtkWindow.html) and use its methods `set_window_progress` and `set_window_progress_pulse`.

See also the [blog post introducing this feature](https://blog.linuxmint.com/?p=3329#:~:text=switched%20to%20Aptdaemon.-,window%20progress,-When%20an%20application) for examples.