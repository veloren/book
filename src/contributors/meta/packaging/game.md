# Packaging the standalone game

The preferred method for shipping Veloren is now [Airshipper](https://gitlab.com/veloren/airshipper), but here is information about packaging the standalone game.

> **Note:**  
> This document is focused mainly on packaging Veloren for Linux, but some information will also be helpful for other platforms.

## General information

Please refer to [this guide](https://book.veloren.net/contributors/introduction.html) for the general setup and compilation instructions.

> **Tip:**  
> As additional reference, see the [veloren-git AUR package](https://aur.archlinux.org/packages/veloren-git), more specifically [the PKGBUILD file](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=veloren-git).  
> It should always have an up-to-date buildtime and runtime dependency list.

## Rust version and Rustup

The specific version of Nightly Rust a given version of Veloren is intended to be compiled with is specified in the `rust-toolchain` file.
If you use rustup, it will install and use the right version automatically. Otherwise you need to make sure you use the correct one yourself.
Veloren will fail to compile on Stable Rust, and we **do not** support compiling it with Rust versions other than the one specified in the `rust-toolchain` file.

## Compile-time options

- It is recommended that you use the `--release` flag so that the resulting binaries are fully optimized.
- In order for the game to use standard (XDG-compliant) directories to save user data instead of trying to save it next to the executable, you need to set the `VELOREN_USERDATA_STRATEGY` environment variable to `system`.
- To compile specific binaries, you need to pass `--bin <NAME>` arguments.

The resulting command to compile the game server and client using the above settings would be:  
`VELOREN_USERDATA_STRATEGY='system' cargo build --release --bin veloren-voxygen --bin veloren-server-cli`  
In this case the resulting binaries will be `target/release/veloren-voxygen` and `target/release/veloren-server-cli`.  

## Other files

- You need to include the assets for the game to run. The expected location for them is `/usr/share/veloren/assets`.
- In the assets folder, we provide a `.desktop`<sup>[[spec]](https://specifications.freedesktop.org/desktop-entry-spec/latest/)</sup> file, an icon and a `.metainfo.xml`<sup>[[spec]](https://www.freedesktop.org/software/appstream/docs/sect-Metadata-Application.html)</sup> file. You should place them as follows:
    - `assets/voxygen/net.veloren.veloren.png` -> `/usr/share/pixmaps/net.veloren.veloren.png`
    - `assets/voxygen/net.veloren.veloren.desktop` -> `/usr/share/applications/net.veloren.veloren.desktop`
    - `assets/voxygen/net.veloren.veloren.metainfo.xml` -> `/usr/share/metainfo/net.veloren.veloren.metainfo.xml`
