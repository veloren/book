# Hosting a Veloren Server

## Introduction

At its core Veloren is split into 2 components, a client (`veloren-voxygen`) and a server (`veloren-server-cli`).  
In *singleplayer* mode, the game starts a server listening on a random port in the background and connects to it automatically.  
In *multiplayer* mode however, Veloren also uses an authentication server (`veloren-auth`). 
This allows players to register just once on our website, and log into any server with the same account, similar to for example Minecraft.

## How to use this guide

1. Follow one of the setup guides:
    - [Running a Server on Your PC](on-your-pc.md)
    - [Running a Server using Docker (For Dedicated Servers)](on-docker.md)
    - [Running a Server on a Raspberry Pi](on-the-rpi.md)
2. Head over to the [Configuring The Server](configuration.md) page to learn how to set it up according to your needs and preferences.
3. (Optional) [Generate a custom world](../world-generation.md).