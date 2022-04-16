# Configuring the server

Whichever route you chose for hosting the server, you might want to configure it. This section contains an explanation of all the config files related to a Veloren server, their purposes and contents.

## The userdata folder structure

After running `veloren-server-cli` for the first time, a `userdata` folder will be created, containing all of it's configuration and data. It's contents will look like this:
```
userdata
├── server
│   ├── saves
│   │   └── db.sqlite
│   └── server_config
│       ├── admins.ron
│       ├── banlist.ron
│       ├── description.ron
│       ├── settings.ron
│       └── whitelist.ron
└── server-cli
    └── settings.ron
```
### server/server_config
This folder is the most interesting to us. It contains various important configuration files.

#### admins.ron
> This file contains a list of UUIDs of players with administrator privileges.  
> You need access to server console to modify it.  
> Example:
> ```ron
> [
>     "f60e23c6-345c-449b-b05a-e431d53fc65c",
> ]
> ```

#### banlist.ron
> This file contains the banlist, and associated information about each ban.  
> Server admins can use in-game commands to modify it.  
> Example:
> ```ron
> {
>     "7ea1a4cd-3002-4fe6-957e-4483f3fda3e7": (
>         username_when_banned: "YuriMomo",
>         reason: "No testing bugs on this server >:(",
>     ),
> }
> ```
#### description.ron
> This file contains the server description - a single quoted string of text.
> You need direct access to the server files to modify it.
> Example:
> ```ron
> "This is the best Veloren server"
> ```

#### settings.ron
> This is the file containing most of the configuration options.  
> Most of the options are self-explanatory.
> You need direct access to the server files to modify it.
> Example:
> ```ron
> (
>     gameserver_address: "0.0.0.0:14004",
>     metrics_address: "0.0.0.0:14005",
>     auth_server_address: Some("https://auth.veloren.net"),
>     max_players: 100,
>     world_seed: 25269,
>     server_name: "Veloren Alpha",
>     start_time: 32400,
>     map_file: None,
>     max_view_distance: Some(65),
>     banned_words_files: [],
>     max_player_group_size: 6,
>     client_timeout: (
>         secs: 40,
>         nanos: 0,
>     ),
>     spawn_town: None,
>     safe_spawn: true,
>     max_player_for_kill_broadcast: Some(20),
> ) 
> ```
> Explanations of non-obvious things:
> - Some values use the `Option` type, which means they can either be set to either `Some(value)` or `None`.
> - `max_player_for_kill_broadcast` might sound scary, but it only prevents chat spam by only sending death messages of others to their group and nearby players if the set player count is exceeded. Setting it to `None` means the server will never broadcast kill messages globally.

#### whitelist.ron
> If this file is not empty, only players whose UUIDs it contains will be able to join the server.  
> Server admins can use in-game commands to modify it.  
> Example:
> ```ron
> [
>      "f60e23c6-345c-449b-b05a-e431d53fc65c", 
> ]
> ```

### server/saves
This folder contains the server database.

### server-cli
This folder only contains the `settings.ron` file with the following contents:
```ron
(
    update_shutdown_grace_period_secs: 120,
    update_shutdown_message: "The server is restarting for an update",
)
```
It allows you to customize the waiting time before restarting to update the server, and the message it uses when warning players about that. This is only used by the Docker hosting method.
