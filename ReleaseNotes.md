**All patch notes and executable downloads will now be posted at :**http://www.simulationcraft.org/download.html

**The complete list of source code changes can be found here :**
http://code.google.com/p/simulationcraft/source/list


# WoW 5.4.x

## SimC 547-1

  * General
    * **Rename various "target" prefixed options to "enemy" prefix**
    * Increase buff uptime reporting precision
    * Small tweaks to waiting time reporting in text results
    * "cancel\_buff" action now works on all relevant buffs
    * Fix channeled dot-autocasting behavior, when the auto-cast misses. Fixes [Issue 1998](https://code.google.com/p/SimulationCraft/issues/detail?id=1998)
    * Fix override.target\_health option
    * Fix fixed\_time option interaction with enemy health percentage
    * Allow actors with tank role to use normal enemy health based simulation model by default
    * Fix a crash bug with dps\_plot\_iterations option. Fixes [Issue 2003](https://code.google.com/p/SimulationCraft/issues/detail?id=2003).
  * Graphical User Interface
    * Add pause simulation feature to GUI
    * Add error page to inform users better of http related errors inside the GUI
    * Add simulation queue feature
    * Change certain options to be editable (threads, iterations, fight length)
    * Small progressbar improvements on lengthy iterations
    * Added "Close other tabs" and "Close all tabs" items to tab bar context menu
    * Change commandline keyboard shortcuts from ARROWKEY to ALT + ARROWKEY
    * Fix results not following page anchors
    * Fix issues with saving results to a file
    * Change tab shortcut from ALT + NUMBER to Cmd + NUMBER on OS X
  * Druid
    * Precast wild mushrooms through pre-combat actions to allow users more control over how/when they are cast
  * Hunter
    * Improved BM Hunter action list and heroic T16 gear setup
    * Improve default action list stampede handling for MM/SV
    * Fixed quad-upgrading on profiles
  * Paladin
    * Added Symbiosis version of Barkskin
    * Fix Eternal Flame
    * Adjust protection paladin default action list
  * Rogue
    * Disallow poison and main gauche procs from Expose Armor. Fixes [issue 2013](https://code.google.com/p/SimulationCraft/issues/detail?id=2013).
  * Shaman
    * Fix Lava Surge behavior when it procs during a Lava Burst cast
  * Warrior
    * Added Enraged Speed glyph support
    * Updated 2+ target aoe default action list for Fury/Arms
    * Updated Fury TG default action list
    * Fix Flurry of Xuen interaction with various class-specific effects
    * Fix Impeding Victory heal coefficient
    * Fix Storm Bolt offhand attack behavior
    * Fix Whirlwind behavior
    * Fix Meat Cleaver expiration on missed Raging Blows
    * Fix a crash with aoe damage + slam sweeping strikes

## SimC 541-02

  * General
    * Deterministic RNG now works correctly with multiple threads.
    * Added new feature: Recently closed tabs. Whenever any tab is closed, it will be saved in this list. Simply mouse over "Close all tabs" and they will show up there.
    * Simulation failures should now always be written into the log file.

  * Warrior
    * Corrected base attack power, should now match in-game numbers. (Only a 30 AP difference.)
    * Shockwave's cooldown is now reduced by 20 seconds when 3+ targets are hit, and this 20 second reduction is done after the reduction from Galakra's trinket.
    * Heroic leap will now have the correct cooldown with a cooldown reduction trinket and death from above glyph.
    * Small action list tweak for TG Fury, as well as splitting TG and SMF into different action lists.

  * Deathknight
    * Blood plague now suffers from crit suppression.

  * Druid
    * Small fixes for resto, still not fully supported.

## SimC 541-01

  * General
    * Added options to close all open simulation tabs, as well as resetting all options to default
    * Added thread\_priority option:
    * thread\_priority=<normal, above\_normal/high,below\_normal/low, lowest, highest>
    * Improved load balancing for multiple thread simulations
    * Bug fix to prevent simulation from never finishing when fight style TargetDummy is selected

  * Warrior
    * Overhauled action list so that it now supports comments, as well as being able to use 'slot=hands' for various on use items


## SimC 540-05

  * General
    * All specs now have profiles for T16
    * Bug fixes, mostly involving raid events with adds
    * Optimized rotations for most specs
    * Multistrike/Cleave trinkets should reflect real game results

  * Rogue
    * Corrected blade flurry mechanics
    * AoC should not work correctly with more abilities

  * Hunter
    * Thrill of the hunt no longer double dips on ability cost reduction.

  * Monk
    * Many bug fixes and enhancements to brewmaster and windwalker

  * Shaman
    * Elemental may now use shamanistic rage

## SimC 540-03
  * General
    * Slight tweaks to TMI
    * Hotfixes from 9/23/13 are implemented
    * Fix so that duplicate charts are not produced
    * Small fix for max weapon damage being off by 1 in some cases
    * Fixed item database for Ordos items.
  * Druid
    * Added Boomkin profiles, feel free to optimize them
    * Updated Action List for Guardian
    * Implemented Cenarion Ward
    * Guardian T16 set bonuses implemented
  * Shaman
    * Optimization for enhancement cooldown usage
    * Re-did flametongue implementation
  * Warrior
    * Fury BIS Profile no longer uses 4 piece tier

## SimC 540
This section is for the gap in release notes. Not everything is included.
  * General
    * All trinkets have been added
    * Most dps set bonuses/relevant glyphs have been implemented
    * Most specs have updated action lists
    * Legendary cloak proc is working
    * Most profiles have been added, but T16N and a few others are not complete
  * Warrior
    * Opportunity Strikes/Sweeping Strikes can proc off each other, 0.1 second ICD on Opportunity Strikes
    * Added automation for swapping stances to account for raid damage, explained here: https://code.google.com/p/simulationcraft/wiki/Warriors

# WoW 5.3.x
## SimC 530-03
  * General
    * Add support for the ilvl 600 cloaks
## SimC 530-02
  * General:
    * Fix Issue with reforge\_plot.csv and chardev.cookies not saved to Application Data Directory on OSX.
    * Fix multithreading Issue/crash on Windows.
  * Death Knight
    * Implementation of various Blood abilities/mechanics
    * Removed gargoyle spell queue lag
  * Druid
    * Implementation of various Guardian abilities/mechanics
  * Mage
    * Presence of Mind and Arcane Power can be used simultaneously
    * Mirror Images no longer cast Fire Blast
    * Reimplementation of Nether Tempest's damage cleaving
    * Living Bomb explodes on unlimited targets and scales with haste
  * Monk
    * Fix intellect to spell power conversion
    * Update default actionlist
  * Paladin
    * Guardian of Ancient Kings can now critically strike in sim
  * Shaman
    * Fix an issue where Fire & Earth Elemental's shared cooldown was incorrectly affected by Glyph of Fire Elemental Totem
    * Track wasted Lava Surge procs
    * Fix Lava Surge's instant cast buff and proc chance
  * Warlock
    * Update Demonology's AOE actionlist and T15H gear

# WoW 5.2.x
## SimC 520-10
  * General
    * Fix issues with multithreading and MinGW introduced in 520-07/520-08
  * Monk
    * Initial implementation of various Mistweaver abilities
  * Rogue
    * Updated T15H profiles to use Renataki's Soul Charm instead of Talisman of Bloodlust
  * Shaman
    * Lava Lash's Flame Shock spreading can now overwrite lower duration Flame Shocks

## SimC 520-08
  * General
    * Convert all T15H profiles to heroic thunderforged gear
    * Added Unerring Vision of Lei-Shen support for Shadow and Elemental
    * Fixed an issue with reported stack uptime for various trinkets
  * Druid
    * Fixed an issue with autoattacks
    * Fixed crit bonus for Bear Form
    * Force Sunfire and Moonfire to snapshot all stats except player crit when being extended
  * Hunter
    * Implement Beast Cleave
  * Mage
    * Fixed an issue with the sim incorrectly calculating Fire and Frost's crit chance
    * Fixed an issue with Arcane Explosion's generation of Arcane Charges
    * Updated AOE profiles
  * Monk
    * Fixed an issue with Rising Sun Kick incorrectly applying its bonus to autoattacks and Tiger Strikes
  * Rogue
    * Fixed an issue with Assassin's Resolve incorrectly not applying to all damage sources
    * Fixed an issue with Sanguinary Vein incorrectly not applying its bonus to Rupture damage
  * Shaman
    * Tweak Elemental's default actionlist
    * Troll elemental shamans no longer try to sync Berserking with Ascendance if using the T15 4p bonus
  * Warlock
    * Various actionlist priority tweaks
  * Warrior
    * Deep Wounds and the Capacitive Primal Diamond proc now benefit from Single-Minded Fury and Seasoned Soldier
    * Improve Fury's AOE actionlist priority

## SimC 520-07
  * General
    * Enable PTR setting
    * Added new actionlist options for channeled spells
    * Fixed proc values for the Fortitude of the Zandalari trinket
    * Fixed a bug with random suffix stats on items not adding to the actor
    * Fixed an issue with the scale\_to\_itemlevel option
    * Change syntax for various actionlist trinket expressions
    * Fixed an issue with abilities that split their damage between all targets and the AOE damage cap
  * Death Knight
    * Update Unholy's disease gaming to be percent based
    * Fixed an issue with the sim never using Icy Touch for Unholy
    * Fixed Blood Boil's attack power coefficient
    * Implement Roiling Blood
    * Update T15H profile to include heroic thunderforged gear
    * The Gargoyle now uses its true casting speed on the PTR
  * Druid
    * DoTs can now snapshot crit
    * Balance now uses Heart of the Wild instead of Nature's Vigil by default
    * Fixed an issue with feral/guardian weapon swaps
    * Fixed an issue with abilities incorrectly consuming Dream of Cenarius damage charges
    * Fix balance's and feral's T15 4p bonuses
  * Mage
    * Updated fire's default action priority list
  * Monk
    * Initial implementation of some Brewmaster abilities
  * Priest
    * Chakra Chastise gives Smite a chance to reset Holy Word: Chastise's cooldown
  * Shaman
    * Fixed issues with lava lash's flame shock spreading and fire nova's eruptions
    * Searing Totem now uses its true casting speed on the PTR
  * Warlock
    * Various T15 profile adjustments
    * Fixed an issue with Rain of Fire ticks not being considered periodic
  * Warrior
    * Implement Glyph of Resonating Power
    * Fixed an issue with Whirlwind's rage cost for Arms

## SimC 520-06
  * General
    * Added experimental buff average uptime graphs (defaults to off; enabled with "buff\_uptime\_timeline=1").
    * Disable Spirit scale factor calculations for Balance, Shadow, and Elemental
    * Fixed an issue with Lootrank and Wowupgrade statweight links
    * Implement "thunderforged" item option
    * Implement thunderforged versions of the 5.2 raiding trinkets
  * Paladin
    * Initial, rough reimplementation of protection paladins
  * Rogue
    * Fixed an issue with Mutilate not benefitting from buffs that fade on main attack
    * Fixed an issue with Marked for Death breaking stealth
    * Small changes to the default actionlists
  * Warlock
    * Fixed an issue with immolation aura doing zero damage
    * Fixed various issues with Infernal/Doomguard cooldowns

## SimC 520-05
  * Death Knight
    * Fix an issue with runeforge import.
    * Make Blood Boil convert to death runes.
  * Hunter
    * Fix Fervor and Black Arrow not being reset by Readiness.
  * Mage
    * Fix Incanter's word getting increasingly OP throughout the fight.
    * Fix Incanter's Ward mana gain not being increased by spell speed.
    * Fix Invocation not removing the cooldown of Evocation.
  * Paladin
    * Fix bug where Sword of Light was applying to the wrong spells, introduced in 520-04.
  * Priest
    * From Darkness, Comes Light / Surge of Darkness 1sec ICD has been removed on live.
  * Shaman
    * Make all overloads proc on impact, not on execute. Restores palpatineish behavior for Chain Lightning and Lava Beam.
  * Warrior
    * Fix Bladestorm cancelling auto-attacks
  * General
    * Fix a crash in debug output.
    * Fix a bug when compling with GCC.
    * Fix weapon damage calculations when the item data is fetched from a web based source.
    * Fix weapon dps scale factor calculation.
    * Fix buff/discharge action names in reports when specifying a custom on-use or on-equip string.

## SimC 520-04
  * General
    * Performance improvement by caching common stat queries (10%-20% depending upon class)
    * Enable residual dot actions (such as Ignite) to work in multi-target scenarios.
    * Adjustments to HecticAddCleave fight style
    * Rudimentary AOE action lists for Death Knights, Rogues, Hunters, Monks, and Warriors. Note that some AoE abilities are still missing from the simulator.
    * Internal item system changes, part I. Only user visible change is the ability to upgrade\_level any item, as long as the ilevel of the item is provided.
    * Restore target reporting to results
  * Death Knight
    * T15H and T15N profile updates
    * Default action list tweaks
    * Implement buggy Razorice runeforge from in-game
  * Druid
    * Make Cat form GCD reduction only apply to Healing Touch spell, instead of all spells
    * Change Feral default action list to use Mangle as the primary Combo Point generator when in low energy situations
  * Hunter
    * Change T15 2PC pet's Lightning Blast to not benefit from haste
  * Mage
    * Inferno Blast now spreads Ignite/Pyro/Combustion to nearby targets
    * Nether Tempest
    * Improvements to default action list generation
    * Make Rune of Power deactivate if the mage moves in the simulator
    * Make Living Bomb apply to correct number of targets
  * Monk
    * Make Fists of Fury split damage between aoe targets
  * Priest
    * Improvements to default action list generation
    * Add one second ICD to Surge of Darkness procs from From Darkness, Comes Light (http://howtopriest.com/viewtopic.php?f=8&t=3403)
  * Warrior
    * Make Blood and Thunder apply to all Thunder Clap targets

## SimC 520-03
  * Death Knight
    * Tier15 2PC melee pet has a slightly better (20%) special attack than the normal ghoul.
  * Hunter
    * Define pet regen in terms of hunter regen instead of computing it based on pet haste
    * Fix steady\_focus so that it is a speed buff rather than a haste buff (so it doesn't affect RPPM and focus regen)
    * Now that we have distinct ranged-speed buffs, those also need to be removed from the melee-speed that pets inherit.
  * Mage
    * The sim won't crash when you import mages below max level now
  * Paladin
    * Fix HOTR not sharing cooldown properly
  * Priest
    * Add queuing Shadowy Apparition behavior.
  * Rogue
    * Fix 4pc gcd reduction to only apply during Shadow Blades
  * Shaman
    * Fix a mana cost issue with Enhancement and Shocks. Practical effect to profiles is 0.
    * Optimize the module to be a bit less stupid w/ regards to haste, and cast time checking.
  * Warlock
    * Update rain of fire ember gain to match 5.2 mechanics.
  * Warrior
    * Implement Sweeping Strikes
  * General
    * The progress bar in the CLI will now estimate time remaining too
    * Scale Factors: Fix ranking if no normalized values are available.
    * Basically every class profile was tweaked in some way, either gear, action lists, or both.
    * Performance optimizations with data collection and attack table, see [r15902](https://code.google.com/p/SimulationCraft/source/detail?r=15902)
    * Add hotfixes from http://us.battle.net/wow/en/forum/topic/8197590653#1
    * Added FightStyle HecticAddCleave (Similar to Horridon)
  * Items
    * Essence of Terror is OnHarmfulSpellHit, not OnSpellDamage.
    * Hotfix Feather of Ji-Kun to be 20% more powerful for all versions (excluding possible Thunderforged ones).
    * Add a PROC\_HARMFUL\_SPELL\_LANDING proc type, because we didn't actually have a way to model trinkets that proc on landing harmful spells but not periodic harmful spell damage. Fixes Essence of Terror and Volatile Talisman of the Shado-Pan Assault.
    * Increase RPPM per http://us.battle.net/wow/en/forum/topic/8197741003
    * Redo our implementation of RPPM mechanic to match new behavior
    * Updated gaze of twin proc rates to most recent posting from http://us.battle.net/wow/en/forum/topic/7923993861?page=109#2169
    * Fix cha-ye's essence of brilliance duration
## SimC 520-02
  * Death Knight
    * Removed outdated hotfix on Death Coil
  * Druid
    * Revert 15% buff to Rip.
  * Mage
    * Fix incorrect Frost T15 4pc implementation
  * Monk
    * Fix Chi tracking for Tiger Palm and Blackout Kick when Combo Breaker is up.
    * Require a hit/crit for Chi tracking purposes, and TEB stack increase.
    * Refund Chi on misses, in addition to dodges and parries.
    * Implement energy refund on misses/parries/dodges, estimated at 80%
    * Require Jab to hit/crit for Chi generation, T15 2PC energy generation, and Combo Breaker proccing.
    * Proc Tiger Power buff only on hit/crit.
    * Xuen, the magnificient white tiger is a guardian, not a pet.
  * Rogue
    * Blade Flurry wasn't correctly ignoring armor
  * Shaman
    * Earthquake wasn't correctly ignoring armor
  * Warrior
    * Dragon Roar wasn't correctly ignoring armor
  * General
    * Hotfixes from http://us.battle.net/wow/en/blog/8953693/
    * Increase Dancing Steel RPPM chance by 15%
    * Only fail id-based item initialization if both stats= and weapon= options are missing.
    * Sync all profiles, a few were not synced and wouldn't run using the included actions.
    * Simulating with the Command Line will now show a progress bar instead of counting down from 10.
    * Deprecate use\_off\_gcd as it is no real option, but just a spell property. See [r15849](https://code.google.com/p/SimulationCraft/source/detail?r=15849) for details.
  * GUI
    * Added stormlash and crit banner to buff selection tab.
## SimC 520-01
  * The PTR option is once again disabled
  * Death Knight
    * Implement proxy Anti-Magic shield, see [r15727](https://code.google.com/p/SimulationCraft/source/detail?r=15727) or the Death Knight's wiki page
  * Monk
    * Improve Chi Wave implementation
  * Paladin
    * Change T14 4pc bonus
  * Priest
    * Shadowy Apparitions was set to 3 max, when it should be 10
  * Rogue
    * Adjust Envenom AP coefficient to accommodate for the 20% buff in damage
  * Warlock
    * Fix an issue with Meta not properly affecting some things (Shadowflame dot and Frag belt in particular)
    * Make extra ticks from Malefic Grasp and Drain Soul use the player's current crit chance, instead of the MG/DS snapshotted crit chance.
  * Warrior
    * Heroic Leap and Thunder Clap weren't benefiting from seasoned solider and other effects
    * A few abilities had an extra 120% modifier for Arms that were removed
    * Whirlwind
      * Was consuming 2x-3x as much rage as it should
      * Now only benefits from raging wind when it's up
      * OH does proper damage
      * Now hits all targets like it should
    * Add support for Glyph of Rude Interruption
    * Track Sword and Board's rage gain separately from shield block
    * A few actions were possibly double dipping in cooldown reduction if they were defined multiple times in an action list
    * Impending Victory was applying weapon damage, which isn't true
    * Hack to allow 3 + 2 abilities in one CS window
  * General
    * Add a new option `affected_role` to raid events. Takes the same values as the player option `role`. If given, only the actors with the specified role will be affected by the raid event.
    * Any raid\_event options that used `<=` or `>=` have been replaced with `_min=` or `_max`=
    * Add crit\_pct to dot expressions
    * Fixed a bug related to interrupt and another related to dot.duration expression
    * Lots of tweaks to RPPM and attack\_speed/attack\_haste based on the new information from GhostCrawler
    * Allow item download to fail, if the user has input the item options through `stats=` as a fallback.
    * Report errors only once, instead of number of threads times.
  * GUI
    * Change the simulate tab
      * It now uses tabs, which should make it more easy to work with multiple profiles, and copy them around.
      * History is preserved, tabs are movable and closeable.

# WoW 5.1.x
## SimC 510-12
  * Shaman
    * Fix an issue with Elemental default action list generation

## SimC 510-11
  * Death Knight
    * Tier15 Heroic profiles
    * Fix Tier15 set bonus detection
    * Fix interaction between main- and off-hand hits on certain Death Knight abilities when dual wielding
  * Druid
    * Tier15 Heroic profiles
    * Spells cast in Cat Form on the PTR are 1sec GCD
    * Adjust Feral default action list to accommodate new trinkets
  * Hunter
    * Tier15 Heroic profiles
    * Implement tier15 set bonuses
    * Fix Beast Mastery mastery applying twice to pets
    * Fix BW affecting stampede damage
    * Fix an issue with Murder of Crows damage delivery
    * Fix Serpent Sting double dipping on mastery, and tick damage calculation
    * Change Dire Beast damage to be stricly AP based
  * Mage
    * Tier15 Heroic profiles
  * Monk
    * Tier15 Heroic profiles
    * Remove Chi tracking bug to reflect live hotfix and update default action list to reflect this
    * Fix T15 set bonus detection
  * Paladin
    * Tier15 Heroic profiles
    * Fix Avenging Wrath cooldown on PTR
  * Priest
    * Updated default action list for both live and PTR.
    * Implemented the new Solace & Insanity, including Mind Flay (Insanity)
    * Initial Tier 15 Heroic Shadow profile added.
    * Fix Divine Star damage
    * Fix/implement issues with T15 set bonuses
  * Rogue
    * Tier15 Heroic profiles
    * Add GCD reduction to T15 4PC set bonus, stacks with GoAR
  * Shaman
    * Initial tier 15 heroic Enhancement profile and action list changes
    * Implement PTR Lava Burst changes
    * Minor default action list adjustments
    * Eliminate Spirit scaling from elemental default scale factors
  * Warlock
    * Tier15 Heroic profiles
    * Fix Rain of Fire resource cost on PTR
    * Adjust default action lists in light of Warlock changes
  * Warrior
    * Tier15 Heroic profiles
    * Fix vengeance gain on non-harmful attacks
    * Fix vengeance capping
    * Improve Whirlwind damage reporting
  * General
    * Update PTR spell data to build ~~16577~~ 16650.
    * Implement Sinister and Capacitive Primal Diamond.
    * Implement Crystal of Insanity ([Issue 1542](https://code.google.com/p/SimulationCraft/issues/detail?id=1542))
    * Implement all DPS trinkets in 5.2 (no pets for Bad Juju for now)
    * Implement a proc delay to discharge procs
    * Add `action.x.(hit|crit)_(damage|heal)` expressions that return the amount of direct hit/crit that action would do with the profile's current stats
    * Add `mastery_value` expression to return the "paperdoll mastery%" of the player
    * Add new option `scale_to_itemlevel` that scales all actors in the sim to the specified ilevel
    * Add new expressions relating to trinket procs, see commit [r15697](https://code.google.com/p/SimulationCraft/source/detail?r=15697) for documentation
    * Stat buffs now allow negative stats
    * Upgrade Fluffy Pillow's default damage for 5.2
    * Support hit/exp cap on wowhead links
    * Fix a rare issue with buffs that have cooldowns
    * Fix a a rare crash issue in sim with back to back executions ([Issue 1539](https://code.google.com/p/SimulationCraft/issues/detail?id=1539))
    * Fix various (small) issues with reforge plots
    * Fixes to challenge mode scaling
## SimC 510-10
  * Death Knight:
    * Tier 15 4 piece DPS set bonus
    * Very preliminary implementation of Tier 15 2 piece DPS set bonus. Minion stats need verification.
    * An error in Death Coil scaling has been corrected, damage is increased at high levels of gear.
    * Fix Festering Strike re-snapshotting dot stats on extend ([Issue 1545](https://code.google.com/p/SimulationCraft/issues/detail?id=1545))
  * Druid:
    * Thrash damage calculation is now accurate.
    * Feral:
      * Significantly higher DPS action list.
      * Tier 15 set bonuses
    * Fix weapon dps scaling.
  * Hunter:
    * Marksman default action list now uses the Careful Aim sub-action list above 80% (was 90%) target health ([Issue 1523](https://code.google.com/p/SimulationCraft/issues/detail?id=1523)).
  * Mage:
    * Remove Glyph of Conjuring; it's no longer in-game.
    * Implement Glyph of Loose Mana ([Issue 1525](https://code.google.com/p/SimulationCraft/issues/detail?id=1525)).
    * Fix Incanters Ward spell power gain calculation.
  * Monk:
    * Implement Chi-tracking bug for Tigereye Brew just as in-game ([Issue 1526](https://code.google.com/p/SimulationCraft/issues/detail?id=1526)).
  * Priest:
    * Remove Holy Priest from Raid\_T14H, Holy implementation still needs updating for MoP ([Issue 1528](https://code.google.com/p/SimulationCraft/issues/detail?id=1528)).
  * Rogue:
    * Tier15 set bonuses
    * Blade Flurry on PTR hits 4 targets
  * Shaman:
    * Enhancement default action list now uses Elemental Blast only if at least one Maelstrom Weapon charge is active.
    * Fix a bug that caused Elemental Blast to sometimes consume Maelstrom Weapon without benefiting from it.
    * Fix a bug that prevented Enhancement weapon-based attacks from receiving the mana discount from Shamanistic Rage.
    * Preliminary Restoration support.
    * Tier 15 set bonuses for Enhancement and Elemental
    * Improve proc counters for Maelstrom Weapon charge waste, and the proc indicators for Maelstrom Weapon stacks during spell cast.
  * Warrior:
    * Remove Bladestorm from the default Arms action list, it's a DPS loss on single target ([Issue 1508](https://code.google.com/p/SimulationCraft/issues/detail?id=1508)).
    * Sample T14H profiles now have gems in their Blacksmithing bracer sockets ([Issue 1524](https://code.google.com/p/SimulationCraft/issues/detail?id=1524)).
    * Small tweaks to the default Fury action priority list.
    * Fix Skull Banner critical strike damage bonus.
  * General:
    * Second attempt to remove Orc expertise from wands ([Issue 1530](https://code.google.com/p/SimulationCraft/issues/detail?id=1530)).
    * Update PTR spell data to build ~~16446~~ ~~16467~~ ~~16486~~ ~~16503~~ ~~16539~~ 16562.
    * Add proxy Skull Banner cast to sim. _override.skull\_banner=number\_of\_casts_ to use. Defaults to two Skull Banner casting proxywarriors of doom. The sim also links it to an early proxy-Bloodlust cast (first 30 seconds of combat), if possible.
    * Fix reforge plot output in HTML reports
    * Support item upgrade levels of up to ilevel 1000 (previously 580)
    * Fix serious problem with multithreading. Multiple threads now have independent rng-seeds and thus independent statistical samples.
## SimC 510-9
  * Death Knight:
    * Howling Blast now properly applies Frost Fever to **all** affected targets.
    * Pestilence should now correctly apply diseases to all affected targets.
    * 5.2 PTR changes (in PTR mode only):
      * Ebon Plaguebringer effect implemented.
      * Reaping affects Icy Touch.
  * Druid:
    * Shifting between forms during simulation should now work properly.
    * Shapeshift actions now properly trigger a 1.5 second GCD, unaffected by haste.
    * Shapeshift actions now properly evaluate conditional expressions.
    * Actions that require a particular shapeshift in-game now do in SimC as well.
    * The default Balance action list now tries to synchronize item uses and profession actions with Celestial Alignment.
    * Thrash damage calculation is now slightly more accurate.
    * Guardian:
      * The multiplier to haste/crit rating while in bear form now applies properly.
      * Incoming Damage no longer provides Rage.
      * Rage is now properly set to 10 on entering Bear Form.
      * Pertinent abilities now properly have no cooldown while Incarnation: Son of Ursoc is up.
      * Savage Defense implemented.
      * Implemented Rage from talent Soul of the Forest.
  * Hunter:
    * The primary target of Glaive Toss now properly takes increased damage.
  * Mage:
    * Implement 2012-12-13 Frost Bomb hotfix: explosion time reduced to 4 from 6 seconds.
    * Fire Mages who are not Orcs have figured out how to use items (the lesser races can be a bit slow).
    * Evocation now works correctly when cast before entering combat to put up the Invocation buff. Use the precast option to specify the time interval between putting the buff up and the actual pull; defaults to 0 seconds.
    * Fixed a bug that was causing Evocation to give the Invocation buff even when interrupted.
    * 5.2 PTR changes (in PTR mode only):
      * Frost Bolt debuff no longer increases Frost Bolt damage.
  * Monk:
    * Properly implement Tigereye Brew.
    * T14 set items are now correctly recognized.
    * 5.2 PTR changes (in PTR mode only):
      * Implement Combo Breaker as passive, and Bottled Fury as the new Windwalker Mastery ability.
      * Implement Chi Wave talent ability.
  * Priest:
    * 5.2 PTR changes (in PTR mode only):
      * Glyph of Holy Fire increases range of Holy Fire, Smite, and Power Word: Solace.
      * Spirit Shell no longer scales with mastery.
      * Power Word: Solace replaces Holy Fire when talented.
  * Rogue:
    * 5.2 PTR changes (in PTR mode only):
      * Preparation is now a baseline ability.
      * Blade Flurry does 75% less damage.
      * Implement the Marked for Death ability.
  * Shaman:
    * 5.2 PTR changes (in PTR mode only):
      * Unleashed Fury increases Lava Burst damage by 10%.
      * Elemental Blast sometimes buffs Agility for Enhancement.
      * Primal Elementals now inherit 20% more spellpower from the Shaman (yes, that's not what the patch notes say - they're wrong).
      * Ancestral Swiftness increases spell haste by 5% and attack speed by 10%.
      * Glyph of Flame Shock no longer extends the duration of Flame Shock.
  * Warlock:
    * 5.2 PTR changes (in PTR mode only):
      * The effects from Glyph of Soul Shards & Glyph of Burning Embers are now baseline.
  * Warrior:
    * Shockwave is now properly an AoE.
    * Reports now track Taste for Blood stacks lost to overflow.
    * 5.2 PTR changes (in PTR mode only):
      * Taste for Blood behavior changes.
  * General:
    * Reforge Plots now scale the amount of stat reforged by a gem itemization multiplier (1 for Strength/Intellect/Agility, 1.5 for Stamina, 2 for secondary stats) to better represent tradeoffs from regemming. The X axis on reforge plots is now effectively in terms of itemization points instead of stat points, so that if e.g. the plot says your DPS is best if you trade 200 haste for crit it means 200 itemization points = 400 points of haste or crit rating.
    * Documented the [line\_cd](http://code.google.com/p/simulationcraft/wiki/ActionLists#Time-based_usages) action option.
    * Tank crit reduction now properly works on special abilities.
    * Vengeance is now properly gained from attacks that miss.
    * Scale factors are now sorted in descending order when scaling over Damage Taken per Second.
    * SimC now supports the legendary questline extra prismatic socket on weapons.
## SimC 510-8
  * Druid:
    * Fixed a bug that would allow a Moonkin to cast Starsurge before the previous Starsurge impacts the target.
    * Fixed another bug that was letting Moonkin react instantly to Shooting Stars procs.
    * Tweak the default action list to Starsurge at a fairly high priority when Shooting Stars is up, to avoid "losing" procs.
  * Mage:
    * Damage from Arcane Missiles is now correctly increased by the stack of Arcane Charge applied by the cast itself.
    * Default action list for Arcane now incorporates Scorch when talented.
    * The Arcane Mage sample profile now talents Scorch.
  * Warrior: Sadly, it's no longer possible to get infinite DPS with Bloodbath.
  * General:
    * Upgraded items should now correctly import from Battle.net.
    * The "Save" button on the Results tab of the GUI should work again.
    * Simulationcraft no longer refuses to recognize Pandaren who have joined the Alliance/Horde as Pandaren. (But seriously, Horde rules).
    * Add support for the [Relic of Chi-Ji](http://www.wowhead.com/item=79330) trinket proc.
    * Correct values for the [Stuff of Nightmares](http://www.wowhead.com/item=86323) trinket.
    * T13 profiles removed. Level to 90 and move on, people.
    * Support for [DTR](http://www.wowhead.com/item=71086) removed.
    * Fixed a bug that was causing unpredictable crashes.
## SimC 510-7
  * Couple of small bugfixes.
## SimC 510-6
  * Priest:
    * Mindbender action should now correctly be added to actionlists of Priests who have the talent.
    * Discipline is basically feature-complete now, and should be considered early beta quality. (Go ahead and play around with it and file issues.)
  * Mage:
    * Dec 10, 2012 hotfix to Critical Mass.
  * Items:
    * Add the rare quality reputation reward trinkets from 5.1.
    * use\_item actions can now optionally refer to a slot name (e.g., "slot=trinket1" or "slot=hands") instead of item name.
    * The Shock-Charger Medallion should now be recognized correctly.
  * General:
    * Simulationcraft now ALWAYS generates UTF-8 output. Should correct issues with the GUI getting confused by the simulator error messages and reporting garbage.
## SimC 510-5
  * Other:
    * Fix a bug where a non-alchemist using an alchemist flask would infinite loop.
    * Mixology increases for MoP flasks are now implemented.
    * Implement MoP style Healthstones.
## SimC 510-4
  * Monk:
    * Only scale off hand stats when they actually apply.
  * Priest:
    * Track the percentage of Smite casts that benefit from the glyph.
    * Disc/Holy don't scale with hit rating, even when DPSing: Divine Fury hitcaps them.
    * Atonement is working again.
  * Warrior:
    * Fix bladestorm working on multiple targets.
  * Timeline: Add function to calculate the average of a timeline. Use it in resource timeline charts.
  * Fix a bug introduced in 510-3 that resulted in item cooldowns not working properly.
## SimC 510-3
  * Druid:
    * Fix the Balance default action list so the druid won't keep spamming Wild Mushroom while moving in an  attempt to get to 5 (3 is the maximum).
    * Counts of total combo points and wasted combo points (due to being at the cap) are appearing in the Procs section of Feral druid reports again.
  * Hunter:
    * Focus cost of Murder of Crows now correctly reduced by The Beast Within.
    * Lynx Rush is now a bleed.
    * Moved Aspect of the Hawk to the pre-combat action list.
    * Don't wait for buffs to use Stampede if the target is going to die soon.
    * Ranged attacks from position ranged front can no longer be blocked.
    * 2012-11-29 hotfixes:
      * Serpent Sting does 100% more damage.
      * Serpent Sting costs 15 (was 25) focus.
      * Improved Serpent Sting does 15% (was 30%) damage up-front.
  * Mage:
    * Default action list now refreshes bombs before the last tick.
    * You can now refer to Frost Bomb as a dot effect (dot.frost\_bomb) in action lists just like Living Bomb.
    * Don't cast bombs if the target will die very soon.
    * Remove Brain Freeze reaction time for Mages specced into Frost Bomb: Frost Bomb has a 100% chance to proc and is therefor predictable.
    * 2012-11-29 hotfixes:
      * Critical Mass critical chance multiplier is 1.5 (was 1.25).
      * Periodic damage from Combustion reduced 50%.
    * Corrected an error in Ignite calculation that was causing damage to be too high.
  * Paladin:
    * Correct typo in the default action list.
  * Priest:
    * Implement Divine Star and Halo correctly.
    * Chakra Chastise buffs damage by 50%, not 15%.
    * Shadow Word: Insanity now correctly works with cycle\_targets=1.
    * Do all talent checking dynamically in the shadow default action list instead of statically at import time.
    * Divine Fury increases hit chance with ALL spells.
    * Power Infusion is now self-only and not a targetable buff.
    * Fix Power Word: Solace and track its mana gain.
    * 2012-11-29 hotfixes:
      * Divine Star now deals 40% more damage and 133% more healing.
  * Other
    * Fix a bug with the enemy tank's melee attack.
    * Update guild ox's loot rank URL.
    * Wowhead profile import code has been deactivated.
## SimC 510-2
  * Hunter:
    * Barrage, Cobra Shot, and Steady Shot are now usable while moving.
  * Mage:
    * Arcane Charge now increases the mana cost of Arcane Blast by 75% per stack instead of 125%. (Tooltip change did not get into 5.1)
  * Paladin:
    * Prioritize Judgment over Crusader Strike under 20% health or when Avenging Wrath is active.
  * General:
    * Remove the obsolete MMO Champion data source module (mmoc).
    * Wowhead talent calculator URLs should again be correctly imported/exported.
    * Upgraded weapons should now have correct damage values.
    * Bows/Guns/Crossbows/Wands should have correct stats again.
    * Implement on-use encodings for the 5.1 trinkets.
## SimC 510-1
  * Death Knight:
    * Soul Reaper no longer resets the swing timer.
  * Druid:
    * Leather Specialization now correctly increases Intellect or Stamina for Resto/Balance or Guardian spec druids.
  * Hunter:
    * Aspect of the Hawk hotfixed to 15% Ranged Attack Power.
  * Mage:
    * Hot streaked pyroblasts shouldn't consume PoM.
    * Initial implementation of Living Bomb explosion when refreshed early
    * Glyphs of Combustion should now work correctly.
  * Monk:
    * Fists of Fury should now work correctly.
    * Windwalker action list updates.
  * Paladin:
    * Fixed a bug that was causing Divine Purpose to trigger 100% of the time.
    * Hammer of Wrath can now be dodged.
    * Ret action list updates.
  * Priest:
    * Greater Heal and PoH now correctly consume Serendipity.
    * Halo should do damage again.
  * Warrior:
    * Avatar no longer increases Rage generation.
  * Warlock:
    * Changes to the AoE action list.
  * General:
    * Fix a bug that was causing proc enchants to not always trigger properly.
    * Add Vengeance Timeline.
    * Implement the Engineering Frag Belt addon.
    * Upgraded items should import correctly.
    * Sha-Touched gems should now import correctly.
    * Add Raid Event options `players_only` (event doesn't affect pets) and `player_chance` (event has given chance of affecting each player).
    * Orcs no longer get 1% expertise from wands.
  * GUI:
    * Add challenge mode option. "Stats won't be exact, but very close."
  * Reports:
    * Move Pawn string to the stat scaling section of the report so it is more prominent.
    * Bring back the automatic lootrank link (link to GuildOx's lootrank with the stat weights pre-filled).
    * Errors are visible at the top of reports again (albeit in a pretty ugly way).

Release notes for older releases are archived at ReleaseNotesArchive.