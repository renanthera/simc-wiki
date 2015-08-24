**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Healing implementation
## Limitations
> Healing has been recently introduced in Simulationcraft, with the priest being the first healer supported so far. It is still young, do not expect the same maturity level as you can be used to in Simulationcraft. For example, fights in Simulationcraft are unidimensional: all players, pets and targets are on the same axis, only the distance from the main target changes. besides, although players can lose health (because they're tanking or suffering from damages on the whole raid), they will continue to perform actions after their death (and there may be some fancy bugs here). As a result, some spells exhibit a behaviour slightly different from their in-game counterparts.

> Regarding the reports, all healing stats will still be labeled as "damages" ("dps" rather than "hps" for example). Besides, only the total healing done will be reported, not the actual healing done or the overhealing.

## Setting up a simulation
> To use healing features in Simulationcraft, import or declare a discipline or holy priest and ensure his role is set to "heal" (should be the default for those specs). We also suggest you add other players, even dummy ones (add single lines such as "warrior=john"). And maybe a tank (use "role=tank").

## Targets
> Regarding the targets, by default it is always the caster himself. Although the default target cannot be changed, you can explicitly specify on every action the target of your choice. You can also add a condition to check the target's health, see [ActionLists](ActionLists.md).
```
 # Cast flash heal on John when he has less than 50% health.
 actions+=/flash_heal,target=John,if=target.health_pct<50
```

> Spells with many targets are detailed in the next section; eligible targets will be friendly, non-pet, targets in range (when relevant) and they will be sequentially chosen (following the declaration or importation order) unless specified otherwise.

## Spells implementation notes
  * Atonement: Defaults to healing the lowest health target in the raid. This behavior can be overriden with the atonement\_target option.
  * Binding Heal: When the default target is the caster himself (default behaviour), the Binding Heal will be used on the first different and eligible target. If none is found, only the "self" part of the Binding Heal will be executed.
  * Divine Hymn: Heals the player with the lowest health in the raid, then the the first two different and eligible targets, whatever their health.
  * Lightwell: at given, customizable, intervals, its target will consume one charge, until exhaustion.
  * Prayer of Mending will first land on its initial target, then jump on the first four different and eligible targets in the raid.

# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface.md) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md).

## Atonement target
It is possible to override the smart targeting of Atonement heals with the **atonement\_target** Priest option. This makes it possible to simulate, for example, all Atonement heals going to a target with Grace.
```
 # Force Atonement heals to target John
 atonement_target=John
```

## Power Word: Shield
> By default PWS will debuff the target with the Weakened Soul debuff and prevent PWS from being cast on that target until it expires. To simulate PWS spam over an entire raid, without having to simulate an entire raid, you can use the 'ignore\_debuff' option.
```
  # Chain spam PWS
  actions+=/power_word_shield,ignore_debuff=1
```

## Lightwell consumption rate
  * The _lightwell_ action is modeled as a hot: at fixed intervals, one charge will be eaten. The _consume\_interval_ (default: 10.0) is the interval, in seconds, between two charges consumption.
```
 # Casts lightwell and have one charge consumed every 5s.
 actions+=lightwell,consume_interval=5
```

## No jumps for prayer of mending
  * The _prayer\_of\_mending_ action has a _single_ option (default: 0) that, when different from zero, will prevent the prayer to jump on more targets.
```
 # Casts prayer of mending, preventing it to jump.
 actions+=prayer_of_mending,single=1
```

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs.md).

  * chakra\_serenity, chakra\_chastise and chakra\_sanctuary can be used to check for chakras.
  * chakra\_pre is triggered when you activate the "chakra" spell and remains until you use any spell that will determine the type of chakra to gain.
  * chakra\_serenity\_crit is the buff gained after using holy word: serenity.
```
 actions+=/flash_heal,if=buff.chakra_pre.up
```

# Reports
We only document here non-obvious entries.