**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Synchronizing weapons
> The _sync\_weaapons_ (default: 0) option on the _auto\_attack_ action can be used to force the synchronization of weapons at the beginning of the fight. When zero, the offhand will be desynchronized by half of its swing time. In game, you always start with your weapons synchronized but target switching and parry rushes often lead you to go unsynchronized.
```
 # Ensure the player will start with synched weapons.
 actions+=/auto_attack,sync_weapons=1
```

## Totems
> There are two totem related action expressions that can be used to query the status of the totem (with the expression `active`) or the remaining time of the totem (with the expression `remains`). In addition to this, there are player scope options for the same queries. Totems can be referred with the syntax "`totem.X.<expression>`", where X can be either a totem name, e.g. `searing_totem` or the totem type (`fire`, `earth`, `water`, `air`).
```
 # Check the activity status of Fire Elemental totem in Searing Totem action
 actions+=/searing_totem,if=!active&!totem.fire_elemental_totem.active

 # Use Mana Spring totem only if there is no Water totem up
 actions+=/mana_spring_totem,if=!totem.water.active

 # Refresh searing totem if there is less than 5 seconds left on the duration
 actions+=/searing_totem,if=remains<5
```

Note that if totem actions are not using expressions, totems will be cast indefinitely as the simulator no longer implicitly adds the "activity" expression into the action. **Always use `if=!active` check or similar expression to check the state of the totem.**

## Lava lash
> The _wf\_cd\_only_ option (default: 0) on the _lava\_lash_ action, when different from zero, only allows lava lash when the windfury weapon is on cooldown. If the windfury weapon is ready, lava lash won't be used.
```
 # Only use lava lash when the windfury weapon is on cooldown.
 actions+=/lava_lash,wf_cd_only=1
```

## Flametongue and windfury weapons
> Both those spells have a _weapon_ setting (default: "both") to allow them to proc either from the main hand or the off hand, or from both. Acceptable values are: "main", "off", "both".
```
 actions+=/windfury_weapon,weapon=both
```

## Fire elemental
> The fire elemental is a pet. To summon it and learn more about pets, see [Characters#Pets](Characters#Pets). It is automatically created when you import an elemental shaman and comes with its own actions list. To summon it, use:
```
actions+=/fire_elemental_totem
```

> The _fire\_elemental:travel_ action forces the fire elemental to come into melee range. It will travel at 10 yards per second.
```
 # This is the first line of the fire elemental's default actions list.
 actions+=/travel

 # You can also use it from the shaman actions list:
 actions+=/fire_elemental:travel
```

## Windfury Weapon
> Windfury weapon has an in-game delay between the swing that procs the 3 attacks, and the actual proc triggering. Simulationcraft currently uses a default of 950ms of delay with a standard deviation of 250ms to model this behavior. You can change the delay values using the options:
```
# Windfury procs will now be delayed by 1200 ms
wf_delay=1.2
# .. with a standard deviation of 500ms
wf_delay_stddev=0.5
```

## Unleash Elements
> The Unleash Flame buff in game suffers from an amount of delay as it expires prematurely due to a fire spell being cast. Combined with the Cataclysm spell queue, this allows Shamans to exploit the delay and cast both a Lava Burst and a queued Flame Shock with the damage buff Unleash Flame provides. Simulationcraft supports the delay and currently uses a delay of 300ms with a standard deviation of 50ms for the delay time. You can change the delay values using the options:
```
# Unleash Flame is now delayed by 500ms
uf_expiration_delay=0.5
# .. with a standard deviation of 100ms
uf_expiration_delay_stddev=0.1
```

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).


# Reports


# Undocumented yet
  * _chain\_lightning_ (clearcasting, conserve, lvb\_cd)