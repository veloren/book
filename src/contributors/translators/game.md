# Translate the Game

### File and directory structure explained

You can see the localization files inside the `assets/voxygen/i18n` directory.
Each file in this directory represents a language (or a variant of it).
The files are named after [the ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).
(`en.ron`, `de_DE.ron`, `pt_BR.ron` etc.)

Veloren uses a key-value system to translate content. Files use the [RON data 
serialization format](https://github.com/ron-rs/ron) (`.ron`).
They must be formatted in UTF-8, without BOM. Each file contains a metadata
section, a key-value localization section and lastly a key-list localization
section. Files also include font settings that will be used in the game and
a `convert_utf8_to_ascii` option, which can be used when translating a language
which has characters that aren't in the font(s) Veloren uses. Don't be afraid
to ask the addition of these characters in our Discord. Each file includes
how to format the file at the top of it.

The metadata section includes a display name and an identifier for the
language. The display name may be freely changed but the identifier should
stay the same after the introduction of a new language:

```rust, ignore
metadata: (
    language_name: "English",
    language_identifier: "en",
)
```

The `string_map` section includes the key-value localization pairs:

```rust, ignore
string_map: {
    /// Start Common section
    // Texts used in multiple locations with the same formatting
    "common.username": "username",
    "common.singleplayer": "Singleplayer",
    "common.multiplayer": "Multiplayer",
    "common.servers": "Servers",
    // and more...
```

Multiline strings must be written like this:

```rust, ignore
        // Message when connection to the server is lost
        "common.connection_lost": r#"Connection lost!
Did the server restart?
Is the client up to date?"#,
```

The `vector_map` section includes the key-list localizations. A localization from
a list is randomly selected when the game needs it:

```rust, ignore
vector_map: {
    "loading.tips": [
        "Press 'G' to light your lantern.",
        "Press 'F1' to see all default keybindings.",
        "You can type /say or /s to only chat with players directly around you.",
        "You can type /region or /r to only chat with players a couple of hundred blocks around you.",
        "To send private message type /tell followed by a player name and your message.",
        // and more...
```

### Localization test explained

Veloren includes a localization test for translated languages. This test
gathers information about every key and compares them with the reference
language (English, `en.ron` file). Then it classifies and counts these
comparisons and prints them in a neat way for translators to inspect.
This guide explains where to find the test and how to read the results of it.

Open [this link](https://gitlab.com/veloren/veloren/-/pipelines) where you
can see a list of pipelines currently running in our CI system. Try to find a
relatively new (top is new) pipeline which is already green and contains the
title `unittests`. Not every pipeline might have one and it is not essential to
get the newest one, just find `unittests` and you are good to go. Then click on
it. A page will open with a black box and a lot of text. You have to scroll up a 
bit and find something like what we see below:

```
-----------------------------------------------------------------------------
Overall Translation Status
-----------------------------------------------------------------------------
            | up-to-date | outdated | untranslated
tr_TR.ron   |     206    |    11    |      19
pt_PT.ron   |     123    |    15    |      98
es_ES.ron   |     213    |     5    |      18
fr_FR.ron   |     100    |    18    |     118
it_IT.ron   |     120    |    17    |      99
ru_RU.ron   |     198    |     6    |      32
de_DE.ron   |     223    |    10    |       3
pt_BR.ron   |     199    |     8    |      29
73.20% up-to-date, 4.77% outdated, 22.03% untranslated
-----------------------------------------------------------------------------
```

This is the indication that you did everything right and got to the statistics.
This is an overview page that shows you the available languages and if there are
some missing or outdated translations. Let's say we want to focus on the German
one, `de_DE`. We have to scroll further up till we get the detailed information:

**Tip:** Use Ctrl+F to search for your language!

```
-----------------------------------
"assets/voxygen/i18n/de_DE.ron"
-----------------------------------
Key hud.bag.stats_title does not have a Git line in its state! Skipping key.
Commit ID of key hud.bag.stats_title in i18n file assets/voxygen/i18n/de_DE.ron is missing! Skipping key.
State       | Key name                                                    | assets/voxygen/i18n/de_DE.ron            | assets/voxygen/i18n/en.ron              
[Unused   ] | char_selection.chest_color                                  | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | None                                    
[Unused   ] | char_selection.create_charater                              | ecb7963730ad2eb8d6e10f6df5dfaf99abccca5b | None                                    
[Outdated ] | char_selection.eye_color                                    | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[Outdated ] | char_selection.plains_of_uncertainty                        | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | ecb7963730ad2eb8d6e10f6df5dfaf99abccca5b
[Outdated ] | char_selection.skin                                         | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | f7d6f76a0458716ceaf5a53d3a70ee7f0fb9eda6
[Outdated ] | common.sound                                                | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | 45217915911ddf1b5ea6a8ff36c2394fd755fcc6
[Outdated ] | gameinput.slot2                                             | f24ba71d9446ea8bcf259020125eaa4290bfde49 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[Outdated ] | hud.auto_walk_indicator                                     | 9b2785aeae5b60984691c18a324b1d62ce2b9ed2 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[Unknown  ] | hud.bag.stats_title                                         | None                                     | 88a938653be9a95128e938d24afba559bf57fdf5
[Outdated ] | hud.chat.loot_msg                                           | 89400264dc0fb9babb93bcdd04f97c4252dcd772 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[Outdated ] | hud.chat.offline_msg                                        | 89400264dc0fb9babb93bcdd04f97c4252dcd772 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[Outdated ] | hud.press_key_to_toggle_debug_info_fmt                      | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | e10f27f4806d9c9493bda4b5990a3d44b317fe10
[NotFound ] | hud.settings.reset_keybinds                                 | None                                     | 8e523364ac8b3a155938c98010562c664d577c57
[Outdated ] | hud.settings.toggle_shortcuts                               | 1af82604b55839275998d6afe7ee51a9ffbfdfe4 | ddaa0a9246abddcd623d32c2c1fcf4cd794882df
[NotFound ] | hud.settings.unbound                                        | None                                     | 198c875559dbb1895249ea5d959b61dbff8901bf
223 up-to-date, 10 outdated, 2 unused, 2 not found, 1 unknown entries
94.49% up-to-date, 4.24% outdated, 1.27% untranslated
```

Here we have detailed information about all language keys used in the German
translation (`de_DE.ron` file) in comparison with the reference English
translation (`en.ron` file). Here is what the `State` section for keys mean:

- `Unused`: The key exists in the German translation but not in the English
  translation. These are keys that have been used before in the game but 
  have been removed since they weren't needed or have been renamed. These
  are safe to remove.
  
- `NotFound`: The key exists in the English translation but doesn't exist in
  the German translation. Here we need your translation!
  
- `Outdated`: The English translation was changed but the German translation
  wasn't updated. This might be a hint that the German version is outdated
  and needs an update. Note that this doesn't necessarily mean that the
  English localization has been changed in a way that it affects the meaning -
  it might simply have been a typo fix.
  
- `Unknown`: This signifies that an error occured while getting information
  about this key. This is not an user issue, so you don't need to worry about
  these keys.

## Guide to translating the game

Guides to help you translate the game, for certain situations. If you get
stuck at any step or need more help (or just have questions) ask us in our
Discord server.

If you are not familiar with Gitlab or Git, feel free to ping `@git-wizard`,
who will always be on deck to help with this.

### Create a translation from scratch

If there is no translation for your language, you can create one by following
these instructions. Remember to replace the Turkish language example with your
own language!

First of all, you need a copy of the Veloren repository. Refer to the
[working with git](../working-with-git.md) section for this.

After you have obtained a copy of the repository, navigate to the `assets/voxygen/i18n`
directory. Here you'll see a list of translations, and the reference English file (`en.ron`).
Make a copy of the `en.ron` file, named after your language. For example, if you want
to translate Turkish, your file would be named `tr_TR.ron`.

Then, you can start editing the file! First go to the metadata section. This
section has the display name and the identifier for your translation. Change
`language_name` to a human readable name in your language (eg. `Türkçe (Türkiye)`,
means `Turkish (Turkey)` in English) and change `language_identifier` to the
identifier of your language (usually same with the file name, eg. `tr_TR`).
Also change the:
```rust, ignore
/// Localization for "global" English
```
section to show your language. For example:
```rust, ignore
/// Localization for Turkish (Turkey)
```

And that's it! You can now start translating any key you want. Don't forget to
preview the changes ingame by [compiling and running](../compiling.md) the game,
and setting the language setting to your new in-translation language. If there
are missing characters, don't worry, you can ask us about these in our Discord
server.

**Tip:** You can set `convert_utf8_to_ascii` option to `true` to
convert everything to ASCII, so that the missing characters can be seen properly.

After you are happy with your translation, commit your changes with a proper
commit message, such as `Added Turkish (Turkey) translation`. Create a new
branch with name `<yourusername>/add-<language>`. Then push your changes and
create a merge request (don't forget to read and tick all the boxes!). You can
notify us on the Discord server that there is a new translation available
(in the **#translation** channel).

### Improving an existing translation

If you are lucky, you may already find that there is a translation for your
language. If you see that it has some missing, incorrect translations or
you think that you have a better translation for something, then this guide
is for you! Don't forget to replace the German example with your own
language (if you aren't translating the German language).

Okay, let's say we want to add the correct translation for the German of `hud.settings.reset_keybinds`.
So we first want to look it up in the reference language (English) [`assets/voxygen/i18n/en.ron`](https://gitlab.com/veloren/veloren/-/blob/master/assets/voxygen/i18n/en.ron).
After the key we find this English sentence: `Reset to Defaults`. We know that
the German equivalent would be `Standarteinstellungen wiederherstellen` (Well,
some of us do :P). Then, we open the translated language (German)
[`assets/voxygen/i18n/de_DE.ron`](https://gitlab.com/veloren/veloren/-/blob/master/assets/voxygen/i18n/de_DE.ron).

If you are already a developer in Gitlab you'll now see an edit button. If you
don't, no need to worry! You can ask in our Discord server for the developer
privileges.

**Tip:** Keep both the reference language and the translated langauge open,
so that you can find in which place your entry is missing by looking at the
line numbers.

Once you are editing the file on Gitlab, go to the place where our entry is
missing and add it here:

```rust, ignore
"hud.settings.awaitingkey": "Drückt eine Taste...",
"hud.settings.reset_keybinds": "Standarteinstellungen wiederherstellen",
```

When you're done, enter a specific commit message such as `update the <language> translation`.
In our example this would be `update the German translation`. You'll then
create a target branch with name `<yourusername>/update-<language>`. An example
would be `xMAC94x/update-de`. Finally, you'll need to create a merge request.
Read and check the boxes to agree that your code will be under the GPL3 license.

You now requested to change the file, and we will then take a look at it and if
we found it okay we will merge it into the game! From that point on your
contribution will land in the `master` branch, and in 24 hours will be shipped
to you via Airshipper.

### Help review pending translations

Someone may have done a translation for your language already. To check this,
you can take a look at the [Merge Requests](https://gitlab.com/veloren/veloren/-/merge_requests) page.
See if you can find a pending merge request with your language (e.g. `de_DE`).
Ask in our Discord server for reporter privileges so you can open it and add
your thoughts / reviews to it.

If you found one, clicking on the `Changes` tab when you're in the MR page you
can see the details of this change. Red lines are old ones that are removed
and replaced by green lines. If you disagree with something that was added,
you can start a discussion by clicking on the respective line. If you don't
see any issues with the proposed changes, feel free to approve the MR or
comment on it. It's important that you approve the MR for translations as we
the developers don't have the knowledge to verify the language (and we don't
want to put everything through Google Translate). So you help us to verify
others contributions resulting in improved game quality.

