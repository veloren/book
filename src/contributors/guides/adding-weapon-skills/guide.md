# Guide: Adding Weapon Skills to Veloren

\\\_ written by @Sam with additions from @James

### Define your skill

The first thing you need to do is define your skill and figure out what parameters it will need.
It is important to do this as sometimes the new skill can be handled by one of the current character states, and if it’s close, then only 1 or 2 additional could be added to a pre-existing character state.

### Adding your skill

Weapon attack skills are handled by character states. As of this edit, these are the following character states (though ComboMelee is in the works and TripleStrike is on the way out).

```rust,ignore
pub enum CharacterAbilityType {
      BasicMelee,
      BasicRanged,
      Boost,
      ChargedRanged,
      ChargedMelee,
      DashMelee,
      BasicBlock,
      TripleStrike(Stage),
      LeapMelee,
      SpinMelee,
  }
```

These character states can be (and are) reused for multiple skills. Your new skill may fit easily into one of these states. The state may need to be adjusted slightly to accomodate your skill. The third alternative is the addition of a new character state. All three of these possibilities are covered in the following sections.

#### If your skill can be handled by an existing character state

Go to `common/src/somp/inventory/item/tool.rs`

Once there, add an additional attack to the weapon which you are adding an attack to. Note that a weapon’s abilities are handled by a vector, with the first ability tied to M1, the second to M2, the third to skillbar slot 1, and additional ones to more skillbar slots (only skillbar slot 1 might be implemented right now).

#### If your skill requires modifying an existing character state

Go to `common/src/states/`.

Open the corresponding character state file. In the Data struct at the top, add the additional fields you need, you’ll also need to add it to every section in the code that updates the character state data (the compiler will throw errors if you forget). Then proceed through the code and change any logic necessary.

Go to `common/src/comp/ability.rs`.

Look for where the fields of the character state are defined. They are defined in 3 places. The top one determines what fields are read from tool.rs, the second one reads from tool.rs, and the third one constructs the Data struct in the character state file. Sometimes you may only need to add the new field to the 3rd section, though usually you’ll need to add your new field to all 3.

Go to `common/src/comp/inventory/item/tool.rs`.

Once there add your new attack to the weapon you want. Also, if any weapon already had the attack, update the fields to include the new variable you added.

#### If your skill requires creating a new character state

Go to `common/src/states/`.

Create a new file, and give it a name appropriate to the character state you are adding. It can be helpful to start by copying a file from a similar character state. Create the logic for your character state, and determine what fields will need to be passed into the state in the Data struct at the top.

Also, in this section, you will need to determine what kind of attack your character state is. Currently there are systems for melee attacks, projectiles, and explosions. There will soon be support for shockwaves and beams. If you need some other system to handle your attack, ping me (@Sam) for assistance.

Go to `common/src/states/mod.rs`.

Add your character state to this file, keep it sorted alphabetically

Go to `common/src/comp/ability.rs`.

In each location every other character state is handled, add your new character state (it can be helpful to search in the file for “leapmelee” or “leap” and just add your character state stuff in each location. The locations to be careful of your logic though are the 3 locations where the fields of your character state are defined (see section for modifying character state for more detail) and where it checks the requirements of entering the character state (though you can almost always just copy what other character states do).

Go to `common/src/comp/inventory/item/tool.rs`.

Add your new character state as an attack for the weapons you want to add it to. Ensure that the fields in this location match the fields passed into the first section of ability.rs.

Go to `common/src/comp/character_state.rs`.

Add your character state to the CharacterState enum (ideally include a short description too). Look in the implementation of CharacterState, if yours is described by any of the functions, add it there.

Go to `common/src/sys/character_behavior.rs`.

Search for any character state (e.g. LeapMelee). Add your character state in the 2 locations the other character states are handled with the same logic.

Go to `common/src/sys/stats.rs`.

Add logic for how your character state affects natural energy regen here. (If it’s an attack or consumes energy it should disable natural energy regen).

### Adding an Ability to the Skillbar

(When skill trees are implemented this section will be updated)

As every weapon currently implemented already has at least 2 abilities, the chances are high you will need to either add your ability to the skillbar or move a currently existing ability to the skillbar. 

In the tool.rs file, the ordering of abilities in the vector determines what slot they’ll be assigned to. The first slot is M1, the second M2, the third skillbar 1, the fourth skillbar 2, etc. So when adding your ability, ensure that it is in the correct location in the abilities vector.

Go to `voxygen/src/hud/hotbar.rs`

Add the weapon type you are adding the third skill to the logic when determining the value for the bool should be present. It should be as simple as adding:

```rust,ignore
else if let ToolKind::Hammer(_) = &kind.kind {
    true
}
```

Add an icon in `assets/voxygen/element/icons`. Skill icons should be 20 x 20 pixels with transparent corner pixels. Check the pins in the assets or veloren-art channel on Discord to find the appropriate color pallet. Ping @Pfau on Discord to see if someone will design a better icon or to get yours approved.

Go to `voxygen/src/hud/img_ids.rs`.

There is a section around line 140 listing all M1 and M2 icon locations. Add your skill here with the path to its icon. If your skill is going on the skillbar, add your skill/icon pair to the "Icons" section around line 270 instead.

Go to `voxygen/src/hud/skillbar.rs`.

If your skill is replacing an M1 or M2 skill, add it to the match around line 620 for M1 and around line 700 for M2.

For M1 and M2, add an arm to the match expression around line 730 to make the skill icon fade when `self.energy.current()` is over the energy drain of your skill. If your skill does not have an energy drain (and should always be available), you do not need to put your skill in this match.

If your skill is going in the hotbar, follow the steps below:

Add a name and description of the skill around line 800 of `voxygen/src/hud/skillbar.rs`. Just look at the logic of the skills currently there. This will add a tooltip and a name for the skill.

Go to `voxygen/src/hud/slots.rs`.

Around line 90 add your skill to the HotbarImage enum.

Around line 120 make the appropriate weapon match return the proper skill from the HotbarImage enum.

Around line 130 add your skill to the match. Copy the logic of one of the other skills herebut make `energy.current() < ENERGY_DRAIN` where `ENERGY_DRAIN` is the energy drain of your skill. This will make the icon fade when the player does not have enough stamina.

In the `image_id` function around line 165, add the path identifier for your skill (copy the logic of the other skills).

### Animations

Ping @Slipped on Discord.
You can also dig through previous MRs (like this one: `https://gitlab.com/veloren/veloren/-/merge_requests/1171/diffs`) if you want to see how to do it yourself (this’ll show where to add stuff, and show you what code for other animations looks like).

### Changelog

Go to `CHANGELOG.md`
Add a line saying you added an attack

