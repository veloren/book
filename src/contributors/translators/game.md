# Translate the Game

### File and directory structure explained

You can see the localization files inside the `assets/voxygen/i18n` directory.
Each directory in this directory represents a language (or a variant of it).
The directories are named after [the ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).
(`en/`, `de_DE/`, `pt_BR/` etc.)

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
language (English, `en/` directory). Then it classifies and counts these
comparisons and prints them in a neat way for translators to inspect.
This guide explains where to find the test and how to read the results of it.

Open [this link](https://gitlab.com/veloren/veloren/-/pipelines) where you
can see a list of pipelines currently running in our CI system. Try to find a
relatively new (top is new) pipeline which is already green and contains the
title `build` in `Stages` column, tap on it and you should find a `unittests`
field. Not every pipeline might have one and it is not essential to
get the newest one, just find `unittests` and you are good to go. Then click on
it. A page will open with a black box and a lot of text. You have to scroll up a 
bit and find something like what we see below:

```
-----------------------------------------------------------------------------
Overall Translation Status
-----------------------------------------------------------------------------
            | up-to-date | outdated | untranslated | unused   | errors  
uk_UA       |     713    |     7    |       0      |     1    |       0
pt_BR       |     699    |    18    |       3      |     3    |       0
PL          |     702    |     2    |      16      |     3    |       0
zh_CN       |     673    |     6    |      41      |     7    |       0
es_ES       |     663    |    13    |      44      |     7    |       0
de_DE       |     670    |     0    |      50      |     7    |       0
fr_FR       |     656    |    11    |      53      |     8    |       0
ja_JP       |     655    |     8    |      57      |     8    |       0
es_la       |       6    |   346    |     368      |     3    |       0
tr_TR       |     340    |    12    |     368      |     2    |       0
ru_RU       |       5    |   343    |     372      |     3    |       0
no_nb       |       6    |   328    |     386      |     2    |       0
nl          |       3    |   305    |     412      |     3    |       0
it_IT       |       1    |   229    |     490      |     4    |       0
pt_PT       |       1    |   135    |     584      |     5    |       0
zh_TW       |       1    |   133    |     586      |    12    |       0
sv          |       1    |   104    |     615      |    13    |       0
vi_VI       |      74    |     2    |     644      |     1    |       0

45.29% up-to-date, 15.45% outdated, 39.27% untranslated
-----------------------------------------------------------------------------
```

This is the indication that you did everything right and got to the statistics.
This is an overview page that shows you the available languages and if there are
some missing or outdated translations. Let's say we want to focus on the Ukrainian
one, `uk_UA`. We have to scroll further up till we get the detailed information:

**Tip:** Use Ctrl+F to search for your language!
**Tip:** If you can't find your language, press 'Complete Raw' to get full log.

```
-----------------------------------
"assets/voxygen/i18n/uk_UA.ron"
-----------------------------------
Key name                                                    | assets/voxygen/i18n/uk_UA/_manifest.ron  | assets/voxygen/i18n/en/_manifest.ron    

	[NotFound]
buff.desc.cursed                                            | None                                     | 531c38c3ad08af5370bfa2cd5f501224b55b4c22
buff.title.cursed                                           | None                                     | 531c38c3ad08af5370bfa2cd5f501224b55b4c22

	[Unused]
hud.settings.cancel_inputs_on_chat                          | ef8926bc5c10fe80bfe7ee8d69763d710c229afb | None                                    

	[Outdated]
common.stats.poise_res                                      | 4717ad25a8fb5856951360d4e01eb741eb289fe4 | 6772e71aaac034ac03917e67988176cbf2772cb1
gameinput.autowalk                                          | 4e7aba5b3f8a2499785bc4f1776eddbdaf6fe96d | a17bb0ad733e0dbe2c649ebb31a94990db438b01
gameinput.secondary                                         | 4e7aba5b3f8a2499785bc4f1776eddbdaf6fe96d | 2e24fcf165545405e13a3eb5f8b3e3eeadf3f1c0
hud.auto_walk_indicator                                     | 4e7aba5b3f8a2499785bc4f1776eddbdaf6fe96d | a17bb0ad733e0dbe2c649ebb31a94990db438b01
hud.map.dungeons                                            | 7be836318bbae1e26b03500b4235eef22e6be4e4 | db573f6b2dc5ae91f33296b07709c4c66c6e4c16
hud.settings.refresh_rate                                   | 7be836318bbae1e26b03500b4235eef22e6be4e4 | 60e2ed3e7dfad7c88fc7c6c1fa2fefefec6240a4
main.login.network_wrong_version                            | 4717ad25a8fb5856951360d4e01eb741eb289fe4 | 2e08c2f76f29e98b29f997bcff6456c373c8117a

711 up-to-date, 7 outdated, 1 unused, 2 not found, 0 unknown entries
98.75% up-to-date, 0.97% outdated, 0.00% untranslated
```

Here we have detailed information about all language keys used in the Ukrainian
translation (`uk_UA` directory) in comparison with the reference English
translation (`en` directory). Here is what the `State` section for keys mean:

- `Unused`: The key exists in the Ukrainian translation but not in the English
  translation. These are keys that have been used before in the game but 
  have been removed since they weren't needed or have been renamed. These
  are safe to remove.
  
- `NotFound`: The key exists in the English translation but doesn't exist in
  the Ukrainian translation. Here we need your translation!
  
- `Outdated`: The English translation was changed but the Ukrainian translation
  wasn't updated. This might be a hint that the Ukrainian version is outdated
  and needs an update. Note that this doesn't necessarily mean that the
  English localization has been changed in a way that it affects the meaning -
  it might simply have been a typo fix.
  
- `Unknown`: This signifies that an error occured while getting information
  about this key. This is not an user issue, so you don't need to worry about
  these keys. But if you've found this, please tell us about it.

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
directory. Here you'll see a list of translations, and the reference English directory
(`en/`).
Make a copy of the `en/` directory, named after your language. For example, if you want
to translate Turkish, your directory would be named `tr_TR/`.

Then, you can start editing the file! First go to the metadata section in `_manifest.ron`.
This section has the display name and the identifier for your translation. Change
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

**Tip:** you don't need to compile game to test your changes, you can
just copy your changes to `assets` directory in app folder.
If you have installed the game via Airshipper look in these
[directories](../../players/airshipper.md#files)

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
is for you! Don't forget to replace the Ukrainian example with your own
language (if you aren't translating the Ukrainian language).

Okay, let's say we want to add the correct translation for the Ukrainian of
`buff.desc.cursed`.
So we first want to look it up in the reference language (English) [`assets/voxygen/i18n/en/buff.ron`](https://gitlab.com/veloren/veloren/-/blob/master/assets/voxygen/i18n/en/buff.ron).
After the key we find this English sentence: `Cursed`. We know that
the Ukrainian equivalent would be `Проклін` (Well,
some of us do :P). Then, we open the translated language (Ukrainian)
[`assets/voxygen/i18n/uk_UA/buff.ron`](https://gitlab.com/veloren/veloren/-/blob/master/assets/voxygen/i18n/uk_UA/buff.ron).

If you are already a developer in Gitlab you'll now see an edit button. If you
don't, no need to worry! You can do the same operations with your fork.

**Tip:** Keep both the reference language and the translated langauge open,
so that you can find in which place your entry is missing by looking at the
line numbers.

Once you are editing the file on Gitlab, go to the place where our entry is
missing and add it here:

```rust, ignore
"buff.title.cursed": "Проклін",
"buff.desc.cursed": "Вас прокляли.",
```
### Getting information about translation
If you are able to compile, you can use special tool to get information about translation.
Basically, it is the same programm that runs on our CI, but you can cut out unneded
information.
For example, you want to get information about Ukrainian translation.

```
$ cargo run --bin i18n-check --features=bin -- uk_UA
```

You can also run it with `--help` argument to find out more ways to use it.

**Note:** arguments go after `--`, it's where `cargo` arguments end and actual
arguments start.

**Note:** you need to commit your changes for `veloren-i18n` to know about it.

### Push changes
When you're done, enter a specific commit message such as `update the <language> translation`.
In our example this would be `update the Ukrainian translation`. You'll then
create a target branch with name `<yourusername>/update-<language>`. An example
would be `juliancoffee/update-uk_UA`. Finally, you'll need to create a merge request.
Read and check the boxes to agree that your code will be under the GPL3 license.

If you don't have Developer role, you will need to push your changes
to your fork and then create MR from your fork to main repo.

```
$ git remote add fork https://gitlab.com/<yourusername>/veloren
$ git push fork <yourusername>/update-uk_UA
```

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

