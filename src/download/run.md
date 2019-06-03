# Run Veloren

After you downloaded Veloren and installed all dependencies, you want to run it.
This are the official recommendations how to run it. At the end we explain why we choose certain options.

## Windows

0. In case you are unfamiliar with some points, please google before asking us, they are already well described on the internet.
1. If you come from windows the first step is to open a CMD
2. Change the directory to the Veloren directory, e.g. `C:\Users\Jennifer\Downloads\veloren>`
3. You need to start the server first, because the client needs it to connect to:
```bash
RUST_LOG=info RUST_BACKTRACE=1 .\target\debug\veloren-server-cli.exe
```
This will open a server listening on `0.0.0.0:59003`. At the time of writing this section there is no way to change it without modifying the source code.
4. Open a second CMD and change to the Veloren directory like in step 1) and 2)
5. Keep the server open and start the client in the second CMD:
```bash
RUST_LOG=info RUST_BACKTRACE=1 .\target\debug\veloren-voxygen.exe
```
6. If you encounter problems check Troubleshooting at the end of this page and if you wont find a solution create a bug according to [Report Bugs](../contribute/bug.md)

## Linux/MacOS

1. start a terminal
2. `cd` in the Veloren directory.
3. You need to start the server first, because the client needs it to connect to:
```bash
RUST_LOG=info RUST_BACKTRACE=1 ./target/debug/veloren-server-cli
```
This will open a server listening on `0.0.0.0:59003`. At the time of writing this section there is no way to change it without modifying the source code.
4. start a second terminal and `cd` to the Veloren directory like in step 1) and 2)
5. Keep the server open and start the client in the second terminal:
```bash
RUST_LOG=info RUST_BACKTRACE=1 ./target/debug/veloren-voxygen
```
6. If you encounter problems check Troubleshooting at the end of this page and if you wont find a solution create a bug according to [Report Bugs](../contribute/bug.md)

## Additional info

### Single-player mode
with the introduction of single-player mode it's no longer necessary to start the server-cli in a separate window, just start veloren-voxygen and press single-player.

### RUST_LOG=info
This environment parameter changes the logging behavior of Veloren. You can assign every component a different value, and depending on the value more or less logs are written.
E.g. `RUST_LOG=info,common=debug,common::net=warning`
Provide the logs to a developer in case you encounter a bug.
Keep in mind that the level `debug` might produce a big log and slows the game down a bit, other levels have no negative side effect on the game, we recommend to always have at least `info` enabled to be able to report bug repots.

### RUST_BACKTRACE=1
This environment parameter switches on backtraces, in case Veloren crashes, it's requiered in case you want to report a bug to the developers, it has no negative side effect, so we recommend to have it enabled all the time.

### Compile and Run
If you compile rust from source via [Compiling from Source](./compiling.md), you can use the command `cargo run --bin veloren-server-cli` or `cargo run --bin veloren-voxygen` to recompile and run server and client. This can be combined with the above environment parameters

## Troubleshooting

- empty so far
