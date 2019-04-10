# Getting Started

Veloren is written in the Rust programming language and is maintained using Git, the industry standard version control system.

## Why Rust?

Rust is a new programming language designed to be fast, safe, and well-suited to concurrent programming. We believe that these attributes make it ideal for game design. As a result, the Veloren engine is extremely quick, very rugged (you'll be hard-pressed to find unintentional crashes or bugs in the codebase), and also multi-threaded (meaning it can take advantage of multi-core CPU architectures).

## Why Git?

Git is an industry standard version control system. It is uses to keep track of different versions of a codebase, and maintains a history of a codebase that can be viewed throughout time. It also makes contributing to the project much easier, since it helps to manage the merging and updating of the codebases maintained by each contributor.

# Installing things

To get started working on Veloren, you'll need to install a few things.

## Rust

Rust can be easily installed on all major desktop operating systems. Follow this link for installation instructions specific to your system.

[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)

## Git

There are many ways to install Git. For those running Linux, your system probably has Git already installed or available to install with your chosen package manager.

For Windows, The ['Git for Windows'](https://gitforwindows.org/) suite is a sensible way to install Git, along with a set of tools that'll make it easier for you to use.

*For Mac OS, there exists other methods. I personally have not used Mac OS, so you'll likely have a better time finding instructions just by googling 'Install Git on Mac OS'. If someone wants to contribute appropriate instructions to this page, please do.*

# GitLab and forking Veloren

By now, you should have both Rust and Git installed.

The following assumes you're using bash shell (on Windows git bash) or a similar one.

## Forking the project

To work on Veloren, you first need to create your own fork of the codebase on gitlab. To do that, login or register on gitlab, and head to the main gitlab page of repository you want to fork (for example https://gitlab.com/veloren/book). Next click the fork button. You may be taken to a page asking to select namespace you wish to fork the project to, just choose your account. You will get redirected to the page of the forked repository

## Local repository setup

### For just compiling/trying it out

1. Clone the repository locally: `git clone https://gitlab.com/veloren/veloren.git`
2. Change your working directory to the cloned repository: `cd fresh`
3. Initialize and download the submodules: `git submodule update --init --recursive`

### For contributing

1. Clone your fork of the repository locally: `git clone <clone url of your fork>`  
· If you already cloned the main repository instead, then change the `origin` remote fetch address:  
`git remote set-url origin <clone url of your fork>`
2. Change your working directory to the cloned repository: `cd veloren`
3. Add `upstream` remote: `git remote add upstream https://gitlab.com/veloren/veloren.git`

## Compiling and running the client

1. Change working directory to `$repo/voxygen` where `$repo` is the path to the repository
2. To compile and run the client with compiler optimizations enabled: `cargo run --release`

## Compiling and running the server

1. Change working directory to `$repo/server-cli` where `$repo` is the path to the repository
2. To compile and run the server with compiler optimizations enabled: `cargo run --release`  
This will open a server listening on `0.0.0.0:59003` address. At the time of writing this section there is no way to change it without modifying the source code.
