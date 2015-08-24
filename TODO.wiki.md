

# Introduction

This page details various features that are either missing from the sim, that would be nice to have, or outright required for certain things. They are in no order of importance.

# TODO
## Generic features
  * Better Area of Effect targeting mechanisms
    * Enemy clustering (aoe may affect enemies in the cluster)
  * Combat phasing
    * Phase specific statistics
  * Better "player\_skill" system
  * Uniform stat types with World of Warcraft client (ranged haste/ap/crit/hit I'm looking at you)

## Raid events
  * Concept of roles for raid effects (e.g., affects tank/healer/ranged dps/melee dps and so on)
  * Improved add support.

## Classes
  * In general, AoE support for all classes
  * Death Knight
    * Blood DPS support

# Nice to Have
  * GUI Paperdoll
  * Multi-Computer SimC ( see [Issue 887](https://code.google.com/p/SimulationCraft/issues/detail?id=887) )
    * propose adding a DistCC like functionality to SimC that will allow me to use the ~10ish computers in my house to spread the load and SimC faster.  Perhaps use Avahi for the network distro code.
  * World of Warcraft client combat log export
  * Improved HTML Output Sorting ( see [Issue 1035](https://code.google.com/p/SimulationCraft/issues/detail?id=1035) )
    * A nice feature would be to be able to sort by damage percentage on the results. Ideally on the web page resulted.
  * Cuda/OpenCL support ( see [Issue 2120](https://code.google.com/p/SimulationCraft/issues/detail?id=2120) )
    * It seems to me like simcraft is one of that rare type of program that could benefit heavily from using the massive parallel computing abilities of a GPU through CUDA or OpenCL. Cryptography has already seen a logarithmic increase in computational performance because each hash is separate. As far as I understand, each simulation is also separate.
  * Buff Reaction Times: Make reaction times dependent on the observer, not on the buff source. ( see [Issue 2064](https://code.google.com/p/SimulationCraft/issues/detail?id=2064) )
  * Allow scaling of all stats when explicitly specified ( see [Issue 950](https://code.google.com/p/SimulationCraft/issues/detail?id=950) )
    * Expect to be able to calculate Scale Factor for X, even if X isn't calculated by default by calculate\_scale\_factors=1