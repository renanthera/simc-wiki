**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Rune expression system

Note: In the following discussion, **_rune type_** means the base type of a rune, whether it is currently a normal rune (e.g, blood), or a death rune.

Each of the rune types can be evaluated using the _blood_, _frost_, and _unholy_ expressions. Each of these expressions returns the number of ready runes of the rune type.
```
 # Use obliterate, if two blood, unholy, or frost runes are ready (either normal or a death rune)
 actions+=/obliterate,if=blood=2|frost=2|unholy=2
```

In addition, capitalizing the first letter of the rune type expression (e.g., Blood) will **evaluate the number of ready base type runes, _and additionally, the number of any ready death runes_**.
```
 # Use blood boil if there are a combination of two blood and death runes ready.
 actions+=/blood_boil,if=Blood=2
```

The expression "death" evaluates the current ready death runes for the actor.
```
 # Use Death and Decay if there are at least two death runes ready
 actions+=/death_and_decay,if=death>=2
```

**Starting from simulationcraft 6.0.3 release 21, there are several new rune system expressions available.**

First, to apply a specifier to the basic rune expression, you can use the word "death" to limit the expression to runes of a base type that are currently death runes. Note that "death.death" is nonsensical, and "Blood.death" is the same as "death" (i.e., capitalizing the first letter of the rune type, and requiring death runes is the same as requiring only death runes to satisfy the expression).
```
# Blood boil if there is only an Unholy(death) rune available
actions+=/blood_boil,if=blood=0&frost.death=0&unholy.death>=1
```

Additionally, there are now several different specifiers that can be applied to the rune expression. Currently, four are defined (`cooldown_min`, `cooldown_max`, `count`, and `frac`).

The `cooldown_min` expression returns the minimum cooldown time in seconds for a specified rune expression (as given by the base rune type, and the specifier). If no runes are found to satisfy the condition, the expression returns a very large number. If there are ready runes that satisfy the condition, the expression returns 0.
```
# Blood boil if a blood rune is about to regenerate to full (and the other blood rune is depleted).
# Rune cost will be satisfied by either Frost(death), or Unholy(death) runes.
actions+=/blood_boil,if=blood.cooldown_min>0&blood.cooldown_min<2
```

Similarly, the `cooldown_max` expression returns the maximum cooldown time in seconds for a specified rune expression (as given by the base rune type, and the specifier). If no runes are found to satisfy the condition, the expression returns 0. If there are only ready runes that satisfy the condition, the expression returns 0.

Next, the `count` expression returns the number of runes given by the combination of base rune type and the specifier. The runes can be in any state (i.e., full, regenerating, depleted).

```
# Blood boil if there are no Blood(death) runes and we can convert a Blood rune to death
actions+=/blood_boil,if=blood.death.count=0&blood>=1
```

Finally, the `frac` (or `fractional`) expression returns the "value" of the current runes given by the base type and specifier. Each rune is either full (value of 1), regeneration (value of ]0..1[), or depleted (value of 0).

```
# Blood boil if blood runes are about to regen to full, and we are going to spend a blood rune to cast the blood boil
actions+=/blood_boil,if=blood.frac>1.75&frost.death=0&unholy.death=0
```


## Incoming damage
The expression `incoming_damage_5s` returns the amount of damage the Death Knight has taken in the previous five seconds.
```
 # Death Strike if the actor has taken 25% of maxhp damage in the previous 5 seconds.
 actions+=/death_strike,if=incoming_damage_5s>=health.max*0.25
```

## Synchronizing weapons
The _sync\_weapons_ (default: 0) option on the _auto\_attack_ action can be used to force the synchronization of weapons at the beginning of the fight. When zero, the offhand will be desynchronized by half of its swing time. In game, you always start with your weapons synchronized but target switching and parry rushes often lead you to go unsynchronized.
```
 # Ensure the player will start with synched weapons.
 actions+=/auto_attack,sync_weapons=1
```

## Presence
The _presence_ action, and its _choose_ property (acceptable values: "blood", "bp", "frost", "fp", "unholy", "up") let you change the presence.
```
 # Choose unholy presence at the top of the actions list.
 actions+=/presence,choose=unholy
```

## Anti-Magic Shell
The _antimagic\_shell_ action allows a Death Knight to simulate the Runic Power gain on incoming damage. The action contains three options: **interval**, **interval\_stddev**, and **damage**. The **interval** option sets the mean of the interval between two consecutive Anti-Magic Shell executions in seconds, and is required to be at minimum the cooldown of the spell. The **interval\_stddev** option sets the standard deviation of the interval between Anti-Magic Shell executions. If specified as less than 1, it is interpreted as a percent of the mean, otherwise it is interpreted as seconds. Finally, the **damage** option sets the amount of incoming damage. The default values for **interval**, and **interval\_stddev** are 60 and 5% respectively. The **damage** option is always required.
```
 # Simulate Runic Power gain on using Anti-Magic Shell to absorb 100000 magic damage every 60 seconds on average.
 actions+=/antimagic_shell,damage=100000
```

## Unholy frenzy target
The target of unholy frenzy can be specified either with the **unholy\_frenzy\_target** (scope: character; default: "") character option, or through the _target_ property of the _unholy\_frenzy_ action.
```
 # Cast unholy frenzy on John.
 unholy_frenzy_target=John

 # Alternative way, from the actions list.
 actions+=/unholy_frenzy,target=John
```

## Available runes
All actions have specific properties you can use in the conditional expressions to check the number of available runes. The _blood_, _frost_, _unholy_ and _death_ keywords return the number of active runes of each type. The _inactive_death_ keyword represents the total number of death runes, whether they are active or not.
```
 # Trigger death and decay if at least two death runes are available.
 actions+=/death_and_decay,if=death>=2
```

## Runes cooldowns
All actions have specific properties you can use in the conditional expressions to check the remaining cooldown on runes. The _blood.cooldown_remains_, _frost.cooldown_remains_, _unholy.cooldown_remains_ and _death.cooldown_remains_ keywords returns the cooldown, in seconds, for the respective rune type.
```
 # Trigger some_spell if there is more than 0.5s remaining on the blood rune cooldown.
 actions+=/some_spell,if=blood.cooldown_remains>0.5
```

## Buffs
Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

  * ebon\_plaguebringer\_track. The ebon plague disease is split into two components: a target debuff (ebon\_plague), which increases magic damages for all dk in the raid and a fake, not reported, player buff (ebon\_plaguebringer\_track) which allow us to count the number of active diseases you have on the target, for scourge strike for example.

## Disease related expressions

(**Since Simulationcraft 6.0.0**) You can shorthand disease (BP, FF, NP) expression checking by using the "disease.`dot_expression`" expression. In this case, all available diseases are checked for the dot expression, and by default, the **first** non-zero value is returned.

```
 # Check that any disease is up on target
 actions=outbreak,if=!disease.ticking
```

In addition, you can prefix the `dot_expression` with "min_" and "max_". In these cases, **all** available disease dots are evaluated, and the minimum, or the maximum value of the evaluation is returned.

```
 # Refresh diseases, if we get full benefit from the refresh
 actions=outbreak,if=disease.max_remains<10
```

# Reports
We only document here non-obvious entries.

## Gains
  * might\_of\_the\_frozen\_wastes: the amount of runic power wasted because you were already capped.
  * power\_refund: the amount of runic power refunded by missed abilities.
  * gains\_rune\_abilities: the amount of runic power generated by some abilities.