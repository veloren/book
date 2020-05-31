# World Server Setup

## Run the world server

The Veloren world server source code is maintained at: https://gitlab.com/veloren/veloren
N.B.: See the [developer](../developers) section for more information on how to compile the source code.

You can also obtain the server in the download section: https://veloren.net/download/

You can then use the `veloren-server-cli(.exe)` to get it running.

## Configure the world server

Running the server is nice, but you'll need some degree of configuration to make the server run with proper settings.

### Server database

The world server executable will use by default the following database file: `./saves/db.sqlite`.
The database location folder can be overriden by setting the environment variable: `VELOREN_SAVES_DIR`.

### Server settings configuration

The world server will need the `server_settings.ron` settings configuration file in the same folder in order to start properly.

N.B.: The file must be in the Rusty Object Notation format (ron) in order to be read properly.

Here a definition of the provided server settings:

| Setting | Description | Default value |
| ------- | ----------- | ------------- |
| gameserver_address | The IP address or dns name and port the world server will listen to. Note that clients will use the port `14004` to try and connect to the world server, so the port should not be changed.  | `"0.0.0.0:14004"` |
| metrics_address | The IP address or dns name and port the world server will listen to for metrics update. | `"0.0.0.0:14005"` |
| auth_server_address | When using `Some(<value>)`: The value is the IP address or dns name the world server will use to connect to the auth server. If you want to disable authentication, you can use the `None` value. The players will still have to enter an account name but won't need any password in that case. | `Some("https://auth.veloren.net")` |
| max_players | The maximum number of simultaneous player connections. | `100` |
| world_seed | The seed number used to setup the random generation of the world. | `5284` |
| server_name | The displayed server name | `"Veloren Server"` |
| server_description | The displayed server description | `"The best Veloren Server"` |
| start_time | The server daylight start time in seconds. | `32400` |
| admins | The array of account name allowed to run admin commands. | `["The", "Veloren", "Team"]` |
| map_file | The world map file to use when starting the server. Note that when `None` is provided, the default world map file is used. the default file is usually located in `assets\world\map` | None |
| persistence_db_dir | The default server executable relative folder where to save the database file (`db.sqlite`).  | `"saves"` |
