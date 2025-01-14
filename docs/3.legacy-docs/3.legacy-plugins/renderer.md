---
description: >-
  This page contains all the required documentation for the Renderer and its
  functions/events.
---

# Renderer

<details>

<summary>PluginEnv</summary>

When plugins are loaded in Cider the `constructor()` in the plugin class is passed a `PluginEnv` object, this object contains:

* `app` - The Electron app
* `store` - Electron Store
* `utils` - Cider utils
* `win` - The renderer window
* `dir` - Path to the plugin directory
* `dirName` - Plugin directory name

</details>

<details>

<summary>Loading frontend plugin(s)</summary>

To load a front end plugin (typically named `index.frontend.js`) from `index.js` `PluginEnv.utils.loadJSFrontend(path: string)` is used.

Example: `PluginEnv.utils.loadJSFrontend(path.join(PluginEnv.dir, "index.frontend.js"))`

</details>

<details>

<summary>utils</summary>

* `getPath(path: string)` - Returns path used by Cider by name.
  * `srcPath` - src/ folder
  * `rendererPath` - renderer/ folder
  * `mainPath` - main/ path
  * `resourcePath` - resources/ path
  * `i18nPath` - i18n/ path
  * `ciderCache` - Cider cache path
  * `themes` - Themes
  * `plugins` - Plugins
* `getLocale(language: string, key: string)`
  * Fetches the i18n locale for the given language.
* `getStoreValue(key: string)`
  * Gets a store value
* `getStore()`
  * Returns store
* `setStoreValue(key: string, value: any)`
  * Sets a store value
* `getWindow()`
  * Gets the renderer window
* `loadJSFrontend(path: string)`
  * Loads a JavaScript file into the renderer, this is the main method of loading front end plugins.
* `playback.` - Controls playback
  * `.play()` - Play
  * `.pause()` - Pause
  * `.playPause()` - Toggles playback
  * `.next()` - Next track in queue
  * `.previous()` - Previous track in queue

</details>

<details>

<summary>Built in events</summary>

Cider plugins support these methods by default, however more can be made with the use of ipcMain and ipcRenderer

* `onReady(win)` - (Required) Executes when the back end is ready
* `onRendererReady()` - Executes when the renderer has finished loading (app.init())
* `onPlaybackStateDidChange(attributes)` - Executes when playback state changes, passes song attributes
* `onNowPlayingItemDidChange(attributes)` - Executes when song changes, passes song attributes
* `onBeforeQuit` - Executes before Cider quits

</details>

### Cider Frontend API (CiderFrontAPI)

| Function/Method   | Usage | Details |
| ----------------- | ----- | ------- |
| StyleSheets.Add   |       |         |
| AddMenuEntry      |       |         |
| Objects.MenuEntry |       |         |

### App Functions/Methods (app.\*)

| Function/Method | Usage | Details |
| --------------- | ----- | ------- |
|                 |       |         |
|                 |       |         |
|                 |       |         |

### Cider Audio (CiderAudio)

| Function/Method | Usage | Details |
| --------------- | ----- | ------- |
|                 |       |         |
|                 |       |         |
|                 |       |         |
