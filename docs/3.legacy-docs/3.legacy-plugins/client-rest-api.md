---
title: "Client REST API - V1"
description: "Learn how to control the client using REST"
---

# REST API

Cider offers a simple REST API to remotely control the app.

URL: http://localhost:9000/api/

## Endpoints

{% tabs %}
{% tab title="/playback" %}
| Endpoint | Description |
| ---------- | ----------------------------------------- |
| /playpause | Toggle between play and pause |
| /play | Play |
| /pause | Pause |
| /stop | Stop the current song |
| /next | Skip to the next song in the queue |
| /previous | Go back to the previous song in the queue |

{% endtab %}

{% tab title="/musickit" %}
| Endpoint | Method | Description | Usage |
| -------- | :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| /v3 | POST | <p>Access the MusicKit instance and use the v3 API routes<br><a href="https://developer.apple.com/documentation/applemusicapi/">https://developer.apple.com/documentation/applemusicapi/</a></p> | <p>Takes 3 parameters.<br><code>route</code><br><code>body</code><br><code>options</code></p> |
| | | | |
| | | | |
| | | | |
| | | | |
{% endtab %}
{% endtabs %}
