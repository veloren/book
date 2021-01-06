# Project Architecture

When we started developing Veloren, we set out to with several aims in mind.

- Modularity: The project should be composed of many interlocking pieces
- Performance: The project should avoid architectural choices that constrain performance
- Avoiding lock-in: The project should avoid forcing the use of certain components where possible

## Crates

Veloren is split into several Rust crates. The purpose of this is twofold.

1) Reduce compilation time by allowing parallel processing of crates during compilation

2) Allow users of the Veloren ecosystem to only depend on specific parts of the project

## Frontends

If you've spent any time around games with an active modding scene, you've no doubt come across games that have had
entirely new graphical frontends written for them that allow you to play the game using different graphics or that view
interesting game data that the default game doesn't usually display, such as the Legends Viewer of Dwarf Fortress. These
frontends are often hackily constructed, requiring direct memory access to the game's RAM, lack significant features, or
require the main game to be running in parallel.

Veloren ditches this approach and instead makes frontends a first-class abstraction. `voxygen`, the default graphical
client frontend, has no inherent coupling with the internal `client` library. It's possible to write entirely new
frontends that display the game's contents in a vastly different way on top of the generic `client` library. Examples of
such alternative frontends include:

- [Teloren, a command-line frontend with nethack-style graphics](https://github.com/zesterer/teloren)
- [`chat-cli`, a chat-only command-line frontend](https://gitlab.com/veloren/veloren/-/blob/master/client/examples/chat-cli/main.rs)

(Is something missing from this list? Feel free to add it)

### `voxygen`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_voxygen)

Voxygen is the default client frontend for Veloren and is the program that users most commonly interact with. It is a
fully maintained and features a fully 3D view of Veloren's world and makes use of all of the game's client features.

### `server-cli`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_server_cli)

`server-cli` is the default server frontend for Veloren. It allows running Veloren servers via a simple command-line
interface that includes both a 'basic' mode (streaming output to `stdout`/`stderr`) and a more complex mode that allows
the inputting of server commands via a simple ncurses-style terminal interface.

## Backends

As mentioned, Veloren implements core gameplay functionality through headless developer-facing libraries. These are:

### `server`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_server)

The core server implementation of Veloren, with all the bells and whistles. It includes APIs for server frontends to
query game state, inject events (such as server-wide broadcasts), and load plugins. In the future, we imagine a plethora
of server frontends catering to many requirements: simple graphical frontends for players wanting to host a LAN game
with friends, or a powerful CLI server frontend backed by a web control panel that allows precise control over game
state and advanced features such as live maps or civilisation stats viewable on the web.

### `client`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_client)

The core client implementation of Veloren. It is non-prescriptive about how a client frontend displays data and allows
clients to connect to servers through one of many 'modes' including chat-only, spectator, and character. The default
client frontend, Voxygen, is 3D, but there's no reason as to why other client frontends couldn't implement displaying
the world using isometric graphics, Dwarf Fortress style layered 2D graphics, or any other representation one could
imagine.

### `world`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_world)

The core world generation implementation of Veloren. The use of this crate is a little more nebulous since world
generation and simulation are under active development, but this crate is intended to allow viewing, generating, and
simulating a Veloren world without a client or server being associated with it. In the future we imagine frontends
existing that allow viewing aspects of world history like Dwarf Fortress' Legends Viewer, or editing of world data to
allow for custom worlds and scenarios.

## Utility crates

Many other crates in the ecosystem are utility crates that contain functionality common to many other crates. These are
not intended for consumption by anything but the core Veloren libraries and should be treated as an implementation
detail. These are:

### `common` (and its sub-crates)

[_Read the docs for this crate_](https://docs.veloren.net/veloren_common)

Implements behaviour and contains definitions that are common to both client and server.

### `network`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_network)

Contains the raw implementation of Veloren's networking utilities.

## Plugins

Veloren has recently gained a plugin API that allows for the development of additional features on top of the core
Veloren experience. While the plugin API is still extremely experimental, we envisage it soon becoming the standard way
to expand the game's features. Plugins are written in any language that may compile to Web Assembly (WASM), although
Rust is so far the only language with official support and bindings. Plugins are fully sandboxed and get shared with
clients when connecting to a server. Plugins may have server-side and client-side behaviour contained within the same
package.

There are several crates associated with plugins:

### `plugin-rt`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_plugin_rt)

The core plugin runtime. This crate facilitates communication with the host engine and manages plugin hooks and IO.

### `plugin-api`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_plugin_api)

Contains type defintions that constitute the plugin interface used to communicate with Veloren. This includes types and
structures used to represent in-game state and communicate about changes in that state.

### `plugin-derive`

[_Read the docs for this crate_](https://docs.veloren.net/veloren_plugin_derive)

Includes utility procedural macros for setting up a plugin, automating some of the more complex APIs provided by
`plugin-rt`.
