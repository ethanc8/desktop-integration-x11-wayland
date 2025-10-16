# Scrollbar steppers

Traditionally, arrow buttons ("steppers") were placed on the scrollbar, allowing the user to 

On Windows, the two steppers are placed on opposite ends of the scrollbar, while on NeXTstep and Mac OS X (prior to its introduction of overlay scrollbars) the two steppers were placed on the bottom/right of the scrollbar. On Unix systems, the position was historically configurable by the user.

## Get the user's preference

This is difficult; ideally, something would eventually be exposed over dconf.

* If the user is on a Qt desktop:
  * If the theme is Breeze:
    * Check `~/.config/breezerc`
  * If the theme is Oxygen:
    * Check `~/.config/oxygenrc`
  * If the theme is Kvantum:
    * Check the user's `kvconfig` (this will require parsing multiple files)
  * Otherwise, assume one stepper at the top and bottom
* If the user is on a Gtk desktop:
  * Assume no steppers

## Supported toolkits

| Toolkit           | Support          | Default behavior | Notes              |
| ----------------- | ---------------- | ---------------- | ------------------ |
| Gtk2              | Yes              | Off              |                    |
| Gtk3              | Yes              | Off              |                    |
| Gtk4              | No               | On               |                    |
| Qt Widgets        | Depends on style | Depends on style |                    |
| Qt Quick Controls | Depends on style | Depends on style |                    |
| Chromium          | Required         | On               | Cannot be disabled |


### Gtk4

In commit 7e525ca6, steppers were removed from the Gtk4 codebase. 

## Configuring

### Gtk

#### Gtk2

This can be configured by the Gtk2 theme, or overridden by the user in `~/.gtkrc-2.0`:

```gtkrc
style "scrollbar-style" {
    GtkScrollbar::has-backward-stepper = 1
    GtkScrollbar::has-forward-stepper  = 1
    GtkScrollbar::has-secondary-backward-stepper = 1
    GtkScrollbar::has-secondary-forward-stepper  = 1
}
class "GtkScrollbar" style "scrollbar-style"
```

#### Gtk3

This can be configured by the Gtk3 theme, or overridden by the user in `~/.config/gtk-3.0/gtk.css`:

```css
scrollbar {
  -GtkScrollbar-has-backward-stepper: true;
  -GtkScrollbar-has-forward-stepper: true;
}
```

### Qt

In Qt, the scrollbars are drawn by the style. Thus, the scrollbar configuration must be done per style.

#### Breeze

`~/.config/breezerc`:

```ini
[Style]
ScrollBarAddLineButtons=2
ScrollBarSubLineButtons=2
```

The default is to not have any steppers; if this is true then the mentioned configuration keys in `~/.config/breezerc` will be empty.

#### Oxygen

`~/.config/oxygenrc`:

```ini
[Scrollbars]
ScrollBarAddLineButtons=1
ScrollBarSubLineButtons=1
```

The default is to one stepper at the top and two at the bottom; if this is true then the mentioned configuration keys in `~/.config/oxygenrc` will be empty.

#### Kvantum

In the user's `kvconfig`, the user should specify under `[Style]` the key `scroll_arrows`, which is true or false.

