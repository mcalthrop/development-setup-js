# development-setup-js

Useful setup instructions forJavascript projects, whether client- or server-side.

> These installation instructions assume you are using macOS. Instructions for other operating systems will vary.

## xcode

Ensure you've got [Xcode installed](https://itunes.apple.com/us/app/xcode/id497799835) – this will enable you to use `git`.

You may have to agree to the OS/X license terms:

- Run from the command line: `xcode-select --install`
- Choose `install tools` from the prompt and `agree` to the terms
- If you receive a message saying "Can't install the software because it is not currently available from the Software Update server"... it's probably because the command line tools are already installed...
- Agree to the license by typing `sudo xcodebuild -license`
- Press enter, then `q`
- Then on the next prompt, type `agree`


## Brew

There are lots of useful utilities available for installation with `brew`.

Install it from here: [brew.sh](http://brew.sh/#install)

## Git

Best use the `brew` version of `git` &ndash; makes it easier to update than the version shipped with xcode:

``` sh
$ brew install git
```

Ensure you're not using the OS/X version of `git`:

``` sh
$ which git
/usr/local/bin/git      # should NOT be /usr/bin/git
$ git --version
git version 2.10.0
```

Configure your name and email address for commits (be sure to use the email address you have registered with gitlab):

``` sh
$ git config --global user.name "Your Name"
$ git config --global user.email "your.name@example.com"
```

And here's a useful start for a `.gitignore` file: [`.gitignore`](.gitignore).

## Linting

### Javascript

On a large project, I usually prefer to use [Airbnb's eslint configuration](https://www.npmjs.com/package/eslint-config-airbnb) as a base, and modify a few of the rules.

However, a more simple approach is to extend the `eslint:recommended` set of rules: [`.eslintrc`](.eslintrc).

## Atom

There are lots of editors you can use; here are instructions for setting up Atom:

1. Download [atom](https://atom.io/), and copy it into your `Applications` folder.

2. If there is no file called `/usr/local/bin/atom`, run this command in your terminal: `sudo ln -s /Applications/Atom.app/Contents/Resources/app/atom.sh /usr/local/bin/atom`
> This will allow you to run `atom` from the terminal.

3. Open Atom, open Preferences (`cmd-,`), click on the _Install_ tab and install the following packages:
  - `atom-ternjs`
  - `color-picker`
  - `emmet`
  - `file-icons`
  - `linter`
  - `linter-ui-default`
  - `linter-eslint`
  - `linter-tslint`
  - `linter-htmlhint`
  - `linter-js-yaml`
  - `linter-sass-lint`
  - `eslint-plugin-html`
  - `open-in-browser`

4. In the _Editor_ panel, make the following changes:
  - **Invisibles** > **Scroll past end** – _check_
  - **Show Indent Guide** – _check_
  - **Show Line Numbers** – _check_
  - **Soft Tabs** – _check_
  - **Tab Type** > _soft_ – must do this – otherwise Atom will insert tab characters

## Zsh

If you already like using `bash`, you'll appreciate using `zsh`.

- Type `brew install zsh`. Type `0` if the prompt ask you about `.zshrc`.
- Type `which zsh` to determine where your new shell has installed.
- Edit `/etc/shells` and add `/usr/local/bin/zsh`
- Type `sudo chsh -s /usr/local/bin/zsh`, then open a new terminal tab – `zsh` will now be the shell running.

## Oh My ZSH

[oh-my-zsh](http://ohmyz.sh/) makes `zsh` even better – check out the [wiki page](https://github.com/robbyrussell/oh-my-zsh/wiki).

Scroll down on the page above for installation instructions.

**Note:** you may want to move the `/usr/local/bin` path to the beginning of your `PATH` definition in your `.zshrc` file:

``` sh
export PATH=/usr/local/bin:$HOME/bin:$PATH
```

Then open a new tab in your terminal app to see the changes.

## Nvm

`nvm` allows you to easily select which version of `node` to use.

Installation instructions are here:

[github.com/creationix/nvm/blob/master/README.markdown](https://github.com/creationix/nvm/blob/master/README.markdown#install-script)

Once installed, have a look at the [`package.json`](../package.json) file, and check the value of the `"node"` property within the `"engines"` object. Use this value to set your `node` version. For example:

``` sh
$ nvm install 6.8.0 && nvm use 6.8.0
```

And to verify that the above process completed correctly, the following command should show the `node` version you selected:

``` sh
$ node --version
```

You should also run this command [to avoid updating the default alias along with node version updates later on](http://stackoverflow.com/a/31859164):

``` sh
$ nvm alias default node
```

## Yarn

Use [`yarn`](https://yarnpkg.com/) instead of `npm` (see [Facebook's post](https://code.facebook.com/posts/1840075619545360) for a description).

Install the CLI like this:

[https://yarnpkg.com/lang/en/docs/install/#mac-tab](https://yarnpkg.com/lang/en/docs/install/#mac-tab)

## Mongo

Install it with `brew`:

``` sh
$ brew install mongodb
```

Run the following command to ensure you have a place for mongo to store the data for your databases:

``` sh
$ [[ ! -d /data/db ]] && sudo mkdir -p /data/db && sudo chown -R $(whoami) /data/db || ls -la /data
```

If everything is fine, the above command should result in something like this:

```
total 0
drwxr-xr-x   3 root       wheel   102 Nov 11 13:06 .
drwxr-xr-x  38 root       wheel  1360 Nov 11 13:06 ..
drwxr-xr-x   8 yourusername  wheel   272 Nov 11 13:10 db
```

