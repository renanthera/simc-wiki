_This documentation is a part of the [TCI](TextualConfigurationInterface) reference._

**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**

# Behaviour
Actions lists are priorities lists: periodically, Simulationcraft scans your character's actions list, starting with the first action (the highest priority ) and continuing until an available action is found, or to the end otherwise. Actions that are not possible at the moment (cooldown not ready, execute phase only, conditions not met) are just considered as not available and the applications jumps to the next one.

Here is a simplified warrior actions list:
```
# If the character has no flask already, use a greater draenic strength one
actions=flask,type=greater_draenic_strength_flask
# Otherwise, use a draenic strength potion if the targets health is below 20 percent and recklessness is up, or if the target will die in 25 seconds.
actions+=/potion,name=draenic_strength,if=(target.health.pct<20&buff.recklessness.up)|target.time_to_die<=25
# Otherwise, starts autoattack if not done already.
actions+=/auto_attack
# Otherwise, pops up the "recklessness" 3 min cooldown if ready.
actions+=/recklessness
# Otherwise, uses bloodthirst if ready.
actions+=/bloodthirst
# Otherwise, use colossus smash if ready.
actions+=/colossus_smash
# Otherwise, use execute (only available when target health is below 20% health but it is always implicit)
actions+=/execute
# Otherwise, use raging blow, but only if target is above 20% health
actions+=/raging_blow,if=target.health_pct>=20
```

A couple pieces of advice for writing actions lists:

1. Do not forget, it is priority-based, it's as simple as that!
1. Do not try to optimize your actions lists for computations performances. Just focus on correctly modeling the gameplay you want.
1. Have doubts? Make Simulationcraft write a combat log for you, with the **log** option, see [Output](Output).

# Syntax
  * **actions** (scope: current character; default: _depends on class and spec_) is the list of actions your character will follow. It is a multi-line string and a sequence of commands using the "/" separator.

```
 # Note how we use the "/" separator and the "+=" appending operator.
 actions=dosomething
 actions+=/dosomethingelse
```

# Available actions

## Basics
  * _auto\_attack_ triggers the auto-attack when it's not already activated. It cannot be used to stopping or resetting auto attacks. Options are:
    1. _sync\_weapons_ (optional, default: 0), when different from zero, will synchronize weapons swings for ambidextrous classes with two weapons with the same swing speed. When zero, the offhand will be delayed by half of its swing time. In game, you always start with your weapons synchronized but target switching and parry rushes often lead you to go unsynchronized. Some mechanics are pretty sensible to weapons being synchronized or note, such as [flurry](http://www.wowhead.com/spell=12972/flurry).
```
 # Ensure the player will always auto attack and will start with synched weapons.
 actions+=/auto_attack,sync_weapons=1
```
  * _snapshot\_stats_ forces simulationcraft to capture your buffed stats values just before the combat actually begins. It has no influence on the simulation itself is it's totally optional. However you need to include it if you want the reports and output to display the correct (non-zero) values for raid-buffed stats. It should be located after all other out-of-combat actions (food, flasks, etc), and BEFORE the first potion.
```
 # Ensure the reports will display correct values for "raid-buffed" stats.
 actions+=/snapshot_stats
```
  * _cancel\_buff_ cancels a buff, just like "/cancelaura" would do in game.
    1. _name_ is the name of the buff to cancel.
```
 # Cancels raging blow buff if 2 stacks are up, which has never been used before in game, but hey, it's an example.
 actions+=/cancel_buff,name=raging_blow,if=buff.raging_blow.stack=2
```
  * _use\_item_ triggers the use of an item.
    1. _name_ is the item's name
    1. Alternatively, you can also specify the _slot_ of the item
    1. **Since Simulationcraft 6.1.2-01** In addition, you can also evaluate the type of stat buff the item triggers with the `use_buff.<stat_type>` expression. It evaluates to 1 if the item triggers the expressed stat, 0 otherwise.
```
 # Uses the "shard of woe" trinket
 actions+=/use_item,name=shard_of_woe,if=cooldown.evocation.remains>86
```
  * _restore\_mana_ forcefully and instantly restores mana.
    1. _mana_ (default: 0) is the amount of mana to restore. When left to zero, mana will be restored to its maximum. The purpose of this action is to let you test out infinite mana scenarios or fights with special mana regeneration mechanics. Since this action has no cooldown, it can be performed many times every second.
```
 # This will restore 500 mana anytime it is triggered.
 actions+=/restore_mana,mana=500
```

## Spells
See the relevant page for each class for more information on non-trivial spells.

Spells are added on a per-class basis. Those keywords are the spells' names, where white spaces are replaced with underscores (`_`) and non-alphanumeric characters are ignored. The list would obviously be too long to write and boring to maintain but you can check your class' source code file (sc\_mage.cpp for mages for example) for the "create\_action" function.
```
 # This will make a feral druid cast Tiger's fury.
 actions+=/tigers_fury
```

## Racials
  * _arcane\_torrent_ triggers arcane torrent (blood elf racial)
```
 actions+=/arcane_torrent
```
  * _berserking_ triggers berserking (troll tracial)
```
 actions+=/berserking
```
  * _blood\_fury_ triggers blood fury (orc racial)
```
 actions+=/blood_fury
```
  * _stoneform_ triggers stoneform (dwarf racial)
```
 actions+=/stoneform
```

## Pets
Pets' actions can be used through a specific syntax: `<petname>:<petaction>`. Relevant options are the ones for the specified pet action.
```
 actions+=/spider:wolverine_bite
```
However most pets actions actually have shortcut keywords you will probably prefer:
```
 actions+=/wolverine_bite
```
Note that pets come with their own default actions lists! You can modify them as you do with any regular character.

## Consumables
  * _food_ can trigger the use of a food.
    1. _type_ is the name of the food to use.
```
 actions+=/food,type=blackrock_barbecue
```
  * _flask_ can trigger the use of a flask.
    1. _type_ is the name of the flask to use.
```
 actions+=/flask,type=greater_draenic_strength_flask
```
  * _health\_stone_ can trigger the use of a health stone.
    1. _health_ or _trigger_ is the absolute hp deficit you must suffer to allow the use of the stone.
```
 # If a character has his health 60k below his maximum, he will use the stone
 actions+=/health_stone,trigger=60000
```
  * _potion_ can trigger the use of a potion. Only 1 potion may be used in combat.
```
 # Triggers the potion use when out of combat or when bloodlust has just started.
 actions+=/potion,name=draenic_strength,if=!in_combat|buff.bloodlust.react
```
  * _augmentation_ can trigger the use of a Augmentation Rune.
    1. _type_ is either focus, hyper or stout.
```
 # Triggers Focus Augmentation Rune.
 actions+=/augmentation,type=focus
```
  * _oralius\_whispering\_crystal_ and _crystal\_of\_infinity_ can trigger the use of the special consumables found in WoW. (**Since Simulationcraft 6.0.3-26**)

## Movement
  * _start\_moving_ triggers a movement phase, it will end only with _stop\_moving_.
  * _stop\_moving_ ends the movement phase.
```
 # Here are fragments of the shadowpriest rotation. When the target health is below 25%, sw:d deals three times more damages and has a chance to make apparitions spawn. This chance is increased while the sp moves. 

 # Do not move when sw:d is on cooldown 
 actions+=/stop_moving,health_percentage<=25,if=cooldown.shadow_word_death.remains>=0.2
 # Start moving when the sw:d cooldown is going to end (we need to stand still to fire it)
 actions+=/start_moving,health_percentage<=25,if=cooldown.shadow_word_death.remains<=0.1
```

## Sequences
Actions sequences are sub-actions chains to execute in a given order. Use the following keyword:

  * _sequence_ declares and triggers a sequence of actions to use in the specified order. Actions are separated with ":".

    1. _name_ (optional, default: "default") is used to name the sequence.

Once one of the sub-actions has been performed, Simulationcraft does not immediately perform the next sub-action in the chain. Instead, it restarts at the beginning of the whole actions list (not the sequence). If the sequence is executed again, then it will trigger the actions which have not been performed yet.
```
# So, some class has three spells: yellow, blue and red. They all share the global cooldown.
actions+=/yellow
actions+=/sequence:red:blue

# On the first gcd, yellow is not ready, red and blue are: the application will execute "red"
# On the second gcd, all spells are ready: the application will execute "yellow"
# On the third gcd, yellow is not ready, red and blue are: the application will execute "blue"
# From now on, the application will only perform "yellow".
```

When all spells have been performed, the sequence is not automatically reinitialized and it will be skipped from now on! You need to use the following keyword:

* _restart\_sequence_ will restart the specified sequence.

  1. _name_ is the name of the sequence to restart.
```
# Here are fragments of the 4.0.6 mage rotation
actions+=/sequence,name=attack:fire_melee:fire_nova:fire_blast
actions+=/restart_sequence,name=attack,moving=0
```

Finally, you can use  _wait\_on\_ready_ (default: -1) on a sequence or one of its sub-actions. When equal to 1, it will force the the application to restart at the beginning of the actions list processing if this spell is not ready. Practically, actions below this one will never be executed. However, things are slightly different for sequences:

  1. If the sequence itself is flagged as wait\_on\_ready, all spells with _wait\_on\_ready=-1_ will be flagged with the value you specified whenever the sequence is restarted.
  1. The sequence will be considered as flagged whenever the next remaining spell is flagged with _wait\_on\_ready=1_.
```
# Here is a sample of an old death knight sequence. Spells have been replaced with their abbreviations to make things easier.
actions+=/sequence,wait_on_ready=1:PS:IT:BS:BS:SS
actions+=/DC
actions+=/restart_sequence,name=default

# At first, because of wait_on_ready, the application will flag all spells with wait_on_ready=1. It means the application will have to wait on every step and until the sequence has been completed. It will never reach the "DC" line even if one of the spells is not ready yet.
# So, the application will perform PS-IT-BS-BS-SS. Then, as long as it can do DC, it will. Once there is not enough runic power left for DC, the sequence will be restarted.
```
Do you have headaches already ? Yes, sequences are tricky, they are rarely used. If you do use them, do it with caution.

## Strict Sequences
Strict Sequences are a breed of sequence, except for they do not need to be reset, and when they are started, they cannot be stopped under normal circumstances. A strict sequence requires all actions in the sequence to be ready for the duration of the sequence.
```
# Arms Warrior will perform Recklessness, bloodbath, colossus smash, mortal strike, whirlwind, whirlwind when all are available.
# The name allows you to call this sequence from other parts of the action list. 
actions+=/strict_sequence,name=swifty:recklessness:bloodbath:colossus_smash:mortal_strike:whirlwind
```

## Waits

  * _wait_ orders the application to stop processing the actions list for a given time. Auto-attacks and such will still be performed.

    1. _sec_ (default: 1) is the number of seconds to wait. It can be a constant or an expression (see the [conditional expressions](#Conditional_Expressions) section).
```
# This orders Simulationcraft to stop processing the actions list for 5s
actions+=/wait,sec=5

# This orders Simulationcraft to stop processing the actions list until only 2s remains before somebuff expires (if 5s remaining, wait 3s).
actions+=/wait,sec=buff.somebuff.remains-2
```

  * _wait\_until\_ready_ orders the player to stop processing the actions list until some cooldown or dot expires. Its only purpose is to improve performances but beware: conditions such as a buff expiration, reaction to heroism/bloodlust, etc, won't be checked.

    1. _sec_ (default: 1) is the maximum time, in seconds, the player will wait. One second is enough, it reduces the actions list processing cost by an order of magnitude. And since some conditions won't automatically wake up the application, it is advised to keep it low. Just as for _wait_, this option can be an expression as well as a simple number.
```
actions+=/wait_until_ready,sec=0.5
```

## Resources
* _pool\_resource_ will force the application to stop processing the actions list while the resource is restored. By default, the primary resource of the spec is pooled. 
    1. _wait_ (default: 0.5) is the time, in seconds, to wait. It is advised to keep this value low so that the resource pooling will only occur as long as the application reaches this very action and as its conditions are satisfied.
    1. _for\_next_ (default: 0), when different from 0, will force the application to wait until the player has enough resources for the following action in list. If the following action already satisfies its resource criteria or if it is made unavailable for other reasons than resource starvation (cooldown for example), then _pool\_resource_ will be ignored.
    1. _extra\_amount_ (default: 0), **must** be used with _for\_next_ parameter. When different from 0, it will require an additional amount of resource to be generated (in addition to the cost of the next action).

```
# First example, without using for_next: the application will pool energy while the player has less than 60 energy and slice and dice must soon be refreshed (within 5s).
actions+=/pool_energy,if=energy<60&buff.slice_and_dice.remains<5
actions+=/slice_and_dice,if=combo_points>=3&buff.slice_and_dice.remains<2

# Second example, with for_next: if the player is not stealthed and has less than 5 combo points but the player has less than 85 energy (the only non-satisfied criteria for shadow dance), then the application will pool energy until the player has 85 or more energy. If the player is stealthed or has 5 combo points, both lines will be skipped.
actions+=/pool_energy,for_next=1,extra_amount=85
actions+=/shadow_dance,if=energy>=85&combo_points<5&buff.stealthed.down
```

# Actions modifiers
All actions have additional options, we're listing them here.

## Selecting the target

* _target_ (default: "") is the action's target.  When empty, it will be the default target (the player himself for healers, the main target for damage dealers and tanks). To force a spell to target yourself, use the syntax `target=self`.
```
# cast power_infusion on actor named John
actions+=/power_infusion,target=John
# cast holy prism on yourself
actions+=/holy_prism,target=self
```
* _cycle\_targets_ will cycle the action through all available targets when set to 1.
```
# Use moonfire on any target that does not currently have it.
actions+=/moonfire,cycle_targets=1,if=!ticking
```
* _max\_cycle\_targets_ will set a maximum amount of targets to cycle through.
```
# Cycles through only 3 targets.
actions+=/moonfire,cycle_targets=1,max_cycle_targets=3,if=!ticking
```

## Usage on specific events only

* _buff.bloodlust.react_ (default: 0), when different from zero, will flag the action as usable only when bloodlust (heroism, time warp, etc) is active. When left to zero, the action will be usable anytime.
```
# Let's use recklessness only under bloodlust.
actions+=/recklessness,if=buff.bloodlust.react=1
```
* _target.debuff.invulnerable.react_ (default: 0), when different from zero, will flag the action as usable only when the target is invulnerable (happens only when you specified an invulnerability raid event). When left to zero, the action will be usable anytime.
```
# Using this at the top of the actions list will force the player to wait (through 0.5s steps) and do nothing while the target is invulnerable.
actions+=/wait,sec=0.5,target.debuff.invulnerable.react=1
```
* _target.debuff.vulnerable.react_ (default: 0), when different from zero, will flag the action as usable only when the target is vulnerable (suffers twice more damages, it happens only when you specified a vulnerability raid event). When left to zero, the action will be usable anytime.
```
# Let's use recklessness only when the target is vulnerable.
actions+=/recklessness,if=target.debuff.vulnerable.react=1
```
* _target.debuff.flying.react_ (default: 0), when different from zero, will flag the action as usable only when the target is flying.
```
# Let's use black arrow only when the target is flying.
actions+=/black_arrow,if=target.debuff.flying.react=1
# Let's use explosive trap only when the target is on the ground.
actions+=/explosive_trap,if=target.debuff.flying.react=0
```
* _moving_ (default: -1), when different from -1, will flag the action as usable only when the players are moving (_moving=1_) or not moving (_moving=0_). When left to -1, the action will be usable anytime. The players happen to move either because of a "movement" raid event, or because of "start\_moving" actions. Note that actions which are not usable while moving do not need to be flagged with "_move=0_", Simulationcraft is already aware of those restrictions.
```
# Let's use typhoon only when the player is moving.
actions+=/typhoon,moving=1
```
* _prev_ returns the previous foreground action executed. This will include gcd and non-gcd actions, such as fireball and bloodbath.
```
# Only use pyroblast when the previous spell used was fireball
actions+=/pyroblast,if=prev.fireball
```
* _prev\_gcd_ returns only the previous action that used a GCD. This will only include actions such as fireball, but not bloodbath.
```
# Only use whirlwind after mortal strike.
actions+=/whirlwind,if=prev_gcd.whirlwind
```
* _prev\_off\_gcd_ returns all off gcd actions that occurred since the previous gcd was executed. So after a warrior uses raging blow, it will track every off-gcd action until another gcd action is executed, then it is reset.
```
# Only use recklessness if bloodbath was just executed.
actions+=/recklessness,if=prev_off_gcd=bloodbath
```

## Time-based usages
* _time_ can be used to make an action usable only when the elapsed time, in seconds, since the beginning of the fight is between specified bounds. It has to be used with the "<=" or ">=" operators. You can specify both an upper and a lower bound. It is especially useful when you want to time an action in respect to your raid events.
```
# Cast bloodlust 20s after the beginning of the fight
actions+=/bloodlust,if=time>=20
```
* _time\_to\_Xpct_ can be used to make an action usable only when the estimated remaining time, in seconds, is between specified bounds. It has to be used with the "<=" or ">=" operators. You can specify both an upper and a lower bound, and you can also set the percent. time\_to\_die will be converted into time\_to\_0pct.
```
# Cast bloodlust 60s before the estimated end the of the fight.
actions+=/bloodlust,if=time_to_die<60
# Cast recklessness if it will be available again for execute range
actions+=/recklessness,if=time_to_20pct>180
```
* _line\_cd_ can be used to force a length of time, in seconds, to pass after executing an action before it can be executed again. In the example below, the second line can execute even while the first line is being delayed because of _line\_cd_.
```
# Cast soulburn exactly once during dark soul (which has a 20s duration)
actions+=/soulburn,line_cd=20,if=buff.dark_soul.up
 
# Cast soulburn during the execute phase when UA is on its last tick
actions+=/soulburn,if=target.health.pct<=20&dot.unstable_affliction.ticks_remain<=1
```

## Cooldowns synchronization
* _sync_ (default: "") can be used to flag an action as unusable while another specified action is not ready. The given value must be the name of the synchronized action. **This line will be executed as soon as the specific action is READY, not when the action is necessarily used.**
```
# Warriors tend to pop their cooldowns at the same time. Recklessness has a 4 mins cooldown, death wish has a 2.4 mins cooldown. Let's force recklessness to wait for dw to be ready.
actions+=/recklessness,sync=death_wish
```

## Health restrictions
* _target.health.pct_ can be used to make an action usable only when the target's health percentage is between specified bounds. It has to be used with the "<=" or ">=" operators. You can specify both an upper and a lower bound.
```
# Starts bloodlust when the target's health is below 25%.
actions+=/bloodlust,target.health.pct<25
```

## Channeling
* _interrupt_ can be used on channeled spells, when set to a non-zero value, to interrupt the channeling when another action with a higher priority is ready. The interrupt will only occur immediately following a tick.
```
# Stop channeling mind flay when any other action with a higher priority is made available.
actions+=/mind_flay,interrupt=1
```
* _interrupt\_if_ can be used on channeled spells to interrupt the channeling if a higher priority action is ready (the same as _interrupt_), the global cooldown has elapsed, **and** the specified conditions are met. The interrupt will only occur immediately following a tick. The conditions are provided using the syntax for conditional expressions.
```
# Stop channeling when there is less than 1s remaining on the mind blast cooldown.
actions+=/mind_flay,interrupt_if=cooldown.mind_blast.remains<1
```
* _interrupt\_immediate_ can be used on a channeled spell that has an _interrupt\_if_ expression to instruct the actor to immediately interrupt the channeled action, even if the global cooldown has not elapsed yet. **Added in Simulationcraft 7.0.3, release 1**
* _chain_ can be used to re-cast a channeled spell at the beginning of its last tick.  This has two advantages over waiting for the channel to complete before re-casting: 1) the gcd finishes sooner, and 2) it avoids the roughly 1/4 second delay between the end of a channel and the beginning of the next cast.
```
# Chain-cast Mind Flay until a higher priority action is ready
actions+=/mind_flay,chain=1
```
* _early\_chain\_if_ has the same effect as _chain_, but with three differences: 1) it only chains the spell if the given expression is true, 2) it can chain the spell at the beginning of any tick, not just the last, and 3) it will not execute during the gcd.
```
# Chain-cast Mind Flay Insanity, restarting the cast early if Devouring Plague is about to fall off
actions+=/mind_flay_insanity,interrupt=1,chain=1,early_chain_if=dot.devouring_plague_tick.remains<=tick_time
```

## Tweaking out the flight speed
* _travel\_speed_ (default: _ingame flight speed_) is the flight speed, in yards per second, of the spell (a fireball for example).
```
# Let's make our fireballs instant.
actions+=/fireball,travel_speed=0
```

## Sequences behaviour
* _wait\_on\_ready_ (default: -1), when equal to 1, will force the the application to restart at the beginning of the actions list processing if this spell is not ready. Practically, actions below this one will never be executed. You can use it to quickly make the end of the list inactive but the main purpose of this option is for sequences, see the [related section](#Sequences).
```
# Let's put wait_on_ready=1 on this line near the end of the balance druid's actions list.
actions+=/wrath,wait_on_ready=1,if=eclipse_dir=-1

# Those last lines will never be executed.
actions+=/starfire
actions+=/wild_mushroom,moving=1,if=buff.wild_mushroom.stack<3
actions+=/moonfire,moving=1
actions+=/sunfire,moving=1
```

## Enemy-Specific Modifiers
* See the article on [enemies](Enemies#Action_Lists).

# Conditional expressions
Conditional expressions are added through the "if" keyword, using the following syntax:
```
# Uses faerie fire if:
# * There are less than three stacks
# * And neither "expose armor" nor "sunder armor" are on the target
actions+=/faerie_fire,if=debuff.faerie_fire.stack<3&!(debuff.sunder_armor.up|debuff.expose_armor.up)
```

Note: the same syntax is used for the _interrupt\_if_ action modifier and the the _sec_ modifier for _wait\_fixed_ actions.

## Operators

### Introduction

Most known operators are the arithmetic ones, so we're going to use them to introduce you to some operators properties. Here are the arithmetic operators accepted by Simulationcraft:

* **`*`** is the multiplication operator: it returns the product of the left and right member.
* **`%`** is the division operator: it returns the division of the left by the right member.
* **`-`** is the either the binary subtraction operator (returns the difference between the left and right members) or the unary negation operator ("-7" returns the opposite of the right member, 7).
* **`+`** is either the binary addition operator (returns the sum of the left and right members) or the unary "plus", which has no effect (+7 transforms 7 into 7).

In addition to the above, Simulationcraft has additional functions defined to perform basic operations on expressions:

* **floor()** will return the previous integer value of the expression given inside the parenthesis
* **ceil()** will return the next integer value of the expression given inside the parenthesis

About the vocabulary we used: **binary** operators are applied to a left and a right member while **unary** operators are applied to their right member only.

Now, let's imagine that you read the "7 + 4 `*` 5" calculus. You know it has to be read as "7 + (4 `*` 5)". Why ? Because the multiplication and division have a higher **priority** and take precedence over the addition and subtraction operator. In the same way, you know that "5 `*` -7" has to be read as "5 `*` (-7)" because unary operators have a higher priority than binary operators.

Finally, what about "500 % 5 `*` 10" ? Multiplication and division operators both have the same priority so there are two ways to read it: "500 % (5 `*` 10)" or "(500 % 5) `*` 10". We need to set up a conventional **reading order** : for Simulationcraft, it will be from **left to right**: when two operators have the same priority, the leftmost one is given a higher priority. We have to understand our calculus as "(500 % 5) `*` 10".

### Logical operators
The first example displayed the use of _logical operators_. Logical operators are:

* **`&`** is the binary AND operator: returns true when both left and right members are true.
* **`|`** is the binary OR operator: returns true when at least one of the left and right members are true.
* **`^`** is the binary XOR operator: returns true when either the left or right member is true, but not both.
* **`!`** is the unary NOT operator: returns true when the right member is false.

```
# The following condition:
actions+=/faerie_fire,if=debuff.faerie_fire.stack<3&!(debuff.sunder_armor.up|debuff.expose_armor.up)

# That means (remember that unary operators take precedence over binary ones):
debuff.faerie_fire.stack <3 AND (NOT(debuff.sunder_armor.up OR debuff.expose_armor.up))

# (debuff.sunder_armor.up OR debuff.expose_armor.up) is true when sunder_armor or expose_armor are up on the target.
# (NOT(debuff.sunder_armor.up OR debuff.expose_armor.up)) is true if none of the two debuffs are up, false if at least one is up.
# As a result, the condition is true when there are less than three stacks of faerie fire and neither sunder_armor nor expose_armor are up.
```

One important note: false is zero. True is anything different from zero. Which means that you can test regular numbers as if they were boolean.
```
# Both syntaxes are valid and do the same thing:
actions=/stance,choose=berserker,if=!in_combat
actions=/stance,choose=berserker,if=in_combat=0
```

### Complete list of operators
Besides the logical operators, let's mention some specific operators we didn't mention so far:

* **`=  `** is the equality comparison operator.
* **`!=`** is the inequality comparison operator.
* **`~  `** is the inclusion operator: it returns true if the left string member is contained in the right string member (**only used for SpellQuery**).
* **`!~`** is the exclusion operator: it returns true if the left string member is not contained in the right string member (**only used for SpellQuery**).
* **`@  `** is the absolute unary operator: it returns the absolute value of its right member.

We also didn't mention the comparison operators: "=" is the equality comparison operator, "<=" is "lesser than or equal", etc... Unequality is achieved through the concatenation of the NOT operator with the equality operator: "!=".

Finally, here is the full operators priorities list, from the highest ones to the lowest ones:

* Function calls (**`floor , ceil`**)
* Unary operators (**`+ , - , @ , !`**)
* Multiplication and division (**`* , %`**)
* Addition and subtraction (**`+ , -`**)
* Comparison operators (**`= , != , < , <= , >= , > , ~, !~`**)
* Binary logical and (**`&`**)
* Binary logical or (**`|`**)

## Operands

### Action properties
Action properties are related to the action you want to perform. They require no specific syntax. The available properties are:
```
# If sw:p has not been used so far or its last occurrence missed, then recast it, provided it's not active or close to expiration.
actions+=/shadow_word_pain,if=(!ticking|dot.shadow_word_pain.remains<gcd+0.5)&miss_react
```

* _execute\_time_ returns whichever is greater: gcd or cast\_time
* _gcd_ is the amount of gcd-time it takes for the current action to execute, accounting for haste.
* _gcd.remains_ returns the amount of time until the player's gcd is ready
* _gcd.max_ returns the hasted gcd-time of the **PLAYER**, not the action. This is useful for wait commands.
* _cast\_time_, is the time (in seconds) which the action will need to execute.
* _cooldown_, for a spell or an usable item, is the initial cooldown duration, in seconds.
* _ticking_, for a dot or a hot, will return 1 if the dot is currently active on your target, 0 otherwise.
* _ticks_, for a dot or a hot, will return the number of ticks done so far since the last time the dot was refreshed.
* _ticks\_remain_, for a dot or a hot, will return the number of remaining ticks before the dot expires.
* _remains_, for a dot or a hot, will return the remaining time, in seconds, before the dot expires. It does NOT apply to buffs and debuffs.
* _tick\_time_, for a dot or a hot, is the time in seconds between ticks, if cast using your current haste.
* _travel\_time_ is the timespan, in seconds, the spell will need to reach its target (a fireball for example).
* _miss\_react_ is 1 if the last occurrence of this action missed or has never been used, 0 otherwise, taking into account the reaction time, as specified through **reaction\_time**. If you specified 0.5s and the miss only occurred 0.3s ago, this property will return 1.
* _cooldown\_react_ is 1 if the cooldown has elapsed, the reaction time for the abrupt reset has elapsed, or the cooldown was reset in a determined way. The expression returns 0 if the reset of the cooldown happened early (e.g., due to a proc or another action) and the cooldown specific reaction time to the abrupt reset of the cooldown has not yet elapsed.
* _cast\_delay_ is 1 if sufficient time has elapsed after the previous player executable action's cast time (including gcd). The time is controlled by two separate parameters, _brain\_lag_ and _brain\_lag\_stddev_.

### Buffs and debuffs
The character's buffs and the raid-friendly debuffs on your target (sunder armor, curses, etc) can all be used through the following syntax: `buff.<aura_name>.<aura_property>` (recommended) or `aura.<aura_name>.<aura_property>` (not recommended, see below). As usual, for the aura name, use underscores instead of white spaces and ignore non-alphanumeric characters.

SimC doesn't have separate concepts of "buff" and "debuff" - we have one generic buff object, so when you apply e.g. a `mortal_strike` debuff to the target, you're really giving them a "buff" named `mortal_strike`. However, we do have APL syntax for both buffs and debuffs based on where you want to search for a given buff.

For example, `debuff.mortal_strike.up` will check the target for a `mortal_strike` buff first, and if it doesn't find anything, will then check the player's buffs. The conditional `buff.mortal_strike.up`, on the other hand, will _only_ check the player, and give up if it doesn't find anything.
```
# Here is how we can check the number of stacks of faerie fire on the target.
actions+=/faerie_fire,if=debuff.faerie_fire.stack<3
# This is how we would check for the presence of a beneficial buff on the player.
actions+=/avengers_shield,if=buff.grand_crusader.react
```

Regarding the list of buffs...

1. The "buff "list will contains a smartly filtered list of buffs and target debuffs. For example, if many warriors are in the raid, every one of them will only have his own version of colossus smash, so that he cannot react to a CS from another warrior. However, this list will contain "sunder\_armor", "expose\_armor" and "faerie\_fire" and those ones will be updated whenever someone in the raid applies it on the target. Finally, it will contains all buffs the character has.
1. The "aura" list, however, is kinda strange and it is advised you not use it unless you're sure you should.
1. The "buff" list also contains special buffs such as:
  * "bleeding" (target is bleeding)
  * "casting" (character is casting)
  * "flying" (character is flying)
  * "raid\_movement" (character is moving because of a "movement" raid event)
  * "self\_movement" (character is moving because of a _start\_move_ action)
  * "stunned" (character is stunned)
  * "invulnerable" (target is invulnerable)
  * "vulnerable" (target is vulnerable)
  * "mortal\_wounds" (character has the mortal strike debuff)
  * "damage\_taken" (**Since Simulationcraft 6.0.1**) (stacking debuff that causes 1% extra damage taken per stack, see enemy action options).
1. The "buff" list also contains buffs for
  * potions (speed\_potion, tolvir\_potion, etc)
  * trinkets (crushing\_matter, etc)
  * stances (defensive\_stance, etc)
  * shapes (moonkin\_form, etc)
  * enchants (landslide\_mh for main hand, etc).
1. If you want to check the complete "buff" and "aura" lists, examine the application's output (not the html report). Under every player's detail, you will see a listing of constant and dynamic buffs: those are the content of the "buff" list. Now, past the players' and targets' details, is a "Auras:" label, with also constant and dynamic buffs: those are the content of the "aura" list.
1. (**Since Simulationcraft 6.0.1**) You can also refer to any potion-based buff by using the `potion` alias as the buff name (i.e., `buff.potion.up`).

For every buff/debuff, the available properties are:

* _remains_ is the remaining time, in seconds, for this debuff. Debuffs with a an infinite duration have a zero value.
* _cooldown\_remains_ is the remaining time, in seconds, for spell's cooldown triggering this buff.
* _up_ is 1 when the debuff currently exists and is active, 0 otherwise.
* _down_ is 0 when the debuff currently exists and is active, 1 otherwise.
* _stack_ is the number of stacks of this buff.
* _max\_stack_ is the maximum possible stack size of this buff.
* _stack\_pct_ returns 100 `*` _stack_ `/` _max\_stack_.
* _react_ is the number of stacks of this buff, taking into account your reaction time, as specified through **reaction\_time**. If you specified 0.5s, the returned value will be the number of stacks there were 0.5s ago.
* _value_ is the buff's value. For a 1200 spell power buff, for example, it will  be 1200.

### Trinket Procs
These commands can be combined with trinkets if you wish to create action lists that react to trinket procs.

Syntax: trinket.has\_stacking\_stat_._stat_._specific stat_._buff expression

All commands that work with buffs will also work with this.

The slot is not required, and can be skipped. If skipped, it will scan both trinket slots. If both trinkets satisfy the buff expression, the maximum value of the buff expressions will be chosen. Examples:
```
# Flags as true if the trinket in slot 2 has the ability to proc an agility stacking proc.
trinket.2.has_stacking_stat.agility

# Flags as true if any trinket has a non-stacking strength proc.
trinket.has_stat.strength

# Flags as true if the trinket in slot 1 has agility proc with more than 10 stacks.
trinket.1.stacking_stat.agility.stack>10

# Flags as true if the trinket in slot 2 procs for over 3000 mastery, non-stacking.
trinket.2.stat.mastery.value>3000

# Flags as true if any trinket has a non-stacking strength proc with more than 5 seconds left on the internal cooldown.
trinket.stat.strength.cooldown_remains>5
```
They can be combined with other conditions:
```
# Save recklessness if the cooldown on the trinket proc is greater than 15, and the cooldown on skull banner is below 20.
actions+=/recklessness,if=trinket.stat.strength.cooldown_remains>15&cooldown.skull_banner.remains<20
```

**Since Simulationcraft 6.0.1 release 1**; You can also express trinket cooldowns through the expression system. Generic syntax is `trinket.(has_|)cooldown.<cooldown_expr>`, where `<cooldown_expr>` refers to any cooldown expression we support. `has_cooldown` requires no cooldown expression. Positional trinket parameters are also supported, see above for example. If the actor has no trinkets with cooldown, both expressions will always return 0. If both trinket slots have a cooldown, the larger cooldown expression return value will be chosen. The system will scan both Equip and Use trinkets in the slot(s), and use either type, if available.
```
# Use Ascendance, if there are no trinket cooldowns ready in the next 10 seconds.
actions +=/ascendance,if=!trinket.has_cooldown|trinket.cooldown.remains>10
```

### Character properties
Character properties require no specific syntax. The available properties are:

* _level_ is the player level.
```
# Shadow fiend is only acquired on lv66 so if we want to test low-level toons...
actions+=/shadowfiend,if=level>=66
```
* _in\_combat_ is zero when not in combat, 1 otherwise.
```
# Set stance before we enter combat
actions=/stance,choose=berserker,if=!in_combat
```
* _name_ and _self_ both return a unique integer (called the "actor\_index") for the player. By default, if the sim encounters an unknown operand, it will attempt to match it to the names of the actors and return the actor\_index if it finds a match. Thus, you can use _name_ and _self_ to perform tests like follows:
```
# Use Reckoning if the boss is targeting another player (see Simulationcraft For Tanks)
actions+=/reckoning,if=target.current_target!=self
# Cast Flash of Light as long as the target's name isn't Bob (see Target Properties section)
actions+=/flash_of_light,if=target.name!=Bob
```
* _ptr_ is zero when using the mechanics from the live server, 1 when using the modifications on ptr.
```
# Starfall is going to be nerfed in the next patch? Then we won't use it anymore.
actions+=/starfall,if=ptr=0
```
* _race_._`<`racename`>`_ evaluates true if `<`racename`>` is equal to the player's race.
```
# Use Berserking only if race is Troll.
actions+=/berserking,if=race.troll
```
* _multiplier_ is the player's damages/healing multiplier. A buff that would increase your damages by 20% would give you a 1.2 multiplier. All damages multipliers are multiplicative (5% and 20% give 1.2\*1.05).
```
# Consumes a potion as soon as we have enough stacked buffs to reach a minimum 30% multiplier.
actions+=/golemblood_potion,if=multiplier>1.3
```
* _spell\_haste_ and _attack\_haste_ are the player's attack and spell factors.  For example, 50% haste on your character sheet corresponds to a _spell\_haste_ or _attack\_haste_ value of 1/1.5=0.667.
```
# Only cast some_slow_spell if its cast time will be reduced to 70% of its base time.
actions+=/some_slow_spell,if=spell_haste<0.7
```
* _rage_, _mana_, _energy_, _focus_, _runic\_power_, _health_ and _soul\_shards_ are the corresponding resources.
```
# Use heroic strike if we have a large enough rage pool
actions+=/heroic_strike,if=rage>60
```
* _`<resource>`.max_ is the current resource maximum amount (should always be 100 for rage and energy).
* _`<resource>`.pct_ is the current resource percentage, between 0 and 100.
* _`<resource>`.deficit_ is the number of lacking resource points for a full resource bar, between 0 and _`<resource>`.max_.
* _`<resource>`.max\_nonproc_ is the resource value a player has before factoring in procs. Basically, it's the maximum resource value a player has out of combat.
* _`<resource>`.pct\_nonproc_ is the resource percentage a player currently has, without factoring in procs. Can go above 100.
```
# Use some_expensive_spell if we have enough mana.
# All three actions are equivalent.
actions+=/some_expensive_spell,if=mana>mana.max*0.5
actions+=/some_expensive_spell,if=mana.deficit<mana.max*0.5
actions+=/some_expensive_spell,if=mana.pct>50
```
* _energy.regen_ and _focus.regen_ are the amount of regenerated points per second for the corresponding resources.
* _energy.time\_to\_max_ and _focus.time\_to\_max_ are the time, in seconds, you would need to fully regenerate the corresponding resources assuming you would not spend anymore. It only takes into account the natural regeneration, not possible procs and such.
```
# Those two statements are equivalent.
actions+=/berserk,if=time_to_max_energy>=2.0
actions+=/berserk,if=(max_energy-energy)/energy_regen>=2.0
```
* _`<resource>`.net\_regen_ is the net resource regen a player has had so far in combat. Basically, it's the resources gained minus resources lost, divided by the current time.
* _stat.`<x>`_ is the value of a certain stat.  _`<x>`_ can be any of: strength, agility, stamina, intellect, spirit, health, maximum\_health, mana, maximum\_mana, rage, maximum\_rage, energy, maximum\_energy, focus, maximum\_focus, runic, maximum\_runic, spell\_power, mp5, attack\_power, expertise\_rating, inverse\_expertise\_rating, hit\_rating, inverse\_hit\_rating, crit\_rating, haste\_rating, weapon\_dps, weapon\_speed, weapon\_offhand\_dps, weapon\_offhand\_speed, armor, bonus\_armor, resilience\_rating, dodge\_rating, parry\_rating, block\_rating, mastery\_rating.
* _incoming\_damage\_X_ will return the damage done to the player in the past X seconds.  For example, a Death Knight may want to put a conditional on Death Strike usage such as:
```
# If damage taken in last 5 seconds exceeds 30% of max health, Death Strike
actions+=/death_strike,if=incoming_damage_5s>health.max*0.3
```
Note: The time can be specified in seconds or milliseconds, but must be an integer.  For fractional parts of a second, milliseconds must be used; for example, `incoming_damage_1500ms` will return the damage taken in the last 1.5 seconds.

### Class-specific

See the relevant page for each class.

### Cooldowns
The character's cooldowns can be used through the following syntax: `cooldown.<spell_name>.<cooldown_property>`. As usual, for the spell name, use underscores instead of white spaces and ignore non-alphanumeric characters. The available properties are:

* _duration_ is the initial duration, in seconds (not the remaining duration).
* _remains_ is the remaining duration, in seconds, before the cooldown is done.
* _up_ indicated if the cooldown is  done (i.e., the associated ability is ready)

```
# Use "aimed shot" if at least 5 seconds remain on "chimera shot".
actions+=/aimed_shot,if=cooldown.chimera_shot.remains>5
```

### Dots
The dots and hots applied by the character on the target can be used through the following syntax: `dot.<dot_name>.<dot_property>`. As usual, for the dot name, use underscores instead of white spaces and ignore non-alphanumeric characters.
```
# If frost fever is going to expire on the target (less than 2 seconds remaining), refresh it with howling blast.
actions+=/howling_blast,if=dot.frost_fever.remains<=2
```

The available properties are:

* _duration_ is the initial duration, in seconds (not the remaining duration) of the current dot. Note that this returns 0 if the dot is not currently ticking.
* _modifier_ is the damages or healing modifier. If your character has a 20% general modifier and a 30% modifier for this dot, it will have a total of 1.2\*1.3=1.56.
* _remains_ is the remaining duration, in seconds, before the dot/hot expires.
* _ticking_ is 1 if the dot is still active on the target, 0 if it faded out.
* _ticks\_added_ is the number of additional ticks that have been added to the dot while it is active. This does not include ticks added from haste at the dot's application.
* _tick\_dmg_ is the non-critical damage of the last tick.
* _ticks\_remain_ are the number of ticks remaining for the current active dot.
* _spell\_power_ last spell\_power snapshot used for dot damage calculation.
* _attack\_power_ last attack\_power snapshot used for dot damage calculation.
* _multiplier_ last multiplier, excluding dynamic target multipliers.
* _haste\_pct_ last haste multiplier.
* _current\_ticks_ the total number of ticks for the current application of the dot.
* _ticks_ the number of ticks that have already happened for the current application of the dot.
* _crit\_pct_ last critical strike percentage snapshot used for dot damage calculation.
* _crit\_dmg_ last critical damage strike bonus percentage used for dot damage calculation.
* (**Since Simulationcraft 6.0.0**) _tick\_time\_remains_ remaining time on the ongoing tick in seconds. 0 if the dot is not ticking.

(**Since Simulationcraft 6.0.0**) You can also check the number of active dots of any type using the `active_dot` expression.
```
# Fire nova if enough Flame Shocks are active
actions+=/fire_nova,if=active_dot.flame_shock>=5
```

### General
General properties require no specific syntax. The available properties are:

* _time_ is the elapsed time, in seconds, since the beginning of the fight
```
# Use bloodlust after at least 20s minimum
actions+=/bloodlust,if=time>20
```
* _time\_to\_bloodlust_ is the time until the next scheduled bloodlust cast, as defined by the `bloodlust_time` and `bloodlust_percent` parameters.
```
# Use avenging wrath as long as bloodlust will not be cast within the next 110 seconds
actions+=/avenging_wrath,if=time_to_bloodlust>110
```
* _active\_enemies_ is the number of active enemy targets.
```
# Use Consecration if there are at least 3 enemies
actions+=/consecration,if=active_enemies>=3
```

### Pet
You can always refer to your pet's properties through the `pet.<pet_name>.<pet_property>` syntax. The pet's name is formatted using underscores instead of white spaces and ignoring non-alphanumeric characters.
```
# Use ice lance if the water elemental's "freeze" cooldown will expired before the end of the gcd.
actions+=/ice_lance,if=pet.water_elemental.cooldown.freeze.remains<gcd
```

Also, note that pets have one additional properties: _active_ is zero when not active, 1 otherwise.
```
# Use "some_spell" if "some_pet" is active.
actions+=/some_spell,if=pet.some_pet.active
```

If the pet is temporary, you can evaluate to its remaining time in Azeroth with the `remains` expression. If the pet is not active, or it is a permanent pet, the expression evaluates to zero.
```
# Cast Frostbolt if Prismatic Crystal is alive during the casting
actions+=/frostbolt,if=pet.prismatic_crystal.remains>cast_time
```

Finally, within a pet's actions list, you can always use its owner's properties through the `owner.<owner_property>` syntax.
```
# Use some_spell if the owner's level is higher than 60.
actions+=/some_spell,if=owner.level>60
```

### Raid Events
You can check for upcoming [Raid Events](RaidEvents) with the syntax `raid_event.event_type.filter`. This will return a value depending on the particular `event_type` and `filter` you choose.

The `event_type` should be the name of the raid event as described in the [Raid Events](RaidEvents#Classic_syntax) documentation. The `filter` is the property of the raid event that you're interested in.
```
# This will cast ice_floes if there's a movement raid event happening within the next second
actions+=/ice_floes,if=raid_event.movement.in<1
# This will only use ice_floes if the duration of that event is greater than 5 seconds
actions+=/ice_floes,if=raid_event.movement.in<1&raid_event.movement.duration>5
```
The list of event types and filters are given below. Event types are described in more detail on the [Raid Events](RaidEvents) documentation page.

**Event Types**

* adds
* casting
* damage\_taken
* damage
* distraction
* flying
* heal
* interrupt
* invulnerable
* movement
* position\_switch
* stun
* vulnerable

**Filters**

* _in_ - returns the time until the next event of the appropriate event type.
* _amount_ - returns the amount of the next appropriate event type. For `damage` and `heal` event types this will return the amount of damage or healing done by the event, and for the `damage_taken` event type it will return the number of stacks of the `damage_taken` debuff being applied to the player. For all other event types this will evaluate to zero.
* _duration_ - returns the duration of the next event of the appropriate event type (zero for event types that have no duration).
* _cooldown_ - returns the cooldown of the next event of the appropriate event type. Note that this is the total cooldown of the ability, not the remaining cooldown.
* _exists_ - returns 1 if an event type of that kind exists in the simulation, 0 otherwise.
* _distance_ or _max\_distance_ - returns the maximum distance of the next event of the appropriate event type.
* _min\_distance_ - returns the minimum distance of the next event of the appropriate event type.
* _to\_pct_ - returns the target health percentage of a heal event, if specified, 0 otherwise.

### Role
You can check the role of the actor using the syntax `role.role_type`. For example,
```
# This will cast Seal of Truth if the players role is "attack"
actions+=/seal_of_truth,if=role.attack
```

The major role types are:

* _attack_ (melee dps and hunters)
* _heal_
* _spell_ (caster dps)
* _tank_
There are some deprecated roles that will also parse (_dps_, _hybrid_), but as they're deprecated they (hopefully) won't show up very often.

### Set bonuses
You can check whether the character currently has a set bonus with the following syntax: `set_bonus.tier<number>_[2pc/4pc]_[caster/melee/tank]`. It will return 1 if the set bonus is active, 0 otherwise. **(Since Simulationcraft 6.0.2)** From Tier 17 onwards, roles should not be specified, only the tier number and the bonus type.
```
# Only use some_spell if the character currently has the T11 2pc caster bonus
actions+=/some_spell,if=set_bonus.tier11_2pc_caster
```

For Tier 17 and beyond:
```
# Only use some_spell if the character currently has the T17 4pc bonus
actions+=/some_spell,if=set_bonus.tier17_4pc
```

See also [equipment - set bonuses](Equipment#Set_Bonuses).

### Spell flights
You can check whether a casted spell is still flying towards its target (a fireball for example) with the following syntax: `action.<spell_name>.in_flight`. It will return 1 if the spell if flying, 0 otherwise.

### Swings
The remaining time, in seconds, on weapon swings can be checked through the following syntax: `swing.<weapon>.remains`. The weapon can be one of the following values: "mh", "oh", "mainhand", "offhand", "main\_hand", "off\_hand".
```
# Arms warriors in burning crusade (at the time slam used to reset the swing timer) could use this to only fire slam if at least 3s were remaining before the next swing:
actions+=/slam,if=swing.mh.remains>3
```

### Target's properties
You can check the target's properties with the following syntax: `target.<property>`
```
# Use cleave if the target has at least 1 add
actions+=/cleave,if=target.adds>0
```

The available properties are:

* _level_ is the target's level.
* _health\_pct_ is the target's health percent, between 0 and 100.
* _adds_ is the number of adds the target has.
* _adds\_never_ is 0 if the target will never have adds (no initial adds and no "adds" raid event), 1 otherwise.
* _time\_to\_die_ is the estimated remaining time, in seconds, before the target dies.
* _distance_ is the distance to the target. Handy for checking spells who have damage based on the distance from the target, such as the Priest Level 90 talents (Divine Star, Cascade, and Halo)
* _current\_target_ (**Simulationcraft 6.0.1 release 1 and later**) is the target's target, usually the tank that currently has "aggro." This can be useful for making conditional tank swaps (see [Simulationcraft For Tanks](SimcForTanks)).
* _name_ is the target's unique identifier (actor\_index). The sim attempts to match unknown operands to the names of each actor, and returns the actor\_index if it finds a match, so this can be used to test against the target's name:
```
# Only cast Smite on Fluffy_Pillow
actions+=/smite,if=target.name=Fluffy_Pillow
```

(**Simulationcraft 6.0.2 release 1 and later**) In addition, you can simply use `target` to refer to the current target of the action. This is currently only useful for Mages.

# Related settings

* **reaction\_time** (scope: global; default: 0.5) is the reaction time, in seconds. It is the time your players will need to notice an aura application (for action conditional expressions using the _react_ keyword) or a spell miss (for action conditional expressions using the _miss\_react_ keyword).
```
# No, I am not that slow!
reaction_time=0.25
```
* **skip\_actions** (scope: current character; default: "") is a sequence of action names to ignore, separated by "/". Actions mentioned in this string will never be performed.
```
# With only three adds, it is wise for John the warrior to still use his poor aoe spells? Let's check!
armory=us,illidan,John
skip_actions=cleave/whirlwind
```
* **default\_actions** (scope: global; default: 0), when different from zero, will force the application to ignore your custom action lists and only use the default action lists for all characters and pets.
```
default_actions=1
```