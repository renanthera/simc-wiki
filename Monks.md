**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._
## Storm, Earth, and Fire

Storm, Earth, and Fire is fully supported in the sim. The action `storm_earth_and_fire` will spawn an enemy on the current target of the action (typically, the primary target of the simulator). There is a single buff and a single debuff involved in determining how many pets the actor has out at any given time, and whether a target has a pet on it. The buff `storm_earth_and_fire` has a maximum stack of two, where the stack count indicates the number of pets out. The debuff `storm_earth_and_fire_target` indicates whether the target has a pet on it.

Executing Storm, Earth, and Fire on a target that already has a pet on it will despawn that pet. Executing Storm, Earth, and Fire on a target that does not have a pet on it, when both pets are out, will despawn both pets. If a target dies, while a pet is on it, the pet is automatically despawned.
```
 # Use Storm, Earth, and Fire on the second and third targets (while they are alive)
 actions+=/storm_earth_and_fire,target=2,if=debuff.storm_earth_and_fire_target.down
 actions+=/storm_earth_and_fire,target=3,if=debuff.storm_earth_and_fire_target.down
```

There are a total of three available pets to summon (storm, earth, and fire pets). Each time the ability is executed, one of the remaining dormant pets is selected. For this reason, the reporting may show all three pet types in use. **This does not mean that all three pets are active at the same time.**

## Resources

The _initial\_chi_ (scope: player, default: 5 for WW, 1 for BrM & MW) option sets the amount of chi the monk actor has at the beginning of the combat.
```
# Set the initial chi of the monk actor to four
initial_chi=4

The _goto\_throttle_ (scope: player, default: 60) option sets the percent number of Gift of the Ox orbs that are picked up
```
## Spells implementation notes

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

### _Keg Smash_
The _keg\_smash_ action has one setting available.
  1. The boolean _dizzying\_haze_ option (default: false) determines whether dizzying haze will be applied or not.
```
 # Execute Keg Smash and apply Dizzying Haze
 actions+=/keg_smash,dizzying_haze=1
```

## Buffs
Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

## Debuffs
Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

### _Mark of the Crane_
The _debuff.mark\_of\_the\_crake_ is used by Windwalkers to see if the target has a Mark of the Crane debuff.

The _spinning\_crane\_kick.count_ is used if you wish to see the total number of Mark of the Crane debuffs are currently on targets. For WoW API developers, Blizzard uses the "count" variable in the spell api to return the Spinning Crane Kick stack number. Hence the reason I used this permutation; for consistency sake.

```
 actions+=/spinning_crane_kick,if=spinning_crane_kick.count>3
```

### _Stagger_
Stagger is part of the Brewmaster active mitigation. Given how unique it is, there is a custom format for it.

1. **Light Stagger** - This is any (Stagger tick damage / Current Player HP) that is below 3.5%

  ```
 # Purify stagger if in Light Stagger or green stagger
 actions+=/purifying_brew,if=stagger.light
  ```
1. **Moderate Stagger** - This is any (Stagger tick damage / Current Player HP) that is between 3.5% and 6.5%

  ```
 # Purify stagger if in Moderate Stagger or yellow stagger
 actions+=/purifying_brew,if=stagger.moderate
  ```
1. **Heavy Stagger** - This is any (Stagger tick damage / Current Player HP) that is over 6.5%

  ```
 # Purify stagger if in Heavy Stagger or red stagger
 actions+=/purifying_brew,if=stagger.heavy
  ```
1. **Stagger Percent** - This compares the percent evaluation to the (Stagger tick damage / Current Player HP).

  ```
 # Purify stagger once stagger percent goes over 2.2%
 actions+=/purifying_brew,if=stagger.pct>2.2
  ```
1. **Stagger Amount** - This evaluates the current Stagger tick damage

  ```
 # Purify stagger once stagger tick damage goes over 10,000 damage
 actions+=/purifying_brew,if=stagger.amount>10000
  ```
1. **Stagger Remains** - This evaluates the remaining duration from stagger

  ```
 # Purify stagger only if stagger remains more than 3 seconds
 actions+=/purifying_brew,if=stagger.remains>3
  ```
1. **Stagger Amount Remains** - This evaluates the remaining amount of damage from stagger

  ```
 # Purify stagger once there is 50,000 damage remaining on the stagger
 actions+=/purifying_brew,if=stagger.amount_remains<50000
  ```

# Reports
We only document here non-obvious entries.