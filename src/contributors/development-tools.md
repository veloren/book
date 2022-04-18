# Installation

If you want to contribute to Veloren in any form you probably need to deal with Veloren's [_source code_](https://en.wikipedia.org/wiki/source_code). Therefore these basic tools have to be installed to interact with it.<br/>

_**Note:** Throughout the book we will mention alot of commands. Therefore we highly recommend getting comfortable with a [terminal]()._

## Git

_Keeping track of Veloren's history_

For **Windows**, The ['Git for Windows'](https://gitforwindows.org/) suite is a sensible way to install Git, along with a set of tools that'll make it easier for you to use.

On **Linux** Git is most likely already installed, if it isn't, use your distribution's package manager to install it.

On recent **MacOS** versions you will be prompted to install Git the first time you run it. Otherwise install it using [Homebrew](https://github.com/homebrew/brew) via `brew install git` or [MacPorts](https://www.macports.org/) via `port install git`.

## Git LFS

_Keeping track of the really big giants out there (aka. asset files)_

[Git LFS](https://github.com/git-lfs/git-lfs/releases) is a Git extension used to store large files like images and audio files. You need to install it in order to download the assets.

1. For **Windows** you can download an installer [here](https://github.com/git-lfs/git-lfs/releases).

    On **Linux** you can use the package manager to install Git LFS, usually the package is called `git-lfs`.

    On **MacOS** you can use [Homebrew](https://github.com/homebrew/brew) via `brew install git-lfs` or [MacPorts](https://www.macports.org/) via `port install git-lfs`.

2. Git LFS needs to be set up by running `git lfs install` or `git-lfs install` (macOS) in a terminal.

**Note:** _git-lfs has a known bug with working off remotes. If you plan to work off a fork, [refer to this section](before-you-contribute.html#forking)._

## Rust

_Keeping us safe and sound to build a reliable and efficient game_

[Rust](https://rust-lang.org) is a general-purpose programming language we use. Refer to the [FAQ](faq.md) section to learn why.

The recommended way of installing Rust is through [Rustup](https://rustup.rs). Follow the instructions carefully and everything should be good.
