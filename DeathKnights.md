**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Rune expression system

**Since Simulationcraft 7.0.3, release 1** Runes are treated as a standard resource in the simulator. Normal resource expressions work on runes, with the exception of the `regen` and `time_to_max` resource expressions.

You can also use rune.time_to_X to return the time until X runes are available.

For example you can use this line to only execute obliterate if the actor has 4 or more runes available, and frost strike if the time until 3 runes are available is superior to the length of the global cooldown.
```
actions+=/obliterate,if=rune>=4
actions+=/frost_strike,if=rune.time_to_3>gcd
```


## Incoming damage
The expression `incoming_damage_5s` returns the amount of damage the Death Knight has taken in the previous five seconds.
```
 # Death Strike if the actor has taken 25% of maxhp damage in the previous 5 seconds.
 actions+=/death_strike,if=incoming_damage_5s>=health.max*0.25
```

## Synchronizing weapons
The _sync\_weapons_ (default: 1) option on the _auto\_attack_ action can be used to force the synchronization of weapons at the beginning of the fight. When zero, the offhand will be desynchronized by half of its swing time. In game, you always start with your weapons synchronized but target switching and parry rushes often lead you to go unsynchronized.
```
 # Ensure the player will start with synched weapons.
 actions+=/auto_attack,sync_weapons=1
```

## Anti-Magic Shell
The _antimagic\_shell_ action allows a Death Knight to simulate the Runic Power gain on incoming damage. The action contains three options: **interval**, **interval\_stddev**, and **damage**. The **interval** option sets the mean of the interval between two consecutive Anti-Magic Shell executions in seconds, and is required to be at minimum the cooldown of the spell. The **interval\_stddev** option sets the standard deviation of the interval between Anti-Magic Shell executions. If specified as less than 1, it is interpreted as a percent of the mean, otherwise it is interpreted as seconds. Finally, the **damage** option sets the amount of incoming damage. The default values for **interval**, and **interval\_stddev** are 60 and 5% respectively. The **damage** option is always required.
```
 # Simulate Runic Power gain on using Anti-Magic Shell to absorb 100000 magic damage every 60 seconds on average.
 actions+=/antimagic_shell,damage=100000
```

## Miscellanous

Army of the dead has an option to set the prepull delay. It only works when army of the dead is used in the precombat APL and won't have any effect otherwise. It takes an integer value between 0 (cast right on pull) and 10. Default value: 6
```
# Simulate the cast of army of the dead 4s before combat begins
actions.precombat+=/army_of_the_dead,delay=4
```

The Magus of the dead azerite trait spawns a magus pet that will melee attack nearby enemies even while casting, you can use the magus_of_the_dead_melee_uptime option to set its melee uptime. Every time the pet tries to melee, it will roll a chance equal to the option to simulate the melee attack. If the roll fails, the attack will miss.
Its default behavior is a 60% melee uptime when summoned during combat, and 0% for pre-pull army of the dead.
This player-scope option takes a number between 0 and 1.
```
# Simulate a melee uptime of 50%, meaning that 50% of the attacks will miss
magus_of_the_dead_melee_uptime=0.5
```