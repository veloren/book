# Download

For most download options visit our [website][1].<br/>
If you are a linux user you probably want to use the packaged versions available below.

_Note: Due to rapid development stable releases are out of date pretty fast._

### Packaging status

#### Flatpak

`flatpak install flathub net.veloren.veloren`

#### Snap

`sudo snap install veloren --edge`

#### Arch

[AUR latest binary release][3]: `yay -Sy veloren-bin`

[AUR latest release][4]: `yay -Sy veloren`

[AUR latest master][5]: `yay -Sy veloren-git`

#### Fedora

[COPR repo][2]: `sudo dnf copr enable atim/veloren -y && sudo dnf install veloren -y`

## Runtime dependencies

These are programs needed for Veloren to run on your device. Refer to [Developer][6] section for build-time dependencies.

On **Linux** you need to have GTK3 installed.

On **Debian** systems additional libraries may need to be downloaded, below is a non-exhaustive list:

- libglib2.0-dev
- libcairo2-dev
- libasound2-dev
- libpango1.0-dev
- libatk1.0-dev
- libgdk-pixbuf2.0-dev
- libgtk-3-dev

And a one liner to download and install them all:<br/>
`sudo apt-get install libglib2.0-dev libcairo2-dev libasound2-dev libpango1.0-dev libatk1.0-dev libgdk-pixbuf2.0-dev libgtk-3-dev`

[1]: https://www.veloren.net/download
[2]: https://copr.fedorainfracloud.org/coprs/atim/veloren/
[3]: https://aur.archlinux.org/packages/veloren-bin/
[4]: https://aur.archlinux.org/packages/veloren/
[5]: https://aur.archlinux.org/packages/veloren-git
[6]: /contributors/developers
