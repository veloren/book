## Hosting a server using Docker

If you want to run a dedicated Veloren server 24/7 follow this.

> **Note:** _We assume general command line and docker-compose knowledge. You will need root access on the server and `docker`, `docker-compose` installed ._

> **Note:** _The default `docker_compose.yml` will automatically keep the game server updated to the latest nightly release._

> **Tip:** Check out the [Docker Compose file reference](https://docs.docker.com/compose/compose-file/compose-file-v3/) for more information about the `docker-compose.yml` file.

### Setup

1. Create a folder for the server data and `cd` into it.
2. Download `docker-compose.yml` from the [repository](https://gitlab.com/veloren/veloren/-/blob/master/server-cli/docker-compose.yml) into the folder.  
`wget https://gitlab.com/veloren/veloren/-/raw/master/server-cli/docker-compose.yml`
3. If needed, open port `14004` (`14005` for metrics) in your firewall.
4. To create and start the containers, run `sudo docker-compose up -d`.  
If you modify the `docker-compose.yml` file, you'll need to run that command again for it to take effect.

> **Tip:** `veloren-server-cli` provides a CLI for modifying the administrator list.  
To add an admin or mod, run `veloren-server-cli admin add -u <USER> -r <ROLE>`, where `ROLE` is one of `Admin`, `Moderator`

### Monitoring and maintenance

- To restart the server, run `sudo docker-compose restart`.
- To view logs, run `sudo docker logs veloren-game-server-master`.
- To access the server's configuration files, open the `userdata` folder automatically created next to `docker-compose.yml`.

### Running commands on a game server using docker (i.e. the dedicated game server setup)

The game server has a CLI interface that can be used to run commands for tasks such as adding admins and moderators.
The steps for accessing this interface while the server is running inside docker are outlined below:

1. Run `docker attach \<game server container ID\>` (If you used the docker-compose file, you can use `veloren-game-server-master` as the ID. Otherwise run `docker ps` to find the ID of the container, then if the ID is for example `e002d350ab26`, run `docker attach e002d350ab26`).
2. You can now run server CLI commands. To see the available options type `help` and press enter.
> **Note:** _Logging output from the server can break up the visualization of command input but this can be ignored and broken up commands will still work._
3. Once you are done, to escape press **Ctrl+p** followed by **Ctrl+q**.

You are done!

