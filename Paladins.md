**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Textual configuration interface
_This section is a part of the [TCI](TextualConfigurationInterface) reference._

Regular spells are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting).

## Buffs
> Regular buffs for this class are not mentioned here, you just have to follow the standard [names formatting rules](TextualConfigurationInterface#Names_formatting.md). Also, don't forget that set bonuses are added as buffs to a character. Buffs can be used in conditional expressions for actions, see [ActionLists#Buffs\_and\_debuffs](ActionLists#Buffs_and_debuffs).

> ### Sacred Shield
> Sacred Shield is coded as a Heal over Time spell that generates an absorb bubble every time it ticks. Thus, you can check its status using the `dot.sacred_shield.<property>` conditional:
```
  actions+=/sacred_shield,if=dot.sacred_shield.remains<3
```
> See the [Dots](ActionLists#Dots.md) section of the [Action Lists](ActionLists) page for the full list of DoT properties you can query.
> For another example, here's how you would tell the sim you want to keep Sacred Shield active on another player:
```
  actions+=/sacred_shield,target=Player_Name,if=target.dot.sacred_shield.remains<3
```

> For convenience, there's also a "dummy" buff for Sacred Shield to allow you to query whether it is up or down. So the APL entry below will also work:
```
  actions+=/sacred_shield,if=buff.sacred_shield.down
```
> You can use the buff properties `up`, `down`, `react`, and `remains` with this buff, the rest are irrelevant. Note that you will not be able to /cancelaura this (or rather, you _can_, but it will just cancel the dummy buff and won't cancel the actual effect of Sacred Shield).

> ### Eternal Flame
> Likewise, Eternal Flame is a HoT, and should be treated as such in conditionals:
```
  actions+=/eternal_flame,if=dot.eternal_flame.remains<3
```
> There is also a "dummy" buff associated with eternal flame. The difference is that this buff is linked to the HoT so that you can cancel both of them on the action priority list.
```
  actions+=/cancel_buff,name=eternal_flame,if=(conditions)
```

## Conditionals
There are some conditionals that are only available to paladins.
> ### Seals
> `seal.name_of_seal` will return true if the seal requested is active. For example, in
```
  actions+=/seal_of_truth,if=seal.insight
```
> `seal.insight` will be true if Seal of Insight is the currently-active seal. This particular line will cast Seal of Truth if you have Seal of Insight active.

> ### Time Until Next HPG
> `time_to_hpg` will return the time until the next holy power generator is available, in seconds. It will also enforce a minimum time equal to the current GCD (i.e. if there's a holy power generator that is off cooldown, but the GCD isn't up for another 350 ms, this will evaluate to 0.350).
```
  #cast SotR if we're at 5 holy power and a holy power generator is available next GCD
  actions+=/shield_of_the_righteous,if=holy_power>=5&time_to_hpg<=gcd.max
```
> Note that this does not do any fancy calculus to figure out if the next GCD actually _will_ be a HPG. It _only_ returns the time until the next HPG is available. If your action list prioritizes other spells over HPGs, then the time until the next HPG is actually cast could be longer than `time_to_hpg`. It should never be shorter, however.

# Reports
> We only document here non-obvious entries.

## Procs
  * parry\_haste: the number of times your swings have been hasted after you parried an attack.