### Backend Development

<details>
<summary markdown="span">PluginEnv</summary>

When plugins are loaded in Cider the `constructor()` in the plugin class is passed a `PluginEnv` object, this object contains:
* `app` - The Electron app
* `store` - Electron Store
* `utils` - Cider utils
* `win` - The renderer window
* `dir` - Path to the plugin directory
* `dirName` - Plugin directory name

</details>

<details>
<summary markdown="span">Load a front end plugin</summary>

To load a front end plugin (typically named `index.frontend.js`) from `index.js`
`PluginEnv.utils.loadJSFrontend(path: string)` is used.

Example: `PluginEnv.utils.loadJSFrontend(path.join(PluginEnv.dir, "index.frontend.js"))`

</details>

<details>
<summary markdown="span">utils</summary>

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
<summary markdown="span">Built in events</summary>

Cider plugins support these methods by default, however more can be made with the use of ipcMain and ipcRenderer

* `onReady(win)` - (Required) Executes when the back end is ready
* `onRendererReady()` - Executes when the renderer has finished loading (app.init())
* `onPlaybackStateDidChange(attributes)` - Executes when playback state changes, passes song attributes
* `onNowPlayingItemDidChange(attributes)` - Executes when song changes, passes song attributes
* `onBeforeQuit` - Executes before Cider quits

</details>

### Frontend Development

<details>
<summary markdown="span">Renderer Helpers</summary>

* `CiderFrontAPI.*`
<details>
<summary>Objects</summary>

* `MenuEntry`
    * `id` - Entry ID for querying
    * `name` - The entry text
    * `onClick` - On click event
</details>

* `AddMenuEntry(entry: CiderFrontAPI.Objects.MenuEntry)` - Add an entry to the Cider menu
* `StyleSheets`
    - Add(href: string) - Load a `.less` stylesheet from a URL

</details>

<details>
<summary markdown="span">Registering a Vue component as a page</summary>

Registering a Vue component is done by adding `plugin.` to the front of the component name.
Pages can then be loaded with `app.appRoute("plugin/<component name without plugin.>")`

</details>

<details>
<summary markdown="span">Accessing static resources from the renderer</summary>

Additional resources in the plugins such as images and other files can be accessed with methods like `fetch()` from `./plugins/:packageName/:file` this resolves to `http://localhost:{port}/plugins/:packageName/:file`

`:packageName` refers to the `name` property in package.json for the plugin.

</details>


<details>
<summary markdown="span">Importing Custom Styhesheets</summary>

Example:

`CiderFrontAPI.StyleSheets.Add("./plugins/:packageName/mystylesheet.less")`

`:packageName` refers to the `name` property in package.json for the plugin.

</details>


<details>
<summary>CiderAudio</summary>

__Note: CiderAudio requires Advanced Audio Functionality to be enabled in the app settings.__

Cider features a custom audio stack, available in the renderer.


* `CiderAudio.context` - Primary AudioContext
* `CiderAudio.source` - Audio Source

CiderAudio contains the following nodes:
* `CiderAudio.audioNodes.gainNode` - Main gain node
* `CiderAudio.audioNodes.spatialNode` - Used by audio spatialization
* `CiderAudio.audioNodes.audioBands` - Used by EQ
* `CiderAudio.audioNodes.vibrantbassNode` - Used to deliver vibrant bass functionality
* `CiderAudio.audioNodes.llpw` - Used by Cider Adrenaline Processor (CAP)
* `CiderAudio.audioNodes.analogWarmth` - Used by Analog Warmth

### audio.js explained
https://github.com/ciderapp/Cider/blob/develop/src/renderer/audio/audio.js

CiderAudio initializes with `CiderAudio.hierarchical_loading()`
Inside the loading process, all audioNodes are cleared and re-initialized and chained based on what the user has enabled.
The designed hierarchy for loading audio functions is as follows:

* `h1 item` - AudioBand (final output)
* `h2 item 1` - AudioBands vibrantbass_h2_1() (vibrant bass node)
* `h2 item 2` - llpw_h2_2() (CiderAudio.audioNodes.llpw)
* `h2 item 3` - analogWarmth_h2_3() (CiderAudio.audioNodes.analogWarmth)
* Spatial Node is always the last node in the chain

</details>

### Publishing to GitHub
Once you have completed your plugin its time to publish!
Create a new repository for the plugin and upload the files.

To have the theme indexed into Cider's built in plugin explorer, add `cidermusicplugin` as a topic on the repository.

Plugins from GitHub in Cider will display the repos README.md file within the Explore Plugins on GitHub page, so be sure to include some screenshots showing off your plugins.

## Resources
[Example Plugin](https://github.com/ciderapp/plugin-schema-poc/tree/main/v2_plugin)

[General Electron Documentation](https://www.electronjs.org/docs/latest/api/app)

[BrowserWindow](https://www.electronjs.org/docs/latest/api/browser-window)

[IPC Main](https://www.electronjs.org/docs/latest/api/ipc-main)

[IPC Renderer](https://www.electronjs.org/docs/latest/api/ipc-renderer)
