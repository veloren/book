# Installation

If you want to contribute to Veloren in any form you probably need to deal with Veloren's [_source code_][1]. Therefore these basic tools have to be installed to interact with it.<br/>

## Git

_Keeping track of Veloren's history_

On **Linux** Git is most likely already installed, if it isn't, use your distribution's package manager to install it.

For **Windows**, The ['Git for Windows'][2] suite is a sensible way to install Git, along with a set of tools that'll make it easier for you to use.

On recent **MacOS** versions you will be prompted to install Git the first time you run it. Otherwise install it using [Homebrew][3] via `brew install git` or [MacPorts][4] via `port install git`.

## Git LFS

_Keeping track of the really big giants out there (aka. asset files)_

Git LFS is a Git extension used to store large files like images and audio files. You need to install it in order to download the assets.

1. On **Linux** you can use the package manager to install Git LFS, usually the package is called `git-lfs`.<br/>
   For **Windows** you can download an installer [here][5].<br/>
   On **MacOS** you can use [Homebrew][3] via `brew install git-lfs` or [MacPorts][4] via `port install git-lfs`.

2. Git LFS needs to be set up by running `git lfs install` or `git-lfs install` (macOS) in a terminal.

_**Note**: Throughout the book we will mention alot of commands. Therefore we highly recommend getting comfortable with one._

[1]: https://en.wikipedia.org/wiki/Source_code
[2]: https://gitforwindows.org/
[3]: https://github.com/Homebrew/brew
[4]: https://www.macports.org/
[5]: https://github.com/git-lfs/git-lfs/releases
