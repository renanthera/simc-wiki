# Expansion-specific options

Note that expansion-specific options may disappear from Simulationcraft versions intended for newer expansions than what is defined here.

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
  * **bfa.jes_howler_allies** (scope: global; default: 0) The number of allies Jes' Howler trinket hits. Accepts values from 0 to 4.
  * **bfa.reorigination_array_stacks** (scope: gobal; default: 0) The number of stacks provided by the Uldir (raidzone) only buff, enabled by the traits "Laser Matrix" and "Archive of the Titans". Stacks are unlocked by killing three raid bosses each week. After doing so for 10 weeks the maximum stack count of 10 is unlocked. Accepts values from 0 to 10.
  * **bfa.secrets_of_the_deep_chance** (scope: global; default: 0.1) The chance to spawn a "rare" droplet (a void droplet). Accepts values from 0 to 1.
  * **bfa.secrets_of_the_deep_collect_chance** (scope: global; default: 1.0) The chance that the actors will pick up the droplets. Accepts values from 0 to 1.
  * **bfa.initial_archive_of_the_titans_stacks** (scope: global; default: 0) The number of stacks of the azerite trait Archive of the Titans to apply at the start of combat. This trait normally applies its first stack 5s into combat and increase by one stack every 5s thereafter. The stacks are reset when entering combat with a raid boss, but in non-raid encounters, such as Mythic+ dungeons, you can typically enter combat with certain number of stacks already present.
  * **bfa.seductive_power_pickup_chance** (scope: global; default: 1.0) Chance of picking up the visage spawned by Seductive Power azerite trait.


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