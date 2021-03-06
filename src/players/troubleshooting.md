# Troubleshooting

Incase you've hit an issue this section might help you resolve it.

## Audio issues

Incase the game crashes with something similar like:

```rust,ignore
INFO veloren_voxygen::logging: Setup terminal and file logging. logdir="<some_path>"
thread 'main' panicked at 'build_output_stream failed with all supported formats: FormatNotSupported', /root/.cargo/registry/src/github.com-1ecc6299db9ec823/rodio-0.10.0/src/engine.rs:158:18
note: run with RUST_BACKTRACE=1 environment variable to display a backtrace
```

then you have to manually disable audio by

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
4.  Save file and retry. Incase it didn't help visit [Reporting Bugs](reporting-bugs.md) page.
