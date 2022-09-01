# Commands
All commands that can be executed in-game are listed below, note that many commands require Admin or Moderator permissions. Arguments surrounded by `<>` are required, `[]` indicates an optional argument.

>Note: The table below is auto-generated from the commands within the Veloren source code using the command `cargo cmd-doc-gen`.

|Command|Description|Requires|Arguments|
|-|-|-|-|
|/adminify|Temporarily gives a player a restricted admin role or removes the current one (if not given)|Admin|`<player> [role]`|
|/airship|Spawns an airship|Admin|`[destination_degrees_ccw_of_east]`|
|/alias|Change your alias|Moderator|`<name>`|
|/buff|Cast a buff on player|Admin|`<buff> [strength] [duration]`|
|/ban|Ban a player with a given username, for a given duration (if provided).  Pass true for overwrite to alter an existing ban..|Moderator|`<player> [overwrite] [ban duration] [message]`|
|/battlemode|Set your battle mode to: * pvp (player vs player) * pve (player vs environment). If called without arguments will show current battle mode.||`[battle mode]`|
|/battlemode_force|Change your battle mode flag without any checks|Admin|`<battle mode>`|
|/build|Toggles build mode on and off|||
|/build_area_add|Adds a new build area|Admin|`<name> <xlo> <xhi> <ylo> <yhi> <zlo> <zhi>`|
|/build_area_list|List all build areas|Admin||
|/build_area_remove|Removes specified build area|Admin|`<name>`|
|/campfire|Spawns a campfire|Admin||
|/debug_column|Prints some debug information about a column|Moderator|`<x> <y>`|
|/disconnect_all_players|Disconnects all players from the server|Admin|`<confirm>`|
|/dropall|Drops all your items on the ground|Moderator||
|/dummy|Spawns a training dummy|Admin||
|/explosion|Explodes the ground around you|Admin|`<radius>`|
|/faction|Send messages to your faction||`[message]`|
|/give_item|Give yourself some items. For an example or to auto complete use Tab.|Admin|`<item> [num]`|
|/goto|Teleport to a position|Admin|`<x> <y> <z>`|
|/group|Send messages to your group||`[message]`|
|/group_invite|Invite a player to join a group||`<player>`|
|/group_kick|Remove a player from a group||`<player>`|
|/group_leave|Leave the current group|||
|/group_promote|Promote a player to group leader||`<player>`|
|/health|Set your current health|Admin|`<hp>`|
|/help|Display information about commands||`[[/]command]`|
|/home|Return to the home town|Moderator||
|/join_faction|Join/leave the specified faction||`[faction]`|
|/jump|Offset your current position|Admin|`<x> <y> <z>`|
|/kick|Kick a player with a given username|Moderator|`<player> [message]`|
|/kill|Kill yourself|||
|/kill_npcs|Kill the NPCs|Admin||
|/kit|Place a set of items into your inventory.|Admin|`<kit_name>`|
|/lantern|Change your lantern's strength and color|Admin|`<strength> [r] [g] [b]`|
|/light|Spawn entity with light|Admin|`[r] [g] [b] [x] [y] [z] [strength]`|
|/make_block|Make a block at your location with a color|Admin|`<block> [r] [g] [b]`|
|/make_npc|Spawn entity from config near you. For an example or to auto complete use Tab.|Admin|`<entity_config> [num]`|
|/make_sprite|Make a sprite at your location|Admin|`<sprite>`|
|/motd|View the server description||`[message]`|
|/object|Spawn an object|Admin|`<object>`|
|/permit_build|Grants player a bounded box they can build in|Admin|`<area_name>`|
|/players|Lists players currently online|||
|/region|Send messages to everyone in your region of the world||`[message]`|
|/reload_chunks|Reloads all chunks loaded on the server|Admin||
|/remove_lights|Removes all lights spawned by players|Admin|`[radius]`|
|/revoke_build|Revokes build area permission for player|Admin|`<area_name>`|
|/revoke_build_all|Revokes all build area permissions for player|Admin||
|/safezone|Creates a safezone|Moderator|`[range]`|
|/say|Send messages to everyone within shouting distance||`[message]`|
|/server_physics|Set/unset server-authoritative physics for an account|Moderator|`<player> [enabled]`|
|/set_motd|Set the server description|Admin|`[message]`|
|/ship|Spawns a ship|Admin|`[destination_degrees_ccw_of_east]`|
|/site|Teleport to a site|Moderator|`<site>`|
|/skill_point|Give yourself skill points for a particular skill tree|Admin|`<skill tree> [amount]`|
|/skill_preset|Gives your character desired skills.|Admin|`<preset_name>`|
|/spawn|Spawn a test entity|Admin|`<alignment> <entity> [amount] [ai]`|
|/sudo|Run command as if you were another player|Moderator|`<player> <[/]command> [args...]`|
|/tell|Send a message to another player||`<player> [message]`|
|/time|Set the time of day|Admin|`[time]`|
|/tp|Teleport to another player|Moderator|`[player]`|
|/unban|Remove the ban for the given username|Moderator|`<player>`|
|/version|Prints server version|||
|/waypoint|Set your waypoint to your current position|Admin||
|/whitelist|Adds/removes username to whitelist|Moderator|`<add/remove> <player>`|
|/wiring|Create wiring element|Admin||
|/world|Send messages to everyone on the server||`[message]`|
|/make_volume|Create a volume (experimental)|Admin||
|/location|Teleport to a location||`<name>`|
|/create_location|Create a location at the current position|Moderator|`<name>`|
|/delete_location|Delete a location|Moderator|`<name>`|


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
|`entity_config`|path to the entity starting from `veloren.assets.common.entity` with `.` as seperator of directory names; with the prefix `common.entity.`! e.g.: `common.entity.dungeon.fallback.boss`|[folder with the enities](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/entity)|  
|`faction`|String of Characters, e.g. "Hello"||
|`hp`| Health Points as number||
|`item`| path to the item starting from `veloren.assets.common.items` with `.` as seperator of directory names; with the prefix `common.items.`! e.g.: `common.items.armor.assassin.belt`  | [folder with the items](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/items) |  
|`kit_name`| name of a kit, e.g. `debug` |[definition of the kits](https://gitlab.com/veloren/veloren/-/blob/master/assets/server/manifests/kits.ron)|  
|`message`| String of Characters, e.g. "Hello"||  
|`name`| String of Characters, e.g. "Hello" ||  
|`num`| number ||  
|`object`| name of the object |[definition of objects](https://docs.veloren.net/veloren_common/comp/body/object/enum.Body.html)|  
|`overwrite`| set to true to overwrite previous ban||  
|`player`| Name of Player's Character||  
|`preset_name`|path to the skillset starting from `veloren.assets.common.skillset` with `.` as seperator of directory names; with the prefix `common.skillset.`! e.g.: `common.skillset.preset.max.sceptre`  | [folder with the skillset](https://gitlab.com/veloren/veloren/-/tree/master/assets/common/skillset) |  
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
