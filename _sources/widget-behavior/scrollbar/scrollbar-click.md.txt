# Clicking in the scrollbar track

There are two different behaviors for what happens when one clicks on the scrollbar track:

* The view scrolls up or down one page
* The view scrolls to the selected position

## Get the user's preference

* If the user is on KDE:
  * Get `[KDE] ScrollbarLeftClickNavigatesByPage` from `~/.config/kdeglobals`
* If the user is on a Gtk-based X11 desktop, or your app is running on XWayland
  * Get `Gtk/PrimaryButtonWarpsSlider` from XSettings
* Otherwise:
  * Get `gtk-overlay-scrolling` from the Gtk `settings.ini`

## Configuring

### Gtk

It is controlled by the [Gtk setting](/interfaces/gtk-settings) [`gtk-primary-button-warps-slider`](https://docs.gtk.org/gtk4/property.Settings.gtk-primary-button-warps-slider.html).

* Set the XSetting `Gtk/PrimaryButtonWarpsSlider`
* Set `gtk-overlay-scrolling` in the Gtk `settings.ini`
* Set `gtk-overlay-scrolling` in `~/.gtkrc-2.0`

It is not configurable via XDG settings or GSettings. 

### Qt

This can be set by the style or by the QPA; QPAs other than KDE don't seem to expose a preference.

#### KDE (QPA)

In `~/.config/kdeglobals`:

```ini
[KDE]
ScrollbarLeftClickNavigatesByPage=true
```

