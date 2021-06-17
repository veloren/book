# Building the Veloren Server for Raspberry Pi

The model of Raspberry Pi you have and the operating system your Pi is running can significantly impact your installation steps and Veloren's performance on your Pi. For the best performance we recommend using the Raspberry Pi model 4 and a 64-bit OS like [Ubuntu Server](https://ubuntu.com/download/raspberry-pi), which is available through the [Raspberry Pi Imaging utility](https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility/). There is a [64-bit beta of Raspberry Pi OS](https://www.raspberrypi.org/forums/viewtopic.php?t=275370) as well.

**Note**: _The amount of RAM on the Pi 4 does not matter. Even the official Veloren server uses well under 2GB of memory most of the time._
## Cross-compiling or not

Cross-compilation means setting up a toolchain for the Raspberry Pi's instruction set on a separate computer in order to compile the Veloren server binary which you then copy onto the Pi.
<br/>

Direct compiling is preferred if:
* You don't want to install and set up as many things on your computer
* You want to be up and running in fewer steps

Cross compiling is preferred if:
* You have a computer setup for development
* You want the compilation step to be faster

**Note**: _Even with cross-compilation it is necessary to clone the `assets` folder from the code repository onto the Pi as these files are not compiled into the server binary._ 

## Direct Compiling

Log in to your Pi using ssh.
<br/>
`ssh <username>@<ip>` and enter password 
Install the [Rust programming language](https://www.rust-lang.org/tools/install) on the Pi if it's not already installed.
<br/>
```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Install Git LFS in order to download the audio and visual assets along with the source code.
<br/>
```shell
sudo apt install git-lfs
```
Git clone the [Veloren codebase](https://gitlab.com/veloren/veloren). You may need to [generate SSH keys](https://docs.gitlab.com/ee/ssh/README.html#generating-a-new-ssh-key-pair) on your Pi for your gitlab account.
<br/>
```shell
git clone https://gitlab.com/veloren/veloren.git
```
Compile the server binary from the code in the Veloren directory.
<br/>
```shell
cd veloren
cargo build --bin veloren-server-cli --release
```
Run the server binary, optionally with `-h` or `--help` to see the list of arguments you can supply.
<br/>
```shell
./target/release/veloren-server-cli
```

**Note**: _Compilation on a Raspberry Pi 4 running Ubuntu Server 64-bit can take around 30 minutes for an optimized build._
<br/>
**Note**: _Remember to replace \<username\> by your own username and \<ip\> by the ip address of your Raspberry Pi!_
<br/>
**Note**: _The process itself is resource heavy. Maybe still consider cross compiling. RAM usage can go over 8G, so you may consider creating a swap (although swap slows down the entire compilation process)_


## Cross Compiling

### Installing Dependencies

Install the following dependencies on the cross compiling machine and the Raspberry Pi:

Cross Compiling PC:

- git
- git-lfs
- cargo (which is installed along with Rust)
- [docker](https://www.docker.com/products/docker-desktop)

Raspberry Pi:

- git
- git-lfs


### Preparing the Raspberry Pi

First we need to clone the Veloren git repository.

```shell
git clone https://gitlab.com/veloren/veloren
```

Next we can reset the repository to the state of the last stable release. To do that we have to find out the git hash of that version. This can be found on [https://gitlab.com/veloren/veloren/-/releases](https://gitlab.com/veloren/veloren/-/releases). The git hash is the sequence in the bottom left corner of the release. This step can be skipped if you want to play with the very latest updates.

```shell
cd veloren
git checkout <git hash>
```

Next we have to create some folders to later put the binary in.

```shell
mkdir target
mkdir target/release
```


Next, we need to add an environment variable to our `.profile`.

```shell
nano ~/.profile
```
In the last line of this file, add the line `export VELOREN_USERDATA="$(pwd)/userdata`

Lastly, we reload our environment to use the new variable

```shell
. ~/.profile
``` 

### Cross Compiling the code

Again we have to clone the Veloren repository to our cross compiling machine, reset it to the state of the latest stable release and setup git-lfs.

```shell
git clone https://gitlab.com/veloren/veloren
cd veloren
git checkout <git hash>
git lfs install
cargo install cross
```

The install command will be different depending on which OS you have running on the Raspberry Pi.
<br/>
If you are using a 64-bit OS like Ubuntu Server with an ARMv8 instruction set, run the command:
```shell
cross build --target aarch64-unknown-linux-gnu --bin veloren-server-cli --release
```
If you are using Raspberry Pi OS which is currently 32-bit and using ARMv7 instruction set for backwards compatibility reasons, run the command:
```shell
cross build --target armv7-unknown-linux-gnueabihf --bin veloren-server-cli --release
```
**Note**: _You may need to register an account on [docker hub](https://hub.docker.com/) and run the `docker login` command in the terminal to access the docker image required for cross-compilation._

When the compilation process has finished, we can move the binary to the Raspberry Pi. If you have ssh enabled on your Raspberry Pi, you can use the `scp` command.

```shell
scp target/<instruction set>/release/veloren-server-cli <username>@<ip>:~/veloren/target/release/veloren-server-cli
```

**Note**: _`<instruction set>` refers to either `aarch64-unknown-linux-gnu` or `armv7-unknown-linux-gnueabihf`, whichever one you used to compile. Remember to replace \<username\> by your own username and \<ip\> by the ip address of your Raspberry Pi!_

## Creating a systemd service

On the Raspberry Pi we can now create a systemd service for the server. To do that, create a service file with the content below.

```shell
sudo nano /etc/systemd/system/veloren-server.service
```

**Note**: _If you cross-compiled the binary, add an environment variable to the `Service` section: `Environment="VELOREN_USERDATA=/home/veloren/target/release/userdata"`_

```
[Unit]
Description=Veloren Server
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
User=<username>
WorkingDirectory=/home/<username>/veloren
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

In case you want to start the server everytime the Raspberry Pi boots, you can enable the service.

```shell
sudo systemctl enable veloren-server.service
```

## Monitoring the server
When the server is running, you can watch your Pi's performance with tools like `htop` or set up a [Prometheus server](https://leanpub.com/rpcmonitor/read) to scrape metrics from your Veloren server at the address`http://<ip>:14005/metrics`.
