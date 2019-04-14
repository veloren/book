# Compile Veloren

Veloren can be compiled under Windows, MacOS and Linux.
Install the programs described in [Toolchain](../contr/toolchain.md).
The following commands needs to be executed in Bash. If you run Windows, get familar with `git bash`.
Open git bash in the location you want to store Veloren (around 100 MB needed).

## Download Source code
```bash
#1 Clone the repository locally
git clone https://gitlab.com/veloren/veloren.git
#2 Change your working directory to the cloned repository
cd veloren
#3 Initialize and download the submodules for assets
git submodule update --init --recursive
```

All of the following commands should be executed from the root directory of the project (usually called "veloren").

## Run the server

You need to start the server first, because the client needs it to connect to.
```bash
cargo run --release --bin veloren-server-cli
```

This will open a server listening on `0.0.0.0:59003`. At the time of writing this section there is no way to change it without modifying the source code.
We decided to include `RUST_LOG` into the command to give more details during runtime and `RUST_BACKTRACE` to give more details during crashes.

## Run the client

Keep the server open and run the client in a seperate window:
```bash
cargo run --release --bin veloren-voxygen
```

## Debugging

You can prepend `RUST_LOG=info` to a command to give more details during runtime and `RUST_BACKTRACE=true` to give more details during crashes.

For example, to start the server with more debug information, run this:
```bash
RUST_LOG=info RUST_BACKTRACE=1 cargo run --release --bin veloren-server-cli
```
