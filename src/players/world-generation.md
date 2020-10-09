# Generating a Custom World

1. Go into your game files (See where [Airshipper](airshipper.md#files) stores files) and find `server_settings.ron`.

2. Change `world_seed:` to your choice, and `map_file:` to `Some(Save),`. Commas must be preserved.

3. Run `veloren_server_cli` from a terminal. (The normal game usually times out, because map generation takes a long time, so it's safer to run a server.)

4. There won't be any output for a while. On a good CPU (e.g. recent Ryzens) worldgen takes roughly 10 minutes, and scales poorly with core count.

5. Eventually it'll say the server is ready. This means the world has successfully generated, and is now running on the server. You can safely kill the server, either by typing `quit[Enter]` or with Ctrl+C.

6. A `maps` folder should now be in your game directory, containing a `map_[long number].bin` file.

7. Back in `server-settings.ron`, change `map_file:` to `Some(Load("maps/map_[long number].bin")),` to make singleplayer load the map on each run. You can rename the file to better keep track of your worlds.

We understand that this is currently an overly lengthy process, and will give it an in-game menu further into development.
