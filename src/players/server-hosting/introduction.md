# Hosting a Veloren Server

At its core, Veloren is split into 2 components - a client (`veloren-voxygen`) and a server (`veloren-server-cli`).  
In singleplayer mode, the game starts a server listening on a random port in the background and connects to it automatically.  
In multiplayer mode however, Veloren also uses an authentication server (`veloren-auth`). 
This allows players to register just once on our website, and log into any server with the same account, similar to for example Minecraft.

> **Note:**  
> While you can use a custom auth server, if you do it, players will see a **security warning** when connecting to your game server.  
> You can also disable authentication completely, but it will allow **anyone** to log in using **any username**, including as a **server admin**.

After reading one of the setup guides, head over to the [Configuring the server](configuration.md) page to learn how to set it up according to your needs and preferences.