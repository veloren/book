# Running Veloren

Veloren is a cross-platform game and can run on Windows, Linux and Mac OS.

If you're only interested in binary builds of the game, check the website at [www.veloren.net](https://www.veloren.net).

# Building Veloren

Building Veloren can be done relatively easily thanks to Cargo, Rust's build and dependency manager.
This tutorial assumes that you have both Git and Rust installed on your system.

## Clone the repository

```
git clone https://gitlab.com/veloren/veloren.git && cd veloren
```

## Set up asset repositories

```
git submodule update --init --recursive
```

## Build and run Voxygen

```
cd voxygen/
cargo run --release
```

If you want to debug crashes that occur, run the following instead.

```
RUST_BACKTRACE=1 cargo run --release
```

If you are on a Windows system, you may need to use `set RUST_BACKTRACE 1` beforehand instead.
