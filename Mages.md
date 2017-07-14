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

By default, Water Elemental casts Water Jet on cooldown and Waterbolt otherwise. If needed, Water Jet can be controlled manually via the `water_jet` action. When used, `water_jet` interrupts Water Elemental's current spell and forces it to cast Water Jet next.

Water Elemental's Freeze can also be controlled manually via the `freeze` action. Freeze will only grant charges of Fingers of Frost when it hits a target that can be crowd-controlled, see below.

Note that when either of these actions is included in the APL, Water Elemental will never use Water Jet unless explicitly instructed to.

```
...
actions+=/water_jet,if=buff.fingers_of_frost.react=0&active_enemies=1
actions+=/freeze,if=buff.fingers_of_frost.react=0&active_enemies>=2
...
```

## Expressions

### Burn phase

`burn_phase` expression evaluates to 1 if burn phase is currently active. `burn_phase_duration` gives the duration (in seconds) of the current burn phase. Outside of burn phase, it returns 0.

### Icicles

Icicles can be tracked in two ways: `buff.icicles.stack` and `icicles`. The former corresponds to the in-game buff that is used for example with Glacial Spike, the latter gives the actual number of Icicles.

As an example, when Frostbolt is cast, the mage gains a stack of the Icicles buff (and `buff.icicles.stack=1`), but the actual Icicle is not created until Frostbolt impacts (therefore `icicles=0`).

### Incanter's Flow

`incanters_flow_dir` can be used to determine if Incanter's Flow is currently gaining or losing stacks.

```
Time                   | 1  2  3  4  5  6  7  8  9 10 11 12 ...
-----------------------+---------------------------------------
Incanter's Flow stacks | 1  2  3  4  5  5  4  3  2  1  1  2 ...
incanters_flow_dir     | 1  1  1  1  0 -1 -1 -1 -1  0  1  1 ...
```

### Ground AoE

Ground AoE can be tracked by `ground_aoe.X.Y`.

`X` can be any of:
* `blizzard`
* `comet_storm`
* `flame_patch`
* `frozen_orb`
* `legendary_comet_storm` - from Shattered Fragments of Sindragosa
* `legendary_meteor_burn` - from Contained Infernal Core
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
actions+=/ice_lance,if=variable.fof_react=0&prev_gcd.1.flurry
```

with the following three lines

```
actions+=/shimmer,if=prev_gcd.2.flurry&prev_gcd.1.ice_lance&debuff.winters_chill.remains>action.ice_lance.travel_time-20%38&variable.fof_react=0
actions+=/ice_lance,if=(variable.fof_react=0|variable.fof_react=1&spell_haste<=0.607)&prev_gcd.1.flurry
actions+=/ice_lance,if=prev_off_gcd.shimmer
```

If you don't want to use Shimmer back to back, you can enforce time between two Shimmers in this way.

```
# Do not allow two Shimmers within 5 sec of eachother.
actions+=/shimmer,line_cd=5,if=...
```

### Cinderstorm

Number of cinders can be controlled globally via `global_cinder_count`, see below.

## Ability options

### Cinderstorm

In Legion, Cinderstorm has a variable number of possible cinder impacts. To model this, SimulationCraft gives the user two separate options. One action-specific("cinders"), and one player-wide(global_cinder_count). By default, Cinderstorm will set "cinders"=6 and global_cinder_count=0. If global_cinder_count is given a value above 0, it will override all action-level "cinders" specified.

Use of global_cinder_count:
```
#Specify mage variables
mage="Mage_Fire_T19P"
level=110
race=orc
role=spell
position=back
talents=1022021
artifact=54:133022:137420:133022:0:748:1:749:6:751:3:754:3:755:3:756:3:759:1:762:1:763:1:1340:1
spec=fire
#give global_cinder_count
global_cinder_count=3

actions=cinderstorm
```

Use of cinders to set a single cinderstorms action to 3:
```
actions=cinderstorm,cinders=3,if=buff.rune_of_power.down
```

## Crowd control

Some abilities have different effect depending on whether the target is susceptible to crowd control. For example, against targets that are immune to crowd control, Freeze will not apply the root effect, it won't trigger any charges of Fingers of Frost and it won't activate Sephuz's Secret.

Target is susceptible to crowd control in these situations:

* Target's level is strictly smaller than player level + 3
* Target is an add spawned by the `adds` raid event
