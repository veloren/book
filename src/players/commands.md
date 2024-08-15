# Commands

All commands that can be executed in-game are listed below, note that many commands require Admin or Moderator permissions. Arguments surrounded by `<>` are required, `[]` indicates an optional argument.

>Note: The tables below are auto-generated from the commands within the Veloren source code using the command `cargo cmd-doc-gen`.

<style>
    table {
        width: 100%;
    }
</style>

## Server Commands

|Command|Description|Requires|Arguments|
|-|-|-|-|
|/adminify|Temporarily gives a player a restricted admin role or removes the current one (if not given)|Admin|`<player> [role]`|
|/airship|Spawns an airship|Admin|`[kind] [destination_degrees_ccw_of_east]`|
|/alias|Change your alias|Moderator|`<name>`|
|/area_add|Adds a new build area|Admin|`<name> <kind> <xlo> <xhi> <ylo> <yhi> <zlo> <zhi>`|
|/area_list|List all build areas|Admin||
|/area_remove|Removes specified build area|Admin|`<name> <kind>`|
|/aura|Create an aura|Admin|`<aura_radius> [aura_duration] [new_entity] [aura_target] <aura_kind> [aura spec]`|
|/ban|Ban a player with a given username, for a given duration (if provided).  Pass true for overwrite to alter an existing ban..|Moderator|`<player> [overwrite] [ban duration] [message]`|
|/battlemode|Set your battle mode to: <ul><li> pvp (player vs player)</li><li>pve (player vs environment)</li></ul> If called without arguments will show current battle mode.||`[battle mode]`|
|/battlemode_force|Change your battle mode flag without any checks|Admin|`<battle mode>`|
|/body|Change your body to different species|Admin|`<body>`|
|/buff|Cast a buff on player|Admin|`<buff> [strength] [duration] [buff data spec]`|
|/build|Toggles build mode on and off|||
|/campfire|Spawns a campfire|Admin||
|/clear_persisted_terrain|Clears nearby persisted terrain|Admin|`<chunk_radius>`|
|/create_location|Create a location at the current position|Moderator|`<name>`|
|/debug_column|Prints some debug information about a column|Admin|`<x> <y>`|
|/debug_ways|Prints some debug information about a column's ways|Admin|`<x> <y>`|
|/delete_location|Delete a location|Moderator|`<name>`|
|/destroy_tethers|Destroy all tethers connected to you|Admin||
|/disconnect_all_players|Disconnects all players from the server|Admin|`<confirm>`|
|/dismount|Dismount if you are riding, or dismount anything riding you|Admin|`<entity>`|
|/dropall|Drops all your items on the ground|Moderator||
|/dummy|Spawns a training dummy|Admin||
|/explosion|Explodes the ground around you|Admin|`<radius>`|
|/faction|Send messages to your faction||`[message]`|
|/give_item|Give yourself some items.
For an example or to auto complete use Tab.|Admin|`<item> [num]`|
|/goto|Teleport to a position|Admin|`<x> <y> <z> [Dismount from ship]`|
|/group|Send messages to your group||`[message]`|
|/group_invite|Invite a player to join a group||`<player>`|
|/group_kick|Remove a player from a group||`<player>`|
|/group_leave|Leave the current group|||
|/group_promote|Promote a player to group leader||`<player>`|
|/health|Set your current health|Admin|`<hp>`|
|/help|Display information about commands||`[[/]command]`|
|/into_npc|Convert yourself to an NPC. Be careful!|Admin|`<entity_config>`|
|/join_faction|Join/leave the specified faction||`[faction]`|
|/jump|Offset your current position|Admin|`<x> <y> <z> [Dismount from ship]`|
|/kick|Kick a player with a given username|Moderator|`<player> [message]`|
|/kill|Kill yourself|||
|/kill_npcs|Kill the NPCs|Admin|`[radius] [--also-pets]`|
|/kit|Place a set of items into your inventory.|Admin|`<kit_name>`|
|/lantern|Change your lantern's strength and color|Admin|`<strength> [r] [g] [b]`|
|/light|Spawn entity with light|Admin|`[r] [g] [b] [x] [y] [z] [strength]`|
|/lightning|Lightning strike at current position|Admin||
|/location|Teleport to a location||`<name>`|
|/make_block|Make a block at your location with a color|Admin|`<block> [r] [g] [b]`|
|/make_npc|Spawn entity from config near you.
For an example or to auto complete use Tab.|Admin|`<entity_config> [num]`|
|/make_sprite|Make a sprite at your location|Admin|`<sprite>`|
|/make_volume|Create a volume (experimental)|Admin|`[size]`|
|/motd|View the server description|||
|/mount|Mount an entity|Admin|`<entity>`|
|/object|Spawn an object|Admin|`<object>`|
|/permit_build|Grants player a bounded box they can build in|Admin|`<area_name>`|
|/players|Lists players currently online|||
|/portal|Spawns a portal|Admin|`<x> <y> <z> [requires_no_aggro] [buildup_time]`|
|/region|Send messages to everyone in your region of the world||`[message]`|
|/reload_chunks|Reloads chunks loaded on the server|Admin|`[chunk_radius]`|
|/remove_lights|Removes all lights spawned by players|Admin|`[radius]`|
|/repair_equipment|Repairs all equipped items|Admin||
|/reset_recipes|Resets your recipe book|Admin||
|/respawn|Teleport to your waypoint|Moderator||
|/revoke_build|Revokes build area permission for player|Admin|`<area_name>`|
|/revoke_build_all|Revokes all build area permissions for player|Admin||
|/rtsim_chunk|Display information about the current chunk from rtsim|Admin||
|/rtsim_info|Display information about an rtsim NPC|Admin|`<npc index>`|
|/rtsim_npc|List rtsim NPCs that fit a given query (e.g: simulated,merchant) in order of distance|Admin|`<query> [max number]`|
|/rtsim_purge|Purge rtsim data on next startup|Admin|`<whether purging of rtsim data should occur on next startup>`|
|/rtsim_tp|Teleport to an rtsim npc|Admin|`<npc index> [Dismount from ship]`|
|/safezone|Creates a safezone|Moderator|`[range]`|
|/say|Send messages to everyone within shouting distance||`[message]`|
|/scale|Scale your character|Admin|`<factor> [reset_mass]`|
|/server_physics|Set/unset server-authoritative physics for an account|Moderator|`<player> [enabled]`|
|/set_motd|Set the server description|Admin|`[locale] [message]`|
|/ship|Spawns a ship|Admin|`[kind] [Whether the ship should be tethered to the target (or its mount)] [destination_degrees_ccw_of_east]`|
|/site|Teleport to a site|Moderator|`<site> [Dismount from ship]`|
|/skill_point|Give yourself skill points for a particular skill tree|Admin|`<skill tree> [amount]`|
|/skill_preset|Gives your character desired skills.|Admin|`<preset_name>`|
|/spawn|Spawn a test entity|Admin|`<alignment> <entity> [amount] [ai] [scale] [tethered]`|
|/sudo|Run command as if you were another entity|Moderator|`<entity> <[/]command> [args...]`|
|/tell|Send a message to another player||`<player> [message]`|
|/tether|Tether another entity to yourself|Admin|`<entity> [automatic length]`|
|/time|Set the time of day|Admin|`[time]`|
|/time_scale|Set scaling of delta time|Admin|`[time scale]`|
|/tp|Teleport to another entity|Moderator|`[entity] [Dismount from ship]`|
|/unban|Remove the ban for the given username|Moderator|`<player>`|
|/version|Prints server version|||
|/waypoint|Set your waypoint to your current position|Admin||
|/weather_zone|Create a weather zone|Admin|`<weather kind> [radius] [time]`|
|/whitelist|Adds/removes username to whitelist|Moderator|`<add/remove> <player>`|
|/wiring|Create wiring element|Admin||
|/world|Send messages to everyone on the server||`[message]`|

## Voxygen Client Commands

|Command|Description|Requires|Arguments|
|-|-|-|-|
|/clear|Clears all messages in chat. Affects all chat tabs.|||
|/experimental_shader|Toggles an experimental shader.||`[Shader]`|
|/help|Display information about commands||`[[/]command]`|
|/mute|Mutes chat messages from a player.||`<player>`|
|/unmute|Unmutes a player muted with the 'mute' command.||`<player>`|

## References

All the parameters that can be used in the commands that can be executed in-game are listed below.

|Parameter|Description|Link|
|-|-|-|
|`ai`| spawned entity has an agent/ai, true/false||
|`alignment`|`wild`, `enemy`, `npc`, `pet`|[code reference](https://docs.veloren.net/src/veloren_common/cmd.rs.html#70)|  
|`amount`| number ||
|`area_name`| name of an area||
|`args...`|additional parameters, e.g. in `/sudo player tell Hello, how are you?` `args...` would be `Hello, how are you?`||
|`ban duration`| duration of the ban, e.g. `3d2h30m`||
|`battle mode`| "pvp" (player vs player) or "pve" (player vs environment)||
|`block`| name of block |[blocks](https://docs.veloren.net/veloren_common/terrain/block/enum.BlockKind.html)|  
|`buff`| Name of Buff; be careful, docs use CamelCase and command expects snake_case, e.g. docs: "IncreaseMaxHealth" command: "increase_max_health"| [docs reference](https://docs.veloren.net/veloren_common/comp/buff/enum.BuffKind.html#)|
|`[/]command`| e.g. `give_item` or `/give_item`||
|`confirm`| "confirm", to confirm||
|`destination_degrees_ccw_of_east`|||
|`duration`| duration in seconds||
|`enabled`| boolean, true/false||
|`entity_config`|path to the entity starting from `veloren.assets.common.entity` with `.` as separator of directory names; with the prefix `common.entity.`! e.g.: `common.entity.dungeon.fallback.boss`|[folder with the entities](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/entity)|
|`faction`|String of Characters, e.g. "Hello"||
|`hp`| Health Points as number||
|`item`| path to the item starting from `veloren.assets.common.items` with `.` as separator of directory names; with the prefix `common.items.`! e.g.: `common.items.armor.assassin.belt`  | [folder with the items](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/items) |
|`kit_name`| name of a kit, e.g. `debug` |[definition of the kits](https://gitlab.com/veloren/veloren/-/blob/master/assets/server/manifests/kits.ron)|  
|`message`| String of Characters, e.g. "Hello"||
|`name`| String of Characters, e.g. "Hello" ||
|`num`| number ||
|`object`| name of the object |[definition of objects](https://docs.veloren.net/veloren_common/comp/body/object/enum.Body.html)|  
|`overwrite`| set to true to overwrite previous ban||
|`player`| Name of Player's Character||
|`preset_name`|path to the skillset starting from `veloren.assets.common.skillset` with `.` as separator of directory names; with the prefix `common.skillset.`! e.g.: `common.skillset.preset.max.sceptre`  | [folder with the skillset](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/skillset) |
|`radius`| a number to define the radius, has to be higher than 0 and lower than 512||
|`r, g, b`| red, green, blue; numbers used to define a color||
|`role`| "admin" or "moderator"||
|`skill tree`| name of a skill tree, e.g. `general`|[skill tree names from code](https://docs.veloren.net/src/veloren_server/cmd.rs.html#2887)|  
|`sprite`| name of the sprite |[definition of sprites](https://docs.veloren.net/veloren_common/terrain/sprite/enum.SpriteKind.html)|  
|`strength`| number||
|`time`|options: `midnight`, `night`, `dawn`, `morning`, `day`, `noon`, `dusk` or %H:%M format e.g. `12:21`|[code reference](https://docs.veloren.net/src/veloren_server/cmd.rs.html#940)|  
|`username`| username of a player||
|`xhi`| point x on hi||
|`xlo`| point x on lo ||
|`x` | point x||
|`yhi`| point y on hi||
|`ylo`| point y on lo||
|`y`| point y||
|`zhi`| point z on hi||
|`zlo`| point z on lo||
|`z`| point z||
