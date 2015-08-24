**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Pets
> Pets can be declared and edited as any character with the **pet** setting (see [Characters#Pets](Characters#Pets)). A couple of notes:
  * Supported pets are not listed here, there are many of them though. Their names follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting). In doubt, you can check the `sc_hunter.cpp` source file and search for `hunter_t::create_pet` to get the list of pets.

  * You do not have to specify talents for pets: you can but, if you don't, they will be automatically set with the relevant default template.

  * The **summon\_pet** setting (scope: character; default: "cat" or "wind\_serpent" for survival hunters) is used to specify the pet this character should use.
```
 # Here are some examples
 summon_pet=wind_serpent
 summon_pet=spirit_beast
 summon_pet=crocolisk
```
  * Finally, you can use the _summon\_pet_ action to summon the pet you previously specified.
```
 # Summon your pet.
 actions+=/summon_pet
```

## Placing a hunter in front of his target
> The **position** setting (scope: character; default: "back") can be used to specify whether the character should in front of the target, or in its back. Acceptable values are "front" and "back"
```
 position=front
```

## Focus fire and pet's frenzy
> The _focus\_fire_ action has a built-in condition, _min\_frenzy_ (default: 1). When provided, it will make the action usable only when your pet has at least the indicated number of frenzy stacks. Make sure not to specify a number larger than the max frenzy stacks (5). This replaces and deprecates the use of the _focus\_fire_ condition.
```
 actions+=/focus_fire,min_frenzy=5
```

## Black Arrow Lock and Load procs
The new special value "lnl\_procs" returns the number of lock and load procs from the black arrow on the current target (or zero if there is not a ticking black arrow).  Since one LnL proc is guarantee per BA, this allows waiting on recasting BA until we've gotten that proc. the example below prioritizes adding black arrow to a target that doesn't have it. If there are none, it recasts on a target that already has procced lock and load.
```
 actions+=/black_arrow,cycle_targets=1,if=!ticking
 actions+=/black_arrow,cycle_targets=1,if=lnl_procs
```

## Focus regen during casting
> (New for 6.0) All hunter action have an additional property, cast\_regen. the property returns the amount of focus regenerated during the execution of the action (casting, channel, or GCD). This enables easier conditionals to protect against focus capping. For example, in MM where only aimed shot can be used to consume focus, an ability might be used unless it would focus cap after casting the ability and aimed\_shot.
```
 actions+=/kill_shot,if=focus_regen+action.aimed_shot.focus_regen<focus.deficit
```

## Traps
> Traps have been recently introduced with just the explosive trap so far. Traps are triggered as soon as they are spawned.
```
 # Will spawn an explosive trap and have the target triggers it.
 actions+=/explosive_trap
```

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

  * killing\_streak\_crits (player): the number of stacks represents the number of consecutive crits with the "kill command" ability.
  * master\_marksman\_fire (player): it is the buff named "ready, set, aim..." in game. It is the buff that occurs once you reach five stacks of master\_marksman.
  * pre\_improved\_steady\_shot (player): the number of stacks represents the number of consecutive steady shots, it is used to trigger the improved steady shot buff.
  * rabid\_power\_stack (pet): the number of stacks gained through the rabid buff (rabid itself has no stack).

# Deprecated
## focus\_fire,five\_stacks=1
The "five\_stacks=1" setting is a special case of the new, more general min\_frenzy, and is equivalent to "min\_frenzy=5"

# Reports
All entries for hunters are fairly obvious and therefore not documented.