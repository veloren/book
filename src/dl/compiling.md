# Compile Veloren

Veloren can be compiled under Windows, MacOS and Linux.
Install the programs described in [Toolchain](../contr/toolchain.md).
The following commands needs to be executed in bash, if you run windows get familar with `git bash`.
Open the git bash in the location you want to store veloren (around 100 MB needed).

## Download Source code
```bash
#1 Clone the repository locally
git clone https://gitlab.com/veloren/veloren.git
#2 Change your working directory to the cloned repository
export repo="$(pwd)/veloren"
cd ${repo}
#3 Initialize and download the submodules for assets
git submodule update --init --recursive
```

in this book we always refer to `${repo}` as the root directory of the veloren source code.
Every code snipped will include a `cd` command to hint from which directory it must be run, if you run it from another directory weird errors might appear.

## Compile Veloren

```bash
cd "${repo}"
#1 Compile the server with cargo
cargo build
```

## Run the Server

You need to run the server first, because the client needs it to connect to.
```bash
cd "${repo}/server-cli"
#1 (Compile) and run the server with cargo
RUST_LOG=info RUST_BACKTRACE=1 cargo run
```

This will open a server listening on `0.0.0.0:59003` address. At the time of writing this section there is no way to change it without modifying the source code.
We decided to include `RUST_LOG` into the command to give more details during runtime and `RUST_BACKTRACE` to give more details during crashes.
Thats also why we removed the `--release` for now, in case of a crash we have more information.

## Run the client

Keep the server open and run the client in a seperate window:
```bash
cd "${repo}/voxygen"
#1 (Compile) and run the server with cargo
RUST_LOG=info RUST_BACKTRACE=1 cargo run
```
