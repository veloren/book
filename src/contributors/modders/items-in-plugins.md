# Adding in-game items from a plugin

To add new armor or weapon types, you don't need to write and compile Rust,
this guide will show you the necessary steps.

## Plugin metadata

First, start from a new, empty directory.
Like [described here](writing-a-plugin.md), we need to create a
`plugin.toml` file:

```toml
# The name of the plugin (lowercase, no spaces)
name = "cool-armor"

# A list of paths to WASM modules in the plugin (not needed for items).
modules = []

# Plugins required by this plugin (currently unsupported, keep this empty)
dependencies = []
```

Please note that all assets are directly stored in this directory,
this means that the normal `assets/` prefix or directory isn't necessary.

Then follow the guide in [armor creation](../guides/adding-armor/guide.md) to
create a voxel file in `voxygen/voxel/armor/<Armor Type>/<Model Name>`, see also
[using multiple models](../guides/multiple-models/guide.md) on how you can
put all pieces into a single VOX files.

For a weapon please follow [this guide](../guides/adding-weapons/guide.md) instead.

Adding new files like `voxygen/voxel/weapon/tool/paddle.vox`,
`common/items/weapons/tool/paddle.ron` or `common/items/armor/hide/lizard_boots.ron`
is straightforward and described in the guides above
(remember to skip the top level `assets/` directory), but
`voxygen/voxel/biped_weapon_manifest.ron` already exists in the game.

Here simply create a new file with the exact same layout as the existing one in `assets/`:

```ron
({
    Tool("common.items.weapons.tool.paddle"): (
        vox_spec: ("weapon.tool.paddle", (-2.5, -4.0, -4.0)),
        color: None
    ),
})
```

Veloren will merge the contents of these RON files when it loads the manifest.

`voxygen/voxel/humanoid_armor_foot_manifest.ron` will also require the `default:` part, although it won't be used:

```ron
((
    default: (
        vox_spec: ("armor.misc.foot.none", (-2.5, -3.5, -2.0)),
        color: None
    ),
    map: {
        "common.items.armor.hide.lizard_boots": (
            vox_spec: ("npc.lizardman.male.foot_r", (-2.5, -3.5, -2.0)),
            color: None
        )
    }
))
```

Then, like described [here](writing-a-plugin.md), create a tar file containing all
the newly created files and put in inside the `assets/plugins/` folder on the server:

```bash
tar -cvf ../my_plugin.plugin.tar *
```

You can find an exemplary plugin on [GitHub](https://github.com/cpetig/veloren-plugin-canoe).

Please keep in mind that for now we don't give any guarantees on plugin compatibility
across Veloren versions, although we might write a plugin migration tool in the
future, similarly to the database migration tool, once we see the need and resources for it.
