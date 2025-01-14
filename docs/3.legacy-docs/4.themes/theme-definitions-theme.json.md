# Theme definitions (theme.json)

`theme.json` files require the following properties:

* `name: string` - The name of the theme
* `description: string` - Brief description of the theme
* `version: string` - Version of the theme
* `author: string` - Theme authors
* `github_repo: string` - The source repository of the theme, this is required for Cider to automatically update the theme. Formatted `<owner>/<repo_name>`
* `pack: array` - (optional) Declare individual LESS files as styles within the package
  * Pack Object Format:
    * `name: string` - Name of the style
    * `file: string` - File name within the package / repo
    * `description: string` - Description of the style
