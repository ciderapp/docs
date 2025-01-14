---
title: "Custom Port for Client Frontend"
description: "Guide on how to change the port the client frontend listens on."
navigation:
  title: "Override Client Port"
  icon: ""
draft: true
---

# Changing the Client Frontend Port

Cider defaults to using port `9000` for the client frontend. If you need to change this port, you can do so by setting the `PORT` environment variable.

**_Note: This only works on Electron Clients. Setting the port on Sabiiro is currently not supported._**

## Setting the Port in the CLI

When running Cider from the CLI you can set the ports as follows:

```bash
PORT=1111 ./cider-2.4.1.appimage
```

This will start the client frontend on port `1111`.

## Setting the Port in a `etc/environment` File

In linux you can set the port in a `etc/environment` file. This file is read by the system on startup and sets the environment variables for all processes. **MacOS users can use the `~/.bash_profile` file.**
