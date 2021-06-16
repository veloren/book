# Cross-Compiling Veloren

As more and more people want to play or develop for Veloren on other platforms, it may come as no surprise that building *on* these platforms might not be the most elegant solution, emulation is quite often slow, and the platform of choice simply doesn't have the necessary resources to build the game in a reasonable amount of time. 

**Please note:** *Documentation of these steps is currently underway, you might need to adjust these for your specific scenario.*

## Linux

### Prerequisites
In order to build for your platform of choice, for example `arm64`, you'll need to install the compiler toolchain for that architecture. In our case, that's `aarch64-linux-gnu-gcc`.

You'll also need the compilation dependencies of the project installed for your architecture. In our example, we used a Raspberry Pi to install all dependencies needed for compiling the project, then the SD Card was plugged into the building system, and it's root filesystem was mounted under `/mnt`.

### Cross-Compiling
The project source tree was cloned to our building machine, in an arbitrary location. Open a terminal and move to the project root, then execute: 

`rustup target add [target]`

where `[target]` is one of the targets from [here](https://doc.rust-lang.org/nightly/rustc/platform-support.html). In our case, that was `aarch64-unknown-linux-gnu`.
After this, you'll need to go in the newly created `.cargo` directory and edit the `config` file. Add the following entry:

```
[target.X]
linker="Y"
```

where `X` was `aarch64-unknown-linux-gnu` in our case, and `Y` was `aarch64-linux-gnu-gcc` respectively. These should correspond with the target mentioned above, and the compiler toolchain respectively (the one you installed as a prerequisite).

For the compilation itself, you'll need to tell Cargo where the correct libraries are. Given that we've mounted the root filesystem of our target at `/mnt`, we can use the `PKG_CONFIG_SYSROOT_DIR` environment variable.

The compilation command looks like this:
```
PKG_CONFIG_SYSROOT_DIR=Z cargo build --release --target X
```
where `X` is the target we're building for, and `Z` is the filesystem root of the platform we're building for. This is where the Raspberry Pi's SD Card was mounted, in our case `/mnt`.

Feel free to adjust the command for your needs, as per the original compilation instructions. You should find the built binaries in the `target` subfolder of the project root.

#### Note

At the time of writing, there is an issue with the `keyboard-keynames` library for `aarch64` and probably others too. Assuming `~/.cargo` is the default location of your Cargo downloads, edit the file located at: `~/.cargo/git/checkouts/keyboard-keynames-0b8339ee617b0344/a97ae50/src/platform/unix/key_layout.rs` and replace all instances of

```
unsafe { &*(utf_key as *const [i8] as *const [u8]) }
```
with
```
unsafe { &*(utf_key as *const [c_char] as *const [u8]) }
```
after which compilation should succeed.
