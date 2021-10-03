# Artists creative heaven

_Introduction into the art of adding artistic content to Veloren_

- [Voxel Models](voxel-models.md)
- [Audio](audio.md)
- [Graphics](graphics.md)

## Saying 'Hello' in one of the art-channels

This is the best way to get in contact with our art-team on Discord.
Plus you already get an idea of how we work together as a team and maybe even get to know some of us.

Artists are showing off their creations on those channels to get feedback or an 'OK' from Core-Devs that their model is ready for being animated and placed into the game.

## Attribution and Licensing

Assets that are (or are adapted from) licensed copyrighted material often have certain requirements including attribution of the source and making note of the modifications.

For example, the Creative Commons licenses generally require attribution with:
- Title of the original work
- Link to the original work
- Author of the original work
- The license name with a link to the full license
- Notes of any modifications to the original work
- If modifications are enough to be considered a derivative/adaptation, the new title and authors

To keep track of attributions and provide a format that can be displayed in the game we have created [`assets/common/credits.ron`](https://gitlab.com/veloren/veloren/-/blob/master/assets/common/credits.ron). **Merge requests that add works requiring attribution should update this file with new entries.** This manifest allows entries with the following fields:
```rust
(
    name: String,
    source_link: String,
    authors: Vec<String>,
    asset_path: String,
    license: String,
    license_link: String,
    modfications: String,
    notes: String,
)
```
Attributing work with no modifications or small modifications from the source can be formatted like:
```rust
(
    name: "Original Title",
    source_link: "https://fonts.com/fancyfont/",
    authors: ["Author One"],
    asset_path: "relative/path/to/fancyfont.ttf",
    license: "CC BY-SA 3.0",
    license_link: "https://creativecommons.org/licenses/by-sa/3.0/",
    modifications: "Trivial modification",
)
```

Derivative work can be formatted in the current scheme like:
```rust
(
    name: "Derivative Title",
    source_link: "https://fonts.com/fancyfont/",
    authors: ["Author Two (derivative)", "Author One (original)"],
    asset_path: "relative/path/to/fancyfont.ttf",
    license: "CC BY-SA 3.0",
    license_link: "https://creativecommons.org/licenses/by-sa/3.0/",
    modfications: "Added additional characters to the font.",
    notes: "Derived from Original Title",
)
```

There is room for improvement in the format for derivatives works and thoughts on this would be welcome! For instance, in the example above original and derivative authors have to be differentiated using a note in parentheses and the title of the original work is listed in the `notes` field.

For now, attribution requirements that don't fit the provided fields can utilize the `notes` field to provide any further information. Additional cases that might need this are:
- Work derived from multiple original works. 
- Work derived from derived work (indication of previous modifications needs to be retained).

**Careful review of the specific license and requests of the original author is advised.**
For more helpful information on the Creative Commons licenses see:
- [https://wiki.creativecommons.org/wiki/Best_practices_for_attribution]()
- [https://creativecommons.org/faq/#attribution]()
