---
description: >-
  This page allows you to figure out the steps and programs needed to compile
  your own version of Cider.
---

# Compiling on macOS

## Getting Started

Recommended / Required Development Utilities

* [NodeJS 14.0.0 or greater](https://nodejs.org/)
* [pnpm](https://pnpm.io/) (_Optional, but highly recommended_)
* [Git](https://git-scm.com)
* [Python 3.8 or greater](https://www.python.org/downloads/)
* [Xcode 11+](https://developer.apple.com/xcode/\))
* Have an Apple Developer Account and be a member of the [Apple Developer Program](https://developer.apple.com/support/compare-memberships/). This is necessary to play music through the app.
* Basic Command Line Knowledge

::alert{type="warning"}
While not required, PNPM is **recommended** for compiling Cider, and you can install it by using:

`npm install -g pnpm`
::

::alert{type="caution"}
To remind you again, if you **don't** have an Apple Developer account to sign the Cider binary after building, it **WILL NOT** work.
::

### Cloning the repository

Open a command prompt window in the directory you'd like Git to clone to and enter the following command

```
git clone https://github.com/ciderapp/Cider.git
```

**Optionally**, if you'd like to use the **Development** branch of Cider to test upcoming features switch your branch by moving your terminal into the directory and using git to checkout the branch by entering the following commands

```
cd Cider/
git checkout develop
```

::alert{type="tip"}
If you'd like to update your repository in the future to keep up to date, use the command _(Make sure you're in the directory, you originally cloned in)_

`git pull`
::

### Installing Dependencies

Now for the fun part, by using `pnpm`, `npm` or `yarn` (we'll be using `pnpm` in this case) enter the following command to automatically obtain all required dependencies for installation.

{% tabs %}
{% tab title="pnpm" %}
```
pnpm install
```
{% endtab %}

{% tab title="npm" %}
```
npm install --force
```
{% endtab %}

{% tab title="yarn" %}
```
yarn install
```
{% endtab %}
{% endtabs %}

::alert{type="note"}
This step could take a little while on some machines.
::

### Create an account to VMP-sign Cider.

What is this for? MacOS doesn't like development Widevine DRM keys for some reason. Therefore, we need to sign our own production keys here. This can be done as follows:

```
python3 -m pip install --upgrade castlabs-evs
python3 -m castlabs_evs.account signup
Signing up for castLabs EVS
 - A valid e-mail address is required for account verification
>> E-mail Address []: me@example.com
>> First Name []: Me
>> Last Name []: Example
>> Organization []: Example, Inc
>> Account Name []: example
>> Password []: XXXXXXXX
>> Verify Password []: XXXXXXXX
Confirming EVS account
 - A confirmation code has been sent to your e-mail address
>> Confirmation Code []: XXXXXX
Discarding authorization token(s)
Refreshing authorization token(s)
```

Remember your account name and password because you will need it later.

Once in a while, you may need to re-authenticate the VMP account. If that is the case:

```
python3 -m castlabs_evs.account reauth
Discarding authorization token(s)
Refreshing authorization token(s)
>> Account Name [example]: 
>> Password []: XXXXXXXX
```

### Create Apple signing keys and app-specific password.

1. In Xcode: Under `Xcode > Preferences (⌘,) > Accounts`, you may add your Apple ID. With your team selected, the View Details... in the bottom right could find you the available certificates for generation/download.
2. After that, select all of the certificates in Keychain Access to generate as a .p12 file. Remember the file location and the .p12 password.
3. [Generate](https://support.apple.com/en-us/HT204397) the app-specific password of your Apple Developer account

### Setting up environment variables.

```
export CSC_LINK= <location to the p12 certificate>
export CSC_KEY_PASSWORD= <p12 certificate password>
export APPLEID= <your Apple Developer email address>
export APPLEIDPASS= <your Apple Developer app-specific password>
```

You can set the environment variables permanently by edit the `~/.bash-profile` file and add the above lines at the bottom of the file.

```
~/.bash-profile
```

### Final fixes

Electron-Packager doesn't like MacOS notarization. You need to manually patch the files in order for it to work properly:

```
cp resources/verror-types node_modules/@types/verror/index.d.ts
cp resources/macPackager.js node_modules/app-builder-lib/out/macPackager.js 
```

### Compiling Cider

This step takes a little while on the first compilation so bear with it as it does what it needs to do.

This will generate a universal signed and notarized binary. (Don't mind the "not working" command line, it works)

{% tabs %}
{% tab title="pnpm" %}
```
pnpm dist:universalNotWorking -p never
```
{% endtab %}

{% tab title="npm" %}
```
npm run dist:universalNotWorking -p never
```
{% endtab %}

{% tab title="yarn" %}
```
yarn dist:universalNotWorking -p never
```
{% endtab %}
{% endtabs %}

::alert{type="warning"}
On some low-end machines this process could take up to \~20-30 minutes. (It will look like it hangs at the notarization part, don't exit it).
::

### Installing Cider

Your new Cider installation setup file is ready for you! You can find your setup executable in your cloned folder directory on your system in the subfolder `dist/` and from there you'll see your new Setup file.

::alert{type="note" title="Success"}
Congrats! You've successfully compiled your own build of Cider!
::