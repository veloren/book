# Guide: Adding sprites to Veloren

\\\_ made by @Pfau

![Image1](image1.png)

### What you need:

- An **IDE** of your choice (A programme that lets you view and edit code)

  > Examples: [VSC](https://code.visualstudio.com/), [Atom](https://atom.io/), [Notepad++](https://notepad-plus-plus.org/downloads/)

- A **Voxel Editor** (To create the sprite model)

  > Example: [Magicavoxel](https://ephtracy.github.io/)

- A [guide](/contributors/introduction.md) on how to compile and run Veloren on your OS.

- A locally cloned branch of Veloren's [nightly version](https://gitlab.com/veloren/veloren).

### Getting Started

Before creating your sprites there are a few things you should know:

- Sprites act like landscape sized blocks that get replaced with small scale models.<br/>
  They can either be set to behave like air (no collision at all) or as solid objects.

- Things like grass should have no collision. While scarecrows and windows should.

- As of now they will always act like a single row of up to three lanscape blocks (33 small scale voxels) above each others.
  That means you can control the collision height of your sprite but not the width.<br/>
  Every part of a sprite that exceeds the x and y-axis bounds of a single block will not clip with figures and objects.

- Sprites act as immovable objects like blocks. They can't be moved around like figures or objects.<br/>
- Sprites can be set to give players a certain item when picked up.<br/>
- Sprites can have certain spawning and orientation rules.

### Naming scheme for .vox files:

- Single words are parted with an underscore (`_`)
- Counting starts at zero.
- Numbers are added with a single dash(`-`) in front of them.
- Your model name should always end with a number, unless you are absolutely positive there isn't going to be an alternative version/design of the item

### Import the model and add it to the codebase

`assets/voxygen/voxel/sprite_manifest.ron`

> Here you define how many variations your sprite can have, how much it sways in the wind and which model(s) to load from the asset folders.

`common/src/terrain/sprite.rs`

> Here you define the sprites' properties like collision, orientation, the height of their "collision frame" or if they can be collected.

### Step by Step: Addition of an example sprite

1. **Adding a voxel model**

   In `assets/voxygen/voxel/sprite_manifest.ron` copy and paste one of the code blocks, eg:
      ```rust,ignore
        Window1: Some((
          variations: [
              (
                  model: "voxygen.voxel.sprite.window.window-0",
                  offset: (-5.5, -5.5, 0.0),
                  lod_axes: (1.0, 1.0, 1.0),
              ),
          ],
          wind_sway: 0.0,
        )),
      ```
   ... and put it behind the last entry in the file, making sure to leave the last `)` at the very end of the file.
   Replace the name of the object (eg, `Window1`), with the name you'd like to call your sprite object (no spaces in the name).

   Next add your .vox model to `assets/voxygen/voxel/sprite/`, either in the appropriate subfolder or create a new folder if it doesn't fit anywhere else. For example, if your sprite is a piece of furniture, add it to the `furniture` subfolder. Follow the naming scheme for .vox files mentioned earlier on this page. 

   In the new codeblock you pasted, edit the `model` section to point to your .vox file; making sure to keep the double-quotes and the comma at the end. In the example above, the file `window-0.vox` was added to the `window` subfolder and the model was defined as `"voxygen.voxel.sprite.window.window-0",`
  
   Next, the center-point of the model needs to be defined in the `offset` section. In your voxel editor, set the workspace to fit your model. If you're using MagicaVoxel, press the button labeled 'Fit Model Size' to do this. The workspace will shrink to fit your model. The center point is half the number of blocks in the x and y axes. For example, in the Window1 codeblock above, the model is 11 x 11 blocks. So we've entered `-5.5, -5.5` for the x-axis and y-axis respectively. Set the z-axis to `0.0` unless the model is supposed to sink into the ground (eg, ore).

   The `lod_axes` refers to an object's level of detail the further away it is from the player. Reducing the level of detail when an object is far away helps with game performance. This setting tells the game how to scale the level of detail reduction across all three axes (x, y, z). For now, just use 1.0 for all three axes, like the Window1 example above, or find another object that is similar to yours and copy it's lod_axes values.

   If your sprite is designed to sway in the wind (eg, grass or flowers), modify the `wind_sway` to a number between 0.0 and 1.0. The higher the number the more it will sway. Take a look at some other objects to get an idea of the what value to use. 

2. **Telling the game the sprite exists and making it solid**

   In `common/src/terrain/sprite.rs`

   Near the beginning of the file, look for a long list of objects with a heaxdecimals number after each object (eg, 0x0A). The name of the objects in this list matches the name in the previous step. For example, in the previous step we were looking at `Window1`. In the list of objects here, we will find ` Window1 = 0x28,`.

   To add your object to this list, scroll down to the bottom of this list (it's pretty long). At the **END** of the list add your object name and give it a value of the next hexadecimal number in the sequence.
   
   > _Tip: hexadecimal numbers range from 0 to 15, but numbers with two digits are represented by a letter: 0 1 2 3 4 5 6 7 8 9 A B C D E F. Notice how 10 is actually A, 11 is B, and so on. So if the last object in the list had a value of 0xB9, the next object would need to be 0xBA. (0xB9 + 1 = 0xBA). If you need help, you can type `0xB9 + 1` into Google and it will tell you the answer._

   Next, if your sprite is solid, and players should collide with it, you need to add it to a function called `pub fn solid_height`. Search for this function in the `sprite.rs` file. This function tells the game how tall the collision box for the object should be. You can skip this if your sprite isn't meant to be collided with and players should move right through it (for example, grass and flowers).
   
   Within the function you will see a long list of objects that looks like this: `SpriteKind::Tomato => 1.65,`. Scroll to the bottom of this list and add your sprite at the end. You'll need to calculate what number value to assign your sprite though. This number is simply the height of your sprite in voxels divided by 11. For example, if your voxel model is 18 voxels tall, the calculation is 18/11 = 1.64. You can find the height of your model by going to your voxel editor and counting the number of blocks. 
   
   _Note: 3.0 is the maximum value that can go in this list. If you have definied multiple variations of a sprite in the previous step, they will all share the same height._

   Finally, in the `pub fn has_ori` function, add your sprite to the end of the list. Follow the examples already there and don't forget the `|` at the start (eg, `| SpriteKind::Window1`). Adding your sprite to this function will allow it to be rotated (oriented) by code when it's spawned in the world.
   
3. **Other properties for the sprite**

   Other than being solid, sprites can also be collectible or minable.
   
   A collectible sprite can be picked up from the world by the player (eg, stones). Or can be opened by the player with an item taken from it (eg, a chest).

   A minable sprite requires a mining tool before it can be collected (eg, an ore).

   The steps required to make sprites collectible or minable are too involved for this page and need be addressed in a separate guide.

   However, for those who wish to dive into the code and figure it out for themselves, here are some pointers to get you started.

   - Add sprite to `pub fn collectible_id` in `common/src/terrain/sprite.rs`.
   - If the sprite requires mining, add it to `pub fn mine_tool` in `common/src/terrain/sprite.rs`.
   - If your sprite is meant to be opened, and will give the player an item, follow the examples for crates and chests in `common/src/terrain/sprite.rs`. This will involve creating a .ron file in `assets/common/loot_tables`.
   - If your sprite is to be collected, and goes into the player's inventory:
      - Create a .ron file for your collectible sprite in subfolder of `assets/common/items` and use an example that most closely matches what your sprite does (eg, food).
      - Add your item to `assets/voxygen/item_image_manifest.ron`. You'll also need to add a copy of your voxel model file to another folder, which is defined in this manifest. Find an item which most closely resembles yours and use it as an example.
      - Add your item `assets/voxygen/voxel/item_drop_manifest.ron` in the appropriate section with similar items.
      - Add your item to `common/src/states/sprite_interact.rs` in the section `fn from(sprite_kind: SpriteKind) -> Self`.

### Making sprites spawn in the world

Sprites are spawned into the world through code, rather than being placed manually. This means in order to make your new sprite spawn where you intend (eg, in a house, field, dungeon, etc), you'll need to be able to modify code.

But... if you're looking for a quick way to see what your sprite looks like in the game, without coding, there is an easier way to marvel at your handiwork. This is useful to check if your sprite is the right size, for example.

- You'll need to compile the code you've written so far in the steps above. There are [other parts](/contributors/compiling.md) of the guide that explain how to do this, but in essence you type: `cargo run`
  - _Tip: Don't be surprised if your compile fails with an error, it's usually just a typo. Take a look at the code you wrote, see if there are any obvious mistakes, and repeat the steps above if necessary_.
- Find and remember the name of the sprite you created in step 1 above. We've been using `Window1` as an example.
- Once your local copy has been compiled, and is running, start a singleplayer game.
- In the game, type: `/make_sprite YourSpriteName` replacing the word "YourSpriteName" with the name of your sprite in step 1.
  - Example: `/make_sprite Window1`
- Your sprite will be spawned where your character is standing. Huzzah!

If you want to take it to the next level, and see your sprite appearing properly in the world, you'll need to get your hands dirty with Rust coding. This is beyond the scope of this page, but here are a few tips to get you started:

- `world/src/layer/scatter.rs` contains code for items such as flowers, twigs, stones, etc. Anything that is 'scattered' about in the environment randomly.
- `world/src/site2/plot/house.rs`contains furniture in houses, such as tables, beds and coat racks.
- Take a look around  `world/src/` for other examples.
- The #new-contributors channel on the Veloren Discord server is a good place to ask questions.

**Congratulations on adding a new sprite to Veloren :)**
