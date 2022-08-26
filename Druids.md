**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**

## APL expressions

* **`ap_check.<allowed overcap = 0>`** Returns false if the action Astral Power + (if enabled) Nature's Balance passive Astral Power over execute time + (if enabled) Shooting Stars 1 proc Astral Power is higher than the maximum Astral Power + allowed overcap (optional). True otherwise.

* **`<action>.ap_check.<allowed overcap = 0>`** Same as above with the distinction that the action is specified.

## Options
* **druid.catweave_bear** (default: 0) Set to utilize the catweaving APL for Guardian Druids.

* **druid.owlweave_bear** (default: 0) Set to utilize the owlweaving APL for Guardian Druids.

* **druid.owlweave_cat** (default: 1) Set to utilize the owlweaving APL for Feral Druids.

* **druid.no_cds** (default: 0) Set to prevent the APL from casting major offensive cooldowns. *Currently only supported for Balance Druid.*

* **druid.affinity_resources** (default: false) When set true, enables resources used specifically by your affinity talent, such as Energy with Feral Affinity.

* **druid.initial_astral_power** (default: 0) Set the amount of astral power at start of combat. APLs are limited to a single pre-cast spell, thus the normal precasting of 2x solar wrath is simulated by the default setting of 8 + single pre-cast solar wrath. When having talented Nature's Balance this is set to 58 to account for the increased starting astral power.

* **druid.initial_moon_stage** (default: 0) Set the starting state of the New Moon talent. 0: New Moon, 1: Half Moon, 2: Full Moon

* **druid.predator_rppm_rate** (default: 0.0) Set the RPPM rate for triggering the Predator talent. This is used as an approximation to simulate how Predator works in-game.

* **druid.initial_pulsar_value** (default: 0.0) Set the initial value of the Primordial Arcanic Pulsar legendary.

### Kyrian
* **druid.kindred_spirits_target** (default: none) Set the character for the druid to bond to. Only bonding to DPS characters is implemented.

  _**THE CHARACTER TO BOND TO MUST BE DEFINED BEFORE THE DRUID.**_

  `single_actor_batch` cannot be true.

  **For Advanced Sim in raidbots.com, you must explicitly add `single_actor_batch=0` to your input.**

  - The bond damage 'kindred empowerment' done by both characters will be attributed to the druid.
  - If the druid has the Kindred Affinity legendary equipped, the buff effect will be based on the bonded character's covenant, and both characters will have their buff effect doubled when the druid casts 'empower bond'.

  For example, to have a balance druid bond to a fire mage:
```
    mage=fire_freddy
    spec=fire
    level=60
    covenant=night_fae

    druid=kyrian_druid
    spec=balance
    level=60
    covenant=kyrian
    druid.kindred_spirits_target=fire_freddy
```

* **druid.kindred_spirits_absorbed** (default: 0.15) Sets percent of pool used up as absorbs or heals.

* **druid.kindred_spirits_dps_pool_multiplier** (default: 0.85) Only in effect when there is no explicit bond and you are simming a DPS druid by itself. Catch-all multiplier to estimate how much of the pool is lost due to mismatches in dps/CD/timings/etc.

* **druid.kindred_spirits_non_dps_pool_multiplier** (default: 1.5) Only in effect when there is no explicit bond and you are simming a non-DPS druid by itself. Catch-all multiplier to estimate how much of the pool you might gain due to non-DPS specs generally gaining a larger pool than their would generate based on their own dps.

* **druid.kindred_affinity_covenant** (default: `night_fae`) Sets the covenant of your bonded partner when using the Kindred Affinity Kyrian legendary. You may also use the name of the corresponding stat granted. Valid values are: `kyrian` `necrolord` `night_fae` `venthyr` `mastery` `versatility` `haste` `crit`

* **druid.lone_empowerment** (default: 0) When set to 1, will treat Kindred Spirits as bonding with nobody and using the Lone Empowerment buff. Only supported for Balance & Feral.

### Night Fae
* **druid.convoke_the_spirits_deck** (default: 5) The number of cards in the deck used to determine if Convoke the Spirits has a chance to cast an exceptional spell when **not** using the Celestial Spirits Night Fae legendary. (Moonkin: Full Moon, Cat: Feral Frenzy, Bear: Pulverize, Caster: Flourish).

### Necrolord
* **druid.adaptive_swarm_prepull_setup** (default: none) String to define healing swarms that are active on allies at combat start. Each swarm entry is delimited by `/`. Swarm entry format is `<min stacks>:<max stacks>:<min duration>:<max duration>:<chance>`
  * Each swarm will have `<chance>` to be active at the start of each iteration.
  * Each swarm will be created with random stacks between `<min stacks>` & `<max stacks>`
  * Each swarm will have random remaining duration between `<min duration>` & `<max duration>`

  For example, to set up swarms with:
  * Swarm 1: 2-4 stacks, 5-10 seconds remaining, 35% chance to be active
  * Swarm 2: 1 stack, 2 seconds remaining, 100% chance to be active
```
druid.adaptive_swarm_prepull_setup=2:4:5:10:0.35/1:1:2:2:1
```

* **druid.adaptive_swarm_jump_distance_melee** (default: 5.0) The average distance of the virtual melee players that are potential targets when a healing swarm jumps from an enemy.

* **druid.adaptive_swarm_jump_distance_ranged** (default: 25.0) The average distance of the virtual ranged players that are potential targets when a healing swarm jumps from an enemy.

* **druid.adaptive_swarm_jump_distance_stddev** (default 1.0) The standard deviation for the previous two options.

* **druid.adaptive_swarm_friendly_targets** (default: 20) The number of friendly targets a healing Adaptive Swarm can jump to.

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

  * bear\_form, cat\_form, moonkin\_form: forms

# Reports
We only document here non-obvious entries.

## Resource gains
  * energy\_refund: the energy refunded by your misses.
  * incoming\_damage: rage generated by incoming damages.

## Procs
  * combo\_points\_wasted: combo points wasted because you were already capped.

## Uptimes
  * energy\_cap: fraction of the fight spent with a full energy bar.
  * rage\_cap: fraction of the fight spent with a full rage bar.