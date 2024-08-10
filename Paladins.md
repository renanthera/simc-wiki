**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Buffs
Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

## Time Until Next HPG
`time_to_hpg` will return the time until the next holy power generator is available, in seconds. It will also enforce a minimum time equal to the current GCD (i.e. if there's a holy power generator that is off cooldown, but the GCD isn't up for another 350 ms, this will evaluate to 0.350).
```
  #cast TV if we're at 5 holy power and a holy power generator is available next GCD
  actions+=/templars_verdict,if=holy_power>=5&time_to_hpg<=gcd.max
```
Note that this does not do any fancy calculus to figure out if the next GCD actually _will_ be a HPG. It _only_ returns the time until the next HPG is available. If your action list prioritizes other spells over HPGs, then the time until the next HPG is actually cast could be longer than `time_to_hpg`. It should never be shorter, however.

Note#2: This is only supported for Retribution Paladin at the moment.

## Blessed Hammer strikes
Blessed Hammer can hit multiple times depending on the size of the target in-game. To reproduce that behavior, the blessed_hammer action has a `strikes` option (float, default: 2, min: 1, max: 10) that can be used to specified the number of time each cast will hit each target.
If the number has decimals, they will be used as a chance to generate an extra strike for every blessed hammer cast.
```
# Hit every enemy 3 times per blessed hammer cast
actions+=/blessed_hammer,strikes=3
```

## Consecration Precombat time
When Consecration is included in the precombat APL, the spell will be used with a special behaviour based on the precombat_time option given to it (default: 2s). The ground aoe's start time will be delayed by 1s to simulate the time the boss takes to run into it. Its duration and cooldown will also be adjusted accordingly.
>Negative values will be handled the same way as some users may find it more intuitive (-3 is 3s before combat starts). The absolute value has to be lower than consecration's total duration, and higher than the player's based gcd duration (1.5s).
```
# Use consecration 3s before combat starts
actions.precombat=consecration,precombat_time=3
```

## Holy Power Generators until two Dawn Stacks
Use `hpg_to_2dawn` to get the currently needed amount of Holy Power Generators to reach two Stacks of Dawn. This is a variable that can be between 6 (6 Holy Power Generators needed until 2 Dawn Stacks are reached) and -2 (Two Dawn Stacks are already reached and you would need one more Holy Power Generator to refresh the Dawn-Buff)
```
# Use Shield of the Righteous when we're about to reach the next Dawn Stack to use it with Hammer of Light
actions.hammer_of_light+=/shield_of_the_righteous,if=hpg_to_2dawn=4
```

## Lightsmith specifics

### Lightsmith's Divine Guidance
```
For each Holy Power ability cast, your next Consecration deals x damage or healing immediately, split across all enemies and allies.
```
Since this ability shares its value between damage and healing, the default implementation for SimCraft is to always heal the Paladin to have a more realistic scenario. The actual implementation tries to mirror what is happening ingame. It will always prefer to heal injured targets before it tries to deal damage. If it heals a total amount of 5 targets, it will deal 0 damage. By default, it will always heal the Paladin, even when the paladin has maximum life.

With 0 targets to heal and 1 enemy, the ability will deal 100% damage.

With 1 target to heal and 1 enemy, the ability will heal 50% (1 target, 2 targets total) and deal 50% damage.

With 4 targets to heal and 1 enemy, the ability will heal 80% and deal 20% damage.

With 1 target to heal and 3 enemies, the ability will heal 25% and deal 75% damage, split between 3 targets (25% each).

With 1 target to heal and 20 enemies, the ability will heal 20% and deal 80% damage, split between 20 targets (4% each).

With 5 targets to heal and 1 enemy, the ability will heal 100% and deal no damage.

To simulate different scenarios, player-scoped options have been introduced to alter this behaviour (see [#player-scoped-options](https://github.com/simulationcraft/simc/wiki/Paladins#player-scoped-options) )

### Holy Armament management
Three new variables have been introduced to handle Holy Armament handling. Holy Armaments can only be cast by using the action `holy_armaments`, which will always alternate between Holy Bulwark and Sacred Weapon, starting with Holy Bulwark)

`next_armament` returns either 0 or 1, depending on which Holy Armament comes next

`holy_bulwark` returns 0

`sacred_weapon` returns 1

```
# Use Holy Armaments when the next Armament is Sacred Weapon, if the buff is not up or can pandemic, AW is not up or the remaining cooldown is less than 30s
actions.standard+=/holy_armaments,if=next_armament=sacred_weapon&(!buff.sacred_weapon.up|(buff.sacred_weapon.remains<6&!buff.avenging_wrath.up&cooldown.avenging_wrath.remains<=30))
```

## Player-scoped Options
`min_dg_heal_targets` (0-5, default 1) - Minimum amount of targets to heal with Lightsmith's Divine Guidance. Will affect the amount of damage Divine Guidance does. Set to 0 (in tandem with `max_dg_heal_targets`) to simulate a Training Dummy scenario. Set to 5 to always have it heal instead of dealing damage.

`max_dg_heal_targets` (0-5, default 5) - Maximum amount of targets to heal with Lightsmith's Divine Guidance. Will affect the amount of damage Divine Guidance does. Set to 0 (in tandem with `min_dg_heal_targets`) to simulate a Training Dummy scenario. Set to 1 to simulate a solo-scenario within a multi actor environment.


# Reports
We only document here non-obvious entries.

## Procs
  * parry\_haste: the number of times your swings have been hasted after you parried an attack.