---
title: "Richer Cider - Discord Plugin"
description: "This website contains all the resources required to compile, create plugins and theme Cider!"
navigation:
  title: "Richer Cider - Discord Plugin"
  icon: ""
draft: "false"
---

# Richer Cider Installation and Setup

### Step 1:

Download & Install NodeJS & NPM at https://nodejs.org

### Step 2:

Download & Install Git at https://git-scm.com

### Step 3:

Install `pnpm` using the following command

```bash
npm install --global pnpm
```

### Step 3:

Open up command prompt and use the following command to clone vencord

```bash
git clone https://github.com/Vendicated/Vencord
```

### Step 4:

Create a file called `richerCider.desktop.tsx` in the `src/plugins` folder (Git created a folder called `Vencord` in wherever your terminal was (make sure it's not in system32)).

<details>
<summary>
Copy and Paste this code into the file.
</summary>
<p>

```tsx
import { Link } from "@components/Link";
import definePlugin from "@utils/types";
import { Forms } from "@webpack/common";
const appIds = [
  "911790844204437504",
  "886578863147192350",
  "1020414178047041627",
  "1032800329332445255",
];
export default definePlugin({
  name: "richerCider",
  description:
    'Enhances Cider (More details in info button) by adding the "Listening to" type prefix to the user\'s rich presence when an applicable ID is found.',
  authors: [
    {
      id: 191621342473224192n,
      name: "cryptofyre",
    },
  ],
  patches: [
    {
      find: '.displayName="LocalActivityStore"',
      replacement: {
        match: /LOCAL_ACTIVITY_UPDATE:function\((\i)\)\{/,
        replace: "$&$self.patchActivity($1.activity);",
      },
    },
  ],
  settingsAboutComponent: () => (
    <>
      <Forms.FormTitle tag="h3">
        Install Cider to use this Plugin
      </Forms.FormTitle>
      <Forms.FormText>
        <Link href="https://cider.sh">Follow the link to our website</Link> to
        get Cider up and running, and then enable the plugin.
      </Forms.FormText>
      <br></br>
      <Forms.FormTitle tag="h3">What is Cider?</Forms.FormTitle>
      <Forms.FormText>
        Cider is an open-source and community oriented Apple Music client for
        Windows, macOS, and Linux.
      </Forms.FormText>
      <br></br>
      <Forms.FormTitle tag="h3">Recommended Optional Plugins</Forms.FormTitle>
      <Forms.FormText>
        I'd recommend using TimeBarAllActivities alongside this plugin to give
        off a much better visual to the eye (Keep in mind this only affects your
        client and will not show for other users)
      </Forms.FormText>
    </>
  ),
  patchActivity(activity: any) {
    if (appIds.includes(activity.application_id)) {
      activity.type = 2; /* LISTENING type */
    }
  },
});
```

</p>
</details>

### Step 5: Move the terminal.

```bash
cd Vencord
```

### Step 6: Install Depenencies

```bash
pnpm install
```

### Step 7: Build with the plugin

```bash
pnpm build
```

### Step 8: Open the Vencord Injector.

<Callout type="warning" emoji="️⚠️">
  Discord needs to be closed before you do this
</Callout>
```bash
pnpm inject
```

### Step 9: Using the GUI

Patch Discord

### Step 10: In Vencord Settings:

Enable the `richerCider` plugin

### Step 11: Profit

<Callout type="error" emoji="⚠️">
  You're no longer allowed to update Vencord, though in most cases Discord updates should be ok, if not just go back to Step 8
</Callout>
