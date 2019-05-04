# Compile Veloren

Veloren can be compiled under Windows, MacOS and Linux.
Install the programs described in [Toolchain](../contr/toolchain.md).
The following commands needs to be executed in Bash. If you run Windows, get familiar with `git bash`.
Open git bash in the location you want to store Veloren (around 100 MB needed).

## Download source code
```bash
#1 Clone the repository locally
git clone https://gitlab.com/veloren/veloren.git
#2 Change your working directory to the cloned repository
cd veloren
#3 Initialize and download the assets from LFS
git lfs install
git lfs checkout
```

If you are having issues with Git LFS, take a look at the troubleshooting section.

All of the following commands should be executed from the root directory of the project (usually called `veloren/`).

## Nightly Rust

Veloren depends on the nightly toolchain of Rust. To switch to it for this project only:
```bash
rustup override set nightly
```

## Start the server

You need to start the server first, because the client needs it to connect to.
```bash
cargo run --release --bin veloren-server-cli
```

This will open a server listening on `0.0.0.0:59003`. At the time of writing this section there is no way to change it without modifying the source code.

## Start the client

Keep the server open and start the client in a separate window:
```bash
cargo run --release --bin veloren-voxygen
```

## Debugging

You can prepend `RUST_LOG=info` to a command to give more details during runtime and `RUST_BACKTRACE=1` to give more details during crashes.

For example, to start the server with more debug information, run this:
```bash
RUST_LOG=info RUST_BACKTRACE=1 cargo run --release --bin veloren-server-cli
```

## Troubleshooting

### Git LFS

When using Mingw64, it not download the files properly. The main issue seems to be that the askpass program is not spawned when using a normal CMD prompt, preventing Git LFS from authenticating via SSH to retrieve the temporary access token. Setting the SSH_ASKPASS, GIT_ASKPASS and DISPLAY variables seems to solve this issue:

```
C:\src>SET "SSH_ASKPASS=C:\Program Files\Git\mingw64\libexec\git-core\git-gui--askpass"
C:\src>SET "GIT_ASKPASS=%SSH_ASKPASS%"
C:\src>SET "DISPLAY=required"
```

If you used the previous submodules system, you can deactivate it with:

```
git submodule deinit --force --all
```
