# Voxygen - 3D client frontend

Voxygen is Veloren's official 3D frontend. It's the frontend that almost all users interact with Veloren though,
although [alternatives do exist](/contributors/developers/codebase-structure.md#frontends). However, almost all
documentation about Veloren assumes that Voxygen is the client frontend in use.

Voxygen is designed to be user-friendly and intuitive.

## `settings.ron`

Voxygen's configuration file can be found in the [`userdata` directory](userdata-folder-structure.md).

### Gamepad Controls

Voxygen supports inputs via a gamepad or game controller. Unfortunately, inputs are not yet configurable through a GUI,
but `settings.ron` can be edited manually via the `controller` section.

### Experimental shaders

Voxygen has several experimental shaders that can be enabled via the `graphics.render_mode.experimental_shaders` option.

Please note that these shaders come with no guarantees: they may be completely broken, mutually-incompatible, or may
melt your GPU. Please do not report rendering bugs if you have them enabled (unless you are quite sure that the bug has
nothing to do with the shaders).

Experimental shaders are explicitly *not* a feature of the game. They may be removed, break, or change at any time and
without warning. They exist purely as a way for developers to try out new rendering ideas and as a fun extra for
experienced players.

Experimental shaders can be enabled by adding them to the relevant section. For example, to enable the `Brickloren`
and `NoNoise` shaders:

```
(
    ...
    graphics: (
        ...
        render_moder: (
            ...
            experimental_shaders: [Brickloren, NoNoise],
            ...
        ),
        ...
    )
    ...
)
```

The order of the shaders is irrelevant.

You can find a list of all available experimental shaders
[here](https://docs.veloren.net/veloren_voxygen/render/enum.ExperimentalShader.html).
