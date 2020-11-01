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
