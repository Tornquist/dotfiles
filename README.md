# dotfiles

A collection of dotfiles and config files that can be installed using rake.
Light and dark mode themes are also included that can be manually used with
their associated tools.

## Setup

### Install/Uninstall

Run `rake install` to install zsh, oh-my-zsh and symlink all the config files.

Run `rake uninstall` to remove the symlinks.

### Homebrew

Run `rake brew` to install homebrew and a collection of base packages.

### MySQL

Run `rake mysql` in trigger `rake brew` and then install and force link mysql 5.7

### Node

Run `rake node` to install `nvm`. The environment configuration is included in the
dotfiles by default, but will only be used when `nvm` is installed.

After installing any changes made by the install script should be verified. In general,
the changes should match configuration already present (what ships be default).

### Ruby

Run `rake ruby` to install `chruby` and `ruby-install` after an auto-triggered
`rake brew`. Like Node/nvm, the chruby configuration is included in the dotfiles
by default, but no ruby versions will be installed by default.

To install the latest stable, use `ruby-install ruby`. Please note,
`ruby-install ruby` without additional flags will leave a `src/` folder in the
home directory.

Following installation, it is recommended to add `chruby X.X.X` to `~/.localrc`
to use the newly installed non-system ruby by default.

## Light/Dark Mode

Includes themes for light and dark mode in iTerm, Sequel Ace (pro), and for the
system wallpaper.

### iTerm 2

1. Import the themes in iTerm with: `Preferences > Profiles > Colors > Color Presets > Import`
1. Move the auto launch script with `rake iterm`
1. Active the script in iTerm with: `Scripts > AutoLaunch > switch_automatic.py`
    * A prompt will appear for the iTerm python runtime. This must be installed.

### macOS

1. Open Automator
1. Create a new application titled `Toggle Light or Dark mode`
1. Drag out `Change System Appearance` from the Library (Default is toggle)
1. Save
1. Open spotlight and start to type `Toggle...`. Select the automation
1. Grant privileges to the automation to control the system

--> The automation can now be used. `cmd+space + "tog" + enter to cycle`

### Sequel Ace

Themes must be manually installed and are for the query editor only.
Autoswitching is not supported, but the application automatically switches
the rest of the interface.

### Xcode

1. Install Xcode
1. Run `rake xcode` to copy the themes to the user folder
1. Set the system to dark mode.
1. Manually select the `DuskDark` theme
1. Set the system to light mode.
1. Manually select the `DuskLight` theme.

### Other Programs

* **Atom**: Autoswitch using the `mojave-dark-mode` plugin
* **TextMate**: Twilight (Dark) vs. IDLE (Light)
