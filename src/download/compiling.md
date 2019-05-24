# Compile Veloren

Veloren can be compiled under Windows, MacOS and Linux.
Install the programs described in [Toolchain](toolchain.md).
The following commands needs to be executed in Bash. If you run Windows, get familiar with `git bash`.
Open git bash in the location you want to store Veloren (around 100 MB needed).
If you are having issues, take a look at the Troubleshooting section.

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

## Compiling server and client

You can use the following command to build the server and flag in release mode, you can omit that flag, to increase compilation speed and enable debug mode, but reduce performance of the game a bit.

```bash
cargo build --release --bin veloren-server-cli && cargo build --release --bin voxygen
```

## Troubleshooting

### Git LFS

To check if Git LFS works correctly:
```
git lfs status
```


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

### Nightly Rust

Veloren depends on the nightly toolchain of Rust. To switch to it for this project only:
```bash
rustup override set nightly
```
