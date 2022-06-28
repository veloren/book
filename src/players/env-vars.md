# Environment Variables

Veloren uses special environment variables to affect game behaviour.
Environment variables should be set before starting the game, search for
tutorials on how to do it in the web.

> NOTE: this list is incomplete, and needs to be expanded.

### VELOREN_ASSETS
Optional variable to point to veloren assets directory.
Not needed if you use Airshipper, but may be useful in more more exotic
scenarios.
### VELOREN_ASSETS_OVERRIDE
Variable to add directory with assets overrides. Recommended if you want to
modify some files, for example different weapon textures.

Linux example:
```bash
$ env VELOREN_ASSETS_OVERRIDE="/home/user/veloren/override_assets/" airshipper run
```
If you have `$VELOREN_ASSETS_OVERRIDE/voxygen/voxel/weapon/caladbolg.vox` with
your modified version of caladbolg.vox, it will be used instead of main
caladbolg.vox file in veloren assets.
### WGPU_BACKEND
May be helpful if your game crashes for no reason. Alternatively, you can
choose it in Airshipper GUI.

Possible values:
- "vulkan"
- "metal" (macOS only)
- "dx12" (Windows only)
- "dx11" (Windows only)
- "primary"
- "opengl" (not supported at the time of writing)
- "secondary"
- "all"
