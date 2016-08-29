**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Rune expression system

**Since Simulationcraft 7.0.3, release 1** Runes are treated as a standard resource in the simulator. Normal resource expressions work on runes, with the exception of the `regen` and `time_to_max` resource expressions.

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
