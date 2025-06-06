# Compiling Veloren

This section covers building Veloren from rust source with `cargo` and running it.

**Note:** _all commands need to be run from the repository._

## Required Libraries

On **Windows** you will need to install the following programs:

* [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)
* [CMake](https://cmake.org/download/#latest)
* [Ninja build system](https://github.com/ninja-build/ninja/releases)
* [Python 3](https://www.python.org/downloads/windows/)

Fortunately, there is a **quick way to install** most of these

1. Download and run the Visual Studio Build Tools and install:
   * C++ tools.
   * Windows 10 SDK.
2. Open a PowerShell terminal and run the following commands:

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
    scoop install cmake ninja python
    ```

    The first two lines install the Scoop package manager and
    the third line installs CMake, Ninja and Python through Scoop in one go.

On **Linux** you will need to have installed GTK3, Python and CMake.

On **Gentoo** you may require having to enable certain use flags for specific packages.

* sys-devel/binutils (with the `gold` use flag to enable the ld.gold linker)
* media-libs/mesa (with the `vulkan`use flag)

On **Debian** systems additional libraries may need to be downloaded, below is a non-exhaustive list:

* g++
* libglib2.0-dev
* libcairo2-dev
* libasound2-dev
* libpango1.0-dev
* libatk1.0-dev
* libgdk-pixbuf2.0-dev
* libgtk-3-dev
* libxcb-shape0-dev
* libxcb-xfixes0-dev
* libudev-dev
* libxkbcommon-x11-dev
* libxcb-xkb-dev

And a one liner to download and install them all:<br/>
`sudo apt install g++ libglib2.0-dev libasound2-dev libcairo2-dev libpango1.0-dev libatk1.0-dev libgtk-3-dev libxcb-shape0-dev libxcb-xfixes0-dev libudev-dev libxkbcommon-x11-dev libxcb-xkb-dev`

On **Fedora** systems additional libraries may need to be downloaded, below is a command to install them:<br/>
`sudo dnf install gcc gcc-c++ binutils-gold cmake alsa-lib-devel libxkbcommon-x11-devel libudev-devel`

On **openSUSE Tumbleweed** systems, additional dependencies may be needed:<br/>
`sudo zypper in binutils-gold alsa-devel systemd-devel libxkbcommon-devel libxkbcommon-x11-devel`

On **macOS** you only need to install cmake.  
This can be done using either **homebrew** or **macports**.
Using homebrew, enter `brew install cmake` or similarly, using macports enter `sudo port install cmake`.  
**Note**: Do not use sudo with homebrew.

**Note:** _Feel free to open an issue incase these dependencies are incorrect._

## Compile and Run Veloren

Run this in a terminal to compile and run Veloren:

```bash
cargo run
```

To compile without running, use `cargo build` instead.

**Note:** _The initial compilation will take from 5min up to 30min therefore grab a tea and some snacks and come back later._

## Compile and Run Veloren Server

```bash
cargo run --bin veloren-server-cli
```

## Logging output

We use [`tracing`](https://crates.io/crates/tracing) to collect logs. They can be filtered by setting the `RUST_LOG` environment variable to the respective level (`error`, `warn`, `info`, `debug`, `trace`).

For all available filtering options visit [the docs](https://docs.rs/tracing-subscriber/0.2.7/tracing_subscriber/filter/struct.EnvFilter.html#examples).

**Tip:** _this works both for the server and client_

## Optimized Release builds

By default debug builds are created which compile faster but run a bit slower than optimized release builds. Unlike many other projects, we've set them up so they're fast enough to be playable. If you want to get optimized builds, add the `--release` flag when calling `cargo`. Keep in mind that compiling release might be very slow!

If you want get familiar with cargo we recommend the [Cargo Book](https://doc.rust-lang.org/cargo/).
