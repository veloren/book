# Translate the game

## Preparation

There are different ways to contribute translations, but the most straightforward
way is by using Git and Rust. You don't need to compile the game, although debug
builds have useful features like hot-reloading for translations, that allow you
to translate the game while running it.
Tooling to check the status of your translations doesn't require compiling the
full game, but it still requires the Rust toolchain.
Read this [guide on basic tooling](../development-tools.md) (the Git LFS extension is important),
[working with git](https://rogerdudler.github.io/git-guide/) (git is not a
user-friendly tool, ask if you don't understand something),
[compile instructions](../compiling.md),
and [contribution instructions](../before-you-contribute.md) (most important).

Alternatively, you can just work directly on [assets](../../players/airshipper.md)
shipped by Airshipper. Beware that updating your game will purge all your work, so
think about using the [VELOREN_ASSETS_OVERRIDE](../../players/env-vars.md#veloren_assets_override) environment variable.

## File and directory structure explained

You can see the localization files inside the `assets/voxygen/i18n` directory.
Each subdirectory inside represents a language, or a variant of it.
The directories are named after [IETF BCP 47](https://www.rfc-editor.org/refs/ref-bcp47.txt) ([RFC5646](https://www.rfc-editor.org/rfc/rfc5646.html)) language tags (e.g. `en/`, `de/`, `pt-BR/`, etc). A language tag is comprised of one or more subtags, separated by hyphens ("-").

This is a comprehensive list of available language subtags:

[IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

Veloren uses a key-value system to translate content. Files use the [Fluent
localization format](https://projectfluent.org) (`.ftl`). Check examples at the
main page and the [syntax guide](https://projectfluent.org/fluent/guide/).

They must be formatted in UTF-8, without [BOM](https://en.wikipedia.org/wiki/Byte_order_mark).
Each language directory contains a `_manifest.ron` file with a metadata section,
font settings that will be used in the game and a `convert_utf8_to_ascii` option,
which can be used when translating a language which has characters that aren't
in the fonts Veloren uses. Don't be afraid to ask for the addition of these
characters to the fonts used by the game via our Discord community

The metadata section includes a display name and an identifier for the
language. The display name may be freely changed but the identifier should
stay the same after the introduction of a new language:

```rust, ignore
metadata: (
    language_name: "English",
    language_identifier: "en",
),
```

> Note: The language identifier must match the name of the containing language folder. This requirement implies the identifier must also comply with the IETF BCP 47 naming standard.

`.ftl` files contain a list of messages in key-value format.

Fluent messages may or may not have variables inside via syntax of [placeables](https://projectfluent.org/fluent/guide/placeables.html).

```fluent
main-servers-other_error = Server general error: { $raw_error }
main-credits = Credits
```

Some messages may have multiple attributes attached to them.
Attributes can have various uses, as of the time of writing we use it to create
randomized messages.

```fluent
loading-tips =
    .a0 = Press '{ $gameinput-togglelantern }' to light your lantern.
    .a1 = Press '{ $gameinput-help }' to see all default keybindings.
    .a2 = You can type /say or /s to only chat with players directly around you.
    .a3 = You can type /region or /r to only chat with players a couple of hundred blocks around you.
```

Fluent also supports plural selectors via
[Unicode rules](https://www.unicode.org/cldr/cldr-aux/charts/30/supplemental/language_plural_rules.html).

```fluent
hud-trade-buy_price = Buy Price: {$coins ->
  [1] 1 coin
  *[other] { $coins } coins
}
```

## Localization test explained

Veloren includes a localization test tool for translated languages. This test
gathers information about every key and compares them with the reference
language. English is the reference language, defined in the `en/` directory.

The tool then classifies and counts these
comparisons and prints them in a neat way for translators to inspect.
This guide explains where to find the test and how to read the results of it.

We have this fancy [web service](https://grafana.veloren.net/d/mNjODNM7z/translations)
to display translations statistics.
![Grafana header](./grafana_header.png)

We will use the Ukrainian translation as our example.
![Grafana for Ukrainian](./grafana.png)

Here we have detailed information about all language keys used in the Ukrainian
translation (`uk` directory) in comparison with the reference language translation (English - `en/` directory).

The `status` section displayed for each key has the following possible values:

- `Unused`: The key exists in the Ukrainian translation but not in the English
  translation. These are keys that have been used before in the game but
  have been removed since they weren't needed or have been renamed. These
  are safe to remove.
  
- `NotFound`: The key exists in the English translation but doesn't exist in
  the Ukrainian translation. Here we need your translation!

- `Outdated`: Currently not available, means that some changes were made to the
English translation, but not to the Ukrainian translation.

## Guide to translating the game

Guides to help you translate the game, for certain situations. If you get
stuck at any step or need more help (or just have questions) ask us in our
Discord server.

If you are not familiar with GitLab or Git, feel free to ping `@git-wizard`,
who will always be on deck to help with this.

## Create a translation from scratch

If there is no translation for your language, you can create one by following
these instructions. Remember to replace the Turkish language example with your
own language!

First of all, you need a copy of the Veloren repository. Refer to the
[working with git](../working-with-git.md) section for this.

After you have obtained a copy of the repository, navigate to the `assets/voxygen/i18n`
directory. Here you'll see a list of translations, and the reference English directory
(`en/`).
Make a copy of the `en/` directory, named after your language. For example, if you want
to translate Turkish, your directory would be named `tr/`.

Then, you can start editing the file! First go to the metadata section in `_manifest.ron`.
This section has the display name and the language identifier for your translation.
Change `language_name` to a human readable name in your language with this format:

```text
<name_in_original_language> (<name_in_english>)
```

For example:

```rust, ignore
metadata: (
    language_name: "Türkçe (Turkish)",
    language_identifier: "tr",
),
```

If the language is a variant spoken in a certain region or country, follow this format:

```text
<name_in_original_language> (<name_in_english> - <region>)
```

Two examples of this case are:

```rust, ignore
metadata: (
    language_name: "Español de España (Spanish - Spain)",
    language_identifier: "es",
),
```

And:

```rust, ignore
metadata: (
    language_name: "Español de Hispanoamérica (Spanish - Latin America)",
    language_identifier: "es-419",
),
```

Remember to set the value of `language_identifier` to match the parent directory's name.

And that's it! **No code changes required**. You can now start translating any key
you want. Don't forget to preview the changes in-game by [compiling and running
](../compiling.md) the game, and setting the language setting to your new
in-translation language. If there are missing characters, don't worry, you can
ask us about these in our Discord server.

**Tip:** You don't need to compile game to test your changes, you can
just copy your changes to `assets` directory in app folder.
If you have installed the game via Airshipper look in these
[directories](../../players/airshipper.md#files).

**Tip:** You can set `convert_utf8_to_ascii` option to `true` to
convert everything to ASCII, so that the missing characters can be seen properly.

After you are happy with your translation, commit your changes with a proper
commit message, such as `Added Turkish (Turkey) translation`. Create a new
branch with the name `<yourusername>/add-<language>`. Then push your changes and
create a merge request (don't forget to read and tick the appropriate checkboxes! **The license checkbox is required**). You can
notify us on the Discord server that there is a new translation available
(in the **#translation** channel).

## Improving an existing translation

If you are lucky, you may already find that there is a translation for your
language. If you see that it has some missing, incorrect translations or
you think that you have a better translation for something, then this guide
is for you! Don't forget to replace the Ukrainian example with your own
language (if you aren't translating the Ukrainian language).

Okay, let's say we want to add the correct translation for the Ukrainian of
`buff-desc-cursed`.
So we first want to look it up in the reference language (English)
`assets/voxygen/i18n/en/buff.ftl`.
After the key we find this English sentence: `Cursed`. The Ukrainian equivalent would be `Проклін`.
Then, we open the translated language (Ukrainian)
[`assets/voxygen/i18n/uk/buff.ftl`](https://gitlab.com/veloren/veloren/-/blob/master/assets/voxygen/i18n/uk/buff.ftl).

**Tip:** Keep both the reference language and the translated language open,
so that you can find in which place your entry is missing by looking at the
line numbers.

Once you are editing the file on GitLab, go to the place where our entry is
missing and add it here:

```fluent
buff-title-cursed = Проклін
buff-desc-cursed = Вас прокляли
```

## Getting information about the translation

If you are able to compile, you can use a special tool to get information about the translation.
Basically, it is the same program that runs on our CI, but you can cut out unneeded
information.
For example, you want to get information about the Ukrainian translation.

```bash
cargo run --bin i18n-check --features=bin -- uk
```

You can also run it with `--help` argument to find out more ways to use it.

**Note:** Arguments go after `--`, it's where `cargo` arguments end and actual
arguments start.

**Note:** You need to commit your changes for `veloren-i18n` to know about it.

## Push changes

When you're done (or even before you start), create a branch with name
`<yourusername>/update-<language>`. An example would be `juliancoffee/update-uk`.
Then create a commit and give it specific commit message such as `update the
<language> translation`. In our example this would be `update the Ukrainian
translation`.
Finally, you'll need to create a merge request. Note that you need to push your
branch to the developer repository, while making a MR from developer repository
to main one.
Read and check the boxes to agree that your code will be under the GPL3 license.

If you have at least the Contributor role, use the `/review` command in the `#new-contributors` channel.
If you don't have it, ask for it and use the command.

You now requested to change the files, and we will then take a look at it and if
we found it okay we will merge it into the game! From that point on your
contribution will land in the `master` branch and, eventually (usually within a week), people will start getting the new translation via Airshipper.

## Help review pending translations

Someone may have done a translation for your language already. To check this,
you can take a look at the [Merge Requests](https://gitlab.com/veloren/veloren/-/merge_requests) page.
See if you can find a pending merge request with your language (e.g. `de` for German).
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
