# Internationalization Developer's Guide

So, if a feature you're working on requires any text, it's probably related to i18n.
This guide will help you on that journey, and covers:
- high-level system overview
- best practices and anti-patterns
- examples

Let's start with quick high level overview.

## Foundational crates

We have two foundational crates with utilities you'll need to use:
- `client/i18n` \
Flesh and blood of our translation capabilities. \
It's based on `fluent-rs` crate and `assets_manager`'s wrapper we have in `common/assets`. \
\
Most useful type from this crate is [Localization](https://docs.veloren.net/veloren_client_i18n/type.Localization.html)
which exposes `get_msg`-family methods, which take i18n key and `get_content` method
which can take `Content` object. Both give you ready-to-use translated string.
- `common/i18n` \
Governs interfaces for localization when you need to do it outside of `voxygen`. \
Most importantly `Content` type which is a recursive type which represents delayed evalution of i18n with required context.

**Tip:** you don't need `Content`, if you're already in `voxygen`. Just use `get_msg` or `get_msg_ctx`.

The point of founational crates is that they are super small, fast to compile, and much more abstract.

## Application crates
Now when you know *what* you can use for translation, let's talk about crates *where* you can use it:

- `voxygen` \
*The* client crate. Manages graphics, audio, and UI. And UI uses text, as you can guess. \
All widgets must have access to `i18n::Localization` there, so if you need a translated string, *do it*.

- `server` and co\
There's much difference in which crate you work really, because they dont't have access to `Localization` object. \
They don't even know what language players use. \
Instead, if you're producing some message server-side, like NPC message, command result, NPC name, you
should use `Content`.

## Assets
It's all good that you can code whatever you want, you still need assets.

So let's check them out:
- `assets/voxygen/i18n/` \
The folder where all Fluent files live. If you want to add new string, pick file that looks good to you,
put new key there and you're good. \
If you think you need to create a new file, please consult translation team.
- `assets/common/` \
Holds various files that pretty much hold `Content` identifiers:
  - `assets/common/entity/**/*.ron` uses `name: Translated` to reference i18n content.
  - `assets/common/npc_names.ron` uses `generic: <i18n-key>` to get translations for names.
  - `assets/common/item_i18n_manifest.ron` is a mapping from item def to its translation.
  - etc

## Best practices & recommendation
Ok, I'll put this in bold: **Keep It Simple**

If you don't remember anything else, remember this. \
Fluent is a powerful format, because localization is hard. We **must** provide the most straightfoward
interface to translators, and introducing our own abstractions and requiring re-usable pieces on top will
lead to bugs.

This goes against traditional rules of programming, where we strive for writing as little code as possible
and reusing as much as possible, but it doesn't work for translations, because we don't know what exactly
to re-use.

### Don't concatenate
To reference Fluent docs. 
```fluent
# ❌ Avoid splitting messages.
reaction-thumbs-up = thumbs up
reaction-smiley-face = smiley face
reacted-with = { $user_name } has reacted with a { $reaction_type }.
```
That looks like correct message in English, but it can fall apart real quick.
What if you add reaction for "Eye roll", which should start with `an` and not `a`?

To avoid such situations, here's a first rule for you: **Don't concatenate**

The same can be rewritten as follows.
```fluent
# ✅ Redundancy helps localizers understand each message in full.
reacted-with-thumbs-up = { $user_name } has reacted with a thumbs up.
reacted-with-smiley-face = { $user_name } has reacted with a smiley face.
reacted-with-eye-roll = { $user-name } has reacted with an eye-roll.
```

There are exceptions to this rule. If you'd have combinatorial number of strings otherwise, you'll be
forced to use concatenation, but please be super careful and consult translation team. \
And if you need to use concatenation, expose the template to give translators maximum control.


### Don't use selectors for logic
```fluent
# ❌ Don't use selectors for logic
dialogue-buy_hire_days = { $days ->
    [1] A day
    [7] A week
    *[other] { $days } days
}
```
The golden rule is that all variants of selectors should have exactly the same meaning. \
If you want to put a logic somewhere, put it in your code and then call the right key.
```fluent
# ✅ Uses attributes for logic, exposes selectors to handle plurals.
dialogue-buy_hire_days =
   .day = A day
   .week = A week
   .unknown = { $days ->
     [one] { $days } day
     *[other] { $days } days
    }
```

### Pay attention to gender
We only recently started doing that, but if possible, try to provide a gender string.
```fluent
hud-chat-online_msg =
    { $user_gender ->
        [she] [{ $name }] si è connessa.
       *[he] [{ $name }] si è connesso.
    }
```
The code for that would look something like that.
```rust, ignore
    // getting the string
    let gender_str = |uid: &Uid| {
        if let Some(pi) = info.player_info.get(uid) {
            match pi.character.as_ref().and_then(|c| c.gender) {
                Some(Gender::Feminine) => "she".to_owned(),
                Some(Gender::Masculine) => "he".to_owned(),
                _ => "??".to_owned(),
            }
        } else {
            "??".to_owned()
        }
    };
    // usage
    localization
        .get_msg_ctx("hud-chat-online_msg", &i18n::fluent_args! {
            "user_gender" => gender_str(uid),
            "name" => name_format(uid),
        })
```
Important bit is in `player_info` which holds `character` which holds gender.
For now, we only support two genders which is unfortunate, but hopefully we'll improve it soon.

### Provide a good example
Translators have different knowledge levels, so try to create some redundancy in English versions.
```fluent
# ❌ [one] doesn't mean *single* item
# ❌ Concatenation makes it harder to see whole picture
hud-trade-buy = Buy Price: { $coin_num ->
    [one] one coin
    *[other] { $coin_formatted } coins
}
```
While, again, it's a correct string, at least when it comes to English, it has some issues.
```fluent
# ✅ Uses [1] for exact match
# ✅ String isn't interrupted by selectors, always full.
hud-trade-buy = { $coin_num ->
    [1] Buy Price: one coin
    *[other] Buy Price: { $coin_formatted } coins
}
```
For example, the correct way to translate it to Ukrainian would be following.
```fluent
hud-trade-buy =
    { $coin_num ->
        [1] Ціна купівлі: одна монета
        [one] Ціна купівлі: { $coin_formatted } монета
        [few] Ціна купівлі: { $coin_formatted } монети
        [many] Ціна купівлі: { $coin_formatted } монет
       *[other] Ціна купівлі: { $coin_formatted } монет
    }
```
But if a person not fully understanding the rules would copy first example, we could get
something like
```fluent
# ❌ 21 would mean [one] as well, while we assume [one] means 1 only
hud-trade-buy = { $coin_num ->
    [one] Ціна купівлі: 1 монета
    *[other] Ціна купівлі: { $coin_formatted } монет
}
```
And because in Ukranian things like "21" follows the same rules as "1", it falls into category
of `[one]`, we would get "Ціна купівлі: 1 монета", which is obviously incorrect, because, well
"21" isn't "1".

So please, consider this when providing English strings.

## Examples
### GUI
Let's say you want to internationalize warning message when some abstraction
will force dropping items.

You'd start by adding a key to fluent file, `assets/voxygen/i18n/en/hud/bag.ftl`.
```fluent
hud-bag-swap_slots_drop_items = { $slot_deficit ->
    [1] This will result in dropping 1 item on the ground. Are you sure?
    *[other] This will result in dropping { $slot_deficit } items on the ground. Are you sure?
}
```
Then you take a function that expects string and use `LocalizationHandle::get_msg_ctx` on it.
```rust,ignore
self.hud.set_prompt_dialog(PromptDialogSettings::new(
    global_state.i18n.read().get_msg_ctx(
            "hud-bag-use_slot_equip_drop_items",
            &i18n::fluent_args! {
                "slot_deficit" => slot_deficit.unsigned_abs(),
            })
        ),
    ),
```
p.s. if you get some lifetime errors, it is Rust, it happens, dancing 
with borrowchecker is out of scope for this guide, may the Feris be with you.
### Server Message
Ok, this is a super simple function, but it allows us to demonstrate how would you use `Content` type.
```rust,ignore
fn handle_version(
    server: &mut Server,
    client: EcsEntity,
    _target: EcsEntity,
    _args: Vec<String>,
    _action: &ServerChatCommand,
) -> CmdResult<()> {
    server.notify_client(
        client,
        ServerGeneral::server_msg(
            ChatType::CommandInfo,
            Content::localized_with_args("command-version-current", [
                ("hash", (*common::util::GIT_HASH).to_owned()),
                ("date", (*common::util::GIT_DATE).to_owned()),
            ]),
        ),
    );
    Ok(())
}
```
`ServerGeneral::server_msg` function takes `Content`, because we need localization, but can't use `LocalizationHandle`. \
Here we're using `Content::localized_with_args` which takes a key you want to localize and list of (key, value) arguments.

And of course, if we define a command, we also need to give it a description, for which you can use `Content` as well.
Deep inside `ServerChatCommand::data()` function you'll need to add this.
```rust,ignore
            ServerChatCommand::Version => {
                cmd(vec![], Content::localized("command-version-desc"), None)
            },
```
Most commands have more complicated data, but `/version` is super simple, we only need to define its description. \
And because it doesn't need any context, we can just use `Content::localized` and not `Content::localized_with_args`.

Last but not least, don't forget to add both strings to `assets/voxygen/i18n/en/command.ftl`.
```fluent
command-version-desc = Prints server version
command-version-current = Server is running { $hash }[{ $date }]
```

## Conclusion
That's all. I tried to cover everything, but I probably missed some things, so don't hesite to ask. \
In general, before making an MR, I strongly recommend reaching out to someone and *talk*. \
And on that note, writing documentation is hard, and the help is always appreciated. If something is
unclear, *you* can improve it. You don't need to know everything to be helpful, you just need to be patient.