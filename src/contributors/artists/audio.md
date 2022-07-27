# Contributing Audio

The best way to contribute audio is to first visit the Discord, ask for a contributor role in the #new-contributors channel, and start a conversation in the #audio channel.

All sound files should be in .ogg format, exported at Variable Bit Rate level 5. The quick and easy way to do this is to export as a .wav, open it in Audacity, and export it again as a .ogg at compression level "5".

# Sound Effects

Most sound effects go in an appropriate folder in `assets\voxygen\audio\sfx\`.

Sound effects that emit from an source in 3D space, like footsteps, hitsounds, and utterances, should be exported as mono.

There are two main ways of triggering a sound effect in-game: sfx events and outcomes.

Sfx events retrieve sfx from the `sfx.ron` file. They are mostly triggered by any of the various `mod.rs`'s in `voxygen\src\audio\sfx\`.

Outcome sfx are retrieved from `sfx.ron` and handled in `voxygen\src\audio\sfx\mod.rs`. Outcomes are emitted from whichever code is related to it, be it combat, server event, etc. The outcome must also be added to `common\src\outcome.rs`.

UI sfx usually stereo sounds that play directly to the player (i.e. not from a place in the world).

There are is also ambience, used for things like wind and rain. These sounds are always stereo. The code for it is in `voxygen\src\audio\ambient.rs`, the files are in `assets\voxygen\audio\ambient`, and its manifest is `assets\voxygen\audio\ambient.ron`.

If possible, have your sfx tested in-game before trying to merge it; ensure it sounds right and plays at the right volume. Be sure to get a second opinion from the Discord channel!

# Music

Music files are found in `assets\voxygen\audio\soundtrack\`. The game retrieves the files via the `soundtrack.ron` file. Music should be normalized at -1dB after mastering.

It is customary to check in with one of the audio leads on Discord to get your music approved for the game.

>Rough loudness guidelines:
> For people with LUFS analysis software, try to keep the max LUFS-S (after normalization) between -14 and -13 for exploration tracks, and between -13 and -12 for combat tracks. If in doubt, compare directly with existing tracks. 

**Exploration**

The game plays exploration music as single, standalone tracks in the background. When one track ends, some time passes before another track plays. Which track is played is determined by which site, biome, and time of day the player is in.

The available sites currently are the overworld, dungeons, caves, and towns.

The available biomes currently are Grassland, Forest, Desert, Snowland, Lake, Mountain, Ocean, Jungle, Savannah and Taiga.  A Swamp biome is planned, but doesn't exist yet. For an up-to-date list of biomes, see `common\src\terrain\biome.rs`.

> It is worth noting that biomes are *descriptive*, not *prescriptive*, when it comes to code. The world doesn't generate based on biomes, and biomes are determined based on existing chunk data.

> Certain biomes supercede others - most notably, snow-covered mountains will count as Snowland. If you want to know exactly how biomes are determined, see `get_biome()` in `world\src\sim\mod.rs`.

Also note that music may play in more than one biome and time of day, though we generally want to minimize this as more music gets added, to give each biome a more distinct tone.

The times of day are day and night.

**The best way to get a feel for the tone of the soundtrack is to simply listen to it.**

Exploration music should have soft starts and endings since they come in at essentially random times.

**Combat**

The current implementation of the combat music system is as follows:

"Combat" as a state is when the player comes within a certain distance of enemies with either high health or high quantity. Currently, combat music is reserved for the old, underground dungeons. Upon the player entering combat, a `start` segment is played. If it ends and combat continues, a `loop` segment is immediately played, before either fading out or playing an `end` segment when combat ends.

- `start` is a short intro *attached to* a `loop`. If the composer is smart, they can shorten this segment by having it somehow transition perfectly into the `loop` *without* playing the entire `loop` itself.

- `loop` is the main portion of the combat music. Since the music only comes in when the player is in a fairly dire situation (mobs of enemies, hard enemies, and bosses), the intensity of the music should be fairly high.

- `end` is a very short cadence coming off the end of the `loop`, and is only played if the fadeout can't complete before the `loop` ends. Should give a sense of finality.

It is important for the transitions and loops to be *smooth*. This means the `loop` must be "exported as loop"; the tail (the residual release/reverb at the end) of the `loop` (and the `start`) must also bleed into its beginning, as well as into the `end`.
