---
title: "Client RPC Documentation"
description: "Documentation for RPC API endpoints accessible by clients external to Cider."
---

# RPC Documentation

### Hostname and Port

All API endpoints are accessible at `http://localhost:10767`.

We've observed that using `127.0.0.1` when IPv4 is disabled tends to break and not connect. We recommend you do not turn off IPv4, but if you are required to do so, try using `[::1]:10767`.

### Authentication

Unless explicitly disabled within Cider, all API requests require a valid API token. You can generate this token, or turn off authentication, from the menu at **Settings -> Connectivity -> Manage External Application Access to Cider** within Cider.

The generated token should be passed in the `apptoken` header of all requests. Do not prefix the token with `Bearer` or any other string; just pass the token by itself in the header.

This token is not required if disabled within the settings menu.

### `/api/v1/playback`

The API endpoints documented below are all nested under `/api/v1/playback`.

#### **GET** `/active`

Responds with an empty body and status code `204: No Content`. This endpoint can be used to quickly check that the RPC server is still active.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **GET** `/is-playing`

Responds with a boolean value indicating whether music is currently playing.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "is_playing": true
}</pre>
</code>
</details>

#### **GET** `/now-playing`

Responds with an Apple Music API response for the currently playing song.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "info": {
    "albumName": "Skin",
    "hasTimeSyncedLyrics": true,
    "genreNames": [
      "Electronic"
    ],
    "trackNumber": 14,
    "durationInMillis": 193633,
    "releaseDate": "2016-05-27T12:00:00Z",
    "isVocalAttenuationAllowed": true,
    "isMasteredForItunes": false,
    "isrc": "AlligatorAUFF01600807",
    "artwork": {
      "width": 600,
      "height": 600,
      "url": "https://is1-ssl.mzstatic.com/image/thumb/Music116/v4/0e/d9/af/0ed9af7b-595d-6e9f-7b2e-c1113f4902f6/3555.jpg/640x640sr.jpg"
    },
    "audioLocale": "en-US",
    "url": "https://music.apple.com/ca/album/like-water-feat-mndr/1719860281?i=1719861213",
    "playParams": {
      "id": "1719861213",
      "kind": "song"
    },
    "discNumber": 1,
    "hasLyrics": true,
    "isAppleDigitalMaster": false,
    "audioTraits": [
      "atmos",
      "lossless",
      "lossy-stereo",
      "spatial"
    ],
    "name": "Like Water (feat. MNDR)",
    "previews": [
      {
        "url": "https://audio-ssl.itunes.apple.com/itunes-assets/AudioPreview116/v4/33/68/51/336851f3-f985-9948-a4dc-579c57b1f326/mzaf_16966411213881300046.plus.aac.ep.m4a"
      }
    ],
    "artistName": "Flume",
    "currentPlaybackTime": 2.066576,
    "remainingTime": 191.566424,
    "inFavorites": false,
    "inLibrary": false,
    "shuffleMode": 0,
    "repeatMode": 0
  }
}</pre>
</code>
</details>

#### **POST** `/play-url`

Triggers playback of an item.

Accepts a `url` of the item to play. This URL can be found by right-clicking on an item and clicking on `Share -> Apple Music` in Cider, `Share -> Copy Link` in the official Apple Music app, or by copying the URL when viewing an item in the Apple Music web app.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "url": "https://music.apple.com/ca/album/like-water-feat-mndr/1719860281"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/play-item-href`

Triggers playback of an item.

Accepts an `href` (Apple Music API identifier).

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "href": "/v1/catalog/ca/songs/1719861213"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/play-item`

Triggers playback of an item.

Accepts a `type` of item to play and an `id` for the item. `type` should be one of the accepted types in the Apple Music API, such as `songs`. Note that the ID is required to be a string, not a number.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "type": "songs",
  "id": "1719861213"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/play-later`

Adds an item to the _end_ of the play queue (played after all other items currently in the queue).

Accepts a `type` of item to play and an `id` for the item. `type` should be one of the accepted types in the Apple Music API, such as `songs`. Note that the ID is required to be a string, not a number.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "type": "songs",
  "id": "1719861213"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/play-next`

Adds an item to the _start_ of the play queue (played next, before all other items in the queue).

Accepts a `type` of item to play and an `id` for the item. `type` should be one of the accepted types in the Apple Music API, such as `songs`. Note that the ID is required to be a string, not a number.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "type": "songs",
  "id": "1719861213"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/play`

Resumes playback of the current item. If no item is playing, the behavior set under the menu **Settings -> Play Button on Stopped Action** in Cider will take effect.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/pause`

Pauses the currently playing item. If no item is playing or if the item is already paused, this will do nothing.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/playpause`

Toggles the play/pause state of the current item. This has the same behavior as calling `/pause` if the item is playing, and `/play` if the item is paused.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/stop`

Stops the current playback and removes the current item. If items are in the queue, they will be kept.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/next`

Moves to the next item in the queue, if any. Autoplay enable/disable status will be respected if the queue is empty (infinity button within the queue panel in Cider).

If no item is currently playing but there is one in the queue, it will be started.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/previous`

Moves to the previously played item, which is the item most recent in the playback history.

If no item is currently playing but there is one in the playback history, it will be started.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **GET** `/queue`

Gets the current queue as a list of Apple Music response objects. Note that this also includes part of the history and the currently playing track.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>[
  {
    "id": "1440559604",
    "type": "song",
    "assetURL": "https://aod-ssl.itunes.apple.com/itunes-assets/Music116/v4/28/7d/75/287d75f0-ec98-845f-377e-57a5c2c8d0c4/mzaf_A1440559604.rphq.aac.wa.m3u8",
    "hlsMetadata": {},
    "flavor": "28:ctrp256",
    "attributes": {
      "albumName": "Bright Lights (Deluxe Version)",
      "hasTimeSyncedLyrics": true,
      "genreNames": [
        "Pop"
      ],
      "trackNumber": 11,
      "durationInMillis": 210634,
      "releaseDate": "2010-02-26T12:00:00Z",
      "isVocalAttenuationAllowed": true,
      "isMasteredForItunes": false,
      "isrc": "UniversalGBUM71028043",
      "artwork": {
        "width": 600,
        "height": 600,
        "url": "https://is1-ssl.mzstatic.com/image/thumb/Music123/v4/e4/53/c8/e453c827-3858-d5c2-e2a2-1b85d772b0ba/10UMGIM30297.rgb.jpg/640x640sr.jpg"
      },
      "composerName": "Ellie Goulding, Richard Stannard & Ash Howes",
      "audioLocale": "en-US",
      "playParams": {
        "id": "1440559604",
        "kind": "song"
      },
      "url": "https://music.apple.com/ca/album/lights-single-version/1440559376?i=1440559604",
      "discNumber": 1,
      "isAppleDigitalMaster": false,
      "hasLyrics": true,
      "audioTraits": [
        "lossless",
        "lossy-stereo"
      ],
      "name": "Lights (Single Version)",
      "previews": [
        {
          "url": "https://audio-ssl.itunes.apple.com/itunes-assets/AudioPreview126/v4/09/97/f4/0997f41b-abf7-bae9-6059-1637b6a12f6c/mzaf_4696029188384744065.plus.aac.ep.m4a"
        }
      ],
      "artistName": "Ellie Goulding",
      "currentPlaybackTime": 48.994104,
      "remainingTime": 161.639896
    },
    "playbackType": 3,
    "_container": {
      "id": "ra.cp-1055074639",
      "type": "stations",
      "href": "/v1/catalog/ca/stations/ra.cp-1055074639",
      "attributes": {
        "requiresSubscription": true,
        "isLive": false,
        "kind": "songSeeded",
        "radioUrl": "itsradio://music.apple.com/ca/station/ra.cp-1055074639",
        "mediaKind": "audio",
        "name": "Unstoppable Station",
        "artwork": {
          "width": 1500,
          "url": "https://is1-ssl.mzstatic.com/image/thumb/Music115/v4/bc/13/27/bc13275c-8b26-802d-771b-d15ae00fb530/mzm.hvpwjsvi.jpg/{w}x{h}AM.RSSB02.jpg",
          "height": 1500,
          "textColor3": "bda69d",
          "textColor2": "e8c4aa",
          "textColor4": "bca08b",
          "textColor1": "eaccc1",
          "bgColor": "0c0e0d",
          "hasP3": false
        },
        "url": "https://music.apple.com/ca/station/unstoppable-station/ra.cp-1055074639",
        "playParams": {
          "id": "ra.cp-1055074639",
          "kind": "radioStation",
          "format": "tracks",
          "stationHash": "CgkIARoFz9KM9wMQBQ",
          "hasDrm": false,
          "mediaType": 0
        }
      },
      "name": "now_playing"
    },
    "_context": {
      "featureName": "now_playing"
    },
    "_state": {
      "current": 2
    },
    "_songId": "1440559604",
    "assets": [
      {
        "flavor": "30:cbcp256",
        "URL": "https://aod-ssl.itunes.apple.com/itunes-assets/Music116/v4/28/7d/75/287d75f0-ec98-845f-377e-57a5c2c8d0c4/mzaf_A1440559604.cphq.aac.wa.m3u8",
        "downloadKey": "",
        "artworkURL": "https://is1-ssl.mzstatic.com/image/thumb/Music123/v4/e4/53/c8/e453c827-3858-d5c2-e2a2-1b85d772b0ba/10UMGIM30297.rgb.jpg/600x600bb.jpg",
        "file-size": 2228,
        "md5": "151e9fe6106256ef388a4b11dae4a672",
        "chunks": {
          "chunkSize": 0,
          "hashes": []
        },
        "metadata": {
          "composerId": "20844291",
          "genreId": 14,
          "copyright": "℗ 2010 Polydor Ltd. (UK)",
          "year": 2010,
          "sort-artist": "Ellie Goulding",
          "isMasteredForItunes": false,
          "vendorId": 2115541,
          "artistId": "338264227",
          "duration": 210634,
          "discNumber": 1,
          "itemName": "Lights (Single Version)",
          "trackCount": 30,
          "xid": "Universal:isrc:GBUM71028043",
          "bitRate": 256,
          "fileExtension": "m4p",
          "sort-album": "Bright Lights (Deluxe Version)",
          "genre": "Pop",
          "rank": 11,
          "sort-name": "Lights (Single Version)",
          "playlistId": "1440559376",
          "sort-composer": "Ellie Goulding, Richard Stannard & Ash Howes",
          "comments": "(Single Version)",
          "trackNumber": 11,
          "releaseDate": "2010-02-26T12:00:00Z",
          "kind": "song",
          "playlistArtistName": "Ellie Goulding",
          "gapless": false,
          "composerName": "Ellie Goulding, Richard Stannard & Ash Howes",
          "discCount": 1,
          "sampleRate": 44100,
          "playlistName": "Bright Lights (Deluxe Version)",
          "explicit": 0,
          "itemId": "1440559604",
          "s": 143455,
          "compilation": false,
          "artistName": "Ellie Goulding"
        }
      },
      {
        "flavor": "28:ctrp256",
        "URL": "https://aod-ssl.itunes.apple.com/itunes-assets/Music116/v4/28/7d/75/287d75f0-ec98-845f-377e-57a5c2c8d0c4/mzaf_A1440559604.rphq.aac.wa.m3u8",
        "downloadKey": "",
        "artworkURL": "https://is1-ssl.mzstatic.com/image/thumb/Music123/v4/e4/53/c8/e453c827-3858-d5c2-e2a2-1b85d772b0ba/10UMGIM30297.rgb.jpg/600x600bb.jpg",
        "file-size": 2104,
        "md5": "b577b5dd0cd5eef7aabce0b4f52fb7f9",
        "chunks": {
          "chunkSize": 0,
          "hashes": []
        },
        "metadata": {
          "composerId": "20844291",
          "genreId": 14,
          "copyright": "℗ 2010 Polydor Ltd. (UK)",
          "year": 2010,
          "sort-artist": "Ellie Goulding",
          "isMasteredForItunes": false,
          "vendorId": 2115541,
          "artistId": "338264227",
          "duration": 210634,
          "discNumber": 1,
          "itemName": "Lights (Single Version)",
          "trackCount": 30,
          "xid": "Universal:isrc:GBUM71028043",
          "bitRate": 256,
          "fileExtension": "m4p",
          "sort-album": "Bright Lights (Deluxe Version)",
          "genre": "Pop",
          "rank": 11,
          "sort-name": "Lights (Single Version)",
          "playlistId": "1440559376",
          "sort-composer": "Ellie Goulding, Richard Stannard & Ash Howes",
          "comments": "(Single Version)",
          "trackNumber": 11,
          "releaseDate": "2010-02-26T12:00:00Z",
          "kind": "song",
          "playlistArtistName": "Ellie Goulding",
          "gapless": false,
          "composerName": "Ellie Goulding, Richard Stannard & Ash Howes",
          "discCount": 1,
          "sampleRate": 44100,
          "playlistName": "Bright Lights (Deluxe Version)",
          "explicit": 0,
          "itemId": "1440559604",
          "s": 143455,
          "compilation": false,
          "artistName": "Ellie Goulding"
        },
        "previewURL": "https://audio-ssl.itunes.apple.com/itunes-assets/AudioPreview126/v4/09/97/f4/0997f41b-abf7-bae9-6059-1637b6a12f6c/mzaf_4696029188384744065.plus.aac.ep.m4a"
      },
      {
        "flavor": "37:ibhp256",
        "URL": "https://aod-ssl.itunes.apple.com/itunes-assets/Music116/v4/28/7d/75/287d75f0-ec98-845f-377e-57a5c2c8d0c4/mzaf_A1440559604.iphq.aac.wa.m3u8",
        "downloadKey": "",
        "artworkURL": "https://is1-ssl.mzstatic.com/image/thumb/Music123/v4/e4/53/c8/e453c827-3858-d5c2-e2a2-1b85d772b0ba/10UMGIM30297.rgb.jpg/600x600bb.jpg",
        "file-size": 2296,
        "md5": "d54100817096454cb074de4daf3ce322",
        "chunks": {
          "chunkSize": 0,
          "hashes": []
        },
        "metadata": {
          "composerId": "20844291",
          "genreId": 14,
          "copyright": "℗ 2010 Polydor Ltd. (UK)",
          "year": 2010,
          "sort-artist": "Ellie Goulding",
          "isMasteredForItunes": false,
          "vendorId": 2115541,
          "artistId": "338264227",
          "duration": 210634,
          "discNumber": 1,
          "itemName": "Lights (Single Version)",
          "trackCount": 30,
          "xid": "Universal:isrc:GBUM71028043",
          "bitRate": 256,
          "fileExtension": "m4p",
          "sort-album": "Bright Lights (Deluxe Version)",
          "genre": "Pop",
          "rank": 11,
          "sort-name": "Lights (Single Version)",
          "playlistId": "1440559376",
          "sort-composer": "Ellie Goulding, Richard Stannard & Ash Howes",
          "comments": "(Single Version)",
          "trackNumber": 11,
          "releaseDate": "2010-02-26T12:00:00Z",
          "kind": "song",
          "playlistArtistName": "Ellie Goulding",
          "gapless": false,
          "composerName": "Ellie Goulding, Richard Stannard & Ash Howes",
          "discCount": 1,
          "sampleRate": 44100,
          "playlistName": "Bright Lights (Deluxe Version)",
          "explicit": 0,
          "itemId": "1440559604",
          "s": 143455,
          "compilation": false,
          "artistName": "Ellie Goulding"
        }
      }
    ],
    "keyURLs": {
      "hls-key-cert-url": "https://s.mzstatic.com/skdtool_2021_certbundle.bin",
      "hls-key-server-url": "https://play.itunes.apple.com/WebObjects/MZPlay.woa/wa/acquireWebPlaybackLicense",
      "widevine-cert-url": "https://play.itunes.apple.com/WebObjects/MZPlay.woa/wa/widevineCert"
    }
  },
  // ...more items of the same format...
]</pre>
</code>
</details>

#### **POST** `/queue`

Not currently functional.

#### **POST** `/queue/move-to-position`

Moves an item in the queue from the `startIndex` to the `destinationIndex`. Optionally returns the queue if passed `returnQueue`.

Note that the index is 1-indexed (starts at 1, not 0). Also note that the queue contains some items that are from the history, so the items visible in the Up Next view in Cider may start at a number higher than 1.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "startIndex": 0,
  "destinationIndex": 1,
  "returnQueue": false
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/queue/remove-by-index`

Removes an item from the queue by its `index`

Note that the index is 1-indexed (starts at 1, not 0). Also note that the queue contains some items that are from the history, so the items visible in the Up Next view in Cider may start at a number higher than 1.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "index": 0
}</pre>
</code>
</details>

#### **POST** `/queue/clear-queue`

Clears the queue of all items.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/seek`

Seeks to a given offset, in seconds, in the currently playing item.

Accepts a `position` in seconds to seek to. Note that `/now-playing` returns a timestamp in milliseconds via the `durationInMillis` key, which should be divided by 1000 to get the duration in seconds.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "position": 30
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **GET** `/volume`

Gets the current playback volume as a number between `0` (muted) and `1` (full volume).

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "volume": 0.5
}</pre>
</code>
</details>

#### **POST** `/volume`

Sets the current playback volume to a number between `0` (muted) and `1` (full volume).

Accepts a `volume` as a number between `0` and `1`.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "volume": 0.5
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/add-to-library`

Adds the currently playing item to the user's library. No effect if already in library.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **POST** `/set-rating`

Adds a rating to the currently playing item. Rating is `-1` for dislike, `1` for like, and `0` for unset.

Accepts a `rating` as a number between `-1` and `1`.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "rating": 1
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **GET** `/repeat-mode`

Gets the current repeat mode as a number. `0` is off, `1` is "repeat this song", and `2` is "repeat".

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "value": 0
}</pre>
</code>
</details>

#### **POST** `/toggle-repeat`

Toggles repeat between "repeat this song", "repeat", and "off".

Note that this method doesn't take the mode to set, just changes to the next mode in the cycle **repeat this song -> repeat -> off**.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

#### **GET** `/shuffle-mode`

Gets the current shuffle mode as a number. `0` is off and `1` is on.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "value": 0
}</pre>
</code>
</details>

#### **POST** `/toggle-shuffle`

Toggles shuffle between "off" and "on".

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

### **GET** `/autoplay`

Gets the current autoplay status as a boolean. `true` is on and `false` is off.

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok",
  "value": true
}</pre>
</code>
</details>

#### **POST** `/toggle-autoplay`

Toggles autoplay between "off" and "on".

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "status": "ok"
}</pre>
</code>
</details>

### `/api/v1/amapi`

The API endpoints documented below are all nested under `/api/v1/amapi`. These API endpoints are generally for more advanced use-cases than the above endpoints, and pass through the raw Apple Music API responses directly with no translation.

#### **POST** `/run-v3`

Makes a request to the given `path` on the Apple Music API and returns the response.

<details>
<summary>Request Body (`application/json`)</summary>
<code>
<pre>{
  "path": "/v1/catalog/ca/search?{very long query string}"
}</pre>
</code>
</details>

<details>
<summary><b>200</b>: OK</summary>
<code>
<pre>{
  "data": {
	// Direct Apple Music API response
  }
}</pre>
</code>
</details>

### `/api/v1/lyrics`

The API endpoint documented below is nested under `/api/v1/lyrics`.

#### **GET** `/:id`

Gets lyrics for the given song ID. Currently non-functional but on track to be fixed soon.

<details>
<summary><b>200</b>: OK</summary>
<code>
// Currently omitted until endpoint is fully functional
</code>
</details>
