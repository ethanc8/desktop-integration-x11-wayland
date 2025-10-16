Title: org.kde.StatusNotifierWatcher D-Bus Interface
Slug: org.kde.StatusNotifierWatcher

# org.kde.StatusNotifierWatcher

## Description

There will be a single `org.kde.StatusNotifierWatcher` service instance registered on the session bus at any given time. The `StatusNotifierWatcher` service is used to keep track of `StatusNotifierItem` instances, enumerate them and notify when new ones are registered or old ones are unregistered.

It is also used to keep track of `org.freedesktop.StatusNotifierHost` instances, to have an easy way to know if there is at least one service registered as the visualization host for the status notifier items. The `org.freedesktop.StatusNotifierHost`s seem to be deprecated implementation details.

### Properties
### org.kde.StatusNotifierWatcher:RegisteredStatusNotifierItems

```
    RegisteredStatusNotifierItems readable as
```

List containing all the registered instances of `StatusNotifierItem`. All elements of the array should correspond to services actually running on the session bus at the moment of the method call.

### org.kde.StatusNotifierWatcher:IsStatusNotifierHostRegistered

```
    IsStatusNotifierHostRegistered readable b
```

True if at least one `StatusNotifierHos`t has been registered with [`RegisterStatusNotifierHost`](#RegisterStatusNotifierHost) and is currently running. If no StatusNotifierHost are registered and running, all StatusNotifierItem instances should fall back using the Freedesktop System tray specification.

### org.kde.StatusNotifierWatcher:ProtocolVersion

```
    ProtocolVersion readable i
```

The version of the protocol the StatusNotifierWatcher instance implements.

### Methods

(RegisterStatusNotifierItem)=
### org.kde.StatusNotifierWatcher.RegisterStatusNotifierItem

```
    RegisterStatusNotifierItem (
      IN serviceOrPath s
    )
```

[Implementation](https://invent.kde.org/plasma/plasma-workspace/-/blob/v6.4.5/statusnotifierwatcher/statusnotifierwatcher.cpp?ref_type=tags#L39)

Register a `StatusNotifierItem` into the `StatusNotifierWatcher`. A `StatusNotifierItem` instance must be registered to the watcher in order to be noticed from both the watcher and the `StatusNotifierHost` instances. If the registered `StatusNotifierItem` goes away from the session bus, the `StatusNotifierWatcher` should automatically notice it and remove it from the list of registered services.

* serviceOrPath: Either
  * The full name of the service on the session bus. Must not start with `/`.
  * An arbitrary path starting with `/`. It does not have to represent a filesystem path or any other type of path.

**Implementation detail:** A unique notifier item ID will be created by concatenating the service name (either passed in `serviceOrPath` or the name of the service calling this method), plus the path (`/StatusNotifierItem` if a service name was passed).

(RegisterStatusNotifierHost)=
### org.kde.StatusNotifierWatcher.RegisterStatusNotifierHost

```
    RegisterStatusNotifierHost (
      IN service s
    )
```

Deprecated implementation detail.

### Signals
### org.kde.StatusNotifierWatcher::StatusNotifierItemRegistered

```
    StatusNotifierItemRegistered (
      service s
    )
```

A new StatusNotifierItem has been registered. StatusNotifierHost implementation should listen this signal to know when they should update their representation of the items.

* service: the session bus name of the instance

### org.kde.StatusNotifierWatcher::StatusNotifierItemUnregistered

```
    StatusNotifierItemUnregistered (
      service s
    )
```

A StatusNotifierItem instance has disappeared from the bus. StatusNotifierHost implementation should listen this signal to know when they should update their representation of the items.

* service: the session bus name of the instance

### org.kde.StatusNotifierWatcher::StatusNotifierHostRegistered

```
    StatusNotifierHostRegistered ()
```

A new StatusNotifierHost has been registered, the StatusNotifierItem instances knows that they can use this protocol instead of the (XEmbed-based) Freedesktop System tray protocol.

### org.kde.StatusNotifierWatcher::StatusNotifierHostUnregistered

```
    StatusNotifierHostUnregistered ()
```

The StatusNotifierHost has been deregistered.
