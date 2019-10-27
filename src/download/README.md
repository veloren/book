# Download

Read this chapter for a detailed description on how to run Veloren and to avoid common pitfalls.

We provide pre-compiled versions of the game for Windows and Linux on <https://www.veloren.net/welcome>. You can run the Windows version on MacOS using [WINE](https://www.winehq.org/) or [compile a native version](/compile/index.md) yourself.

## Runtime dependencies

These are programs needed for Veloren to run on your device. Refer to [Compile](/compile/index.md) section for build-time dependencies.

On **Linux** you need to have GTK3 installed.

## Nightly

Currently we provide 64-bit developement builds for Linux and Windows:

**Windows**: https://www.airshipper.songtronix.com/latest/windows  
**Linux**: https://www.airshipper.songtronix.com/latest/linux

Download the version for your operating system and extract it, then open the `veloren-voxygen.exe` (Windows and WINE) or `veloren-voxygen` (Linux) file.

*Note: MacOS and 32-bit systems are supported but you need to [compile the game for them yourself](/compile/index.html). Additionally, you can run the Windows version on MacOS using [WINE](https://www.winehq.org/)*

## Releases

Due to rapid developement stable versions become outdated fast and might be **incompatible with the public server**. You can find them on [our website](https://www.veloren.net/welcome) or install one of the release packages listed below.

### Packaging status

#### Fedora

[COPR repo](https://copr.fedorainfracloud.org/coprs/atim/veloren/): `sudo dnf copr enable atim/veloren -y && sudo dnf install veloren -y`

#### Arch

[AUR latest binary release](https://aur.archlinux.org/packages/veloren-bin/): `yay -Sy veloren-bin`

[AUR latest release](https://aur.archlinux.org/packages/veloren/): `yay -Sy veloren`

[AUR latest master](https://aur.archlinux.org/packages/veloren-git): `yay -Sy veloren-git`
