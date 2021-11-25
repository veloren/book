# Generating or loading a custom world

1. Open your singleplayer or server's settings file. See [here](userdata-folder-structure.md).

2. Set your custom `world_seed`, and `map_file` to `Some(Save)`.

3. Launch your game as normal, whether you're doing it through singleplayer or the server cli.

4. The generation process can take a significant length of time, with little indication that it's running properly. 10 minutes on a good CPU is expected, for standard-sized worlds. Eventually, it will load into the new world.

5. The world will be saved in a `maps` folder, as a binary file. Set `map_file` to `Some(Load("maps/<filename>.bin")),`, else it will try to regenerate it each time.

## map\_file Options

| Value                            | Description                                                                                                            |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `None`                           | Loads the default world map, located in the `assets/world/map` folder.                                                 |
| `Some(Generate(([options])))`    | Generates a new world, using `world_seed`, and starts the server using it. **Does not save the resulting world file.** |
| `Some(Save(([options])))`        | Same as with `Generate`, but will save the world as a binary file in a `maps` directory.                               |
| `Some(Load("maps/example.bin"))` | Loads a map from file                                                                                                  |

## Generation Options

The options above can be filled out to change the size of generated maps, and to change the scale of mountains within them. Options you do not wish to change can be left blank, and will be replaced by defaults, however you must keep the spare braces. Manually writing out the default set of options would give `Some(Generate((x_lg: 10, y_lg: 10, scale: 2.0)))`.

#### World size

`x_lg` and `y_lg` give the binary logarithm of the number of chunks along each axis of the world, that is, `x_lg: 10` results in a world 2^10=1024 chunks wide.

Each increment doubles length, and each decrement halves it. Rectangular worlds are fully supported, however each doubling of each dimension also roughly doubles world generation time and RAM consumption, which can quickly get out of hand.

A maximum of 14 is supposed to be supported in each dimension, giving a square world 524 km across, roughly equivalent to the United Kingdom in area, but it would look pretty bad due to the current lack of tectonics simulation, which becomes more important at larger scales. 13x13 is the largest so far attempted.

#### World scale

`scale` simply changes the scale of mountains, landmasses, etc. A value of `4.0` grants a roughly Earthlike scale, although a larger-than-default world is recommended for this. Going beyond `4.0` is not considered supported, but generally works. As a guide, the tallest mountains will be a little taller than this value, in kilometres.

## Loading a pre-generated map with a specific seed

Navigate to your server's or singleplayer settings file like shown [here](userdata-folder-structure.md).

In there 
1. Change the world seed, e.g. `world_seed: 40382,`\

2. Change `map_file` to something like\
`map_file: Some(Load("userdata/server/maps/map_1624935538562.bin")),`\

3. Optionally you can also set a spawn town: `spawn_town: Some("Elden"),`

Make sure to use the correct filepath (from the root of your veloren folder) and filenames!\
There needs to be a `,` behind all of these inputs or the server will use the fallback settings template file.\

Note: The filepath used in this example requires the creation of an additional folder called "maps" inside the userdata/server folder.

## Map Viewer

If you are able to compile, you can also try an example map generator and viewer application. Run the following command from your local repository, depending on preferred terminal.

Unix-like:

`RUST_LOG="info,veloren_world=debug" cargo run --release --example water`

Windows, cmd:

`set RUST_LOG=info,veloren_world=debug&& cargo run --release --example water`

Windows, PowerShell:

`$env:RUST_LOG="info,veloren_world=debug"; cargo run --release --example water`

By default it will load the default world from the `assets` folder. Input a custom seed [here](https://gitlab.com/veloren/veloren/-/blob/34c3bab6ad5046b059f824b94118cbe657f6c286/world/examples/water.rs#L42), and change two lines below if you want to generate or load a different world.

This method **will** indicate progress through world generation, progressing from `Erosion iteration 0` through to `99`, and so is recommended for larger worlds.

Once the map loads, the default view shows temperature and humidity overlays. Press T and H to disable them, respectively, and M to enable real map colours. F4 will take a screenshot.

The map viewer is somewhat unresponsive, so you may need to hold keys for a moment for them to take effect.

## Troubleshooting

If loading a custom world fails or the default map is still loaded, double check you haven't mistyped any of the settings. A common mistake is forgetting to place one of the trailing commas inside the settings `.ron` file(s).
