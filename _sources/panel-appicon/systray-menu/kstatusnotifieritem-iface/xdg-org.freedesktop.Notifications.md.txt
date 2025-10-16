Title: org.freedesktop.Notifications D-Bus Interface
Slug: org.freedesktop.Notifications

# org.freedesktop.Notifications

## Description





### Properties
### org.freedesktop.Notifications:Inhibited

```
    Inhibited readable b
```



### Methods
### org.freedesktop.Notifications.Notify

```
    Notify (
      IN app_name s,
      IN replaces_id u,
      IN app_icon s,
      IN summary s,
      IN body s,
      IN actions as,
      IN hints a{sv},
      IN timeout i,
      OUT unnamed_arg8 u
    )
```



* app_name: 

* replaces_id: 

* app_icon: 

* summary: 

* body: 

* actions: 

* hints: 

* timeout: 



### org.freedesktop.Notifications.CloseNotification

```
    CloseNotification (
      IN id u
    )
```



* id: 



### org.freedesktop.Notifications.GetCapabilities

```
    GetCapabilities (
      OUT caps as
    )
```





### org.freedesktop.Notifications.GetServerInformation

```
    GetServerInformation (
      OUT name s,
      OUT vendor s,
      OUT version s,
      OUT spec_version s
    )
```





### org.freedesktop.Notifications.Inhibit

```
    Inhibit (
      IN desktop_entry s,
      IN reason s,
      IN hints a{sv},
      OUT unnamed_arg3 u
    )
```



* desktop_entry: 

* reason: 

* hints: 



### org.freedesktop.Notifications.UnInhibit

```
    UnInhibit (
      IN unnamed_arg0 u
    )
```



* unnamed_arg0: 


### Signals
### org.freedesktop.Notifications::NotificationClosed

```
    NotificationClosed (
      id u,
      reason u
    )
```



id
  

reason
  



### org.freedesktop.Notifications::ActionInvoked

```
    ActionInvoked (
      id u,
      action_key s
    )
```



id
  

action_key
  



### org.freedesktop.Notifications::NotificationReplied

```
    NotificationReplied (
      id u,
      text s
    )
```



id
  

text
  



### org.freedesktop.Notifications::ActivationToken

```
    ActivationToken (
      id u,
      activation_token s
    )
```



id
  

activation_token
  


