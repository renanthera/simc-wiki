**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Pets
Pets can be declared and edited as any character with the **pet** setting (see [Characters#Pets](Characters#Pets)). A couple of notes:
  * Supported pets are not listed here, there are many of them though. Their names follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting). In doubt, you can check the `sc_util.cpp` source file and search for `util::pet_type_string` to get the list of pets.

  * The **summon\_pet** setting (scope: character; default: "turtle") is used to specify the pet this character should use.
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
The **position** setting (scope: character; default: "back") can be used to specify whether the character should start in front of the target, or at its back. Acceptable values are "front", "ranged_front", "back", and "ranged_back".
```
 position=front
```

## Focus regen during casting
(New for 6.0) All hunter actions have an additional property, cast\_regen. The property returns the amount of focus regenerated during the execution of the action (casting, channel, or GCD). This enables easier conditionals to protect against focus capping. For example, in MM where Aimed Shot can be used to consume focus, an ability might be used unless it would focus cap after casting the ability and aimed\_shot.
```
 actions+=/steady_shot,if=cast_regen+action.aimed_shot.cast_regen<focus.deficit
```

## Estimating "real" cooldown durations
Several hunter spells and abilities have mechanics that can reduce their base cooldown durations significantly by the time they are ready again. Two custom expressions exist to give values closer to what the final cooldown durations are after accounting for reductions: "duration_guess" and "remains_guess", each replacing the generic cooldown expressions "duration" and "remains" respectively.
```
 actions+=/trueshot,if=cooldown.trueshot.duration_guess+buff.trueshot.duration>target.time_to_die
 actions+=/bestial_wrath,if=cooldown.aspect_of_the_wild.remains_guess>5
```

# Reports
All entries for hunters are fairly obvious and therefore not documented.