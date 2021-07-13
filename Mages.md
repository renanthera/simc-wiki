**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Actions

### Burn phase

Burn phase can be started by `start_burn_phase` and stopped by `stop_burn_phase`. These actions set and reset the `burn_phase` flag, which can then be used in conditions of other actions.

```
actions=start_burn_phase,if=!burn_phase&cooldown.evocation.remains<20
actions+=/stop_burn_phase,if=prev_gcd.1.evocation
actions+=/arcane_blast,if=burn_phase
...
```

### Water Elemental

Water Elemental's Freeze can be controlled manually via the `freeze` action.

```
...
actions+=/freeze,if=ground_aoe.comet_storm.remains>0.6
...
```

## Expressions

### Burn phase

`burn_phase` expression evaluates to 1 if the burn phase is currently active. `burn_phase_duration` gives the duration (in seconds) of the current burn phase. Outside of the burn phase, it returns 0.

### Mana Gem

The remaining charges of a Mana Gem can be obtained by using the `mana_gem_charges` expression.

### Incanter's Flow

`incanters_flow_dir` can be used to determine if Incanter's Flow is currently gaining or losing stacks.

```
Time                   | 1  2  3  4  5  6  7  8  9 10 11 12 ...
-----------------------+---------------------------------------
Incanter's Flow stacks | 1  2  3  4  5  5  4  3  2  1  1  2 ...
incanters_flow_dir     | 1  1  1  1  0 -1 -1 -1 -1  0  1  1 ...
```

`incanters_flow_time_to.<stack number>.<stack type>` evaluates to the remaining time (in seconds) until the next occurrence of the specified stack. When the buff is in the desired state, this expression evaluates to 0.

`stack_number` is a whole number between 1 and 5, `stack_type` can be `up`, `down` or `any`. `up` checks only stacks on the raising part of the cycle, `down` checks stacks on the falling part of the cycle and `any` checks both types.

### Ground AoE

Ground AoE can be tracked by `ground_aoe.X.Y`.

`X` can be any of:
* `blizzard`
* `comet_storm`
* `flame_patch`
* `frozen_orb`
* `meteor_burn`

`Y` can be any of:
* `remains`

If the specified ground AoE is currently not active, this expression evaluates to 0.

For example:

```
...
actions+=/flurry,if=buff.brain_freeze.react&prev_gcd.1.frostbolt&ground_aoe.frozen_orb.remains=0
...
```

### Firestarter and Searing Touch

The expression `firestarter.active` can be used to check if Firestarter is active. Time until Firestarter becomes inactive is represented by `firestarter.remains`. See below.

```
actions=fireball,target_if=firestarter.active
# Cast Fireball on any target that will make it crit.
```

The expression `searing_touch.active` functions in the same way. Time until Searing Touch becomes active is represented by `searing_touch.remains`.

### Winter's Chill

The expression `remaining_winters_chill` provides an approximation of the number of remaining Winter's Chill stacks, accounting for spells that are currently in flight.

### Hot Streak

The expression `hot_streak_spells_in_flight` provides the number of spells that are currently in flight (to any target) and are capable of triggering Hot Streak.

### Kindling
The expression `expected_kindling_reduction` returns the expected amount of time left until Combustion's cooldown is ready as a fraction of Combustion's cooldown based on the rate that Kindling has been reducing the cooldown.

## Mage options

### Firestarter and Searing Touch

By default, the health of enemies decreases uniformly from 100% to 0%. However, in a raid setting, the raid DPS is not constant and the health doesn't decrease uniformly. This has an effect on the duration of the Firestarter and Searing Touch phases.

`mage.firestarter_duration_multiplier` and `mage.searing_touch_duration_multiplier` (1.0 default) can be used to change the duration of those phases to better match the given fight.

For example, `mage.firestarter_duration_multiplier=0.3` reduces the duration of the Firestarter phase by 70%.

### Freeze effects

Since all freeze effects available in simc break on damage and thus almost never last their full duration, we opted to use one shared duration for all of them. In Battle for Azeroth, all freeze effects are guaranteed to last at least 1 s, which is why simc uses 1 s as the default freeze duration.

`mage.frozen_duration=<time in seconds>` overrides this default duration with a user-specified value. When `frozen_duration` is set to 0 or lower, freeze effects are assumed to be permanent.

### Focus Magic

If the Mage has the Focus Magic talent selected, `mage.focus_magic_interval=<time in seconds>` and `mage.focus_magic_relstddev=<fraction of interval>` can be used to control the average time between hits that would trigger Focus Magic from the player you buff. The `mage.focus_magic_crit_chance` option controls the chance that these hits are crits and will actually trigger Focus Magic. Setting `mage.focus_magic_interval=0` will prevent the effect from ever triggering. The standard deviation of the distribution used for the interval is equal to `mage.focus_magic_interval * mage.focus_magic_relstddev`.

`mage.focus_magic_trade=<0/1>` automatically enables the 30 min 5% crit buff whenever the mage is using the Focus Magic talent. 

### Arcane Missiles

Sometimes, there can be a benefit from chaining Arcane Missiles quickly. `mage.arcane_missiles_chain_delay=<time in seconds>` and `mage.arcane_missiles_chain_relstddev=<fraction of interval>` control the average time after a tick when Arcane Missiles will be chained.

### Mirrors of Torment

`mage.mirrors_of_torment_interval=<time in seconds>` can be used to control how often triggers of Mirrors of Torment will attempt to trigger relative to the time when the debuff is applied.

### Overriding APL variables

The default Mage APLs include several variables, which can be configured through the `apl_variable` option.

#### Fire APL Variables

* `apl_variable.disable_combustion=<0/1>` If set to 1, Combustion will not be used in the simulation.
* `apl_variable.firestarter_combustion=<0/1>` If set to 1, Combustion will be used while Firestarter is active.
* `apl_variable.hot_streak_flamestrike=<number of targets>` The number of target at which Hot Streaks should be spent on Flamestrike outside of Combustion.
* `apl_variable.hard_cast_flamestrike=<number of targets>` The number of target at which Flamestrike will replace Fireball as filler outside of Combustion.
* `apl_variable.combustion_flamestrike=<number of targets>` The number of targets at which a Flamestrike Combustion will be used instead of a Pyroblast Combustion.
* `apl_variable.arcane_explosion=<number of targets>` The number of targets at which Arcane Explosion will be used as filler (higher priority than Flamestrike filler).
* `apl_variable.arcane_explosion_mana=<percentage of mana>` The percentage of mana to conserve when using Arcane Explosion.
* `apl_variable.combustion_shifting_power=<number of targets>` The number of targets at which Shifting Power will be used during Combustion.
* `apl_variable.combustion_cast_remains=<number of seconds>` The number of seconds remaining on the cast before Combustion when Combustion will be used.
* `apl_variable.overpool_fire_blasts=<number_of_seconds>` The number of seconds early (or late if negative) to start pooling Fire Blasts for Combustion.
### Disciplinary Command

`mage.prepull_dc=<0/1>` can be used to automatically trigger the Disciplinary Command buff when combat begins. This roughly corresponds to obtaining two of the three buffs before combat starts (by using Arcane Explosion, Frost Nova, or Flame Patch and then changing specialization) and triggering the crit damage buff with the precast.

## Crowd control

Some abilities have a different effect depending on whether the target is susceptible to crowd control. For example, against targets that are immune to crowd control, Freeze will not apply the root effect.

Target is susceptible to crowd control in these situations:

* Target's level is strictly smaller than player level + 3
* Target is an add spawned by the `adds` raid event
