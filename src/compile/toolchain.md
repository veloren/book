# Installing tools

This section describes which tools you need to install on your system to compile Veloren from source.

# Rust

Rust can be easily installed on all major desktop operating systems. Follow this link for installation instructions specific to your system.

<https://www.rust-lang.org/tools/install>

Because Veloren uses the nightly version of Rust, please make sure you install it:
```
rustup toolchain install nightly
```

We have a [toolchain file](https://github.com/rust-lang/rustup.rs#the-toolchain-file) in the repository so you only need to have rust nightly installed and it will be chosen automatically.

# Git

On **Linux** Git is most likely already installed, if it isn't, use your distribution's package manager to install it.

For **Windows**, The ['Git for Windows'](https://gitforwindows.org/) suite is a sensible way to install Git, along with a set of tools that'll make it easier for you to use.

On recent **MacOS** versions you will be prompted to install Git the first time you run it. Otherwise install it using [Homebrew](https://github.com/Homebrew/brew) via `brew install git` or [MacPorts](https://www.macports.org/) via `port install git`.


## Git LFS
Git LFS is a Git extension used to store large files like images and audio files. You need to install it in order to download the assets.

On **Linux** you can use the package manager to install Git LFS, usually the package is called `git-lfs`.

For **Windows** you can download an installer [here](https://github.com/git-lfs/git-lfs/releases).

On **MacOS** you can use [Homebrew](https://github.com/Homebrew/brew) via `brew install git-lfs` or [MacPorts](https://www.macports.org/) via `port install git-lfs`.

On all platforms, after installation the setup needs to be completed:
```
git lfs install
```

# Bash
All commands for compiling Veloren yourself are written for bash, if you run un windows use the `git bash` included in the git package.

After you installed everything, continue with [local repository setup](./repo.md)
