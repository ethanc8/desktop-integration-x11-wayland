# XEmbed-based protocol

This interface allows to send X windows to be embedded into the system tray via XEmbed. It does not work in sandboxed applications.

## Specification

[Freedesktop.org System Tray Protocol Specification](https://specifications.freedesktop.org/systemtray-spec/0.3/)

## Implementations

### Application-side

#### Showing a menu, implemented client-side

* Gtk3 provides [`Gtk.StatusIcon`](https://docs.gtk.org/gtk3/class.StatusIcon.html)
* Qt5 provides [`QSystemTrayIcon`](https://doc.qt.io/archives/qt-5.15/qsystemtrayicon.html)
* The following fall back to `Gtk.StatusIcon`:
  * libxapp: [`XAppStatusIcon`](https://projects.linuxmint.com/xapp/reference/XAppStatusIcon.html)
  * [libappindicator](https://launchpad.net/libappindicator)
  * Electron: [`Tray`](https://www.electronjs.org/docs/latest/api/tray?utm_source=chatgpt.com)

#### Showing full popup applets

This must be implemented by the application itself; no toolkit provides support for this.

### Tray-side

#### Trays

* GNOME shell extension: [gnome-shell-extension-appindicator](https://github.com/ubuntu/gnome-shell-extension-appindicator)
* [xfce4-panel notification area](https://docs.xfce.org/xfce/xfce4-panel/systray) ([source](https://github.com/xfce-mirror/xfce4-panel/blob/master/plugins/systray/systray-manager.c))
* [LXPanel systray](https://github.com/lxde/lxpanel) ([source](https://github.com/lxde/lxpanel/tree/master/src/systray))
* [MATE panel systray](https://github.com/mate-desktop/mate-panel)
* [tint2 systray](https://github.com/semplice/tint2)
* a lot of other lightweight panels have their own systrays



