# Conditional expressions
Conditional expressions allow complex composition of conditions, and are usually added to action priority list through the "if" keyword, using the following syntax:
```
# Uses faerie fire if:
# * There are less than three stacks
# * And neither "expose armor" nor "sunder armor" are on the target
actions+=/faerie_fire,if=debuff.faerie_fire.stack<3&!(debuff.sunder_armor.up|debuff.expose_armor.up)
```

The same syntax is used for the _interrupt\_if_ action modifier and the the _sec_ modifier for _wait\_fixed_ actions.

Player Expressions are also used for raid event player\_if filter.

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
* Binary logical xor (**`^`**)
* Binary logical or (**`|`**)

## Operands

### Actions
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
* _multiplier_ is the player's highest damages/healing multiplier for the schools used by the action. A buff that would increase your damages by 20% would give you a 1.2 multiplier. All damages multipliers are multiplicative (5% and 20% give 1.2\*1.05).
```
# Consumes a potion as soon as we have enough stacked buffs to reach a minimum 30% multiplier.
actions+=/golemblood_potion,if=multiplier>1.3
```

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

* You can also express trinket cooldowns through the expression system. Generic syntax is `trinket.(has_|)cooldown.<cooldown_expr>`, where `<cooldown_expr>` refers to any cooldown expression we support. `has_cooldown` requires no cooldown expression. Positional trinket parameters are also supported, see above for example. If the actor has no trinkets with cooldown, both expressions will always return 0. If both trinket slots have a cooldown, the larger cooldown expression return value will be chosen. The system will scan both Equip and Use trinkets in the slot(s), and use either type, if available.
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
* _name_ and _self_ both return a unique integer (called the "actor\_index") for the player. By default, if the sim encounters an unknown operand, it will attempt to match it to the names of the actors and return the actor\_index if it finds a match. Thus, you can use _name_ and _self_ to perform tests like follows:
```
# Use Reckoning if the boss is targeting another player (see Simulationcraft For Tanks)
actions+=/reckoning,if=target.current_target!=self
# Cast Flash of Light as long as the target's name isn't Bob (see Target Properties section)
actions+=/flash_of_light,if=target.name!=Bob
```
* _in\_combat_ is zero when not in combat, 1 otherwise.
```
# Set stance before we enter combat
actions=/stance,choose=berserker,if=!in_combat
```
* _ptr_ is zero when using the mechanics from the live server, 1 when using the modifications on ptr.
```
# Starfall is going to be nerfed in the next patch? Then we won't use it anymore.
actions+=/starfall,if=ptr=0
```
* _bugs_ is zero when bugs are disabled, else it returns 1. Useful when a bug is implemented but will likely be fixed soon. (It's enabled by using the token option "bugs=1" or "bugs=0")
```
# In 7.1.5, casting Shadow Dance before going in combat let you extends the stealth buff, so it's worth to use with Subterfuge talent. Will likely be fixed in 7.2!
actions.precombat+=/shadow_dance,if=talent.subterfuge.enabled&bugs
```
* _is\_add_ is true if the player is a add.
* _is\_enemy_ is true if the player is a enemy.
* _spell\_haste_ and _attack\_haste_ are the player's attack and spell factors.  For example, 50% haste on your character sheet corresponds to a _spell\_haste_ or _attack\_haste_ value of 1/1.5=0.667.
```
# Only cast some_slow_spell if its cast time will be reduced to 70% of its base time.
actions+=/some_slow_spell,if=spell_haste<0.7
```
* _attack\_speed_ is the player's attack speed.
* _mastery\_value_ is the player's mastery value.
* _position\_front_ is true if the player is in front of its target.
* _position\_back_ is true if the player is in the back of its target.
* _time\_to\_bloodlust_ is the time until the next scheduled bloodlust cast, as defined by the `bloodlust_time` and `bloodlust_percent` parameters.
```
# Use avenging wrath as long as bloodlust will not be cast within the next 110 seconds
actions+=/avenging_wrath,if=time_to_bloodlust>110
```
* _raw\_haste\_pct_ is the players raw haste percentage.
  
  Note: raw means: Base + Passive + Gear (overridden or items) + Player Enchants + Global Enchants

* _incoming\_damage\_X_ will return the damage done to the player in the past X seconds.  For example, a Death Knight may want to put a conditional on Death Strike usage such as:
```
# If damage taken in last 5 seconds exceeds 30% of max health, Death Strike
actions+=/death_strike,if=incoming_damage_5s>health.max*0.3
```
  Note: The time can be specified in seconds or milliseconds, but must be an integer.  For fractional parts of a second, 
  milliseconds must be used; for example, `incoming_damage_1500ms` will return the damage taken in the last 1.5 seconds.

* _time\_to\_die_ is the estimated remaining time, in seconds, before the player dies.
* _time\_to\_pct`<health_pct>`_ is the estimated remaining time, in seconds, before the player reaches `<health_pct>` of health.

#### Resource expressions
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
* _`<resource>`.net\_regen_ is the net resource regen a player has had so far in combat. Basically, it's the resources gained minus resources lost, divided by the current time.
* _stat.`<x>`_ is the value of a certain stat.  _`<x>`_ can be any of: strength, agility, stamina, intellect, spirit, health, maximum\_health, mana, maximum\_mana, rage, maximum\_rage, energy, maximum\_energy, focus, maximum\_focus, runic, maximum\_runic, spell\_power, mp5, attack\_power, expertise\_rating, inverse\_expertise\_rating, hit\_rating, inverse\_hit\_rating, crit\_rating, haste\_rating, weapon\_dps, weapon\_speed, weapon\_offhand\_dps, weapon\_offhand\_speed, armor, bonus\_armor, resilience\_rating, dodge\_rating, parry\_rating, block\_rating, mastery\_rating.

#### Split expressions

##### 2 Parts
* _variable_._`<`variablename`>`_ evaluates to the current value of the player's variable.

* _equipped_._`<`item_id`>`_ or _equipped_._`<`item_name`>`_ evaluates to true if the player has the specified item equipped.

* _main_hand_._1h_, _main_hand_._2h_, _off_hand_._1h_, _off_hand_._2h_ evaluates to true if the player has the specified weapon type equipped.

* _race_._`<`racename`>`_ evaluates true if `<`racename`>` is equal to the player's race.
```
# Use Berserking only if race is Troll.
actions+=/berserking,if=race.troll
```

* _spec_._`<`spec_name`>`_ evaluates true if `<`spec_name`>` is equal to the player's specialization.
```
# Use Haunt only if spec is affliction
actions+=/haunt,if=spec.affliction
```

* _role_._`<`role_name`>`_ evaluates true if `<`role_name`>` is equal to the player's role.
   The major role types are:

   * _attack_ (melee dps and hunters)
   * _heal_
   * _spell_ (caster dps)
   * _tank_

   There are some deprecated roles that will also parse (_dps_, _hybrid_), but as they're deprecated they (hopefully) 
   won't show up very often.
```
   # This will cast Seal of Truth if the players role is "attack"
   actions+=/seal_of_truth,if=role.attack
```

* _stat_._`<`stat_name`>`_ returns the amount of stat you have.
```
# Use smash only if players strength is above 1000
actions+=/smash,if=stat.strenght>1000
```

* _using\_apl_._`<`apl\_name`>`_ returns true if the specified apl is explicitly used by the player.

* _active\_dot_._`<`dot\_name`>`_ returns the number of dots with the given name currently active on all targets.
```
# Fire nova if enough Flame Shocks are active
actions+=/fire_nova,if=active_dot.flame_shock>=5
```

* _movement_._remains_ returns the amount of remaining movement time of the player.
* _movement_._distance_ returns the amount of remaining movement distance of the player.
* _movement_._speed_ returns the current movement speed.

##### 3 Parts

* _spell_._`<`spell\_name`>`_._exists_ returns true if a spell with the given name exists for the player.
* _talent_._`<`talent\_name`>`_._enabled_ returns true if the talent with the given name is active/selected for the player.
* _artifact_._`<`artifact\_spell_name`>`_._enabled_ returns true if the artifact-spell with the given name is active for the player.
* _artifact_._`<`artifact\_spell_name`>`_._rank_ returns the active rank of the artifact-spell with the given name for the player.

### Set bonuses
You can check whether the character currently has a set bonus with the following syntax: `set_bonus.tier<number>_[1pc/2pc/.../8pc]`. It will return 1 if the set bonus is active, 0 otherwise. 
```
# Only use some_spell if the character currently has the T21 4pc bonus
actions+=/some_spell,if=set_bonus.tier21_4pc
```

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
* _tick\_time\_remains_ remaining time on the ongoing tick in seconds. 0 if the dot is not ticking.

### General
General properties require no specific syntax. The available properties are:

* _time_ is the elapsed time, in seconds, since the beginning of the fight
```
# Use bloodlust after at least 20s minimum
actions+=/bloodlust,if=time>20
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

* With WoW 8.0 (BFA) you can also filter by custom [Raid Events](RaidEvents) names. The new syntax is: `raid_event.type_or_name.filter`. You can name a raid event through its ,name=<myCustomName> option.

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

With WoW 8.0 (BFA):
* _up_ - returns true if there is at least 1 raid event currently up. Prefer up over _remains_ if it satisfies your needs.
* _remains_ - returns the remaining duration of the raid event currently up which has the longest remaining duration. Does not take into account not yet up raid events.


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