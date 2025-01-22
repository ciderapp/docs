---
title: App Documentation
description: A list of various bits of documentation for the app.
---

# Client Protocol Schema

The client uses a set list of protocols, including custom and overriding ones for AM apps. This is a list of all the protocols that the client uses.
- cider
- itms
- itmss
- music
- itunes

## URL Schema

The URL schema is as follows:
```protocol://{action}/{type}/{id}```

The available actions are:
- play
- open

The available types are:
- s (song)
- a (album)
- p (playlist)
- r (radio)

The ID must be the catalog ID of the item as the library item may not be available.

## Additional Protocols

The client also handles additional protocols such as:
- Apple Music URLs: `protocol://music.apple.com/...`
- Our Discord Server: `protocol://discord`
- Our GitHub: `protocol://github`
- OpenCollective: `protocol://donate`
- An AppData URL: `protocol://appdata` (For troubleshooting)
- Any standard app route. Such as `protocol://settings` or `protocol://am/home`
