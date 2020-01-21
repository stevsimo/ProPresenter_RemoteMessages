# ProPresenter-RemoteMessages
Websocket to display and hide Messages in ProPresenter, without the ProPresenter-Operator needing to confirm any message request.
We use this, for our Kids-Team, to display a number to the main display, if a child needs picking up. This helps as the Kids are in a different part of the building.

This document refers to *ProPresenter 6*.

Both the Remote Control and the Stage Display protocols are unencrypted text-based websocket connections from the client to the ProPresenter instance.

Note, both the Remote Control and the Stage Display interface must be enabled in ProPresenter, if done they both operate over the *Remote Control* network port.
Also one must be in the same network as ProPresenter is.

## Remote Control


### Connecting

```javascript
ws://[host]:[port]/remote
```

### Authenticate

COMMAND TO SEND:

```javascript
{"action":"authenticate","protocol":"600","password":"control"}
```
* protocol is used to perform a version check. ProPresenter 6 seems to check for a value here of at least 600 - otherwise it denies authentication and returns "Protocol out of date. Update application"

EXPECTED RESPONSE:

```javascript
{"controller":1,"authenticated":1,"error":"","action":"authenticate"}
```

### Request Current Stage Display Layout

COMMAND TO SEND:

```javascript
{"acn":"psl"}
```

EXPECTED RESPONSE (also used when stage display is updated):

```javascript
{"acn":"psl","uid":"[STAGE DISPLAY UID]"}
```

### Send Message
Display a message identified by its index.

COMMAND TO SEND:

```javascript
{"action":"messageSend","messageIndex":0,"messageKeys":"["key1","key2"....]","messageValues":"["Value1","Value2"...]"}
```

### Hide a Message
Hide a message identified by its index

COMMAND TO SEND: 

```javascript
{"action":"messageHide","messageIndex","0"}
```
