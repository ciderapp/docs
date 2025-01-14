---
title: "Client RPC Documentation"
description: "This website contains all the resources required to compile, create plugins and theme Cider!"
navigation:
  title: "Client RPC"
  icon: ""
draft: "false"
---

# RPC Documentation

All of the endpoints are paths that point to `http://localhost:10769`, we've observed that sometimes using `127.0.0.1` when IPv4 is disabled (don't do that btw) tends to break and not connect. We're not fixing this as it's user error for turning off IPv4, but if you cannot do anything about it, try using `[::1]:10769`.

### **GET** `/active`

This will respond as quickly as possible with an empty `204: No Content` response, it can be used to quickly check that the RPC is still active.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/currentPlayingSong`

This will respond with an Apple Music API Response for the currently playing song, the following is an example response.

<details>
<summary><b>200</b>: OK</summary>

```json
{
  "info": {
    "albumName": "Skin",
    "artistName": "Flume",
    "artwork": {
      "bgColor": "aa96c7",
      "height": 600,
      "textColor1": "040a06",
      "textColor2": "1b1937",
      "textColor3": "25262c",
      "url": "https://is1-ssl.mzstatic.com/image/thumb/Music122/v4/20/84/1b/20841bcf-a7c1-8048-08ba-ea03e33dbdce/3614598524069.png/{w}x{h}bb.jpg",
      "width": 600
    },
    "audioLocale": "en-US",
    "audioTraits": ["atmos", "lossless", "lossy-stereo", "spatial"],
    "composerName": "Harley Streten, Amanda Warner & Peter Wade Keusch",
    "currentPlaybackProgress": 0.63,
    "currentPlaybackTime": 123.059955,
    "discNumber": 1,
    "durationInMillis": 193633,
    "endTime": 1686069277080,
    "genreNames": ["Electronic"],
    "hasLyrics": true,
    "hasTimeSyncedLyrics": true,
    "isAppleDigitalMaster": false,
    "isMasteredForItunes": false,
    "isPlaying": true,
    "isVocalAttenuationAllowed": true,
    "isrc": "MtheoryLLCAUFF01600807",
    "kind": "song",
    "name": "Like Water (feat. MNDR)",
    "playParams": {
      "id": "1481729389",
      "kind": "song"
    },
    "previews": [
      {
        "url": "https://audio-ssl.itunes.apple.com/itunes-assets/AudioPreview112/v4/9d/12/c3/9d12c393-bc10-14ba-b70b-a8ad27fb21b7/mzaf_1376031537628674471.plus.aac.ep.m4a"
      }
    ],
    "releaseDate": "2016-05-27T12:00:00Z",
    "remainingTime": 70573.04500000001,
    "songId": "1481729389",
    "startTime": 1686069083447.045,
    "status": "playing",
    "trackNumber": 14,
    "url": {
      "appleMusic": "https://music.apple.com/au/song/1481729389",
      "cider": "https://cider.sh/link?play/s/1481729389",
      "songLink": "https://song.link/i/1481729389"
    }
  }
}
```

</details>

### **GET** `/addToLibrary`

This will save the currently playing track to the user's library. If no music is playing, this will do nothing.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/isPlaying`

This will return a JSON string stating if the player is currently actively playing a song or not.

<details>
<summary><b>200</b>: OK - Playing</summary>
```json
{
	"is_playing": true
}
```
</details>

<details>
<summary><b>200</b>: OK - Not Playing</summary>
```json
{
	"is_playing": false
}
```
</details>

These are the only 2 potential responses to this request, if it is anything else, it's safe to assume something broke.

{/\*

    IMO the next 3 endpoints should be PUT or POST but they're GET because why not. (playPause, play, pause -Amaru8)

    -d3rpp

\*/}

### **GET** `/toggleAutoplay`

This will change the autoplay setting to its opposite value and return the updated value in a JSON string.

<details>
<summary><b>200</b>: OK - Enabled</summary>
```json
{
	"autoplay": true
}
```
</details>

<details>
<summary><b>200</b>: OK - Disabled</summary>
```json
{
	"autoplay": false
}
```
</details>

These are the only 2 potential responses to this request, if it is anything else, it's safe to assume something broke.

### **GET** `/playPause`

This is functionally equivalent to clicking the play/pause button within the application.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/play`

This is functionally equivalent to clicking the play button within the application, if music is already playing, this will do nothing.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/pause`

This is functionally equivalent to clicking the pause button within the application, if music is already paused, this will do nothing.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/stop`

This is functionally equivalent to clicking the STOP button within the application, if nothing is happening, this will do nothing

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/next`

This will skip to the next song, behaviour is identical to clicking the button within the application.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/previous`

This will skip to the previous song, behaviour is identical to clicking the button within the application.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/seekto/{t}`

**_Where_**

- `t` is the time you'd like to skip to in seconds

Set the playhead to this time in the song, you can use `/currentPlayingSong` to get the time, (using the `durationInMillis` property divided by 1,000 to get the duration in seconds).

This will always return `204` and if the call fails or the song is too long, it will silently fail, it is recommended that you check the song's actual length before running this function.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/show`

Will show the window and demand user attention on the screen

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/hide`

Will hide the window, if enabled this will minise it to the system tray as well.

<details>
<summary><b>204</b>: No Content</summary>
```json
// No Response Body...
```
</details>

### **GET** `/album/{id}`

**_Where_**

- `id` is the ID of the album you'd like to lookup

This will run a query of the Apple Music API using the signed in user's account and will pipe the response back to here.

This will always return a 200 but with a different JSON Structure

<details>
<summary><b>200</b>: OK - Failed Lookup</summary>
```json
{
	"errors": [
		{
			"code": "40400",
			"detail": "Resource with requested id was not found",
			"id": "", // redacted
			"status": "404",
			"title": "Resource Not Found"
		}
	]
}
```
</details>

<details>
<summary><b>200</b>: OK - Successful Lookup</summary>
```json
{
	"data": [
		{
			"attributes": {
				"artistName": "nihmune",
				"artwork": {
					"bgColor": "94888c",
					"height": 3000,
					"textColor1": "110c0d",
					"textColor2": "181313",
					"textColor3": "2b2426",
					"textColor4": "312a2b",
					"url": "https://is1-ssl.mzstatic.com/image/thumb/Music116/v4/a2/12/49/a21249ee-8827-cc8c-0664-abf341404a76/artwork.jpg/{w}x{h}bb.jpg",
					"width": 3000
				},
				"contentRating": "explicit",
				"copyright": "℗ 2022 Swag Records",
				"genreNames": [
					"Pop",
					"Music",
					"Comedy"
				],
				"isCompilation": false,
				"isComplete": true,
				"isMasteredForItunes": false,
				"isSingle": true,
				"name": "Cpr - Single",
				"playParams": {
					"id": "1606000385",
					"kind": "album"
				},
				"recordLabel": "Swag Records",
				"releaseDate": "2022-01-21",
				"trackCount": 1,
				"upc": "196697480390",
				"url": "https://music.apple.com/us/album/cpr-single/1606000385"
			},
			"href": "/v1/catalog/us/albums/1606000385",
			"id": "1606000385",
			"relationships": {
				"artists": {
					"data": [
						{
							"href": "/v1/catalog/us/artists/1559436668",
							"id": "1559436668",
							"type": "artists"
						}
					],
					"href": "/v1/catalog/us/albums/1606000385/artists"
				},
				"tracks": {
					"data": [
						{
							"attributes": {
								"albumName": "Cpr - Single",
								"artistName": "nihmune",
								"artwork": {
									"bgColor": "94888c",
									"height": 3000,
									"textColor1": "110c0d",
									"textColor2": "181313",
									"textColor3": "2b2426",
									"textColor4": "312a2b",
									"url": "https://is1-ssl.mzstatic.com/image/thumb/Music116/v4/a2/12/49/a21249ee-8827-cc8c-0664-abf341404a76/artwork.jpg/{w}x{h}bb.jpg",
									"width": 3000
								},
								"composerName": "cupcakKe",
								"contentRating": "explicit",
								"discNumber": 1,
								"durationInMillis": 208170,
								"genreNames": [
									"Pop",
									"Music",
									"Comedy"
								],
								"hasLyrics": true,
								"isAppleDigitalMaster": false,
								"isrc": "QZFZ22277497",
								"name": "Cpr",
								"playParams": {
									"id": "1606000776",
									"kind": "song"
								},
								"previews": [
									{
										"url": "https://audio-ssl.itunes.apple.com/itunes-assets/AudioPreview126/v4/43/4e/37/434e37de-5b84-63fc-9cfd-b50f7b2f4aec/mzaf_15590872885935990851.plus.aac.p.m4a"
									}
								],
								"releaseDate": "2022-01-21",
								"trackNumber": 1,
								"url": "https://music.apple.com/us/album/cpr/1606000385?i=1606000776"
							},
							"href": "/v1/catalog/us/songs/1606000776",
							"id": "1606000776",
							"type": "songs"
						}
					],
					"href": "/v1/catalog/us/albums/1606000385/tracks"
				}
			},
			"type": "albums"
		}
	]
}
```
</details>

For More information on the structure of this response, consult the [Apple Music API Docs](https://developer.apple.com/documentation/applemusicapi/songsresponse)

### **PUT** `/rating/{type}/{id}/{rating}`

**_Since_** Cider version `2.1.3`

**_Where_**

- `type` is the type of content you're submitting a rating for, this can be `song`, `music-video`, `album`, or `playlist`
- `id` is the ID of the content in question, you can get it from `/currentPlayingSong`
- `rating` is the rating you'd like to push
  - `-1` is a dislike
  - `0` resets the rating
  - `1` is a like

<details>
<summary><b>200</b>: OK - Successful Rating Added</summary>
```json
{
    "data": [
        {
            "attributes": {
                "value": 1
            },
            "href": "/v1/me/ratings/songs/1140574590",
            "id": "1140574590",
            "type": "ratings"
        }
    ]
}
```
</details>

<details>
<summary><b>204</b>: NO CONTENT - Rating Removed</summary>
```js
// no body
```
</details>

### **GET** `/audio`

Get the current volume, this will return plain-text as a floating point number between 0 and 1 inclusive

<details>
<summary><b>200</b>: OK - Volume Fetched</summary>
```js
0.98
```
</details>

### **GET** `/audio/{volume}`

Set the volume slider, will set the in-app volume, not the system volume.

requires a floating point value between 0 and 1, (e.g. `/audio/0.8`).

<details>
<summary><b>204</b>: NO CONTENT - Volume Set</summary>
```js
// ... no body
```
</details>

### **GET** `/rating/{type}/{id}`

**_Since_** Cider version `2.1.3`

**_Where_**

- `type` is the type of content you're submitting a rating for, this can be `song`, `music-video`, `album`, or `playlist`
- `id` is the ID of the content in question, you can get it from `/currentPlayingSong`

<details>
<summary><b>200</b>: OK - Successful Lookup</summary>
```json
{
    "data": [
        {
            "attributes": {
                "value": 1
            },
            "href": "/v1/me/ratings/songs/1140574590",
            "id": "1140574590",
            "type": "ratings"
        }
    ]
}
```
</details>

<details>
<summary><b>200</b>: Error - Unsuccessful Lookup</summary>
```json
{
    "errors": [
        {
            "code": "40400",
            "detail": "Resource with requested id was not found",
            "id": "... REDACTED ...",
            "status": "404",
            "title": "Resource Not Found"
        }
    ]
}
```
</details>
