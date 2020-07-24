# Building the Veloren Server for Raspberry Pi

**Note**: _This was only tested on pre-alpha version 0.6.0_

## Installing Dependencies

Install the following dependencies on the cross compiling machine and the raspberry pi:

Cross Compiling PC:

- git
- git-lfs
- arm-linux-gnueabihf-glibc

Raspberry Pi:

- git
- git-lfs

## Checking Compatibility

To check if your glibc is compatible with your Raspberry Pi, run these commands in the terminal:

Cross Compiling PC:

```shell
arm-linux-gnueabihf-ld --version
```

Raspberry Pi:

```shell
ld --version
```

The version number in the first line of the output on the raspberry pi has to be greater than or equal to the one on your cross compiling machine. If the version number is smaller, you need to take a different pc with a lower glibc version as cross compiling machine, update your os on the raspberry pi, or if your raspberry pi is already up to date, change the os of the raspberry pi to one with a greater glibc version.

## Preparing the Raspberry Pi

First we need to clone the Veloren git repository.

```shell
git clone https://gitlab.com/veloren/veloren
```

Next we need to reset the repository to the state of the last stable release, to do that we have to find out the git hash of that version. This can be found on [https://gitlab.com/veloren/veloren/-/releases](https://gitlab.com/veloren/veloren/-/releases). The git hash is the sequence in the bottom left corner of the release.

```shell
cd veloren
git checkout <git hash>
```

Now we have to setup git-lfs for the cloned repository.

```shell
git lfs install
```

Lastly we have to create some folders to later put the binary in.

```shell
mkdir target
mkdir target/release
```

## Cross Compiling the code

Again we have to clone the Veloren repository to our cross compiling machine, reset it to the state of the latest stable release and setup git-lfs.

```shell
git clone https://gitlab.com/veloren/veloren
cd veloren
git checkout <git hash>
git lfs install
```

Now we need to set the appropriate linker for the ARM architecture of the raspberry pi.

```shell
printf '\n[target.armv7-unknown-linux-gnueabihf]\nlinker = "arm-linux-gnueabihf-gcc"' >> .cargo/config
```

<br/>

---

**Note**: _If you want to compile for version 0.6.0, you have to manually fix one little bug that sneaked in the stable release._

```shell
nano common/src/util/mod.rs
```

In line 8 change the underlined 1 to a 0

```rust,ignore
pub static ref GIT_DATE: &'static str = GIT_VERSION.split("/").nth(1).expect("failed to retrieve git_date!");
/*                                                                 ¯                                       */
```

---

<br/>

In the next step we will install the rust ARM target.

```shell
rustup target add armv7-unknown-linux-gnueabihf
```

Now we compile the Veloren server.

```shell
cargo build --target armv7-unknown-linux-gnueabihf --bin veloren-server-cli --release
```

When the compilation process has finished, we can move the binary to the raspberry pi. If you have ssh enabled on your raspberry pi, you can use the scp command.

**Note**: _Remember to replace \<username\> by your own username and \<ip\> by the ip address of your raspberry pi!_

```shell
scp target/armv7-unknown-linux-gnueabihf/release/veloren-server-cli <username>@<ip>:~/veloren/target/release/veloren-server-cli
```

## Creating a systemd service

Back on the raspberry pi we can now create a systemd service for the server. To do that, create a service file with the content below.

```shell
sudo nano /etc/systemd/system/veloren-server.service
```

**Note**: _Remember to replace \<username\> by your own username!_

```
[Unit]
Description=Veloren Server
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
User=<username>
WorkingDirectory=/home/<username>/veloren/target/release/
ExecStart=/home/<username>/veloren/target/release/./veloren-server-cli

[Install]
WantedBy=multi-user.target
```

Now our service is ready and can be started.

```shell
sudo systemctl start veloren-server.service
```

To watch how the server starts and to see debug info, you can use the following command.

```shell
sudo journalctl -f -u veloren-server.service
```

In case you want to start the server everytime the raspberry pi boots, you can enable the service.

```shell
sudo systemctl enable veloren-server.service
```
