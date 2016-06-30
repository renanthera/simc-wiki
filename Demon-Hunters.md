**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

## Expressions

* **soul_fragments**: The number of active, consumable soul fragments.
* **greater_soul_fragments**: The number of active, consumable greater soul fragments.
* **lesser_soul_fragments**: The number of active, consumable lesser soul fragments.
* **blade_dance_worth_using** and **death_sweep_worth_using**: Compares the effectiveness of Blade Dance / Death Sweep and compares it to the corresponding fury spender (Chaos Strike or Annihilation) and evaluates to true if it is worth using over the fury spender. The logic for this is implemented as follows:  

> For both sides of the equation, count the number of Demon's Bites, x, needed to generate the fury for the spender. Add the damage of the spender to the damage of x Demon's Bites, and divide the sum by the sum of their GCDs ( 1 + x ). The full formula is then:
```
demons_bite_per_dance = blade_dance_cost / demons_bite_fury
demons_bite_per_chaos_strike = ( chaos_strike_cost - 20 * crit_chance ) / demons_bite_fury
( blade_dance_damage + demons_bite_per_dance * demons_bite_damage ) / ( 1 + demons_bite_per_dance ) > ( chaos_strike_damage + demons_bite_per_chaos_strike * demons_bite_damage ) / ( 1 + demons_bite_per_chaos_strike )
```

## Special Actions

* **pick_up_fragment**: Move to and consume a nearby Soul Fragment. Any if expression (if provided) will be evaluated at both the start of the movement and when reaching the fragment, which may result in the action being executed without a fragment being consumed. See action options section for more details on how to use this action.

## Action Options

* **fel_rush,jump_cancel=1**: The Fel Rush is cast without causing the Demon Hunter to move.
* **pick_up_fragment,type=x**: The type of soul fragment to be picked up. Valid options: *greater*, *lesser*, *all* or *any*. Default: *all*
* **pick_up_fragment,mode=x**: The mode that determines which fragments should be prioritized. Valid options: *closest* or *nearest* or *close* or *near*, *newest* or *new*, *oldest* or *old*. Default: *oldest*

# Reporting

## Procs

* **delayed_swing__out_of_range**: An auto-attack was delayed due to the player being outside of melee range of the target.
* **delayed_swing__channeling**: An auto-attack was delayed due to the player channeling a spell.
* **soul_fragment**: A greater soul fragment was consumed.
* **soul_fragment_lesser**: A lesser soul fragment was consumed.
* **demon_blades_wasted**: A Demon Blades proc was wasted by a proc occurring while the Demon Hunter already had the maximum number of pooled charges of Demon Blades. 
* **demons_bite_in_meta**: Demon's Bite was used during Metamorphosis. This is intended to be used as a optimization metric for APL fury pooling logic.
* **felblade_reset**: Felblade's cooldown was reset. 
* **fel_barrage**: Fel Barrage gained a charge from a damaging melee ability.
* **fueled_by_pain**: Metamorphosis was invoked by the Fueled by Pain artifact trait.
* **soul_fragment_expire**: A soul fragment expired without being consumed. 
* **soul_fragment_overflow**: A soul fragment was spawned while the player was already at the maximum number of soul fragments of that type.