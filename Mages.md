**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface.md) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md).

## Targeting

(**Since Simulationcraft 6.0.2**) Mages in Warlords of Draenor get a talent called Prismatic Crystal (PC), that necessitates a rethinking of the targeting model in Simulationcraft. As such, to allow Mages to explore different strategies with PC, they have a custom targeting system.

In conventional Simulationcraft, each ability has its own target. Mages, on the other hand have a single shared target between all abilities (the current target of the Mage). Mages can change their current target, and also PC will forcibly swap their current target to itself, to model in game behavior. Note that when PC despawns, as a convenience, the simulator will automatically target the Mage's primary target.

### Choose target

To support proper targeting, a new action has been introduced. The `choose_target` action allows mages to change targets instantaneously.

```
# Change target to default target, if Prismatic Crystal is active
actions+=/choose_target,if=pet.prismatic_crystal.active
```

Specifying the target for the action is done through the `name` option. The name option scans through actors in the sim, and matches the option value with their name. The scanning is prioritized in the order of mage's pets, hostile targets, friendly players. As a shorthand, the `name` option can be omitted for targeting the default target of the Mage, or also the alias `default` used as the name of the default target.

By default, any if= expression passed to the `choose_target` action checks the mage's current target for validity. This behavior can be changed with the `check_selected` option (possible values 0/1), which forces the action to check the If= conditions against the potential selected target.

### Expressions

The `current_target` expression evaluates to the current target of the Mage, under the new targeting system.

```
# Execute Frostbolt, if the current target of the Mage is an enemy named Fluffy_Pillow
actions+=/frostbolt,if=current_target=Fluffy_Pillow
```

In addition, the `default_target` expression evaluates to the primary target of the Mage (by default Fluffy\_Pillow, controllable through the `target` option for the player).
```
# Execute Frostbolt, if the current target of the Mage is the default enemy in the sim
actions+=/frostbolt,if=current_target=default_target
```

### Important notes

  * The `cycle_targets` option works normally with the mage targeting system. If specified for an action, the Mage's current target is ignored for that action, and the (cycled) target of the action is used instead.
  * The `target` option for actions is current unavailable for mages

## Ability Tracking and Custom Flags

> In order to facilitate simpler APL conditions for certain abilities, custom expressions have been implemented.

> Due to the complexity of controlling when to pyro camp vs. build ignite for combustion, the _pyro\_chain_ flag exists. Together with actions _stop\_pyro\_chain_ and _start\_pyro\_chain_ they allow for more simple entering / exiting periods where spell priorities shift significantly. Effectively, this allows us to force the mage to have the option of occupying different states - see Mage Fire APL, circa SoO MoP / WoD era, for examples of how this is taken advantage of.

```
   # start_pyro_chain toggles pyro_chain to 1 (true)
   actions+=/start_pyro_chain

   # Combustion will only be cast if pyro_chain is = 1 (true)
   actions+=/combustion,if=pyro_chain

   # stop_pyro_chain toggles pyro_chain to 0 (false), in this case if combustion is on cooldown
   actions+=/stop_pyro_chain,if=cooldown.combustion.remains>0
```

## Water Elemental

Water elemental in Warlords of Draenor casts "Water Jet" that debuffs the target, and generates Fingers of Frost charges for the mage. You can control the behavior how Water Jet is cast using the _water\_jet_ action. If _water\_jet_ action is omitted from the Action Priority List, the Water Elemental will automatically cast the spell when its cooldown has elapsed.

```
 # Manually cast Water Jet, when the mage has no Fingers of Frost charges
 actions+=/water_jet,if=buff.fingers_of_frost.react=0
```