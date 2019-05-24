# Installing tools

This chapter describes which tools you need to install on your system to compile Veloren from source.

## Rust

Rust can be easily installed on all major desktop operating systems. Follow this link for installation instructions specific to your system.

<https://www.rust-lang.org/tools/install>

Because Veloren uses the nightly version of Rust, please make sure you install it.

<https://github.com/rust-lang/rustup.rs#working-with-nightly-rust>

## Git

There are many ways to install Git. For those running Linux, your system probably has Git already installed or available to install with your chosen package manager.

For Windows, The ['Git for Windows'](https://gitforwindows.org/) suite is a sensible way to install Git, along with a set of tools that'll make it easier for you to use.

*For Mac OS, there exists other methods. I personally have not used Mac OS, so you'll likely have a better time finding instructions just by searching for 'Install Git on Mac OS'. If someone wants to contribute appropriate instructions to this page, please do.*

### Git LFS
You also need to make sure you have Git LFS installed. It's needed to store large files like images and audio files.
Without Git Lfs you can't run the game

## Bash
All commands for compiling Veloren yourself are written for bash, if you run un windows use the `git bash` included in the git package.

After you installed everything, continue with [Compiling from Source](./compiling.md)
