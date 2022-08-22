# Airshipper

![Airshipper](https://songtronix.com/airshipper-0.4.0.gif)

Airshipper is a cross-platform Veloren launcher taking care of keeping Veloren up to date.
Due to our frequent updates it is the recommended way of installing Veloren.

### Download

Visit the [download page](https://veloren.net/download/) to download Airshipper.

### Files

Airshipper stores its files in the following directories depending on your operating system:

|       OS        |                        Path                         |
| :-------------: | :-------------------------------------------------: |
|     Windows     |               `%appdata%/airshipper`                |
|      Linux      |            `~/.local/share/airshipper`              |
| Linux (Flatpak) | `~/.var/app/net.veloren.airshipper/data/airshipper` |
|      MacOS      |     `~/Library/Application Support/airshipper`      |

Airshipper will support profiles in future and and already stores the game files in a profile called `default`.  
Logs, screenshots, assets are all located in the [`userdata` directory](userdata-folder-structure.md) inside a profile.

### Troubleshooting

If airshipper does not open or display correctly, you can use the CLI by

1. Opening a terminal

   > On Windows press `[Windows] + [R]`. Then type `cmd` and hit `enter`.

2. Type `airshipper run` and hit enter
3. Enjoy the game.
