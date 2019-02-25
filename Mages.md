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

`burn_phase` expression evaluates to 1 if burn phase is currently active. `burn_phase_duration` gives the duration (in seconds) of the current burn phase. Outside of burn phase, it returns 0.

### Incanter's Flow

`incanters_flow_dir` can be used to determine if Incanter's Flow is currently gaining or losing stacks.

```
Time                   | 1  2  3  4  5  6  7  8  9 10 11 12 ...
-----------------------+---------------------------------------
Incanter's Flow stacks | 1  2  3  4  5  5  4  3  2  1  1  2 ...
incanters_flow_dir     | 1  1  1  1  0 -1 -1 -1 -1  0  1  1 ...
```

`incanters_flow_time_to.<stack number>.<stack type>` evaluates to remaining time (in seconds) until the next occurence of the specified stack. `stack_number` is a whole number between 1 and 5, `stack_type` can be `up`, `down` or `any`. `up` checks only stacks on the raising part of the cycle, `down` checks stacks on the falling part of the cycle and `any` checks both types.

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

### Firestarter

The expression `firestarter.active` can be used to check if Firestarter is active. Time until Firestarter becomes inactive is represented by `firestarter.remains`. See below.

```
actions=fireball,target_if=firestarter.active
# Cast Fireball on any target that will make it crit.
```

### Brain Freeze

`brain_freeze_active` expression helps distinguish between normal and Brain Freeze empowered Flurry casts. This expression evaluates to 1 (`true`) if the last Flurry was cast with Brain Freeze, otherwise it evalutes to 0 (`false`).

## Mage options

### Firestarter

Firestarter's value hugely depends on a raid composition. In a single actor simulations, it is usually overvalued.

`firestater_time` can be used to combat this. It turns off the standard Firestarter behavior and gives Fireball and Pyroblast 100% crit chance for the specified time after combat starts.

Note that with this option, Firestarter won't have any effect on enemies that join the fight later (for example `adds` raid event).

```
mage=Mage
level=110
...
spec=fire

firestarter_time=20
# Firestarter is only active for the first 20 seconds
```

### Greater Blessing of Wisdom

Arcane mages benefit from the extra mana gained from Greater Blessing of Wisdom. `blessing_of_wisdom_count` can be used to simulate this exact scenario.

```
mage=Mage
level=110
...
spec=arcane

blessing_of_wisdom_count=2
# Two paladins buffed us with GBoW
```

### Shimmer Ice Lance

This combo can be enabled via `allow_shimmer_lance`. When set to true, Shimmer temporarily reduces Ice Lance's travel time (as if the player was 20 yd closer). Note that this doesn't actually model player movement.

If you want to try it out, you can make the following change to the default APL. Replace this Ice Lance line

```
actions+=/ice_lance,if=!buff.fingers_of_frost.react&prev_gcd.1.flurry
```

with the following three lines

```
actions+=/ice_lance,if=prev_gcd.1.flurry
actions+=/ice_lance,if=prev_off_gcd.shimmer&debuff.winters_chill.remains>travel_time
actions+=/shimmer,if=spell_haste<=0.666&prev_gcd.2.flurry&charges>=1&!buff.fingers_of_frost.react
```

If you don't want to use Shimmer back to back, you can enforce time between two Shimmers in this way.

```
# Do not allow two Shimmers within 5 sec of eachother.
actions+=/shimmer,line_cd=5,if=...
```

### Freeze effects

Since all freeze effects available in simc break on damage and thus almost never last their full duration, we opted to use one shared duration for all of them. In Battle for Azeroth, all freeze effects are guaranteed to last at least 1 s, which is why simc uses 1 s as the default freeze duration.

`frozen_duration=<time in seconds>` overrides this default duration with a user specified value. When `frozen_duration` is set to 0 or lower, freeze effects are assumed to be permanent.

## Crowd control

Some abilities have different effect depending on whether the target is susceptible to crowd control. For example, against targets that are immune to crowd control, Freeze will not apply the root effect.

Target is susceptible to crowd control in these situations:

* Target's level is strictly smaller than player level + 3
* Target is an add spawned by the `adds` raid event
