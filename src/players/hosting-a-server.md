# Hosting a Server

This section will describe how to setup a Veloren server.

> **Note**: _There are multiple ways to setup a Veloren server therefore this book explains the most common and easiest approaches._

At its core, Veloren is split into a client (`veloren-voxygen`) and a server (`veloren-server-cli`). In singleplayer mode, the game starts a server listening on a random port in the background and connects to it automatically.  
In multiplayer mode however, Veloren also uses an authentication server (`veloren-auth`). 
This allows players to register just once on our website, and log into any server with the same account, similar to for example Minecraft.

> **Note:**  
> While you can use a custom auth server, if you do it, **players will see a security warning** when connecting to your game server.
> 
> You can also disable authentication completely, but it will allow **anyone** to log in using **any username**, including as a **server admin**.

## Hosting a server on your PC
If you want to play with your friends and do not have a dedicated server follow these instructions.

### Preparing to host a LAN-only server
If you want to play with family or friends on your local network, follow the steps outlined in this section.

Find your local IP address:
1. Some Linux Distros:
   1. Open the Terminal.
   2. Type `ip -br -4 addr | grep -v 'lo '` and press enter.
      > **Example output:**  
      > `wlp3s0 UP 192.168.100.13/24 192.168.100.14/24`  
   3. The first ip address after `UP`, without the part after the `/` is what you're looking for.  
   In the example that's `192.168.100.13`.
2. MacOS / Other Linux Distros:
   1. Open the Terminal.
   2. Type `ifconfig | grep 'inet ' | grep -v 127.0.0.1` and press enter.
      > **Example output:**  
      > `inet 192.168.12.37  netmask 255.255.255.0  broadcast 192.168.1.255`  
   3. The first IP address after `inet` is what you're looking for.  
   In the example that's `192.168.12.37`.
3. Windows:
   1. Open CMD (type `cmd.exe` into the start menu and press enter).
   2. Type `ipconfig | findstr IPv4` and press enter.
      > **Example output:**  
      > `IPv4 address. . . . . . . . . . . : 127.0.0.1`  
      > `IPv4 address. . . . . . . . . . . : 192.168.3.24`  
      > `IPv4 address. . . . . . . . . . . : 192.168.3.25`  
   3. Find the first address which isn't `127.0.0.1`.  
   In the example that's `192.168.3.24`.

### Preparing to host a server open to the internet

> **Note**: _You will need access to the router and knowledge about port forwarding._

If you want to play with people over the internet, follow this section.

1. Port forward port `14004` TCP and UDP on your router.
2. [Find your public IP address](https://www.showmyipaddress.eu/).

### Launching the server
*Follow these instructions after completing the preparations from one of the previous sections*

1. Using the server provided by Airshipper:  
   *This is a good option if everyone playing uses Airshipper.*
   1. [Find your game installation folder](airshipper.md#files).
   2. Go into `profiles/default`.
   3. Launch `veloren-server-cli[.exe]`.
2. Using a custom server executable:  
   *This is a good option if you want to for example play an older release.*
   1. Open the folder with extracted game files.
   2. Make sure you have the `assets` folder in the same place as the server executable.
   3. Launch `veloren-server-cli[.exe]`.

Share your IP address with the other players.

Enjoy the game!

## Hosting a server using Docker

If you want to run a dedicated Veloren server 24/7 follow this.

> **Note**: _We assume general command line and docker-compose knowledge. You will need root access on the server and `docker`, `docker-compose` installed ._

> **Note**: _The default `docker_compose.yml` will automatically keep the game server updated to the latest nightly release._

> **Tip:** Check out the [Docker Compose file reference](https://docs.docker.com/compose/compose-file/compose-file-v3/) for more information about the `docker-compose.yml` file

### Setup
1. Create a folder for the server data and `cd` into it.
2. Download `docker-compose.yml` from the [repository](https://gitlab.com/veloren/veloren/-/blob/master/server-cli/docker-compose.yml) into the folder.  
`wget https://gitlab.com/veloren/veloren/-/raw/master/server-cli/docker-compose.yml`
3. If needed open port `14004` (`14005` for metrics) in your firewall.
4. To create and start the containers, run `sudo docker-compose up -d`.  
If you modify the `docker-compose.yml` file, you'll need to run that command again for it to take effect.

> **Note:** While normally you would use the server console to add  administrators, you can't do that yet with our `docker-compose.yml`.
Instead, run `veloren-server-cli` on your PC, do `admin add your_username` then `quit` in it's console, and just copy the `userdata/server/admins.ron` file to your dedicated server.

### Monitoring and maintenance

1. To restart the server, run `sudo docker-compose restart`.
2. To view logs, run `sudo docker logs veloren-game-server-master`.
3. To access the server's configuration files, open the `userdata` folder automatically created next to `docker-compose.yml`.

You are done!

**Note**: _This will automatically keep the game server updated to the latest nightly release._

### Running commands on a game server using docker (i.e. the dedicated game server setup)

The game server has a CLI interface that can be used to run commands for tasks such as adding admins and moderators.
The steps for accessing this interface while the server is running inside docker are outlined below:

1. Run `docker attach \<game server container ID\>` if you used the docker-compose file, you can use `veloren-game-server-master` (otherwise run `docker ps` to find the ID of the Veloren container, then if the ID is for example `e002d350ab26`, run `docker attach e002d350ab26`).
2. You can now run server CLI commands. To see the available options type `help` and press enter.  
**Note:**: _Logging output from the server can break up the visualization of command input but this can be ignored and broken up commands will still work._
3. Once you are done, to escape press **Ctrl+p** followed by **Ctrl+q**.


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
