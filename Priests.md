**Is there an error? Something missing? Funky grammar? Do not hesitate to reach out on Discord to the [Priest team](https://github.com/orgs/simulationcraft/teams/priest/members).**

# Sim Module notes
The module is broken up into the following parts:
- Main Priest file - Holds base spells or other things available to more than one spec. ([sc_priest.cpp](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest.cpp) and [sc_priest.hpp](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest.hpp))
- Spec Files - Specialization specific implementations
  - [Discipline](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest_discipline.cpp)
  - [Holy](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest_holy.cpp)
  - [Shadow](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest_shadow.cpp)
- [APL File](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/apl/apl_priest.cpp) - Stores the Action Priority List for each spec.
- [Pet File](https://github.com/simulationcraft/simc/blob/shadowlands/engine/class_modules/priest/sc_priest_pets.cpp) - Handles all pets for Priest's (Shadowfiend, Mindbender, and Eternal Call to the Void Tentacles).

# Spell implementation notes
The following spells are mentioned due to oddities with the implementation that are not straightforward or require more clarification. If a spell is not mentioned here you can find it in the correct base or spec file with a typical implementation. Feel free to reach out in discord if you have questions.

## Shadow Weaving (Shadow Priest Mastery)
The Shadow Priest Mastery is not currently applied automatically by SimC due to improper spelldata. To get around this we apply this benefit manually to each priest spell with the `affected_by_shadow_weaving` option. This is turned off by default, so any spells that _are_ affected by mastery should have `affected_by_shadow_weaving = true;` added into the constructor. This should be done for priest or pet spells.

## Power Infusion
Power Infusion assumes that the actor is using the spell for its self-use only. To change this behavior, you need to set the option `priest.self_power_infusion=0`. Doing so will change the uptime of PI of the actor to 0%.

### Power Unto Others (Conduit)
This Conduit only works if you have `priest.self_power_infusion=0` or if you have the legendary Twins of the Sun Priestess equipped, as otherwise the actor is using PI on itself.

## Mind Blast
For the APL, Mind Blast by default will not work with typical `cast_while_casting=1`. This is because you can only cast this spell while casting Mind Flay or Mind Sear AND you have Dark Thoughts active. To make the APL easier to understand rather than having all these conditional checks there is a `only_cwc` option for Mind Blast only. This option defaults to `false` and with this you can have a separate APL line for the CWC Mind Blast.

## Power Word: Shield
By default Power Word: Shield will debuff the target with the Weakened Soul debuff and prevent PWS from being cast on that target until it expires. To simulate PWS spam over an entire raid, without having to simulate an entire raid, you can use the 'ignore\_debuff' option.
```ini
  # Chain spam PWS
  actions+=/power_word_shield,ignore_debuff=1
```

# Bugs
By activating `bugs=1` inside your character's sim you will get access to the following bugs:
- [Dark Thought Mind Sear Proc Rate](https://github.com/WarcraftPriests/sl-shadow-priest/issues/101)
- [Ghost Void Bolt Hit](https://github.com/SimCMinMax/WoW-BugTracker/issues/678)
- [Wrathful Faerie Insanity Gen](https://github.com/SimCMinMax/WoW-BugTracker/issues/777)

# Custom Options
## Self Power Infusion
To simulate giving away Power Infusion to someone else you can use `priest.self_power_infusion` (`default=1`). This option controls if the actor casts and gives themselves Power Infusion. See the section above on [Power Infusion](Priests#power-infusion) implementation details for more info.

## Boon of the Ascended (Kyrian Covenant Ability)
When running a sim for a player that is apart of the Kyrian covenant (`covenant=kyrian`) you will get access to a new ability: Boon of the Ascended. This ability gives you access to Ascended Blast (replaces Mind Flay / Smite) and Ascended Nova (8yd range) and will explode with Ascended Eruption (15yd range) based on the amount of stacks. By default the sim will cast all of these abilities and assume you are in range of ALL targets (unless you have added targets outside of the range). To disable this you can easily use these options:

- `priest.use_ascended_nova=0` (default: `1`)
- `priest.use_ascended_eruption=0` (default: `1`)

## Mindgames (Venthyr Covenant Ability)
This ability gives a total of 20insanity, however in order to get the full amount the target you cast it on must heal and do damage to break the shield. A player is given 10 insanity for each component that is broken up to a total of 20. By default SimC only assumes that the damage amount is broken, so the actor is only given 10 insanity. You can easily overwrite this with the following options:

- `priest.mindgames_damage_reversal=1` (default: `1`)
- `priest.mindgames_healing_reversal=0` (default: `0`)

These options also control the extra healing or damage that actors get when these are flipped on. So with `priest.mindgames_damage_reversal=1` the actor will generate a healing event in SimC by default (unless `priest.ignore_healing` is turned on). Additionally if `priest.mindgames_healing_reversal=1` the sim will create the damage reversal event as a child action to Mindgames. Both of these reversals assume the ENTIRE shield is broken, rather than a partial shield.

**Note:** to see the report output for healing actions you'll want to enable `enable_dps_healing=1`.

## Fae Guardians (Night Fae Covenant Ability)
Part of this ability increases the rate of which major cooldowns recharge, Shadowfiend/Mindbender and Power Infusion for Priests. You can simulate this effect being given to other players by changing the option `priest.self_benevolent_faerie=0` to false (default: `priest.self_benevolent_faerie=1`). When you disable this the sim will also turn off the automatic application of Wrathful Faerie when casting Fae Guardians. This is because it is impossible to give someone the full 20s value of Fae Guardians CDR from the Benevolent Faerie (you must target them) and still get the Wrathful Faerie. The sim then casts a Shadow Word: Pain right after Fae Guardians to apply this faerie on your current target.

## Cauterizing Shadows
When using the Cauterizing Shadows legendary you will see corresponding healing output whenever Shadow Word: Pain debuffs **expire**. This does **NOT** trigger if the sim refreshes the dot, or the target dies to match in-game behavior. When this does trigger, we assume that a default of 3 allies get the healing (by replicating the healing to the actor for each ally). To configure this you can adjust `priest.cauterizing_shadows_allies=x`, where X should be `0`, `1`, `2`, or `3` (default).

***

# Healing implementation
Healing sims are not currently supported in SimC. The following section is leftover from the last time this was worked on.

## Limitations
Fights in Simulationcraft are unidimensional: all players, pets and targets are on the same axis, only the distance from the main target changes. besides, although players can lose health (because they're tanking or suffering from damages on the whole raid), they will continue to perform actions after their death (and there may be some fancy bugs here). As a result, some spells exhibit a behaviour slightly different from their in-game counterparts.

Regarding the reports, only the total healing done will be reported, not the actual healing done or the overhealing.

## Setting up a simulation
To use healing features in Simulationcraft, import or declare a discipline or holy priest and ensure his role is set to "heal" (should be the default for those specs). We also suggest you add other players, even dummy ones (add single lines such as "warrior=john"). And maybe a tank (use "role=tank").

## Targets
Regarding the targets, by default it is always the caster himself. Although the default target cannot be changed, you can explicitly specify on every action the target of your choice. You can also add a condition to check the target's health, see [ActionLists](ActionLists).
```ini
 # Cast flash heal on John when he has less than 50% health.
 actions+=/flash_heal,target=John,if=target.health_pct<50
```

Spells with many targets are detailed in the next section; eligible targets will be friendly, non-pet, targets in range (when relevant) and they will be sequentially chosen (following the declaration or importation order) unless specified otherwise.