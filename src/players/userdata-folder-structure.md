# Userdata Folder Structure

The `userdata` folder unifies all player and server configuration in a single place, which should be transferrable between different Veloren installations from v0.8 onwards.

The folder will be next to your Veloren executable, or in your repository's root if self-compiling. See [where Airshipper stores files](airshipper.html#files) if using the launcher.

Airshipper currently stores the items under the `voxygen` heading outside of `userdata`, but this will change in the future.

- voxygen
  - logs
    - voxygen.log.\<date of log\>
  - [settings.ron](#settingsron-voxygen-edition)
  - [profile.ron](#profileron)
- singleplayer
  - saves
    - db.sqlite
  - server\_config
    - [settings.ron](#settingsron-server-edition) (Some entries ignored)
    - [description.ron](#descriptionron)
    - [whitelist.ron](#whitelistron) (Ignored)
    - [banlist.ron](#banlistron) (Ignored)
    - [admins.ron](#adminsron) (Ignored)
- server
  - saves
    - db.sqlite
  - server\_config
    - [settings.ron](#settingsron-server-edition)
    - [description.ron](#descriptionron)
    - [whitelist.ron](#whitelistron)
    - [banlist.ron](#banlistron)
    - [admins.ron](#adminsron)
- server-cli
  - [settings.ron](#settingsron-server-cli-edition)

## settings.ron (voxygen edition)

Contains all of the settings accessible from the in-game GUI, and usually shouldn't require manual intervention.

The main thing not accessible from main game menus is gamepad keybindings, which can only be changed by directly editing the file.

## profile.ron

Contains hotbar infomation, per-character and per-server. Should never need to be manually modified.

## settings.ron (server edition)

This file is intended for manual editing, and should never be overwritten by the game. If the file is in an invalid state, the server will emit a warning in including the position of the error, create a settings.template.ron file full of the default values, and start up with all default values.

| Setting                 | Description                                                                                                                                                                            | Default value                      |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `gameserver_address`    | Address and port the game server will listen to. Note that clients will use the port `14004` by default. _Changing the port will require to specify it in the client too._             | `"0.0.0.0:14004"`                  |
| `metrics_address`       | Address and port the game server will expose [prometheus](https://prometheus.io) metrics.                                                                                              | `"0.0.0.0:14005"`                  |
| `auth_server_address`   | When using `Some(<value>)`: The value is the IP address or domain the **game server and client** will use. If you want to disable authentication, you replace `Some(...)` with `None`. | `Some("https://auth.veloren.net")` |
| `max_players`           | Maximum number of players connected to the game server.                                                                                                                                | `100`                              |
| `world_seed`            | seed number used to setup the random generation of the world.                                                                                                                          | `59686`                            |
| `server_name`           | displayed server name                                                                                                                                                                  | `"Veloren Alpha"`                  |
| `start_time`            | Server daylight start time in seconds.                                                                                                                                                 | `32400`                            |
| `map_file`              | Sets which map to load. [See here](world-generation.html#map_file-options) for allowed values.                                                                                         | `None`                             |
| `max_view_distance`     | The maximum view distance that clients may request. Useful for low-RAM servers.                                                                                                        | `Some(30)`                         |
| `banned_words_files`    | List of files containing words to be censored. None are distributed by default.                                                                                                        | `[]` (Empty array)                 |
| `max_player_group_size` | The maximum party size players can have, for purposes of XP sharing and ignoring friendly fire.                                                                                        | `6`                                |
| `client_timeout`        |                                                                                                                                                                                        | `(secs: 40, nanos: 0,)`            |

## description.ron

Contains the introductory chat message clients get when entering the server, as a quoted string. Can be multiple lines.

Example:
```
"This is the best Veloren server"
```

## whitelist.ron

Contains a list of whitelisted account IDs, and is considered disabled if empty. Heavily recommended to use the `/whitelist add/remove` ingame command, rather than manual editing.

Example: Result of using `/whitelist add Treeco` and `/whitelist add treeco2`.

```
[
    "6f15b915-074f-f78d-df88-34fb33e4e13f",
    "3445349e-d03c-64bf-6ecf-a15806275a1f",
]
```

## banlist.ron

Contains a list of banned accounts, and reasons. Heavily recommended to use the `/ban` and `/unban` ingame commands, rather than manual editing.

Example: Result of using `/ban Treeco General nuisance` and `/ban treeco2 alt account`.

```
{
    "6f15b915-074f-f78d-df88-34fb33e4e13f": (
        username_when_banned: "treeco2",
        reason: "alt account",
    ),
    "3445349e-d03c-64bf-6ecf-a15806275a1f": (
        username_when_banned: "Treeco",
        reason: "General nuisance",
    ),
}
```
## admins.ron

Contains a list of admin account IDs. Heavily recommended to use `admin add/remove ` from the server's TUI, rather than manual editing. There is no in-game command to permanently add admins, for security reasons.

Example: Result of using `admin add Treeco`.

```
[
    "ee193d08-8f5a-4862-a279-1a8c4bd357f3",
]
```

## settings.ron (server-cli edition)

The settings in this file govern the warning period the server gives for automatic shutdowns for updates.
