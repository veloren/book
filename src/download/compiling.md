# Compile Veloren

Veloren can be compiled under Windows, MacOS and Linux.
Install the programs described in [Toolchain](toolchain.md).
The following commands needs to be executed in Bash. If you run Windows, get familiar with `git bash`.
Open git bash in the location you want to store Veloren (around 100 MB needed).

## Download source code

Clone the repository
```bash
git clone https://gitlab.com/veloren/veloren.git
```

Change your working directory to the cloned repository
```
cd veloren
```

All of the following commands should be executed from the root directory of the project (usually called `veloren/`).

Next, check if Git LFS works correctly:
```
git lfs status
```

## Nightly Rust

Veloren depends on the nightly toolchain of Rust. To switch to it for this project only:
```bash
rustup override set nightly
```

## Start the game

This will start the actual game.
You can connect to other servers or start a singleplayer server using the GUI.
```bash
cargo run --bin veloren-voxygen
```

You can append `--release` to allow more optimizations at the cost of longer compile times.

## Start a dedicated server

If you want to host your own server, run:
```bash
cargo run --release --bin veloren-server-cli
```

This will open a server listening on `0.0.0.0:59003`. At the time of writing this section there is no way to change it without modifying the source code.

## Debugging

You can prepend `VELOREN_LOG=info` to a `cargo` command to give more details during runtime and `RUST_BACKTRACE=1` to give more details after crashes.

For example, to start the server with more debug information, run this:
```bash
VELOREN_LOG=info RUST_BACKTRACE=1 cargo run --release --bin veloren-server-cli
```

## Troubleshooting

### Git LFS

When using Mingw64, it does not download the files properly. The main issue seems to be that the askpass program is not spawned when using a normal CMD prompt, preventing Git LFS from authenticating via SSH to retrieve the temporary access token. Setting the SSH_ASKPASS, GIT_ASKPASS and DISPLAY variables seems to solve this issue:

```
C:\src>SET "SSH_ASKPASS=C:\Program Files\Git\mingw64\libexec\git-core\git-gui--askpass"
C:\src>SET "GIT_ASKPASS=%SSH_ASKPASS%"
C:\src>SET "DISPLAY=required"
```

If you used the previous submodules system, you can deactivate it with:
```
git submodule deinit --force --all
```
