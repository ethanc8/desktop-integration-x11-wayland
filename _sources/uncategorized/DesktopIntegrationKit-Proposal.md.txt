# DesktopIntegrationKit proposal

## Rationale

### Why make a DesktopIntegrationKit?

* Desktop integration is a difficult endeavor
* In order for GNUstep applications to be native we must integrate with desktops
* If we can deliver better desktop integration than Electron, Gtk, Qt, Flutter, etc. (which all have desktop integration flaws that are obvious to any end user), we can gain a significant advantage over them

### What does "desktop integration" mean?

The article ["Advice for the next dozen Rust GUIs"](https://raphlinus.github.io/rust/gui/2022/07/15/next-dozen-guis.html) brought up these points, but there may be others:

* What is the binary size for a simple application?
* What is the startup time for a simple application?
* Does text look like the platform native text?
* To what extent does the app support preferences set at the system level?
* What subset of expected text control functionality is provided?
  * Complex text rendering including BiDi
  * Support for keyboard layouts including “dead key” for alphabetic scripts
  * Keyboard shortcuts according to platform human interface guidelines
  * Input Method Editor
  * Color emoji rendering and use of platform emoji picker
  * Copy-paste (clipboard)
  * Drag and drop
  * Spelling and grammar correction
  * Accessibility (including reading the text aloud)

As a list of things I think we should deal with:

* Getting the icon onto the taskbar/dock/homescreen
* User notifications
* Manage taskbar/dock/homescreen icon (context menu, progress bar, unread notification dots)
* Follow system color scheme (use dark or light mode, follow accent color, and possibly follow the entire color scheme)
* Dealing with the sandbox/packaging system (flatpak, snap, macOS sandbox, etc)
* Most of what's included in the [XDG desktop portals](https://flatpak.github.io/xdg-desktop-portal/docs/api-reference.html):
  * Getting the user account
  * Requesting autostart
  * Dealing with the sandbox to access cameras, clipboard, etc
  * Using system file picker to access files including from outside the sandbox
  * Making a global keyboard shortcut
  * Inhibiting sleep, screen locking, etc
  * Capturing input
  * Finding the location of the device
  * Printing from within the sandbox
  * Starting screencasts and taking screenshots
* Copy/paste and drag-and-drop between GNUstep and native apps
  * We will want to handle copy-and-paste and drag-and-drop between GNUstep apps in the OpenStep style

I'm not sure whether the text support/input method support should go into DesktopIntegrationKit, gnustep-back, or gnustep-gui -- probably needs to be in a mix of them all.

### Why not do this in GNUstep-GUI?

* On the same window system there may exist multiple different desktops that need to be dealt with separately
  * So we can't just deal with it using the gnustep-back backends
* Many parts of desktop integration are independent of GUI toolkit
  * DesktopIntegrationKit does not need to assume you're using gnustep-gui
  * This could help us get outside contributions, but our use of Objective-C might make that less likely

## Basic design

* DesktopIntegrationKit itself provides a few things:
  * APIs for apps to use directly
    * DesktopIntegrationKit APIs
    * UserNotifica

### Things that require desktop integration but are also in themes' purview





