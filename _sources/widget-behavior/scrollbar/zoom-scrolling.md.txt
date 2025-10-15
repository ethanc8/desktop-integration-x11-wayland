# Zoom scrolling

Zoom scrolling is a Gtk-only feature, and is one of the reasons that the Gtk developers felt comfortable removing the scrollbar steppers. 

## Constant-speed zoom scrolling

Long-pressing or shift-clicking on the scrollbar knob, then moving it in a direction, will cause it to move very slowly until you release the mouse click.

## Variable-speed zoom scrolling

Right-clicking on the scrollbar outside the knob will cause scrolling at a somewhat faster pace than the constant-speed zoom scrolling. The user can then move the mouse cursor further from the scrollbar to increase the speed.

## Further reading

Videos can be found on the [Gtk development blog](https://blog.gtk.org/2017/10/11/a-scrolling-primer/). Note that it uses odd terminology.
