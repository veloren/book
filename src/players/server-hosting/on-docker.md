# Hosting a server using Docker

If you want to run a dedicated Veloren server 24/7 follow this.

> **Note:** _We assume general command line and docker-compose knowledge. You will need `docker` and `docker-compose` installed on the server. You will likely also need root access to access docker._

> **Tip:** _Check out the [Docker Compose file reference](https://docs.docker.com/compose/compose-file/compose-file-v3/) for more information about the `docker-compose.yml` file._
## Setup

> **Note:** _The default `docker_compose.yml` will automatically keep the game server updated to the latest nightly release._

1. Create a folder for the server data and `cd` into it.
2. Download the sample `docker-compose.yml` from [the repository](https://gitlab.com/veloren/veloren/-/blob/master/server-cli/docker-compose.yml) into the folder.  
`wget https://gitlab.com/veloren/veloren/-/raw/master/server-cli/docker-compose.yml`
3. If needed, open port `14004` (`14005` for metrics) in your firewall.
4. To create and start the containers, run `sudo docker-compose up -d`.  
If you modify the `docker-compose.yml` file, you'll need to run that command again for it to take effect.
5. Add moderators/admins by following [the instructions below](#running-commands-inside-the-docker-container)

> **Note:** _If you used the provided docker-compose file, you can use `veloren-game-server-master` in place of `<CONTAINER_ID>` in the following instructions._
## Monitoring and maintenance

- To restart the server, run `docker-compose restart`.
- To view logs, run `docker logs <CONTAINER_ID>`.
- To access the server's configuration files, open the `userdata` folder automatically created next to `docker-compose.yml`.

## Running commands inside the docker container

The game server has a CLI interface that can be used to run commands for tasks such as adding admins and moderators.
The steps for accessing this interface while the server is running inside docker are outlined below:

1. Run `docker attach <CONTAINER_ID>`  
Otherwise run `docker ps` to find the ID of the game server container,  
then if the ID is for example `e002d350ab26`, 
run `docker attach e002d350ab26`.
2. You can now run server CLI commands. To see the available options type `help` and press enter.
3. Once you are done, to escape press **Ctrl+p** followed by **Ctrl+q**.

> **Tip:** _To add an admin or mod, use `admin add <USER> <ROLE>`. `<ROLE>` can be either `Admin` or `Moderator`._

> **Note:** _Logging output from the server can break up the visualization of command input but this can be ignored and broken up commands will still work._

You are done!

