# Writing a plugin

This guide will show you how to write a simple server-side (and client-side) plugin for Veloren. Please note that both
the plugin API and the process for plugin development is under active development and we currently make no stability
guarantees about APIs, tooling, etc. If in doubt, please check this page to find the latest information.

It's also important to remember that the plugin API is still very new and not much functionality is supported. We hope
that by publishing this tutorial and encouraging people to experiment with the plugin API that we might start to build
consensus on a future direction and future features for the API. If you're interested in helping out, reach out to us!

## Example code

You can find the code for this example plugin [here](https://gitlab.com/veloren/my_plugin).

## Requirements

- Knowledge of basic Rust

- Ability to use simple unix-like terminals and commands

- An *up-to-date* instance of Veloren (a local repository is preferred for compatibility purposes)

*Note: Having problems? Feel free to ask in #learning on the Veloren Discord server.*

## Overview

Plugins for Veloren are written in Web Assembly (herein referred to as 'WASM'), a code format originally designed for
high-performance, memory-safe web executables, but also perfectly suited to a variety of other applications. This
implies the following things about Veloren plugins:

- They are [sandboxed](https://en.wikipedia.org/wiki/Sandbox_(computer_security))

- WASM does not yet have a well-defined host ABI, so communication with the game engine is event-driven

- They are portable and will work on all architectures and platforms

- Plugins are stored server-side and get sent to clients when they connect to a server

## Setting up

We assume that you're using either a Unix-like system, or some environment with similar properties (like WSL or Cygwin).

*Note: from now on, where you see `my_plugin`, replace this with the name of your plugin.*

First, create a new cargo project.

```
cargo new --lib my_plugin
```

Plugins have multiple entrypoints (i.e: ways to request things from the plugin) that may be invoked by the game. To
ensure we make all of these appropriately accessible to the game, add the following to `Cargo.toml`:

```toml
[lib]
crate-type = ["cdylib"]
```

Because Veloren's plugin API is unstable, we're going to depend on Veloren's git repository. In `Cargo.toml`, add the
following to `[dependencies]`:

```toml
veloren-plugin-rt = { git = "https://gitlab.com/veloren/veloren.git" }
```

The `veloren-plugin-rt` crate wraps the plugin API, event handler derive macros, and a series of other useful bits and
pieces together into what we colloquially call the 'plugin runtime' (rt).

Because we need to compile our plugin to a WASM module, first ensure that the appropriate toolchain is installed (and
works) by running the following:

```
cargo build --target wasm32-unknown-unknown
```

If you get a `error[E0463]: can't find crate for `core`, you can install the relevant version of `core` using the
following `rustup` command:

```
rustup target add wasm32-unknown-unknown
```

You will also require the nightly version of the Rust compiler. If you are not already using nightly, you can set a
directory-specific override for this with the following command (ensure you are in the `my-plugin` directory before
running this):

```
rustup override set nightly
```

## Packaging the plugin

Plugins are packaged in uncompressed (compression may later be supported, but is not currently) `.tar` archives. Each
archive contains a file with the extension `.plugin.toml` that specifies plugin metadata and any number of WASM modules
(conventionally with the extension `.wasm`). `plugin.toml` looks like the following:

```toml
# The name of the plugin (lowercase, no spaces)
name = "my_plugin"

# A list of paths to WASM modules in the plugin

modules = []

# Other plugins that this plugin depends on (currently not supported)
dependencies = []
```
```

We'll want to start off by creating a single module. Let's call it 'main'. Start off by adding it to the `modules` set
like so:

```toml
modules = ["my_plugin.wasm"]
```

To package the plugin, we can copy the compiled WASM module from the previous steps located at
`target/wasm32-unknown-unknown/debug/my_plugin.wasm` into a packaging directory of your own making, along with the
`plugin.toml`, and then use the `tar` command (or your favourite tar-capable archive manager) to package them up. The
following command, executed from within the packaging directory, should work fine:

```
tar -cvf ../my_plugin.plugin.tar *
```

You might want to automate this process with a script because you'll be doing it often. A simple shell script would
likely suffice.

In the future, we'd like to create a cargo subcommand that automates this step, but this hasn't yet been done.

For reference, I just use a simple shell script with the following contents:

```sh
cargo build --target wasm32-unknown-unknown
cp target/wasm32-unknown-unknown/debug/my_plugin.wasm build_dir/.
cd build_dir
tar -cvf ../my_plugin.plugin.tar plugin.toml my_plugin.wasm
cd ..
```

## Running the plugin

To run the plugin, simply copy it into the `plugins` directory in the asset directory of Veloren. The plugin will be
sent over the network to connecting clients, so it's important that it's accessible to the server only (or Voxygen if
you wish to run the plugin in singleplayer).

In my case, this just involves copying the final archive to `assets/plugins/my_plugin.tar` within my local repository
and running the game.

When a server starts (or when singleplayer is started) you should see messages similar to the following in the console:

```
Jun 11 10:05:27.723  INFO veloren_common_state::plugin: Searching "/home/zesterer/projects/veloren/assets/plugins" for plugins...
Jun 11 10:05:27.723  INFO veloren_common_state::plugin: Loading plugin at "/home/zesterer/projects/veloren/assets/plugins/my_plugin.plugin.tar"
Jun 11 10:05:27.733  INFO veloren_common_state::plugin: Loaded plugin 'my_plugin' with 1 module(s)
```

If you got this far, congratulations: you've officially created a plugin for the game!

## Handling events

At this point, it's worth taking a brief look over the documentation for the plugin API,
[here](https://docs.veloren.net/veloren_plugin_api/). Although we are depending on `veloren-plugin-rt`, the API crate is
exported by the runtime crate. We're now ready to write our first event handler for our plugin.

In `lib.rs`, enter the following:

```rs
use veloren_plugin_rt::{*, api::{*, event::*}};

#[event_handler]
pub fn on_load(load: PluginLoadEvent) {
    emit_action(Action::Print(String::from("Hello, Veloren!")));
}
```

This is worth taking a little time to explain, especially if you're not so familiar with Rust.

```rs
use veloren_plugin_rt::{event_handler, api::event::*};
```

Here, we import the necessary macros, types and functions we need to write our plugin.

```rs
#[event_handler]
pub fn on_load(load: PluginLoadEvent) { ... }
```

Here, we declare a new functon that accepts a
[`PluginLoadEvent`](https://docs.veloren.net/veloren_plugin_api/event/struct.PluginLoadEvent.html). We use the
`event_handler` attribute to tell the runtime that we'd like to use this function as an *event handler* that will be
called when the event of the specified type occurs.

```rs
emit_action(Action::Print(String::from("Hello, Veloren!")));
```

We've already mentioned a way to receive inputs to the plugin, via event handlers. How do we act upon those events?
Through `Action`s! An `Action` is a thing that you want the server to perform, and you can use the `emit_action` and
`emit_actions` function to have the server perform them.

If you run the server with the newly compiled plugin, you should now see the following in the server console:

```
Jun 11 10:20:16.087  INFO veloren_common_state::plugin::module: Hello, Veloren!
```

If you're running the game in singleplayer, you'll see this twice: once for the internal server, and once for the
internal client (once it's received the plugin from the server).

## Chat commands

We're going to expand our plugin such that when we type `/ping` into the chat, the player gets the response `Pong!`.
Why? No specific reason, but it's a good demonstration of chat functionality.

Add the following to `lib.rs`:

```rs
#[event_handler]
pub fn on_command_ping(chat_cmd: ChatCommandEvent) -> Result<Vec<String>, String> {
    Ok(vec![String::from("Pong!")])
}
```

The only thing to explain here is something that might be a little unexpected given the previous example: the return
type.

Every implementer of the `Event` trait (such as `PluginLoadEvent`, `ChatCommandEvent`, etc.) also specifies a response
that is required of it. In the case of `PluginLoadEvent`, the response is simply `()`, which is why we didn't need to
explicitly return anything from the `on_load` event. The return type for `ChatCommandEvent` is different, however: it
expects either a list of message responses to the command, or an error message should the command syntax be invalid.

If you run the game with the newly compiled plugin and then enter the world, you should be able to type `/ping` into the
chat and receive a `Pong!` as a response.

## Global state

There's a final feature of the plugin API to talk about before this tutorial ends: the management of *global state*.

If you're more than a little familiar with Rust, that might sound like a scary word: but given that event handlers are
themselves 'global' (i.e: they're communicating with just a single instance of the game that loaded the plugin they are
in), it also makes sense that any data you want to store about the state of the game in your plugin must also be global.

Thankfully, the plugin API has a feature for this!

To define the type of your global state, you can add the `global_state` attribute above a type like so:

```rs
#[global_state]
#[derive(Default)]
struct State {
	ping_count: u64,
}
```

It's also important that it implements the `Default` trait: this is needed because we do not yet provide a way for the
global state to be initialised via the `on_load` event handler.

To access this global state in an event handler, simply add a second parameter to the event handler like so:

```rs
#[event_handler]
pub fn on_command_ping(chat_cmd: ChatCommandEvent, state: &mut State) -> Result<Vec<String>, String> {
    state.ping_count += 1;
	Ok(vec![format!("Pong! The total number of pings so far is {}", state.ping_count)])
}
```

Now any player can use `/ping` and the server will tell them how many times the command has been used since the server
started!

## Future topics

Possible future topics to cover include:

- More event handlers
- Modifying entity attributes
- Persistent plugin state
- Controlling NPC AI
- Plugin-specific assets
