# Gtk.Settings

[Gtk4 API documentation](https://docs.gtk.org/gtk4/class.Settings.html) | [Gtk3 API documentation](https://docs.gtk.org/gtk3/class.Settings.html)

In Gtk3, Gtk.Settings checks the following sources, in order:
* XSettings ([mapping](https://github.com/GNOME/gtk/blob/3.24.51/gdk/x11/gdksettings.c#L27))
* The `settings.ini`

In Gtk4 prior to Gtk 4.22, Gtk.Settings checks the following sources, in order:
* If on X11, XSettings ([mapping](https://github.com/GNOME/gtk/blob/4.20.2/gdk/x11/gdksettings.c#L27))
* If on Wayland:
  * The [XDG Desktop Portal Settings portal](xdg-settings)
  * If the portal was inaccessible, from GSettings (dconf) 
  * [The mapping for both](https://github.com/GNOME/gtk/blob/4.20.2/gdk/wayland/gdksettings-wayland.c#L309) is the same
* The `settings.ini`

In Gtk 4.22, [the GSettings fallback will be removed](https://gitlab.gnome.org/GNOME/gtk/-/issues/7727). However, most desktops will configure a fallback to xdg-desktop-portal-gtk, which will proxy the requests to GSettings.

Note that not all Gtk.Settings can be configured via XSettings or the Settings portal.
