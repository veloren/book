# Performance

On this page you'll find tips and tricks to help you get the most out of Veloren.

## Introduction

Veloren's world might be mostly made of cubes, but don't be fooled! Veloren's world is expansive and detailed and the
base game has many graphical effects. On highest settings, Veloren can require a very powerful computer to run. Do not
expect to be able to throw all of the sliders up to their maximum and expect the game to run perfectly.

## Identifying your bottleneck

Most of the time, poor performance in Veloren results from one of 3 'bottlenecks'. See below for information about these
cases, how to identify them, and how to rectify them.

### Fragment-limited

If you're *fragment-limited*, performance gets worse if the amount of time required to render each pixel increases. If
reducing your internal resolution improves your framerate, this likely applies to you. To rectify this situation, you
can:

- Reduce internal resolution (an anti-aliasing technique can improve the look of the game at lower resolutions)
- Reduce cloud rendering quality
- Switch to fluid rendering to 'cheap'
- Lower shadow map resolution or switch to 'cheap' shadows
- Reduce or disable bloom

### Vertex-limited

If you're *vertex-limited*, anything that results in the game rendering more polygons to the screen worsens your
performance. If reducing sprite or entity view distance improves your framerate, this likely applies to you. To rectify
this situation, you can:

- Reduce the view distance (reduces the amount of terrain the game must render)
- Reduce the sprite/entity/entity detail view distance
- Reduce the LoD distance
- Reduce LoD detail

### CPU-limited

If you're *CPU-limited*, the performance of the game is limited by the speed of your CPU and not the GPU. If your CPU
usage is regularly very high, this likely applies to you. Sadly, these are a limited number of things you can do to
rectify this situation because most of the CPU's work is *essential* to the functioning of the game. That said, you can:

- Reduce your view distance (fewer entities and less terrain data to process)
- Switch to multiplayer (now it's the server's job to simulate the world and generate terrain)
- Close any other programs you may have open

## What compromise are you looking for?

Veloren has a much larger number of settings (and a wider range of those settings) than most other games. We don't like
it when games artifically limit the way we play, so Veloren is designed to allow you to choose the effects *you* care
about. Here are a few archetypes you might fit into, along with some tips you might want to follow:

### The pixel perfectionist

You care about precision. It frustrates you when games have [aliasing artifacts](https://en.wikipedia.org/wiki/Jaggies).
You expect every pixel to be an immaculate work of art in its own right. You're the sort of person that plays Morrowind,
but only with 8x super-sampling. You might want to:

- Increase 'Internal Resolution' (more than 1.0x corresponds to
  [super-sampled anti-aliasing](https://en.wikipedia.org/wiki/Supersampling), i.e: SSAA)
- Disable FXAA (it can create subtle artifacts)
- Increase shadow map resolution

### The low-power underdog

You just want Veloren to be playable on your hardware. You're willing to sacrifice the more fancy graphical effects, but
ideally without the game looking like the arse end of a donkey. Anything above 20 fps and 240p is a success in your
books. You might want to:

- Switch to 'cheap' shadows
- Switch cloud rendering to 'low' or 'minimal'
- Reduce internal resolution (you can enable an anti-aliasing technique like FXAA or HQX to soften the blow)
- Switch 'fluid rendering' to 'cheap'
- Reduce the maximum FPS to avoid your GPU overheating
- Try enabling the '`BareMinimum`' [experimental shader](voxygen.md#experimental-shaders)

### The god-ray god

You sprinkle bloom on your breakfast cereal every morning. You're not happy until your game looks like an underwater
disco. The only program you run more than Veloren is 'ReShade'. You might want to:

- Increase 'bloom'
- Increase 'point glow'
- Switch 'light rendering mode' to 'high'
- Increase cloud rendering to 'high' or even 'ultra' (beware: *very* expensive)
- Decrease 'internal resolution' to free up your GPU for more post-processing effects
- Switch 'fluid rendering' to 'shiny'
- Enable 'camera smoothing' in 'Gameplay' for improved aesthetics
- Give some of the [experimental shaders](voxygen.md#experimental-shaders) a try

### The 144hz gamer

Your senses have been honed over decades to detect sub-millisecond latencies. Back in the day, you ran consoles in NTSC
configurations for the extra 4.97 frames per second over PAL. Merely glancing at a screen with a refresh rate in the
double digits causes you to vomit. You've already disabled 'motion interpolation' on your TV, and the TVs of everybody
you know. You might want to:

- Increase the maximum FPS to 'unlimited'
- Switch 'present mode' to 'vsync uncapped' to reduce tearing
- Reduce 'internal resolution' so your GPU has less work to do per frame
- Switch to 'exclusive fullscreen' to minimise any latencies that might be imposed by your window manager
- Ensure that 'camera smoothing' is disabled in the gameplay settings
- Use the 'GPU timings' tool to figure out what areas of rendering are taking the most time
