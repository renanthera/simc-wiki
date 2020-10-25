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

## Indomitable Justice
Indomitable Justice is an azerite trait (azerite ID 235) that increases the damage of Judgment based on the difference between the player's current hp percentage and its target's.
You can set a specific % health to use with the player-scope option indomitable_justice_pct (integer value, default: 0).
```
# Set the indomitable justice trait to be used as if the player was always at 75% health
indomitable_justice_pct=75
```
>A value of 0 (or if you don't use the option) will automatically use 100% health for Retribution and Holy Paladins, and 80% health for Protection Paladins.

>A value of -1 (or any negative value) will use a "realistic" model, checking the player's health throughout the simulation.

>Any value higher than 100 will be lowered to 100.

# Reports
We only document here non-obvious entries.

## Procs
  * parry\_haste: the number of times your swings have been hasted after you parried an attack.