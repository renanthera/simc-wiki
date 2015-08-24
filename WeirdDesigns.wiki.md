I was asked to note those little weird things while working on the doc, so here it is.



# Misc

  * **travel\_variance** should rather be named **spell\_flight\_stddev**. The stddev suffix is widely used and a de facto standard, and "spell\_flight" is more explicit than "travel".
  * **deterministic\_rng**, when enabled, should use the **seed** value rather than a built-in value (just keep the built-in value when seed is zero).
  * **dps\_plot\_step** should be replaced with a **dps\_plot\_range**. Currently, the user has to mentally multiply dps\_plot\_step by dps\_plot\_points in order to know how much the delta will be. I guess the value of the dps\_plot\_range should be half of the total range (delta if total ranged is `[-delta; +delta]`).
  * **report\_precision** should have its default value set to 1 since it only affects scale\_factors and since our scale factors are not that precise. Maybe rename it to "scale\_factors\_decimals".
  * **output**: it seems like there is no consistent behaviour between what is redirected by this option and what is not. I guess the progression marks (10... 9... 8...) should be left on the standard output while the rest could be on the output log. Some things could also be on both (just progression marks on stdout, everything on the file).
  * **log** should not be a boolean, rather a file path, to be consistent with **combat\_log**, **csv** and such. The log would be directed to this file rather than stdout.
  * **csv** is really weird in its present state. What about **xml** ?
  * **enchant\_strength**, **default\_enchant\_strength** and alike should be renamed. Of course they are fake enchants but their names are not explicit. Besides, default\_enchant\_strength is not the default value for **enchant\_strength**: they sums up together. I recommend "strength\_bonus" and "global\_strength\_bonus".

# Characters importation
## Problems
There is a lot of mess here. Many inconsistent and fluctuating patterns across those commands. Here is a quick reminder of the supported syntaxes so far, which are all different:
  * armory: `<region>,<server>,<player1>[,<player2>,<player3>,...]` Playername can be prefixed with "!" for inactive spec.
  * guild: `<guildname>[,options]`
  * wowhead: `wowhead=<id>` OR `wowhead=<region>,<server>,<playername1>[,<playername2>,...]`

Other problems:
  * The **default\_server** and **default\_region** settings are only supported by **guild** and **player**.
  * **player** is a total mess and should just be removed. It looks like a failure at an unification attempt. Right now it is just redundant and confusing, giving no added value to the application. I didn't detail it here but it works with its own specific syntax (again).
  * Spec choice is always supported but in two different ways, one being non-explicit (the use of an exclamation mark), and only giving choice between "active" and "inactive", not between "primary" and "secondary".

## Suggestions
**player** is a total mess and should just be removed. The supported syntaxes for the other options could be:

  * armory:
    * armory=`<player1>[,<player2>,<player3>,...][,spec=active]` (use default\_server and default\_region)
    * armory=`<region>,<server>,<player1>[,<player2>,<player3>,...][,spec=active][,cache=1]`
    * NB1: for parsing purposes, just check whether the first parameter is one of the two letters codes in order to know which syntax was used. Use the equality sign to differentiate between names and options.
    * NB2: of course, this syntax has one disadvantage: you cannot import John, !Bill and Roger, you have to use two lines (one for active spec, one for inactive). But it is still better: explicit, allow the use of default\_server and default\_region, and has a cache setting.
  * guild:
    * guild=`<guild>[,options]`
    * guild=`<region>,<server>,<guild>[,options]`
    * NB: same syntax as armory, minus the spec choice since it's not relevant, and more options here.
  * wowhead:
    * wowhead=`<player1>[,<player2>,<player3>,...][,cache=1]` (players can be ID or names)
    * wowhead=`<region>,<server>,<player1>[,<player2>,<player3>,...][,cache=1]` (players must be names)
    * NB: same syntax as armory, minus the spec choice since it's not relevant (could be added later). PlayerN could be names or ID, just check whether they are integers or not.

Amory, guild and wowhead could use the very same parser, just with different provided option sets and returned options table, all of that with very few posterior checks to perform.

# Combat duration

Combat duration has been changed and is now cleaner. However, the **max\_time** setting should probably be renamed, it is no longer a maximum time since the average combat fight will converge towards this value. It was probably named in the past at a time when convergence was achieved on every fight rather than on the average fight duration over all fights.

  * **max\_time** should renamed into **combat\_length**. Or not, it depends on your choice for convergence.
  * **vary\_combat\_length** should be renamed into **combat\_length\_variation** (vary\_combat\_length seems to be a boolean's name)
  * Maybe output a warning if both **target\_health** and **max\_time** are non-zero.

# Deprecated

Those characters options are deprecated:
  * **flask**, **elixir**, **food**

Other options :
  * The "movement" raid event has an unused options: "to".

Raid events :
  * amount\_stddev for the "damages" raid event.