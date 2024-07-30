# Configuring The Server

Whichever route you chose for hosting the server, you might want to configure it. This section contains an explanation of all the config files related to a Veloren server, their purposes and contents.

## The userdata folder structure

After running `veloren-server-cli` for the first time, a `userdata` folder will be created, containing all of it's configuration and data. It's contents will look like this:

```txt
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

> **Tip:** _To add an admin or mod by username, type `admin add <USER> <ROLE>` into the server console._
> _`<ROLE>` can be either `admin` or `moderator`._

#### admins.ron
> This file contains a list of UUIDs of players with administrator privileges.
>
> You need access to server console to modify this file.
>
> Example:
>
> ```ron
> [
>     "f60e23c6-345c-449b-b05a-e431d53fc65c",
> ]
> ```

#### banlist.ron
> This file contains the list of banned players, and associated information about each ban.

> Server admins can use in-game commands to modify this file.
>
> Example:
>
> ```ron
> {
>     "7ea1a4cd-3002-4fe6-957e-4483f3fda3e7": (
>         username_when_banned: "YuriMomo",
>         reason: "No testing bugs on this server >:(",
>     ),
> }
> ```
>
#### description.ron
> This file contains the server description (also known as 'Message Of The Day' (MTOD)), and server rules.
>
> Both support localisation. If the user's locale matches one of the entries, they will see the corresponding
> localised entry for both.
>
> If the `rules` field is set to `Some("...")` rather than `None`, users will see the rules when they first join the
> server, with a mandatory 'accept' button (any changes to the rules will also cause them to be shown to users again).
>
> The `default_locale` field determines which set of descriptions users are shown if their locale does not match any of
> those present in the file (by default, this field is `"en"` i.e: English).
>
> Server admins can use in-game commands to modify this file.
>
> Example:
>
> ```ron
> V2((
>     default_locale: "en",
>     descriptions: {
>         "en": (
>             motd: "This is the best Veloren server",
>             rules: None,
>         ),
>     },
> ))
> ```

#### settings.ron
> This is the file containing most of the configuration options.
>
> Most fields are self-explanatory, but more information can be found [here](https://docs.veloren.net/veloren_server/settings/struct.Settings.html).
>
> You need direct access to the server files to modify this file.
>
> Example:
>
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
>
> > **Note:** While you can use a custom auth server, if you do it, players will see a **security warning** when connecting to your game server.
>
> > **Note:** While you can disable authentication completely, it would allow **anyone** to log in using **any username**, including as a **server admin**.
>
> Explanations of non-obvious options:
>
> - Some values use the `Option` type, which means they can either be set to either `Some(value)` or `None`.
> - `max_player_for_kill_broadcast` might sound scary, but it only prevents chat spam by only sending death messages of others to their group and nearby players if the set player count is exceeded. Setting it to `None` means the server will never broadcast kill messages globally.

#### whitelist.ron
> If this file is not empty, only players whose UUIDs it contains will be able to join the server.
>
> Server admins can use in-game commands to modify this file.
>
> Example:
>
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
