# Hosting a Server

This section will describe how to setup the different Veloren server components.

## Basic Veloren communication structure

Veloren is composed of the Veloren client (veloren-voxygen), the world server (veloren-server),
and the authentication server (auth-server).

The Veloren client (what players see and use) connects to the world server when the multiplayer option is selected.

When setup with authentication support, the world server is using the authentication server to log the player in,
and know wheter the player can be accepted into the world.

-> The authentication server stores the player account data as a sqlite database.

The Veloren world server then let the player manage his/her character and login into the world.
It manages the different player's character data, the world creation and update, and the communication
between players.

-> The world server also stores the characters data as a sqlite database.

The next sections will describe how to setup the different servers.
