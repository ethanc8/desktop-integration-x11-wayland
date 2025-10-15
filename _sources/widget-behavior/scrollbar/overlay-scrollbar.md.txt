# Overlay scrollbars

**Overlay scrollbars** are scrollbars which are hidden when not in use. When the user moves the mouse pointer, a very narrow scrollbar knob is shown, and if the user moves the pointer to the location of the scrollbar, the knob will widen and the user will be able to use it.

## Get the user's preference

Toolkits and applications should read the [XDG setting](/interfaces/xdg-settings) `org.gnome.desktop.interface overlay-scrolling`.

## Supported toolkits

| Toolkit           | Support | Default behavior | Notes                 |
| ----------------- | ------- | ---------------- | --------------------- |
| Gtk2              | No      | Off              |                       |
| Gtk3              | Yes     | On               |                       |
| Gtk4              | Yes     | On               |                       |
| Qt Widgets        | No      | Off              |                       |
| Qt Quick Controls | Yes     | Off              | Not user-configurable |
| Mozilla           | Yes     | On               |                       |
| Chromium          | Yes     | Off |                       |

## Configuring

### Gtk

It is controlled by the [Gtk setting](/interfaces/gtk-settings) [`gtk-overlay-scrolling`](https://docs.gtk.org/gtk4/property.Settings.gtk-overlay-scrolling.html).

To configure this:
* Set [XDG setting](/interfaces/xdg-settings) `org.gnome.desktop.interface overlay-scrolling`
* Set GSetting/dconf setting `org.gnome.desktop.interface overlay-scrolling`
* Set `gtk-overlay-scrolling` in the Gtk `settings.ini`

Even though Gtk3 does not support setting this setting via GSettings, setting it via GSettings seems to work after restarting the Gtk3 apps.

This setting cannot be set via XSettings.

Overlay scrolling is not supported in Gtk2.

#### Notes

The Gtk developers [do not intend for this to be user-configurable](https://bugzilla.gnome.org/show_bug.cgi?id=790677):

> What we will not add is a user-accessible toggle, or an environment variable. This is an application developer decision, not a toolkit setting. If the application developer wants to provide an application-specific setting and wire it to the GtkScrolledWindow API, it's entirely in their capacity to do so.

However, the Gtk developers may have changed their mind, as this is now exposed as an accessibility setting in GNOME (see bug [gnome-control-center#1701](https://gitlab.gnome.org/GNOME/gnome-control-center/-/issues/1701)).

### Firefox and Mozilla derivatives

The user should set `widget.gtk.overlay-scrollbars.enabled` in `about:config`.

### Chromium, Chromium derivatives, and Electron applications

This is supposed to work, but it appears that Chromium is stuck without overlay scrollbars at least on Chromium 143.

This can be configured by using the `--enable-features` command-line flag, or by accessing `chrome://flags`.

```bash
chromium --enable-features=OverlayScrollbar
```

The `FluentScrollbar` and `FluentOverlayScrollbar` features allow enabling the redesign of the scrollbar to match Microsoft's Fluent design (see the [visual spec](https://docs.google.com/document/d/1haDpb1QIh2PaLwsQD1i4WHFq_5_jSK3XK9lhgSs4WkM/edit?tab=t.0), [technical design doc](https://docs.google.com/document/d/1GCmz2nbJV1XiopoLHnlrVaHCjhQMdiyDfPN_a22OIjU/edit?tab=t.0), and [Chromium bug](https://issues.chromium.org/issues/40213017)). 

Google [appears to intend to](https://issues.chromium.org/issues/427971927) check `org.gnome.desktop.interface overlay-scrolling` in a future release.
