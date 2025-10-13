# Scrollbar position

Since the 2000s, the standard position of scrollbars has been on the right for vertical scrollbars and on the bottom for horizontal scrollbars. Gtk and Qt, along with most new cross-platform toolkits, place the scrollbar on the right and bottom as is standard, and the user cannot configure this.

However, by default, GNUstep locates vertical scrollbars on the left (as NeXTstep did). This is only configurable by loading a theme that places scrollbars on the right.

## Get the user's preference

Toolkits and applications should assume that scrollbars are to be placed on the right and bottom.
