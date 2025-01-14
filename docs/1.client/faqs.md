---
title: Troubleshooting FAQs
description: The main Frequently Asked Questions for Cider application support.
---

# Troubleshooting FAQs

::alert{type="note"}
This is essential knowledge for the debugging process, please read these before creating an issue.
::

## How to find the Application Data Directory

The location of your application data varies depending on your operating system, see your platforms path below:
- MS Store: `%localappdata%\packages\27554FireDevElijahKlauman.CiderEA_270bejk4xgzqp\LocalCache\Roaming\C2Windows`
- Windows (non-MS Store): `%appdata%\C2Windows`
- Linux: `$HOME/.config/sh.cider.genten`
- MacOS: `/Library/Application Support/sh.cider.genten`


## Why is my DiscordRPC status not appearing?

Try the following if Discord Rich Presence is not appearing on Discord.

<details>

<summary>Discord Desktop Client Only</summary>

Ensure you only have the Discord desktop client, not the web client open. As Cider is not directly connected to Discord we cannot have your status showing when not connected to Cider directly through Discord's Rich Presence functionality.

</details>

<details>

<summary>Activity Status Message</summary>

Make sure that 'Display current activity as a status message' is enabled in your Activity Status category in the Discord settings. Cider will not appear as a game, so do not manually add it.

<img src="https://i.imgur.com/3znfOMh.png" alt="Discord Activity Status Message" data-size="original">

</details>

<details>

<summary>Snapcraft Store Issues</summary>

If you are using Discord from the Snap Store, you are advised to install from a different source (Discords Website or using another package manager). The Snap Store version of Discord is known to have issues with DiscordRPC.

</details>

<details>

<summary>Permissions and Elevation</summary>

Ensure that you are running Discord on a level that is below Cider. If Discord is being elevated, Cider will be unable to connect. Furthermore, **ensure that Discord is started first**. Cider has to connect to Discord and this is only done on Cider's launch. So make sure Discord is started before Cider.

</details>

## Cider is Skipping or Not Playing Explicit Songs

If you are experiencing this issue, your account might have content restrictions set to "Clean". Login to [Apple Music Web](https://beta.music.apple.com), go to Profile Picture > Settings, then login again and check the "Content Restrictions" under "Parent Controls". 

Make sure that Music is set to **Explicit**.

::alert{type="note"}
It could potentially be a case where explicit playback is restricted in your country, in this case you may need to change your Apple Account region to resolve this.
::

## Why do I keep getting 'localtunnel.me connection refused' on macOS?

This is a fairly rare case and can be resolved fairly easily. Follow the steps below and it should resolve your issue:
1. Disable any Antivirus and/or Firewall present on your device. These can conflict with the WebSocket API in the client and will cause this error. (ESET is a known offender for this.)
2. Ensure you do not have a VPN on or any policies enabled on your device that can affect network traffic. Company managed devices may also have policies blocking this.
3. Check that you do not have Cider running already - and that nothing is running on the same port that Cider operates under - `10767`.

Outside of this advice, there is an [open issue on localtunnel](https://github.com/localtunnel/localtunnel/issues/658) for it, unfortunately we are stuck with it as one of the key components in Cider uses it as a dependency. We cannot help further on this issue.

## Why is the app launching with a blank screen on Linux?

This is a somewhat common issue for those on OpenSuse and other distro's that require their `/etc/hosts` file to manually set. To resolve this issue, you will need to ensure that your `/etc/hosts` file is set up correctly. See the example below for how it should look:

```bash
127.0.0.1 localhost
::1 localhost
127.0.0.2 YOUR_HOSTNAME
```