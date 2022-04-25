## Game Questions
- [Is there a death punishment?](#is-there-a-death-punishment)
- [Is there voxel building?](#is-there-voxel-building)
- [Is the map infinite?](#is-the-map-infinite)

## Technical Issues
- [Airshipper crashes on launch.](#airshipper-crashes-on-launch)
- [Game crashes on launch.](#game-crashes-on-launch)
- [Cannot connect to the server.](#cannot-connect-to-the-server)
- [Game is lagging.](#game-is-lagging)

## Answers

### Is there a death punishment?
> No, not right now. But there will be in the future, presumably losing durability.

### Is there voxel building?
> There is some destruction - you can mine ore chunks and certain kinds of rock with a pickaxe.\
> \
> Building isn't intended to be a major part of the game though and is currently only available for server admins and in singleplayer mode through commands. [You can read more about it here](building.md)

### Is the map infinite?
> The map is finite, and will stay that way. There are many reasons to have a finite map, for one it allows us to do advanced simulation (erosion, economy, etc.). Which creates a more meaningful and consistent world. That doesn't mean that we can't have a big world though. 

### Airshipper crashes on launch
> Airshipper doesn't work for some people, you could try updating your graphic drivers. But you can still open the game by using airshipper in the console via the command `airshipper run`.

### Game crashes on launch
> - With airshipper you can switch graphics mode by pressing the cogs next to the play button. If none of the graphic modes you can select work, you could try to update your video drivers. Otherwise your GPU might be too old to run Veloren 😔
> - If you start the game through console you can switch graphics mode by setting the __WGPU_BACKEND__ environment variable to either `dx12`, `dx11` or `vulkan`. 
>    - In windows cmd: `set WGPU_BACKEND="vulkan"`
>    - In powershell: `$env:WGPU_BACKEND="vulkan"`
>    - On Mac and Linux: `export WGPU_BACKEND="vulkan"`

### Cannot connect to the server
> For some people switching DNS server fixes this problem. [Here is a guide](https://www.hellotech.com/guide/for/how-to-change-dns-server-windows-mac). \
> \
> In the worst case you'd have to use a VPN to connect to the server.

### Game is lagging
> - If you have latency issues, it can help to enable "Lossy terrain compression" and lower View Distance in Graphics settings. 
 _Note: The game server is hosted in germany so expect high latency if you're geographically far away._
>  - If you have fps issues, the best settings to change are:
>    - Cloud Rendering Mode to Cheap
>    - Shadow Rendering Mode to None
>    - Fluid Rendering Mode to Cheap
>    - Select a lower Internal Resolution
>    - Put Bloom and Point Glow at 0%.
> 
> If you're still having issues with fps you could try enabling the BareMinimum experimental shader. [Here is a guide how to enable experimental shaders.](voxygen.md#experimental-shaders)
