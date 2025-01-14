---
description: >-
  This page contains documentation on the functions included in the
  CiderFrontAPI.
---

# Frontend API

<details>

<summary>Renderer Helpers</summary>

* `CiderFrontAPI.*`

<!---->

* `AddMenuEntry(entry: CiderFrontAPI.Objects.MenuEntry)` - Add an entry to the Cider menu
* `StyleSheets`
  * Add(href: string) - Load a `.less` stylesheet from a URL

</details>

<details>

<summary>Registering a Vue component as a page</summary>

Registering a Vue component is done by adding `plugin.` to the front of the component name. Pages can then be loaded with `app.appRoute("plugin/<component name without plugin.>")`

</details>

<details>

<summary>Accessing static resources from the renderer</summary>

Additional resources in the plugins such as images and other files can be accessed with methods like `fetch()` from `./plugins/:packageName/:file` this resolves to `http://localhost:{port}/plugins/:packageName/:file`

`:packageName` refers to the `name` property in package.json for the plugin.

</details>

<details>

<summary>Importing Custom Stylesheets</summary>

Example:

`CiderFrontAPI.StyleSheets.Add("./plugins/:packageName/mystylesheet.less")`

`:packageName` refers to the `name` property in package.json for the plugin.

</details>

<details>

<summary>CiderAudio</summary>

**Note: CiderAudio requires Advanced Audio Functionality to be enabled in the app settings.**

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

#### audio.js explained

https://github.com/ciderapp/Cider/blob/develop/src/renderer/audio/audio.js

CiderAudio initializes with `CiderAudio.hierarchical_loading()` Inside the loading process, all audioNodes are cleared and re-initialized and chained based on what the user has enabled. The designed hierarchy for loading audio functions is as follows:

* `h1 item` - AudioBand (final output)
* `h2 item 1` - AudioBands vibrantbass\_h2\_1() (vibrant bass node)
* `h2 item 2` - llpw\_h2\_2() (CiderAudio.audioNodes.llpw)
* `h2 item 3` - analogWarmth\_h2\_3() (CiderAudio.audioNodes.analogWarmth)
* Spatial Node is always the last node in the chain

</details>
