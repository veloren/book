# Building

Veloren is primary an action-adventure RPG rather than a sandbox building game. Despite this, it does provide some
features that allow for limited in-game building.

## Build Mode

Build mode can be enabled with the `/build` command. When enabled, players can add (Right Click), remove (Left Click)
and pick (Middle Click) blocks in build regions for which they have permission. Build mode is not considered a canonical
part of the Veloren experience. It is a fun feature to use if you wish to experiment with the game's features.

### Regions

*TODO: Add documentation for region manipulation commands*

By default, there is a region that covers the entire world named `world`. You can enable permissions for it with
`/permit_build world` (this requires admin permissions).

### The `vox_spawn` branch

There exists a highly experimental branch called `vox_spawn`. It adds a client-side command that hooks into build mode
and uses it to "3D print" (row by row) [`.vox`](https://ephtracy.github.io/index.html?page=mv_main) models into the game
world. Generally, this process is fairly quick and all but the largest models typically take less than a minute to fully
spawn in. If you're an admin wanting to spawn structures into your world, it might be worth designing the structures
with a voxel modelling tool first and using `vox_spawn` to spawn them into the world to avoid the structure being lost
forever if the chunk unloads.

## Persistence

By default, Veloren does not persist changes made to the world. Unloading a chunk will lead to any changes made to it
being lost. However, as of 2021-08-14, Veloren has an experimental persistence system built into the game. It is not
enabled by default.

### Enabling

To enable persistent building, the `persistent_world` feature must be enabled when compiling the game (this is enabled
by default). In addition, the server must have the `experimental_terrain_persistence` flag set to `true` in the server
`settings.ron` file (this also works for singleplayer). This flag does not exist in the settings file by default and
must be added manually by the server owner.

Once enabled, you will see a log entry in the server console (or the main game console if in singleplayer) on startup,
as well as a message when toggling build mode.

### **Important** Information

The experimental terrain persistence is not an officially supported feature. While some attempts are made to not
arbitrarily break things between subsequent updates, *this is not a guarantee* and it is quite possible that updates may
corrupt, delete, or otherwise break persisted terrain data at any time. Additionally, no stability guarantees are made
(although you can still report bugs relating to the feature): enabling the feature may result in crashes, instability,
lag, etc.

The experimental terrain persistence feature is not simply unfinished: it is a stop-gap until a proper, more restricted
player-oriented building system is developed. It is not intended to evolve into such a system, nor is it intended to be
compatible with it: it exists only to facilitate server admins adding minor customisation to their servers, to be
enjoyed by players, until such a time at which a reliable, forward-compatible, player-oriented building system is
developed.

As one might expect, updates to the game can often subtly (or not so subtly as the case may be) break persisted terrain
data. For example, significant changes to world generation may result in structures built with the system appearing at
the wrong altitude, clipping inside of other generated structures, or perhaps even overridden/removed entirely. As
before, no guarantees are made about this. If world generation changes significantly or you switch out the map file, the
best thing to do is probably to remove the terrain directory and start afresh.

### How does it work?

On server startup, the terrain persistence system creates the `{DATADIR}/terrain/` directory if it does not exist
already where `{DATADIR}` is the server's data directory (`userdata/singleplayer/` or `userdata/server/`, in most
cases). This directory can be changed using the `VELOREN_TERRAIN` environment variable.

The feature hooks into various actions performed as the game runs: newly loaded chunks will have persisted changes
applied on top of them, and unloaded chunks will have their changes persisted to disk. Any modifications made via either
build mode or the `/make_sprite` and `/make_block` commands will be recorded. The same does not apply to other kinds of
block modification: blocks mined with the pickaxe or discolored/destroyed with explosions will not be recorded. This
means that players are not able to permanently damage structures spawned in by server admins.

See the [original merge request](https://gitlab.com/veloren/veloren/-/merge_requests/2662) for more detailed technical
information.

### What is it for?

As mentioned, the terrain persistence system is not intended to be player-facing. Build mode is neither intuitive nor
well-integrated into the rest of the game. We do not account for it in any of the game's existing mechanics, and it is
even possible to cause the server and clients to crash, lag, or freeze if building at an altitude that is too high or
low.

We intend terrain persistence to be a way for server admins to customise the experience of the server for players with
pre-built structures that may be interacted with. Below are a few ideas to get you started:

- Gliding courses demarcated with pillars and hoops for glider racing

- A custom spawn zone complete with crafting stations and meeting areas for players

- Mining challenges (using mineable blocks like `WeakRock` and ores) that players can partake in. Because mining is not
  persisted, any mined blocks will naturally regenerate when the chunk reloads!

- Custom mazes and climbing/jumping challenges for players with rewards in the form of chests/ores/etc.

- Pixel artwork and sculptures dotted around the world [for players to find](https://en.wikipedia.org/wiki/Geocaching)

- Visual customisations to existing world structures like towns and dungeons that make them more interesting to explore

If you do something neat with this feature, feel free to tell us! It might even get featured in the weekly blog!





















