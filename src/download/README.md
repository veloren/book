# Download

Read this chapter for a detailed description on how to run Veloren and to avoid common pitfalls.

## Download

- **[Windows](https://download.veloren.net/latest/windows)**
- **[Linux](https://download.veloren.net/latest/linux)** or check [the packaging section](#packaging-status)
- **[Airshipper](https://www.songtronix.com)** (Launcher)
- **MacOS**: You can run the Windows version using [WINE](https://www.winehq.org/) or [compile a native version](/compile/index.md) yourself

## Stable

If you want to download a stable release (e.g. 0.3, 0.4) you can visit our [website](https://www.veloren.net/welcome).

*Note: Due to rapid development stable releases are out of date pretty fast.*

## Runtime dependencies

These are programs needed for Veloren to run on your device. Refer to [Compile](/compile/index.md) section for build-time dependencies.

On **Linux** you need to have GTK3 installed.

On **Debian** systems additional libraries may need to be downloaded, below is a non-exhaustive list:

- libglib2.0-dev
- libcairo2-dev
- libasound2-dev
- libpango1.0-dev
- libatk1.0-dev
- libgdk-pixbuf2.0-dev
- libgtk-3-dev

And a one liner to download and install them all:
`sudo apt-get install libglib2.0-dev libcairo2-dev libasound2-dev libpango1.0-dev libatk1.0-dev libgdk-pixbuf2.0-dev libgtk-3-dev`

### Packaging status

#### Fedora

[COPR repo](https://copr.fedorainfracloud.org/coprs/atim/veloren/): `sudo dnf copr enable atim/veloren -y && sudo dnf install veloren -y`

#### Arch

[AUR latest binary release](https://aur.archlinux.org/packages/veloren-bin/): `yay -Sy veloren-bin`

[AUR latest release](https://aur.archlinux.org/packages/veloren/): `yay -Sy veloren`

[AUR latest master](https://aur.archlinux.org/packages/veloren-git): `yay -Sy veloren-git`