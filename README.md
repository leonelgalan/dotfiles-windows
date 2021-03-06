﻿# Leonel's dotfiles for Windows

A collection of PowerShell files for Windows, including common application installation through `Chocolatey` and `npm`, and developer-minded Windows configuration defaults. 

Completely based in Jay Harris's own _dotfiles-windows_.

## Installation

### Using Git and the bootstrap script

You can clone the repository wherever you want. (I like to keep it in `~\Projects\dotfiles-windows`.) The bootstrapper script will copy the files to your PowerShell Profile folder.

From PowerShell:
```posh
git clone https://github.com/leonelgalan/dotfiles-windows.git; cd dotfiles-windows; . .\bootstrap.ps1
```

To update your settings, `cd` into your local `dotfiles-windows` repository within PowerShell and then:

```posh
. .\bootstrap.ps1
```

Note: You must have your execution policy set to unrestricted (or at least in bypass) for this to work: `Set-ExecutionPolicy Unrestricted`.

### Git-free install

> **Note:** You must have your execution policy set to unrestricted (or at least in bypass) for this to work. To set this, run `Set-ExecutionPolicy Unrestricted` from a PowerShell running as Administrator.

To install these dotfiles from PowerShell without Git:

```bash
iex ((new-object net.webclient).DownloadString('https://raw.github.com/leonelgalan/dotfiles-windows/master/setup/install.ps1'))
```

To update later on, just run that command again.

### Add custom commands without creating a new fork

If `.\extra.ps1` exists, it will be sourced along with the other files. You can use this to add a few custom commands without the need to fork this entire repository, or to add commands you don't want to commit to a public repository.

My `.\extra.ps1` looks something like this:

```posh
# Git credentials
# Not in the repository, to prevent people from accidentally committing under my name
Set-Environment "GIT_AUTHOR_NAME" "Leonel Galan"
Set-Environment "GIT_COMMITTER_NAME" $env:GIT_AUTHOR_NAME
git config --global user.name $env:GIT_AUTHOR_NAME
Set-Environment "GIT_AUTHOR_EMAIL" "leonelgalan@gmail.com"
Set-Environment "GIT_COMMITTER_EMAIL" $env:GIT_AUTHOR_EMAIL
git config --global user.email $env:GIT_AUTHOR_EMAIL

Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
```

Extras is designed to augment the existing settings and configuration. You could also use `./extra.ps1` to override settings, functions and aliases from my dotfiles repository, but it is probably better to [fork this repository](#forking-your-own-version).

### Sensible Windows defaults

When setting up a new Windows PC, you may want to set some Windows defaults and features, such as showing hidden files in Windows Explorer. This will also set your machine name and full user name, so you may want to modify this file before executing.

```post
.\windows.ps1
```

### Install dependencies and packages

When setting up a new Windows box, you may want to install some common packages, utilities, and dependencies. These could include node.js, [Chocolatey](http://chocolatey.org/) packages, Windows Features and Tools via [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx), and Visual Studio Extensions from the [Visual Studio Gallery](http://visualstudiogallery.msdn.microsoft.com/).

```posh
.\deps.ps1
```

> The scripts will install Chocolatey, node.js, ruby and python if necessary.

> **Visual Studio Extensions**  
> Extensions will be installed into your most current version of Visual Studio. You can also install additional plugins at any time via `Install-VSExtension $url`. The Url can be found on the gallery; it's the extension's `Download` link url.


## Forking your own version

If you do fork for your own custom configuration, you will need to touch a few files to reference your own repository, instead of mine.

Within `/setup/install.ps1`, modify the Repository variables.
```posh
$account = "leonelgalan"
$repo    = "dotfiles-windows"
$branch  = "master"
```

Within the Windows Defaults file, `/windows.ps1`, modify the Machine
name on the first line.
```posh
(Get-WmiObject Win32_ComputerSystem).Rename("MyMachineName") | Out-Null
```

Finally, be sure to reference your own repository in the git-free installation command.
```bash
iex ((new-object net.webclient).DownloadString('https://raw.github.com/$account/$repo/$branch/setup/install.ps1'))
```

## Feedback

Suggestions/improvements are
[welcome and encouraged](https://github.com/leonelgalan/dotfiles-windows/issues)!

## Original Author

| [![twitter/leonelgalan]https://s.gravatar.com/avatar/fd50f61387b63900335c8556f86237be?s=70)](http://twitter.com/leonelgalan "Follow @leonelgalan on Twitter") |
|---|
| [Leonel Galan](http://twitter.com/leonelgalan/) |

## Thanks to…

* [jayharris](http://twitter.com/jayharris/) for his [dotfiles-windows](https://github.com/jayharris/dotfiles-windows) which this repository is forked after.
* @[Mathias Bynens](http://mathiasbynens.be/) for his [OS X dotfiles](http://mths.be/dotfiles), which this repository is modeled after.
