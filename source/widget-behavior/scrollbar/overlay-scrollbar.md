# Overlay scrollbars

**Overlay scrollbars** are scrollbars which are hidden when not in use. When the user moves the mouse pointer, a very narrow scrollbar knob is shown, and if the user moves the pointer to the location of the scrollbar, the knob will widen and the user will be able to use it.

## Get the user's preference

Toolkits and applications should read `org.gnome.desktop.overlay-scrolling` from dconf.

```bash
gsettings get org.gnome.desktop.interface overlay-scrolling
```

## Supported toolkits

| Toolkit           | Support | Default behavior | Notes                 |
| ----------------- | ------- | ---------------- | --------------------- |
| Gtk2              | No      | Off              |                       |
| Gtk3              | Yes     | On               |                       |
| Gtk4              | Yes     | On               |                       |
| Qt Widgets        | No      | Off              |                       |
| Qt Quick Controls | Yes     | Off              | Not user-configurable |
| Mozilla           | Yes     | On               |                       |

## Configuring

### Gtk

The user or desktop environment should set `org.gnome.desktop.overlay-scrolling` in dconf:

```bash
gsettings set org.gnome.desktop.interface overlay-scrolling false # or true
```

### Firefox and Mozilla derivatives

The user should set `widget.gtk.overlay-scrollbars.enabled` in `about:config`.


