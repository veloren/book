# Compiling Veloren
This section covers building Veloren from source and running it.  
Reminder that **all commands** need to be run from the repo directory.

## Compile-time dependencies

On Linux, you might need to install the following dependencies:

- build-essential
- libudev-dev
- libxcb-shape0-dev
- libxcb-xfixes0-dev

And a one liner to download and install them all (apt based systems):

`sudo apt-get install build-essential libudev-dev libxcb-shape0-dev libxcb-xfixes0-dev`

## Compiling

To compile and run the client
```
cargo run
```

To compile and run standalone server
```
cargo run --bin veloren-server-cli
```

To compile without running, use `cargo build` instead.

## Optimized Release builds

By default debug builds are created which compile faster but run a bit slower than optimized release builds. 
Unlike many other projects, we've set them up so they're fast enough to be playable. 
If you want to get optimized builds, add the `--release` flag when calling `cargo`. 
Keep in mind that compiling Release might be very slow!
