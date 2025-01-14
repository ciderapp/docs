# Creating a Theme

If one does not already exist, create a new theme directory in the user data folder.

* **Windows:** `%appdata%/Cider/themes`
* **Mac:** `~/Library/Application Support/Cider/themes`
* **Linux:** `~/.config/Cider/themes`

Create a new folder in the themes directory with the name of your theme.

* This folder needs to contain the following files:
  * `index.less` - The main theme file
  * `theme.json` - Contains several properties for your theme
* You can clone a starter template from here: [Theme Starter Template](https://github.com/ciderapp/CiderThemeTemplate)

In Cider, select the theme in the settings.

Cider has automatic hot reloading for themes in the userdata folder.

### Useful Resources

* The default styles.less can be found in: [src/renderer/style.less](https://github.com/ciderapp/Cider/tree/main/src/renderer/style.less)
* [Less.js documentation](https://lesscss.org/)
