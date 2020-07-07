# Project Structure

Veloren is designed in an extremely modular manner. You can think of it more as an ecosystem of interconnected projects than a single project. At its heart are a variety of Rust libraries (crates) hosted in the main directory.

## common

[_Read the docs for this crate_](https://docs.veloren.net/veloren_common)

`common` is a crate that contains functionality common to many parts of the project. This includes things like networking code, the physics system, voxel manipulation code and other utility code. If something occurs both client-side and server-side, it's a safe bet that it's implemented in `common`.

## server

[_Read the docs for this crate_](https://docs.veloren.net/veloren_server)

In Veloren, there is no single 'server program'. Instead, there are a variety of server front-end programs that make use of `server`, a library that implements the server-side component of Veloren. This allows anybody to implement their own server front-end, and will permit servers with web control panels, web status interfaces, command-line interfaces, and GUI interfaces for LAN games.

## server-cli

[_Read the docs for this crate_](https://docs.veloren.net/veloren_server_cli)

This crate is a command-line only front-end for the `server` crate. It's very simple, and serves as the vanilla, default front-end for Veloren servers.

## client

[_Read the docs for this crate_](https://docs.veloren.net/veloren_client)

Similar to `server`, `client` is a library that implements the client-side component of Veloren. It is not tied to any particular front-end and instead is designed to be a generic client implementation upon which graphical front-ends can be built.

## chat-cli

[_Read the docs for this crate_](https://docs.veloren.net/veloren_chat_cli)

`chat-cli` is a command-line client front-end that permits chat communication with a Veloren server from the user's console. It doesn't allow the user to control a character on a server, but it does allow the user to talk with other players via the server's chat system.

## voxygen

[_Read the docs for this crate_](https://docs.veloren.net/veloren_voxygen)

Voxygen is the best-known crate in the Veloren ecosystem, particularly to those that spend more time playing the game than developing it. It is the primary client front-end for Veloren and implements a fully 3D view of the game world. It is the reference implementation of the game and the program that virtually all users are intended to interact with.

## world

[_Read the docs for this crate_](https://docs.veloren.net/veloren_world)

This crate implements the world generation and simulation aspects of Veloren. It is currently used only by the `server` crate, but has been kept separate from the rest of the ecosystem such that third-party tools may make use of it for things like visualising the state of a world.

## network

[_Read the docs for this crate_](https://docs.veloren.net/veloren_network/)

Crate to handle high level networking of messages with different requirements and priorities over a number of protocols.
