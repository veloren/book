# Authentication Server Setup

## Run the server locally

Running the server locally is described in the previous sections.

Setting up a server reachable from the outside without dedicated server requires also the following:

- Configure your router to forward data from your external (WAN) IP to the server machine for the port 14004.
- Run `veloren-server-cli(.exe)` and adjust settings to setup the administrators, server name, authentication and IP connection address in the `server_settings.ron` file.

N.B.: The connection address can be set to `0.0.0.0` on the local server machine to listen to the default route.

N.B.2.: Your server machine firewall must be setup to accept communication to this port.

## Use custom authentication

If you want to use custom authentication, you'll need to setup the world server value to your authentication server machine IP address or name. E.g.: `auth_server_address: Some("<auth-server-ip-or-name>")`

If you want to disable authentication, you can set the `auth_server_address` value to `None`.


## Setting up a dedicated server

In order to setup a dedicated server, you'll need to secure it!
`A server is like a baby and needs attention to not be exploited by others. -SongTronix`

docker-compose files are provided for both the world server and the auth servers in order to ease deployment.

### For automatic updates (for those who wants the latest versions)

Setup your docker & docker-compose to run:
- https://gitlab.com/veloren/veloren/-/blob/master/server-cli/docker-compose.yml

Note that those versions can become unstable at any time. the world server will use the official authentication server in that case.
