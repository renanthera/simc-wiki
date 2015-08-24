**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface.md) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md).

## Synchronizing weapons
> The _sync\_weapons_ (default: 0) option on the _auto\_attack_ action can be used to force the synchronization of weapons at the beginning of the fight. When zero, the offhand will be desynchronized by half of its swing time. In game, you always start with your weapons synchronized but target switching and parry rushes often lead you to go unsynchronized.
```
 # Ensure the player will start with synched weapons.
 actions+=/auto_attack,sync_weapons=1
```

## Combo points
> Combo points can be used in conditional expressions for actions (see [ActionLists](ActionLists.md)) through the _combo\_points_ character property.
```
 # Use eviscerate when you have 5 combo points
 actions+=/eviscerate,if=combo_points=5
```

> The **initial\_combo\_points** setting (scope: current character; default: 0) can be used to start the fight with the given number of combo points. Only values within `[0; 5]` will be accepted.
```
 # Start the fight with two combo points.
 initial_combo_points=2
```

> The Anticipation talent allows Rogues to store up to 5 Combo Points in a buff called "Anticipation". The `anticipation_charges` expression allows you to return the current number of Anticipation stacks. This is a shorthand for `buff.anticipation.stack`.
```
 # Dispatch if we have room to generate Anticipation charges
 actions+=/dispatch,if=(combo_points<5(talent.anticipation.enabled&anticipation_charges<4)
```

## Poisons
  * _apply\_poison_ instantly changes the poisons on the player's weapons. The action won't be performed if the poisons already match your specifications or if you specified inactive poisons for both weapons.
    1. _main\_hand_ and _off\_hand_ (default: none) are used to specify the poison to use on every weapon. Acceptable values are: "deadly", "instant" or "wound". Other values will result in an inactive poison being applied.
```
 actions+=/apply_poison,main_hand=instant,off_hand=deadly
```

**Since Simulationcraft 6.1.2, release 2** The `poisoned_enemies` expression evaluates to the number of enemy actors currently poisoned with either lethal or non-lethal poison.

## Tricks of the trade target
> The target of tricks of the trade can be specified either with the **tricks\_of\_the\_trade\_target** (scope: character; default: "") character option, or through the _target_ property of the _tricks\_of\_the\_trade_ action. **Note: This option has been removed in Simulationcraft 6.0.0 and newer.**
```
 # Cast tricks of the trade on John.
 tricks_of_the_trade_target=John

 # Alternative way, from the actions list.
 actions+=/tricks_of_the_trade,target=John
```

## Honor among thieves
> For single actor simulations, Honor Among Thieves can be approximated through the use of the `honor_among_thieves` action. The action allows the user to generate HAT combo points at a specific interval. Defaults to 2.3 seconds, with a standard deviation (of a normal distribution) of 100 milliseconds.
```
 # Generate some HAT combo points
 actions.precombat+=/honor_among_thieves,cooldown=2.3,cooldown_stddev=0.1
```
> Note that this proxy Honor Among Thieves action is disabled if the Subtlety Rogue is simulated in an environment with other player profiles.

> The **virtual\_hat\_interval** setting (scope: current character; default: -1) can be used to tweak out the frequency of HaT procs. **Note: This option has been removed in Simulationcraft 6.0.0 and newer.**
    1. When equal to zero, Simulationcraft will genuinely reproduce the mechanic, monitoring critical hits from other members in the raid.
    1. When lesser than zero, the interval between consecutive procs will be the minimum possible one according to this talent's rank, plus 200 ms. I.e., with 3 talent points, it will proc every 2.2s.
    1. When greater then zero, the given value will be the interval, in seconds, between two procs.
```
 # Let's use the exact mechanic, it requires to have other players in the simulation.
 virtual_hat_interval=0

 # Let's force HaT to proc every 3s.
 virtual_hat_interval=3

 # Let's have HaT proc as often as possible (every 2.2s with 3 talent points)
 virtual_hat_interval=-1
```

## Expose armor
> In game, you cannot apply expose armor if faerie fire or sunder armor are already applied. Simulationcraft offers you an _override\_sunder_ (default: 0) option on the _expose\_armor_ action to change this behaviour and replace faerie fire and sunder armor when this setting is different from zero. **Note: This action has been removed in Simulationcraft 6.0.0 and newer.**
```
 actions+=/expose_armor,override_sunder=1
```

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs.md).

  * deadly\_proc: when this buff is up, your deadly poison is applied on the target.
  * poison\_doses: the number of stacks is the number of doses currently applied.
  * stealthed: when up, you are stealthed.

## Weapon Swapping

**Since Simulationcraft 6.1.2-01** Rogues have an experimental weapon swapping mechanism in the simulator. Two new options, `main_hand_secondary` and `off_hand_secondary` allows a profile to specify a secondary weapon to main and off hand, respectively. Both options use the normal item option format.

In addition, there is a new action `swap_weapon` that performs a weapon swap for the profile. Currently, weapon swap incurs a GCD of 1.0 seconds, resets the swing timer(s) of the swapped weapons, and resets the RPPM-related timers. The action has two options, `slot` that specifies the slot to swap (valid values are _main_, _off_, or _both_, with default of _main_). The second option, `swap_to` specifies what set to swap to, with valid values of _primary_ and _secondary_ and a default of _secondary_.

```
# Specify secondary main/offhands
main_hand_secondary=oregorgers_acidetched_gutripper,id=113874,bonus_id=567,enchant=mark_of_the_thunderlord
off_hand_secondary=oregorgers_acidetched_gutripper,id=113874,bonus_id=567,enchant=mark_of_the_thunderlord

# .. and swap to them in certain situations (and swap back to primary when needed)
actions+=/swap_weapon,slot=both,swap_to=secondary,if=active_enemies>1
actions+=/swap_weapon,slot=both,swap_to=primary,if=active_enemies=1
```

# Reports
We only document here non-obvious entries.

## Uptimes
  * energy\_cap : the percentage of the fight time spent with a full energy bar.