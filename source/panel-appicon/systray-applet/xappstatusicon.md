# XAppStatusIcon

This used by Linux Mint and on the Cinnamon desktop, it's unclear if the other desktops support it. The D-Bus interface is not specified.

* [Design notes](https://github.com/linuxmint/xapp/pull/67)

## Implementations

### Application-side

* libxapp provides [XAppStatusIcon](https://projects.linuxmint.com/xapp/reference/XAppStatusIcon.html)
  * It falls back to Gtk.StatusIcon, which uses the [XEmbed-based protocol](xembed)

### Tray-side

* libxapp provides [XAppStatusIconMonitor](https://projects.linuxmint.com/xapp/reference/XAppStatusIconMonitor.html)

#### Trays

* Cinnamon's systray (added to the panel by default)
* Plugin for xfce4-panel: [xfce4-xapp-status-plugin](https://github.com/linuxmint/xfce4-xapp-status-plugin)
* Plugin for MATE panel: [mate-xapp-status-applet](https://github.com/linuxmint/xapp/tree/master/status-applets/mate)
