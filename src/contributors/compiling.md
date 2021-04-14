# Compiling Veloren

This section covers building Veloren from rust source with `cargo` and running it.

**Note**: _all commands need to be run from the repository._

## Required Libraries

On **Windows** you will need [Visual Studio Build Tools](https://visualstudio.microsoft.com/de/downloads/).

**Note**: _Install "C++ tools" and "Windows 10 SDK", you won't need to install Visual Studio itself so scroll down and open "Tools for Visual Studio \<year\>" to find the latest buildtools._

On **Linux** you need to have `GTK3` installed.

On **Debian** systems additional libraries may need to be downloaded, below is a non-exhaustive list:

- libglib2.0-dev
- libcairo2-dev
- libasound2-dev
- libpango1.0-dev
- libatk1.0-dev
- libgdk-pixbuf2.0-dev
- libgtk-3-dev
- libxcb-shape0-dev
- libxcb-xfixes0-dev
- libudev-dev
- libxkbcommon-x11-dev
- libxcb-xkb-dev

And a one liner to download and install them all:<br/>
`sudo apt install libglib2.0-dev libasound2-dev libcairo2-dev libpango1.0-dev libatk1.0-dev libgtk-3-dev libxcb-shape0-dev libxcb-xfixes0-dev libudev-dev libxkbcommon-x11-dev libxcb-xkb-dev`

On **Fedora** you can follow this [awesome guide](https://kwiecien.us/building-veloren-on-fedora.html).

**Note**: _Feel free to open an issue incase these dependencies are incorrect._

## Compile and Run Veloren

Run this in a terminal to compile and run Veloren:

```bash
cargo run
```

To compile without running, use `cargo build` instead.

**Note**: _The initial compilation will take from 5min up to 30min therefore grab a tea and some snacks and come back later._

## Compile and Run Veloren Server

```bash
cargo run --bin veloren-server-cli
```

## Logging output

We use [`tracing`](https://crates.io/crates/tracing) to collect logs. They can be filtered by setting the `RUST_LOG` environment variable to the respective level (`error`, `warn`, `info`, `debug`, `trace`).

For all available filtering options visit [the docs](https://docs.rs/tracing-subscriber/0.2.7/tracing_subscriber/filter/struct.EnvFilter.html#examples).

**Tip**: _this works both for the server and client_

## Optimized Release builds

By default debug builds are created which compile faster but run a bit slower than optimized release builds. Unlike many other projects, we've set them up so they're fast enough to be playable. If you want to get optimized builds, add the `--release` flag when calling `cargo`. Keep in mind that compiling release might be very slow!

If you want get familiar with cargo we recommend the [Cargo Book](https://doc.rust-lang.org/cargo/).
