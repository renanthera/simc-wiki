# Expansion-specific options

Note that expansion-specific options may disappear from Simulationcraft versions intended for newer expansions than what is defined here.

## Shadowlands

### Covenants

 * **covenant** (scope: player; default: none) A new player option that takes a covenant identifier or tokenized name. This will enable the corresponding covenant ability for the player's class.
 * **soulbind** (scope: player; default: empty) A new player option that takes a `/` delimited list of soulbind abilities and conduits. Each conduit has a rank specified after the conduit identifier separated by a `:`. Note that the simulator currently does not check whether the combination of soulbinds and conduits is possible. This is a conscious decision to give the users the most flexibility in how they want to express their soulbind-related effects in an actor profile. This may change in the future if it turns out that we need to apply limitations to the valid set of soulbinds. You can also use the tokenized name of the conduit or soulbind ability as the identifier. This option will not do anything if a covenant is not selected for the actor.

 Soulbind token schemes:
 * `conduit_id:rank`
 * `tokenized_conduit_name:rank`
 * `soulbind_spell_id`
 * `tokenized_soulbind_name`

### Runeforge Legendaries

Runeforge legendary effects are applied to items through bonus ids. A list of Runeforge legendary effects and their bonus ids (see column 1) can be found here: https://github.com/simulationcraft/simc/blob/shadowlands/engine/dbc/generated/item_runeforge.inc

### Other 9.0 options
 * **shadowlands.combat_meditation_extend_chance** (scope: global; default: 1.0) The chance that the player picks up each orb to extend Combat Meditation soulbind ability.
 * **shadowlands.pointed_courage_nearby** (scope: global; default: 5; min: 0; max: 5) The number of nearby allies and enemies for the Pointed Courage soulbind ability. The player does not count as an ally, but pets do.
 * **shadowlands.lead_by_example_nearby** (scope: global; default: 2; max: 4) The number of nearby allies for the Lead by Example soulbind ability.
 * **shadowlands.stone_legionnaires_in_party** (scope: global; default: 0) The number of other players in each player's party with the Stone Legion Heraldry trinket.
 * **shadowlands.crimson_choir_in_party** (scope: global; default: 0) The number of other players in each player's party with the Cabalist's Hymnal trinket.
* **shadowlands.judgment_of_the_arbiter_arc_chance**
 * **shadowlands.volatile_solvent_type** (scope: global; default: none) The type of corpse/buff you've consumed for the Volatile Solvent soulbind. Multiple types can be specified, delimited by `/` or `:`.  Valid types are:
    - Corpse type: "humanoid", "beast", "dragonkin", "elemental", "giant"
    - Buff type: "mastery", "primary", "crit", "magic", "physical"
* **shadowlands.disable_soul_igniter_second_use**
* **shadowlands.unbound_changeling_stat_type**
 * **shadowlands.anima_field_emitter_mean** (scope: global; default: 0) Average number of seconds that the player will receive the haste buff
 * **shadowlands.anima_field_emitter_stddev** (scope: global; default: 0) Standard deviation number of seconds that the player will receive the haste buff


## Battle for Azeroth

### Azerite

Battle for Azeroth introduces Azerite powers to specific item slots. Simulationcraft supports the specification of selected azerite powers for items, and the actor-level overriding of azerite powers.

 * **azerite_powers** (scope: item; default: empty) A new item option that takes a `/` or `:` delimited list of azerite power identifiers. Note that the simulator currently does not check whether the item is allowed to be azerite empowered. This is a conscious decision to give the users the most flexibility in how they want to express their azerite-related effects in an actor profile. This may change in the future if it turns out that we need to apply limitations to the valid set of items that can be empowered. You can also use the tokenized name of the azerite power as the identifier.
 * **azerite_level** (scope: item; default: 0) A new item option that specifies the azerite level of an item. Azerite level maps to an actual item level through a game table. Values from 1 to 300 are supported. Note that any item can be given an azerite level, not just the necklace in Battle for Azeroth.
 * **azerite_override** (scope: player; default: empty) An option that takes a list of `/` delimited azerite power override specifications. Each azerite power override is of the format `tokenized_power_name:ilevel` or `power_id:ilevel`. A special `ilevel` value of 0 will disable the azerite power for the actor, no matter the source (i.e., item, or other azerite power override specifications). You can also use the azerite power id as the name of the azerite power.
 * **disable_azerite** (scope: global; default: empty) An option that allows the user to disable some or all sources of azerite-related effects from the simulator. An option value `items` will disable azerite-related effects from item sources, and an option value `all` or `1` will disable all azerite-related effects (i.e., items and overrides) from the simulator. 

Additionally, the player expression `azerite.<tokenized_power_name>.enabled` will evaluate to `1` if the actor has the azerite power selected (through items or overrides). Otherwise the expression will evaluate to `0`. Player expression `azerite.<tokenized_power_name>.rank` evaluates to the number of items the actor has that has `<tokenized_power_name>` selected, or the number of overrides specified for the power..

A map containing the power ID, spell ID and name of each azerite trait can be found here:
https://github.com/simulationcraft/simc/blob/bfa-dev/engine/dbc/generated/azerite.inc

### Azerite-power and item specific options

A number of azerite powers and items have characteristics that can be customized through expansion specific options. All of the following options are in the sim scope (i.e., global option that affects all actors in the profile). The following options are currently implemented.

  * **bfa.battlefield_debuff_stacks** (scope: global; default: 2) The number of damage events each actor is allowed to generate from each Battlefield Focus / Precision azerite trait proc on a target. Accepts values from the range 1-25.
  * **bfa.gutripper_default_rppm** (scope: global; default: 1.0) The proc chance of the Gutripper azerite power when the target has more than 30% health.
  * **bfa.jes_howler_allies** (scope: global; default: 4) The number of allies Jes' Howler trinket hits. Accepts values from 0 to 4.
  * **bfa.reorigination_array_stacks** (scope: gobal; default: 0) The number of stacks provided by the Uldir (raidzone) only buff, enabled by the traits "Laser Matrix" and "Archive of the Titans". Stacks are unlocked by killing three raid bosses each week. After doing so for 10 weeks the maximum stack count of 10 is unlocked. Accepts values from 0 to 10.
  * **bfa.secrets_of_the_deep_chance** (scope: global; default: 0.1) The chance to spawn a "rare" droplet (a void droplet). Accepts values from 0 to 1.
  * **bfa.secrets_of_the_deep_collect_chance** (scope: global; default: 1.0) The chance that the actors will pick up the droplets. Accepts values from 0 to 1.
  * **bfa.initial_archive_of_the_titans_stacks** (scope: global; default: 0) The number of stacks of the azerite trait Archive of the Titans to apply at the start of combat. This trait normally applies its first stack 5s into combat and increase by one stack every 5s thereafter. The stacks are reset when entering combat with a raid boss, but in non-raid encounters, such as Mythic+ dungeons, you can typically enter combat with certain number of stacks already present.
  * **bfa.seductive_power_pickup_chance** (scope: global; default: 1.0) Chance of picking up the visage spawned by Seductive Power azerite trait.
  * **bfa.initial_seductive_power_stacks** (scope: global; default: 0) How many stacks of Seductive Power buff to apply when the combat starts.
  * **bfa.randomize_oscillation** (scope: global; default: 1) Randomize Oscillation state of Variable Intensity Gigavolt Oscillating Reactor at the beginning of combat.
  * **bfa.auto_oscillating_overload** (scope: global; default: 1) Automatically cast Oscillating Overload (the On-Use effect of Variable Intensity Gigavolt Oscillating Reactor) when the V.I.G.O.R. Engaged buff reaches its maximum stack count. Disabling this option will enable `use_items` and `use_item` actions to control the triggering of Oscillating Overload.
  * **bfa.zuldazar** (scope: global; default: 0) Specifies whether the players are in Zuldazar, which is relevant for the Gift of the Loa set bonus from Battle of Dazar'alor.
  * **bfa.covenant_period** (scope: global; default: 1.0) Specifies the period (in seconds) of Treacherous Covenant updates (i.e. buff application or expiration).
  * **bfa.covenant_chance** (scope: global; default: 1.0) Chance of gaining Treacherous Covenant buff on each update (see **bfa.covenant_period**). This roughly corresponds to the buff uptime.
  * **bfa.incandescent_sliver_chance** (scope: global; default: 1.0) Chance of gaining a stack of Incandescent Sliver buff on each tick. When the random roll fails, a stack is removed (as if someone without the trinket was standing next to the actor).
  * **bfa.fight_or_flight_period** (scope: global; default: 1.0) Specifies the period (in seconds) of Fight or Flight proc attempts (as if the player was dropping below 35% hp in-game).
  * **bfa.fight_or_flight_chance** (scope: global; default: 0) Chance of triggering Fight or Flight buff (in the limits of the buff's own internal cooldown) on each attempt (see **bfa.fight_or_flight_period**).
  * **bfa.harbingers_inscrutable_will_silence_chance**, **bfa.harbingers_inscrutable_will_move_chance** (scope: global; default: 0.0 `silence_chance`, 1.0 `move_chance`) Specify the distribution of the three possible outcomes of a Harbinger's Inscrutable Will proc. `silence_chance` gives the fraction of projectiles that silence the player, `move_chance` gives the fraction of projectiles that do not silence the player but require movement, the remaining projectiles do not silence nor require movement. If `silence_chance + move_chance > 1`, `silence_chance` takes priority. For example: `silence_chance=0.4 move_chance=0.2` results in 40% procs silencing the player, 20% moving the player and 40% doing nothing. `silence_chance=0.8 move_chance=0.6` results in 80% procs silencing the player and 20% moving the player.
  * **bfa.aberrant_tidesage_damage_chance** (scope: global; default: 1) Chance that the player is above 60% HP when Leggings of the Aberrant Tidesage proc.
  * **bfa.fathuuls_floodguards_damage_chance** (scope: global; default: 1) Chance the player is above 90% HP when Fa'thuul's Floodguards proc.
  * **bfa.grips_of_forsaken_sanity_damage_chance** (scope: global; default: 1) Chance the player is above 90% HP when Grips of Forsaken Sanity proc.
  * **bfa.stormglide_steps_take_damage_chance** (scope: global; default: 0) Chance every second that the player takes damage which will remove the Untouchable buff.
  * **bfa.lurkers_insidious_gift_duration** (scope: global; default: 0) Overrides the duration of the Lurker's Insidious Gift trinket buff. A value of 0 will use the buff's maximum duration.
  * **bfa.abyssal_speakers_gauntlets_shield_duration** (scope: global; default: 0) Overrides the duration of the Ephemeral Vigor buff from Abyssal Speaker's Gauntlets. A value of 0 will use the buff's maximum duration. If the absorb shield is fully consumed by damage taken by the player, the effect will end.
  * **bfa.trident_of_deep_ocean_duration** (scope: global; default: 0) Overrides the duration of the Custody of the Deep absorb buff from Trident of Deep Ocean. A value of 0 will use the buff's maximum duration. If the absorb shield is fully consumed by damage taken by the player, the effect will end. Note that the effect is rppm based on damage taken only, and will not proc in the normal scenario of a non-tank simulation.
  * **bfa.legplates_of_unbound_anguish_chance** (scope: global; default: 1.0) Set the chance that the check for having a higher health percentage than the target succeeds. Note: since the proc is rppm-based, a reduced chance won't affect the number of procs linearly. As this replaces the health percentage check entirely, setting the enemy's fixed health percentage will not affect the proc's behaviour unless you also change this setting. Accepts values from 0 to 1.
#### 8.2 Rise of Azshara options
  * **bfa.loyal_to_the_end_allies** (scope: global; default 0) Set the number of allies that have the azerite trait Loyal to the End. Each ally increases the mastery bonus you gain from this trait, up to a maximum of 4 allies. Accepts values from 0 to 4.
  * **bfa.loyal_to_the_end_ally_death_chance** (scope: global; default 0.0) When an ally who has this trait dies, you are granted a buff to your haste, mastery, critical strike rating equal to the mastery rating you get from this trait. If this option is set, every 60s a check will be made to see if there is a chance equal to the setting that the buff will be triggered. Accepts values from 0.0 to 1.0.  
  **bfa.loyal_to_the_end_ally_death_timer** (scope: global; default 60; minimum 1) can be used to set the frequency in seconds in which the check is made.
  * **bfa.undulating_tides_lockout_chance** (scope: global; default 0.0) If you fall below 50% hp, undulating tides will give you a shield and give you a debuff that prevents any damage procs for 45s. If this option is set, every 60s a check will be made to see if there is a chance equal to the setting that the debuff will be triggered. Accepts values from 0.0 to 1.0.  
  **bfa.undulating_tides_lockout_timer** (scope: global; default 60; minimum 1) can be used to set the frequency in seconds in which the check is made.
  * **bfa.blood_of_the_enemy_in_range** (scope: global; default 1.0) Set the chance that you will be in range for the Blood of the Enemy major power. This ability is a 12 yd point blank area of effect that, at appropriate ranks, grants you an 'increased critical hit damage' buff and afflicts an 'increased chance to be critically hit' debuff on the enemy. This option simulates the chance that you will be out of range, thus doing no damage and not afflicting the debuff, while still getting the buff. Accepts values from 0.0 to 1.0.
  * **bfa.worldvein_allies** (scope: global; default 0) Set the amount of allies also using the Worldvein Resonance minor. At about 3 allies you will have 100% uptime on 4 stacks of the buff when using the rank 3 version of this essence.
  * **bfa.shiver_venom** (scope: global; default 0) Specify whether items that rely on the Shiver Venom debuff from Shiver Venom Relic should assume the debuff is present. Applies to Shiver Venom Crossbow and Shiver Venom Lance.
  * **bfa.leviathans_lure_base_rppm** (scope: global; default 0.5) Leviathan's Lure has a base rppm on the main damage proc which is increased over time by the trinket's second proc. This base rppm is currently unknown, and can be set with this option. Accepts values from 0.0 to 2.0.
  * **bfa.aquipotent_nautilus_catch_chance** (scope: global; default 1.0) Aquipotent Nautilus sends out a wave which damages enemies then returns to you. Catching the returning wave will lower the cooldown by 30s. The chance to catch the returning wave can be set with this option. Accepts values from 0.0 to 1.0.
  * **bfa.zaquls_portal_key_move_chance** (scope: global; default 0.0) Za'qul's Portal Key will summon a void tear which will open a portal to grant to a buff when you move near the tear. This option sets the chance that you will be forced to move to open the portal. Accepts values from 0.0 to 1.0.
  * **bfa.anuazshara_unleash_time** (scope: global; default _disabled_) Anu-Azshara, Staff of the Eternal will unleash its damage if you fall below 10% hp or mana. This option will set, in seconds, how many seconds into combat this will happen. Accepts minimum value of 1.
  * **bfa.nazjatar** (scope: global; default 1) Set to 0 to disable Nazjatar/Eternal Palace only special effects.
  * **bfa.storm_of_the_eternal_ratio** (scope global; default 0.05) Certain Storm of the Eternal effects grant crit/haste rating that is split between your raid. This option sets ratio of the total amount that will apply to you. Accepts values from 0.0 to 1.0.
  * **bfa.font_of_power_precombat_channel** (scope: global; default _disabled_) This option will set how many seconds before combat you will begin channeling the trinket Azshara's Font of Power. If this option is left disabled (but the action is present in the precombat APL, e.g. `actions.precombat+=/use_item,name=azsharas_font_of_power`), the trinket pre-channel timing will be adjusted to accomodate actions that follow it in the precombat APL.  
For example, if you set `bfa.font_of_power_precombat_channel=10` you will be considered to have begun channeling 10s before combat start, and will enter combat with a 24s buff, the trinket on 110s cooldown, and shared trinket cooldown of 10s. Accepts values from 0 to 34.
  * **bfa.arcane_heart_hps** (scope global; default 0) Sets the healing per second done on top of the sim damage. Note that not all healing in game is counted for this (E.g. leech). This healing would need to be deducted from the hps seen in game. Accepts any positive int value.
  * **bfa.ripple_in_space_proc_chance** (scope global; default 0) Sets the chance to proc the ripple in space minor. Chance is checked every second and cannot proc while on cooldown. Accepts values from 0.0 to 1.0.

#### 8.3 - Visions of N'Zoth  options

* **bfa.voidtwisted_titanshard_percent_duration** (scope global; default 0.5) How long the crit buff lasts (as a percentage). For example 1 provides full duration (15 seconds) and 0.5 would provide half duration (7.5 seconds)
* **bfa.surging_vitality_damage_taken_period** (scope global; default 0) Sets how often to create a fake damage event to attempt to proc Surging Vitality.
* **bfa.manifesto_allies_start** (scope global; default 0; max 12) Number of allies within 8 yards when the trinket is used (more allies = lower crit)
* **bfa.manifesto_allies_end** (scope global; default 4; max 4) Number of allies within 5-20 yards(depending on cloak rank) when the first buff ends (more allies = more vers)
* **bfa.echoing_void_collapse_chance** (scope global; default 0.15; max 1) Chance that the Echoing Void collapses on ability use which deals AOE damage.
* **bfa.void_ritual_increased_chance_active** (scope global; default 0) Set to 1 to simulate the increased proc chance when allies are near you.
* **bfa.symbiotic_presence_interval** (scope global; default 22) Approximate interval in seconds between raid member major essence uses that trigger Symbiotic Presence (The Formless Void).
* **bfa.whispered_truths_offensive_chance** (scope global; default 0.75) Percentage of Whispered Truths reductions to be applied to offensive spells.
* **bfa.nyalotha** (scope: global; default: 1) Specifies whether the players are in Ny'alotha, which is relevant for the Titanic Empowerment set bonus.
* **bfa.infinite_stars_miss_chance** (scope global; default: 0.0) Chance to have an Infinite Stars proc miss (useful for single target sims)

### Azerite Essences
Battle for Azeroth introduced Azerite Essences as a different empowerment system to the necklace. Contrary to the Azerite Trait system of Head, Shoulders, and Chest these Essences consist of two separate effects. A major and a minor one. The necklace offers two types of slots. One Major slot, which activated the major **and** minor effect of the applied essence and 2 minor slots, which activate only the minor effects. Selection and replacement of the essences happens for free in any resting area. SimulationCraft offers the following additional option to add these effects to a profile.

* **azerite_essences** (scope: character, default empty) Enables the provided azerite essences for that character (and any who inherits from it). format: `token/token/token`. An example will be provided below.

Token schemes:
* `essence_id:rank`
* `essence_id:rank:type`
* `spell_id`

`essence_id` can either be found in `AzeriteEssence.db2` or uses the tokenized form of the essence name
* `rank`: 1...4
* `type`: 0 (minor) **or** 1 (major)
* `spell_id`: passive milestone spell id

Only 2 or 3 element tokens for major/minor powers allowed. If 2 element tokens are used, the first element is the major essence, and the two subsequent tokens are the minor essences. In 3 element tokens, ordering does not matter. Placement of passive milestone spells is irrelevant.

**Typical essence IDs**
```
4    Worldvein
5    Focusing Iris
6    Purification Protocol
7    Anima of Life and Death
12   Crucible of Flames (Concentrated Flames)
14   Condensed Life-Force / Guardian of Azeroth
15   Ripple in Space
22   Vision of Perfection
23   Blood of the Enemy
27   Lucid Dreams
28   Unbound Force
32   Conflict and Strife
35   Breath of the Dying
36   Spark of Inspiration
37   The Formless Void
```

**Examples**

Enables Lucid Dreams major and minor effect.
```
azerite_essences=27:3
```
Enables Crucible of Flames major and Ripple in Space minor.
```
azerite_essences=12:3/15:3
```
Enables Crucible of Flames major and Ripple in Space minor but this time uses their type explicitly to order them freely.
```
azerite_essences=ripple_in_space:3:0/crucible_of_flames:3:1
```

### Corruption

Battle for Azeroth introduced gear corruption in patch 8.3. This system adds new affixes on gear, as well as two new substats: Corruption and Corruption Resistance. 
Non-azerite gear obtained in patch 8.3 from seasonal content can come with new powers on top of their regular stats. These bonuses are associated with a Corruption stat increase on the item. Players can remove ("cleanse") the corruption effects from an item or chose to equip it and offset Corruption with Corruption Resistance, obtained from the new legendary cloak and new Azerite Essences.
You can affect the corruption on a player with the following options:
 * **gear_corruption** and **gear_corruption_resistance** (scope: player) will override the total corruption and total corruption resistance from a profile's gear.
 * **enchant_corruption** and **enchant_corruption_resistance** (scope: player) will add (or substract if provided a negative value) the amount specified to the profile's current corruption or corruption resistance
 * **enchant** (scope: item) can be used in the same way as with regular stats to add a fake enchantment to an item, artificially increasing its Corruption or Corruption Resistance stat

```
# Override the gear_corruption and gear_corruption_resistance to 30 to ensure that Heart of Darkness is always active
gear_corruption=30
gear_corruption_resistance=0

# Add 30 corruption to a profile
enchant_corruption=30

# Substract 50 corruption resistance from a profile
enchant_corruption_resistance=-50

# Enchant an item with +15 corruption
wrists=dragonbone_vambraces,id=174170,bonus_id=4824/1517,enchant=15Cor
```

## Legion

### Items

Legion introduced several trinkets that require a separate option to control an aspect of the trinket simulation model.

 * **legion.infernal_cinders_users** (scope: global; default: 1; range: 1..20) The number of actors in the simulated raid environment wearing the Infernal Cinders trinket. _Note that Simulationcraft does not automatically infer the number of users from the raiding environment, it must be set with this option._
 * **legion.engine_of_eradication_orbs** (scope: global; default: 4; range: 0..4) The number of orbs each user of Engine of Eradication will pick up. Simulationcraft does not model any sort of movement-based picking up of the orbs.
 * **legion.void_stalkers_contract_targets** (scope: global; default: -1 [all targets]; range: 1..) Number of targets each Void Stalker's Contract trinket pet hits.
 * **legion.specter_of_betrayal_overlap** (scope: global; default: 1.0; range: 0..1) Uniform probability of overlapping multiple Specter of Betrayal trinket effects. Conversely, at probability `1 - legion.specter_of_betrayal_overlap` the simulator will only pulse the most recent Specter of Betrayal effect.
 * **legion.cradle_of_anguish_resets** (scope: global) Defines a list of time values delimited by `,`, `:`, or `/` when the actor loses all stacks of Cradle of Anguish effect. This is intended to simulate the effect of the actor being below 50% health. _Note that the "must be over 80% health to gain stacks" is currently not modelled in Simulationcraft._
* **legion.archimondes_hatred_reborn_damage** (scope: global; default 1.0; range: 0..1) Defines how much of the absorb shield provided by the legendary trinket Archimonde's Hatred Reborn on use effect is consumed and turned into damage when it expires. _Simulationcraft doesn't model damage taken by tanks in a realistic manner so the value is just set at 100% by default._

### Miscellaneous
 * **legion.feast_as_dps** (scope: global; default: true) Controls whether Lavish Suramar Feast is always treated as giving DPS stats (i.e., str, agi, or int), instead of a role-based behavior. With role-based behavior, the feast will grant stamina instead of primary stat for actors that have `role=tank` defined.

### Pantheon trinket system

The empowered pantheon trigger system is modelled as a combination of proxy users based on user input and the items carried by actors defined in the simulation profile. Each "proxy user" represents another actor in the environment who owns the type of trinket specified and attempts to proc it. Internally, each proxy user is represented by a discrete real-ppm object to simulate the proxy user attempting to proc their representative trinket throughout combat.

The current ruleset of the pantheon empowerment system (as of 2017-11-14) is as follows:
1) Require a combination of at least 4 active base trinket buffs
2) Treat Aman'Thul's Vision as a "wildcard buff", allowing each to count for 1.
3) Treat any number of Aggramar's Conviction, Golganneth's Vitality, Eonar's Compassion,
   Khazgoroth's Courage, and Norgannon's Prowess as a single buff; one buff of the given type
   will satisfy (a single) buff for the empowerment state check
4) Once at least 4 base trinket buffs are up, trigger empowerment on all real actors who have
   buffs up. Note that this can result in more than 4 empowerment buffs to trigger (if multiples
   of the trinkets in 3. are up currently)

#### Options

There are several sim-scope options that control the behaviour of the system.

 * **legion.pantheon_trinket_interval** (scope: global; default: 1) Sets the interval between attempts to proc the proxied pantheon base trinket buffs.
 * **legion.pantheon_trinket_interval_stddev** (scope: global; default: 0; range: 0..1) Sets the percentage amount of standard deviation from the mean in terms of **legion.pantheon_trinket_interval**.
 * **legion.pantheon_trinket_users** (scope: global) Creates proxy pantheon trinket users to the simulation environment. The format of the option is a '/'-delimited set of tokens of the form: `<type>:<haste%>`, where `<type>` is one of 'am', 'go', 'kh', 'eo', 'no', 'ag', for Aman'Thul's Vision, Golganneth's Vitality, Khaz'goroth's Courage, Eonar's Compassion, Norgannon's Prowess, and Aggramar's Conviction, respectively. The `<haste%>` value is the paperdoll haste value of the proxy caster. Multiple values of the same trinket type can be defined (also with different haste% values). _Note that some of the trinkets do not scale with haste. The system will automatically ignore haste% values given for such trinkets (based on client data)._
```
#Set up a 20 man proxy raid (19 additional users emulated) consisting of 9 Aman'Thul and 2 of each additional trinket
#20% character sheet haste is used for all relevant trinkets
legion.pantheon_trinket_users=am/am/am/am/am/am/am/am/am/go:0.2/go:0.2/kh/kh/eo:0.2/eo:0.2/no/no/ag/ag
```