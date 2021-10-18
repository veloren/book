# Hosting a Server

This section will describe how to setup a Veloren server.<br/>

**Note**: _There are multiple ways to setup a Veloren server therefore this book explains the most common and easiest approaches._

Veloren is composed of the Veloren client (veloren-voxygen), the game server (veloren-server-cli),
and the authentication server (auth-server).

When setup with authentication support (default), the game server is using the authentication server to log the player in.

**Note**: _Without authentication the server will allow anyone to log in with any name including those with admin access!_

## Setup local game server

If you want to play with your friends and do not have a dedicated server follow these instructions.

**Note**: _You will need access to the router and knowledge about port forwarding._

1. Setup
   1. Port forward `14004` on your router.
2. Launch game server `veloren-server-cli(.exe)`
   - check [Airshipper](airshipper.md#files) section to find out where the files are
   - or download Nightly from the [website](https://veloren.net/download).
     > **Note**: _The `assets` folder is required to be next to the game server._
3. [Give out your IP](https://www.showmyipaddress.eu/)
4. _Optionally_ disable authentication by replacing `auth_server_address: Some(...)` with `auth_server_address: None`

Enjoy the game!

## Setup dedicated game server

If you want to run a dedicated Veloren server 24/7 follow this.<br/>

**Note**: _You will need access to the server, `docker`, `docker-compose` installed and we assume general command line and docker-compose knowledge._

1. Setup
   1. Create folder `/opt/veloren-server` (feel free to name it differently).
   2. Copy `docker-compose.yml` from the [repository](https://gitlab.com/veloren/veloren/-/blob/master/server-cli/docker-compose.yml) into the folder.
   3. If needed open port `14004` (`14005` for metrics) in your firewall.
2. Start it
   1. Run `docker-compose up -d` as root.
   2. View logs with `sudo docker logs veloren-game-server-master`.

You are done!

**Note**: _This will automatically keep the game server updated to the latest nightly release._

### Running commands on a game server using docker (i.e. the dedicated game server setup)

The game server has a CLI interface that can be used to run commands for tasks such as adding admins and moderators.
The steps for accessing this interface while the server is running inside docker are outlined below:

1. Run `docker ps` to see the list of running docker container and their IDs.
2. Copy the container ID of the Veloren game server.
3. Run `docker attach <game server container ID>` (e.g. if the ID is `e002d350ab26` then run `docker attach e002d350ab26`).
4. You can now run server CLI commands. To see the available options type `help` and press enter.  
    **Note:**: _Logging output from the server can break up the visualization of command input but this can be ignored and broken up commands will still work._
5. Once you are done, to escape press **Ctrl+p** followed by **Ctrl+q**.


