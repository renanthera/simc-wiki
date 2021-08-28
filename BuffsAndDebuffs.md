_This documentation is a part of the [TCI](TextualConfigurationInterface) reference._

**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**

# Introduction

By default, Simulationcraft adds every buff you can have in an optimal 20-man raid (Bloodlust, Battle Shout, Fortitude, etc).

# Optimal raid
  * **optimal\_raid** (scope: global; default: 1), when different from zero, will make your characters benefit from every helpful buffs you're supposed to have in a 20-man raid. It does include a bloodlust at the start of the fight. It does not include raid-specific buffs. If you simulate a whole raid, it may be a good idea to disable this setting to have buffs and debuffs being dynamically applied throughout the course of the simulation and your players' actions lists.
```
 # This will leave you with absolutely no buff, unless the self buffs you cast on your actions list.
 optimal_raid=0
```

# Overrides
You can override the helpful buffs and target debuffs you benefit from the **optimal\_raid** setting and explicitly disable or enable them, one by one. All those settings have a global scope and their default value is the last specified **optimal\_raid** setting, or 1 if not specified.

Beware! You need to declare the overrides **`***`after`***`** you declared **optimal\_raid**!

  * Unique buffs and debuffs
    * **override.bloodlust** (see the relevant section below)
    * **override.arcane_intellect**
    * **override.battle_shout**
    * **override.power_word_fortitude**
    * **override.chaos_brand**
    * **override.mystic_touch**
    * **override.windfury_totem**

  * Specials
    * **override.bleeding** will flag your target as permanently bleeding

# Heroism/bloodlust

The default settings will lead Simulationcraft to cast the bloodlust at the start of the fight.

  * **override.bloodlust** (scope: global; default: equal to **optimal\_raid**, or 1 if never specified) will force the application to automatically cast bloodlust (or not, when zero) at the end of the fight (or the beginning, see the next option).
```
 #This line enables optimal_raid but then disables the automatic use of bloodlust.
 optimal_raid=1
 override.bloodlust=0
```

  There are two possible triggers for bloodlust, one based on the elapsed or the remaining time, another one based on the target's health. The simulation checks every 1s if one of the triggers is satisfied and will use bloodlust if that's the case. Both triggers can be disabled. Note that those settings won't affect the manually casted bloodlusts (used through the actions list), only the bloodlusts casted through **optimal\_raid** or **override.bloodlust**.

  * **bloodlust\_percent** (scope: global; default: 0), when greater than zero, is the percent of the target health below which bloodlust will be triggered. When zero, this trigger is disabled.
  * **bloodlust\_time** (scope: global; default: 0), when greater than zero, is the elapsed time threshold, in seconds, since the beginning of the fight. When lesser than zero, it is the estimated remaining time threshold, in seconds, before the target dies. Anytime this threshold is reached, bloodlust will be triggered. When zero, this trigger is disabled.
```
 # This example enables optimal_raid. Bloodlust will be used as soon as one of there are less than 100s before the end of the fight, or when the target falls below 20% health.
 optimal_raid=1
 bloodlust_time=-100
 bloodlust_percent=20
```

# External buffs

Certain buffs that can be used on a player by other players can be enabled through options.

  * **Permanent buffs** (scope: player; default: 0), when set to 1, will make your character benefit from the specified permanent buff given by another player.
    * **external\_buffs.focus\_magic** 
```
# The player will benefit from Focus Magic for the entire simulation.
external_buffs.focus_magic=1
```
  * **Timed buffs** (scope: player; default: disabled), specifies the times when the specified buff will be cast on your character by another player. Individual times are separated with `/` characters.
    * **external\_buffs.power\_infusion**
    * **external\_buffs.benevolent\_faerie**
    * **external\_buffs.blessing\_of\_summer**
    * **external\_buffs.blessing\_of\_autumn**
    * **external\_buffs.blessing\_of\_winter**
    * **external\_buffs.blessing\_of\_spring**
    * **external\_buffs.conquerors\_banner**
    * **external\_buffs.rallying\_cry**
    * **external\_buffs.pact\_of\_the\_soulstalkers**
    * **external\_buffs.kindred\_affinity**
        * The stat given will be determined by the covenant of the player.
        * The player will have a constant buff at base value.
        * At each timestamp, the buff will be doubled for 10s.
```
# Power Infusion will be cast on the player at 0 seconds, 120 seconds, and 240 seconds.
external_buffs.power_infusion=0/120/240

# Fae Guardians will be cast on the player at 0 seconds, 90 seconds, 180 seconds, and 270 seconds.
external_buffs.benevolent_faerie=0/90/180/270

# Disable Power Infusion if the option was already enabled.
external_buffs.power_infusion=
```
# Targeted buffs

When both **optimal\_raid** and the relevant **override.xxx** are disabled and you're performing a simulation with many characters, targeted buffs such as "tricks of the trade" have features to let you specify their targets.

There are two ways to do so:
```
 # Let's make John the rogue use tricks of the trade on Bill
 armory=us,illidan,John
 tricks_of_the_trade_target=Bill

 # Or we can specify it in John's actions list:
 armory=us,illidan,John
 actions+=/tricks_of_the_trade,target=Bill
```

The following buffs support those two mechanics (**xxx\_target** and a _target_ for the corresponding action):
  1. tricks of the trade

  * The relevant key words (**tricks\_of\_the\_trade\_target**) have the "current character" scope and are empty by default (no target). The corresponding actions are not included in the default actions lists (unless they can be casted on self).