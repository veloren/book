# Troubleshooting

In case you've hit an issue this section might help you resolve it.

## Audio issues

In case the game crashes with something similar like:

```rust,ignore
INFO veloren_voxygen::logging: Setup terminal and file logging. logdir="<some_path>"
thread 'main' panicked at 'build_output_stream failed with all supported formats: FormatNotSupported', /root/.cargo/registry/src/github.com-1ecc6299db9ec823/rodio-0.10.0/src/engine.rs:158:18
note: run with RUST_BACKTRACE=1 environment variable to display a backtrace
```

If you are using Arch Linux, try installing the `pulseaudio-alsa` package, `pacman -S pulseaudio-alsa`.

Otherwise you have to manually disable audio by

1.  making sure Veloren is closed.
2.  locating `settings.ron` (See where [Airshipper](airshipper.md#files) stores files)
3.  edit it and replace `output: Automatic` with `output: Off`. It should look like:
    ```rust,ignore
    audio: (
        master_volume: 1,
        music_volume: 1
        sfx_volume: 1,
        max_sfx_channels: 10,
        output: Off, // The important line!
    ),
    ```
4.  Save file and retry. In case it didn't help visit [Reporting Bugs](reporting-bugs.md) page.

## Graphical issues

In Arch Linux, it is necessary to install a rendering backend such as `vulkan-radeon` or `vulkan-intel` to fix graphical issues in Airshipper. Otherwise the game will not start and will result in a "Voxygen has panicked" error.

![Graphical issues](https://media.discordapp.net/attachments/464698017283440640/887397846259744809/Graphical_glitches.png)

## Airshipper and/or Veloren fail to start

If the launcher or game fail to start and starting from console only prints an error like `[wayland-client error] Attempted to dispatch unknown opcode 0 for wl_shm, aborting`, the issue is likely to be a compatibility issue with wayland.
As a workaround the windowing backend can be forced to X11 by setting the env variable `WINIT_UNIX_BACKEND=x11`.

## PS4 or other controller not working

Currently only XInput controllers are supported on Windows. This means that controllers like the PS4, Switch, and some older generic controllers won't work with Veloren.

In order to work around this, a program such as [DS4Windows](https://github.com/Ryochan7/DS4Windows/releases) can be used. Both a text and video tutorial on how to use DS4Windows can be found [here](https://ryochan7.github.io/ds4windows-site/#howto).

