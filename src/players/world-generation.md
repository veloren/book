# Generating a Custom World

1. Open your singleplayer or server's settings file. See [here](userdata-folder-structure.md).

2. Set your custom `world_seed`, and `map_file` to `Some(Save)`.

3. Launch your game as normal, whether you're doing it through singleplayer or the server cli.

4. The generation process can take a significant length of time, with little indication that it's running properly. 10 minutes on a good CPU is expected, for standard-sized worlds. Eventually, it will load into the new world.

5. The world will be saved in a `maps` folder, as a binary file. Set `map_file` to `Some(Load("maps/<filename>.bin")),`, else it will try to regenerate it each time.

## map\_file Options

| Value                            | Description                                                                                                            |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `None`                           | Loads the default world map, located in the `assets/world/map` folder.                                                 |
| `Some(Generate)`                 | Generates a new world, using `world_seed`, and starts the server using it. **Does not save the resulting world file.** |
| `Some(Save)`                     | Same as with `Generate`, but will save the world as a binary file in a `maps` directory.                               |
| `Some(Load("maps/example.bin"))` | Loads a map from file                                                                                                  |

## Advanced Methods

If you are able to compile the game, you can generate maps with custom sizes and terrain scales, through the same steps as above.

To change map size, edit the `x` and `y` values [here](https://gitlab.com/veloren/veloren/-/blob/34c3bab6ad5046b059f824b94118cbe657f6c286/world/src/sim/mod.rs#L68). Each increment will **double** map scale. Be warned that worldgen times similarly increase, and that actually loading larger worlds can be quite RAM-heavy.

To change terrain scale, edit [here](https://gitlab.com/veloren/veloren/-/blob/34c3bab6ad5046b059f824b94118cbe657f6c286/world/src/sim/mod.rs#L455). `4.0` is based on earth-like values, and gives a much grander scale to terrain than the default.

## Map Viewer

If you are able to compile, you can also try an example map generator and viewer application. Run `RUST_LOG="info,veloren_world=debug" cargo run --release --example water` from your local repository.

By default it will load the default world from the `assets` folder. Input a custom seed [here](https://gitlab.com/veloren/veloren/-/blob/34c3bab6ad5046b059f824b94118cbe657f6c286/world/examples/water.rs#L42), and change two lines below if you want to generate or load a different world.

This method **will** indicate progress through world generation, progressing from `Erosion iteration 0` through to `99`, and so is recommended for larger worlds.

Once the map loads, the default view shows temperature and humidity overlays. Press T and H to disable them, respectively, and M to enable real map colours. F4 will take a screenshot.

The map viewer is somewhat unresponsive, so you may need to hold keys for a moment for them to take effect.

## Troubleshooting

If the default map loads despite changes you have made, double check you haven't mistyped any of the settings. In particular, you must not remove the trailing commas from the `.ron` files.
