# Troubleshooting

Veloren runs on many operating systems, architectures, GPUs, and system configurations. Sometimes, things don't work!

This page contains a list of common problems and solutions.

Use the links below to navigate to the section most relevant to you. You can also use the search functionality at the
top of the page to search for keywords.

- [⛔ Crashes](#-crashes)

- [🎨 Graphics](#-graphics)

- [🎧 Audio](#-audio)

- [🎮 Input & Controllers](#-input-and-controllers)

If you've found a solution to a problem that wasn't mentioned here, you can
[contribute to this section](../contributors/writers/extend-this-book.md)!

If you can't find a solution to your problem here, you can ask for help from the community:

- [Discord Community](https://discord.gg/ecUxc9N)

- [Reddit Community](https://www.reddit.com/r/Veloren/)

- [Matrix Community](https://matrix.to/#/!XE8JMjIKOzVcryA0kc:conduit.rs?via=conduit.rs&via=matrix.org&via=tchncs.de)

If you think you've encountered a more serious bug, you can
[report the bug on GitLab](https://gitlab.com/veloren/veloren/issues).

---

# ⛔ Crashes

Although we try to ensure that Veloren is as stable as possible, there are a small number of things that can cause the
game to crash. Thankfully, many of these are fixable!

## Airshipper won't start (or crashes on startup)

Possible solutions:

- [Update your graphics drivers](#drivers)

- [Run Airshipper in compatibility mode](#compatibility-mode)

### Compatibility Mode

Airshipper can run in a mode where the user interface does not appear, known as 'compatibility mode'. In this mode,
Airshipper will automatically download and run the latest version of Veloren for you.

- On Windows, compatibility mode can be used with the dedicated 'Airshipper: Compatibility Mode' icon

- On all platforms, entering `airshipper run` into your console will start Airshipper in compatibility mode

## Veloren (Voxygen) crashes on startup

Possible solutions:

- [Update your graphics drivers](#drivers)

- Switch to another [graphics backend](#graphics-backend)

- Try [disabling audio](#disablingaudio)

---

# 🎨 Graphics

Veloren requires that your computer supports one of the following:

- DirectX (Windows only, version **11.2** or above)

    - *(note: recent versions of Airshipper require DirectX 12, but [compatibility mode](#compatibilitymode) should still work)*

- Vulkan (Windows and Linux only, version **1.2** or above)

- Metal (Mac OS only)

If your computer does not support one of these, you may not be able to run the game.

## Drivers

Running Veloren might require that you update your graphics drivers, or install them if you do not already have them.

- If running Windows, you can follow [this guide](https://www.pcgamer.com/how-to-update-drivers/) to update your
  graphics drivers

- If running Linux, you can follow [this guide](https://linuxconfig.org/install-and-test-vulkan-on-linux) to install
  Vulkan drivers. Please note that many distributions *do not* have Vulkan drivers pre-installed: the fact that other
  games run fine is not an indication that you have Vulkan drivers installed!

- If running Mac OS, you may need to perform a system update to obtain the latest drivers

## Graphics Backend
<video width="640" height="460" autoplay loop muted>
  <source src="https://cdn.discordapp.com/attachments/464698017283440640/1016333211472764928/airshipper_qDdxbKVHnq.mp4" type="video/mp4">
  Your browser does not support video tag
</video>

On some platforms, Veloren can be run using one of several different graphics APIs.

You can switch between the available graphics backends in the Airshipper Settings.

- On Windows, the following graphics backends are supported:

    - DirectX 11

    - DirectX 12

    - Vulkan

- On Linux, only Vulkan is supported (however, Veloren has been known to run well through
  [WINE](https://www.winehq.org/) using backends supported on Windows, so this may be an option for you)

- On Mac OS, only Metal is supported

If you're running airshipper in [compatibility mode](#compatibility-mode), you can still change graphics backend by opening the file `%appdata%/airshipper/airshipper_state.ron` in a text editor. 
Near the bottom of the file you'll find the line `wgpu_backend: Auto,`, change that to `wgpu_backend: DX11,`

## Airshipper is missing UI elements or flickers when moving the mouse

![Airshipper graphics problems](https://media.discordapp.net/attachments/464698017283440640/887397846259744809/Graphical_glitches.png)

To fix this, you may need to [update your graphics drivers](#drivers).

## Graphical glitches in-game

![In-game graphics problems](https://cdn.discordapp.com/attachments/464698017283440640/1015302288685928498/unknown.png)

You may need to update [update your graphics drivers](#drivers).

Alternatively, switching to another [graphics backend](#graphics-backend) may solve the problem.

Ensure that your computer has the required [graphics support](#-graphics).

---

# 🎧 Audio

## Audio not working

On Linux, you might need to install ALSA configuration for PulseAudio.

- For Arch Linux, this means installing the `pulseaudio-alsa` package. You can do this with `pacman -S pulseaudio-alsa`

## Disabling Audio

In particularly dire cases, it may be necessary to disable audio in Veloren to avoid crashes or similar problems. You
can do this by:

1.  making sure Veloren is closed.
2.  locating `settings.ron` (See where [Airshipper](airshipper.md#files) stores files)
3.  editing it and replacing `output: Automatic` with `output: Off`. It should look like:
    ```rust,ignore
    audio: (
        master_volume: 1,
        music_volume: 1
        sfx_volume: 1,
        max_sfx_channels: 10,
        output: Off, // The important line!
    ),
    ```
4.  saving the file and running the game again.

---

# 🎮 Input and controllers

## Mouse is invisible or window resizing isn't working properly when using Wayland on Linux

Although Veloren does support Wayland, this support can sometimes be buggy.
These problems may be fixed by explicitly specifying an xcursor theme for the
program to use. To do that, first run the following command in a terminal to
get a usable theme:

```
find /usr/share/icons/ -type d -name "cursors" | head -1 | awk -F / '{print $5}'
```

Set the `XCURSOR_THEME` environment variable to the result. If you got `Adwaita`, for example, you would
do the following:

- If using Airshipper, add `XCURSOR_THEME=Adwaita` to the 'Environment Variables' field in the settings

- If running as a standalone program, have your desktop environment set `XCURSOR_THEME` to `Adwaita` when running
the game

- If running via the command line, prepend `XCURSOR_THEME=Adwaita` to the command you use to run the game, like
  `XCURSOR_THEME=Adwaita ./veloren-voxygen`

If that doesn't work, you can try using the `xwayland` compatibility layer when running.

- If using Airshipper, add `WINIT_UNIX_BACKEND=x11` to the 'Environment Variables' field in the settings

- If running as a standalone program, have your desktop environment set `WINIT_UNIX_BACKEND` to `x11` when running the
  game

- If running via the command line, prepend `WINIT_UNIX_BACKEND=x11` to the command you use to run the game, like
  `WINIT_UNIX_BACKEND=x11 ./veloren-voxygen`

## PS4 or other controller not working

Currently only XInput controllers are supported on Windows. This means that controllers like the PS4, Switch, and some
older generic controllers may not work with Veloren.

In order to work around this, a program such as [DS4Windows](https://github.com/Ryochan7/DS4Windows/releases) can be
used. Both a text and video tutorial on how to use DS4Windows can be found
[here](https://ryochan7.github.io/ds4windows-site/#howto).

---
