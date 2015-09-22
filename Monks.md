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
```
The _goto\_throttle_ (scope: player, default: 60) option sets the percent number of Gift of the Ox orbs that are picked up
```
# Set the percent of GotO orbs that are picked up to 40.5%
goto_throttle=40.5
```
The _eh\_reset\_throttle_ (scope: player, default: 10) option sets the percent amount of time that the player falls below 35% HP. Since Sims go into negative health values, a good chunk of the fight can be below 35%. So we need to throttle the resetting of Expel Harm so that it doesn't always trigger for most of the fight
```
# Set the percent amount of time spent below 35% HP to 33.3%
eh_reset_throttle=33.3
```
## Spells implementation notes

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

### _Stance_
The _stance_ action has one setting available.
  1. The _choose_ option (default: empty) is the stance string to which the _stance_ action will switch to.
```
 # Choose Sturdy Ox stance
 actions+=/stance,choose=sturdy_ox
```

### _Keg Smash_
The _keg\_smash_ action has one setting available.
  1. The boolean _dizzying\_haze_ option (default: false) determines whether dizzying haze will be applied or not.
```
 # Execute Keg Smash and apply Dizzying Haze
 actions+=/keg_smash,dizzying_haze=1
```

## Buffs
Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

### _Tigereye Brew_
Split into _buff\_tigereye\_brew_ and _buff\_tigereye\_brew\_use_ because they share the same name in game.

### _Elusive Brew_
Split into _elusive\_brew\_stacks_ and _elusive\_brew\_activated_ because they share the same name in game.

## Debuffs
Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

### _Rising Sun Kick_
The _debuff.rising\_sun\_kick_ is used to increase Yellow damage attacks for Windwalkers and Mistweavers
```
 # Rising Sun Kick if the Rising Sun Kick debuff has less than 3 seconds remaining on the target
 actions+=/rising_sun_kick,if=debuff.rising_sun_kick.remains<3
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
1. **Stagger Remains** - This evaluates the remaining amount of damage from stagger

  ```
 # Purify stagger once there is 50,000 damage remaining on the stagger
 actions+=/purifying_brew,if=stagger.remains<50000
  ```

# Reports
We only document here non-obvious entries.