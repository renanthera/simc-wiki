

# WoW 5.0.x
## SimC 505-6
  * Druid:
    * Feral: don't try to use Nature's Swiftness when the character doesn't have the talent.
  * Mage:
    * Presence of Mind's buff is no longer triggering with a delay, so you can use it instantly.
  * Priest:
    * Corrected Mindbender mana return to 1.46% per swing instead of 4%.
    * Binding Heal targets heals two targets, not necessarily the target and caster.
  * Shaman:
    * Elemental: Prioritizing FS over LvB can lose Lava Surge procs under movement. Optimize the FS condition to shave a couple % of run time.
    * Tweak Enhancement default action list.
  * Warrior:
    * Arms: BiS gear changes.
    * Fury: Changes to the BiS gearset and action priority list.
  * General:
    * Correct a bug that broke multitarget fights in 505-5.
    * Add support for item retrieval from Battle.net.
    * Fix a bug in item\_db\_source option parsing.
    * Fix a bug causing a crash after simulating when both the debug and output option are used together.
    * Update PTR data to build 16297.
    * While parsing the "armory=" option, don't override the user-specified server with the default server when the region is defaulted.
    * Reforge plot data is written to output if no separate reforge plot output file is specified.
  * GUI:
    * The user-specified order for item DB sources now correctly applies to imports as well as simulations.
    * German localization.
  * HTML Reports
    * Update to latest version of jQuery.
    * Add the "thumbnail" player option to associate an image with a player for reports.
    * Display wowhead tooltips for pet abilities too, not just the player's own.
  * Items:
    * [Iron Belly Wok](http://www.wowhead.com/item=89083) is now implemented.
    * Ensure LFR loot from MSV is properly recognized as such.
## SimC 505-5
  * Druid:
    * Hurricane now does damage.
    * Hurricane and Astral Storm are now AoEs.
    * Rework of the Balance default action priority list to include multidotting and AoE.
  * Priest:
    * Inner Fire now correctly stacks **additively** with the 10% raid spellpower buffs instead of multiplicatively.
  * Shaman:
    * Thunderstorm is now an AoE.
    * Reported DPE/DPET of Earth Shock now includes the contribution from Fulmination.
  * Warrior:
    * Raging Blow only consumes one stack of the buff Raging Blow, not all of them.
  * General:
    * AoE: Most abilities with a fixed maximum number of targets were actually affecting one less than that number. For example, Chain Lightning now hits the intended three targets instead of two.
    * Plots: Save Data to csv file, similar to reforge plots
    * GUI: Don't offer statistics\_level = 8, as it usually requires too much memory for 32bit executables
    * Attack Mechanics: Attacks now react dynamically to position changes ( front / back ) when calculating parry and block chances.
    * Arcane Torrent now correctly returns 2% of max mana.
  * Items:
    * [Blossom of Pure Snow](http://www.wowhead.com/item=89081) is now implemented.
    * Don't cancel sim on addon decode failure.
## SimC 505-4
## SimC 505-3
## SimC 505-2
  * Hunter:
    * Hunter: rename start\_attack\_t token. Fixes a reporting bug with auto attacks.
  * Mage:
    * Change Combustion implementation.
  * General:
    * Item: Don't error on back/cloak addon 'goblin\_glider'.
    * GUI: Add option to specify multiple enemies.
    * GUI: Add scale\_over option.
    * Scaling: Save a players name to his sample\_data containers ( dps, hps, etc. ) and improve printing of that name in the html report.
    * Add player race expression.
## SimC 505-1
## SimC 504-5
## SimC 504-4
  * Heal: Change smart heal heuristic.
## SimC 504-3
  * General
    * Print error message if invalid race string is specified.
    * Build 15952 DBC data.
    * Fix compilation on GCC 4.7
    * Fix Blood Fury to not grant double Attack Power to certain classes
    * Fix generic crit suppression to match in game behavior
  * Change DMC trinket ICD to 55 seconds, approximate other trinkets to 60sec ICD
  * Death Knight
    * Implement Plague Leech
    * Fix Scourge Strike shadow damage coefficient, Runic Empowerment, Runic Corruption, Blood Tap
    * Update T14H profiles, Ghoul / Army of the Dead base damage scaling and swing speeds
  * Druid
    * Balance default action list tweaks
    * Add Balance T14 normal and preraid profiles
    * Fix Nature's Swiftness
    * Fix Celestial Alignment behavior to match in-game
    * Fix Savage Roar interaction with Glyph of Savagery
    * Implement Predatory Swiftness, Tier 14 feral set bonuses
  * Hunter
    * Turn on scaling with expertise
    * Fix pet focus regen rate
    * Implement Kindred Spirits
    * Change Cobra Strike to apply only to active pet
    * Fix a Murder of Crows model
  * Mage
    * Update Tier14 2 piece bonus
  * Monk
    * Fix Tiger Strikes, Way of the Monk, Tiger Power, Zen Sphere explosion, Spinning Crane Kick, Tier 14 set bonus issues
    * Implement Chi Torpedo, Rushing Jade Wind, Rising Sun Kick debuff spreading, Expel Harm
    * Update Invoke Xuen
  * Priest
    * Tier14 heroic profile tweaks
  * Rogue
    * Fix Subtlety mastery granting too much bonus to Slice and Dice
    * Subtlety action list changes
  * Shaman
    * Fix primal elementalist, issue with the default action list and non- EM/PE combinations, Stormblast interaction with Static Shock
  * Warrior
    * Change Cleave/Overpower to use weapon damage, instead of normalized weapon damage
    * Implement Heroic Throw, Wild Strike, Dragon Roar, Avatar, Bloodbath, Storm Bolt, Skull Banner, Tier 14 set bonuses
    * Fix Bladestorm, Shockwave, Bloodthirst rage gain, Enrage / Berserker Rage interaction, Fury mastery, Crazed Berserker, Heroic Leap, Raging Blow
    * Add Fury 1h, 2h, Arms Tier 14 heroic profiles
  * Warlock
    * Implement Tier 14 set bonuses

## SimC 504-2
  * General
    * Add Healing Target
    * Track Enemy Healing Decades
    * Add option target\_level+= to specify a relative target level
    * Fix some targetdata buff merging problems
    * Use iofstream for html report
    * Improve iteration\_adjust, so that the effective average simulation length better matches the to be expected max\_time with vary\_combat\_length > 0.
  * Hunter
    * Crows benefit from BM mastery.
## SimC 504-1
## SimC 503-1
      * Fix a major issue in http::cache\_load().


  * Druid: Mirror Images cast wrath http://mop.wowhead.com/spell=110691, although they are broken right now (~30 dmg does not seem intended)


  * Add "mophead" item source. Remove "mmoc" item source (from defaults). Fix composite\_spell\_hit().


  * Update the hunter profiles to epic cata gems, reforge for expertise, enchant/jc, etc.

  * The succubus has a 3.0 second swing timer.


  * Update dual-wielding warlock pet mechanics. Add PreRaid to auto\_path.


  * Add generate\_Warlock\_PreRaid.simc. Regenerate profiles.


  * Fix compiler warnings. Fix pets inheriting 100% of owner attack speed. Add option "save\_gear\_comments" to enable those informative comments with non-overridden stats under each gear line - option defaults to off. Regenerate warlock profiles, plus move the PreRaid profiles into their own folder.


  * Shaman:
> Clip swings during Ascendance too.


  * Shaman:
> Fix auto attack swing clipping for Enhancement.
> Fix one in a billion issue with Ascendance and auto attacks.


  * Warlock pets no longer secretly get spell power from their base intellect.


  * Shaman:
> Fix segmentation fault with Ancestral Swiftness.
> Fix Elemental Mastery not benefiting melee swing speed.


  * Death Knight:
> Modernize Rune of Cinderglacier.


  * Death Knight:
> Modernize Rune of Razorice, and make it an attack, not a spell.
> Make Howling Blast apply Frost Fever.
> Fix Sudden Doom proccing.


  * Death Knight:
> Reforge Unholy to spell hitcap with expertise.
> Fix Scourge Strike shadow damage. It's still off by a few points, but very close to what it is currently in MoP beta.

  * Death Knight:
> Add generator profile, generate profiles.
> Add Frost dual wield profile.
> Frost sims, and produces results.


  * Improve chart school-color not found message.

  * Death Knight:
> Overhaul Base and Unholy abilities, Unholy is mostly done.


  * Priest: Adjust Holy Word Sanctuary.


  * Fix Elemental Force enchant and add a colour for Elemental Damage.


  * Priest: Fix Mind Sear Mastery procs.
  * Priest: Add level 90 talents to init\_actions()


  * Add hunter profiles to the main raid test profiles.


  * MoP chardev profiler import support now working.


  * Implement new Thrill of the Hunt. Any attack procs a Thrill of the Hunt buff. when the buff is up, AS and MS are free; they consume the buff in their execute functions.


  * Use dbc data for Sword of Light / Guarded by the Light regen


  * Update Ret/Prot paladin "extra" regen with numbers from GC.


  * Add Warlock\_PreRaid.simc.


  * Update autoextract.bat to work with Blizzard's new DBC/MPQ organization.


  * Fix saving of heroic/lfr flags for items. Make some adjustments to warlock profiles. Hellfire generates 3 fury per tick per target, not 2.


  * Add Warlock level 90 pre-raid profiles.


  * Add a couple of MoP trinket procs.


  * Death Knight:
> Add support for death rune costing abilities.


  * Extract death rune costs, apparently new thing in MoP.
> Rip apart DK module.


  * Druid:
> > Default balance talents: SotF is more dps than Incarnation

  * Druid: Update default action list for balance


  * Paladin: Update to 15851. Still missing level 90 talents.
  * Paladin: Add in a 5% every 1.5second "extra" mana regen for Ret and Prot.


  * Player\_t: Remove next pointer.


  * Change sim\_t::player and target list, use actor\_list for player\_t

> disposal.


  * Small rogue cleanups.


  * Rename impact\_s to impact, schedule\_travel\_s to schedule\_travel.
> Fix monk\_t::get\_target\_data.


  * Druid:
> Update various Feral and Guardian power coefficients.


  * Fix damage parameter for murder of crows.


  * Druid
> > Fix Shooting Stars proc to work with stateless


  * Monk: reduce baseline energy regen to 8.0/s


  * Action State:

> - Add Heal state which contains total\_result\_amount, which contains
> effective heal + overheal.
> - Pass state to player\_t::asses\_heal and target\_mitigation.


  * Action State:
> Pass state from action\_t::assess\_damage() to player\_t::assess\_damage()


  * Remove no\_buffs and no\_debuffs options from discharge procs - it's not supported by stateless, and is no longer in use anyway.


  * Fix wrath of tarecgosa double dipping.


> Fix compiler warning.


  * Removing Non-Stateless 4:
> - Move schedule\_travel\_s and impact\_s to sc\_action.cpp
> - Use action state for action\_t::assess\_damage


  * Removing Non-Stateless 3:
> - Completely remove non-stateless code in execute() and tick().
> - Remove stateless flag
> - remove haste() and total\_haste() functions.


  * Fix error with composite\_expertise, move it directly to attack\_t.


  * Removing Non-Stateless 2:
> Remove target\_debuff and its variables, remove snapshot(), remove most
> total\_foo() functions.


  * Removing Non-Stateless 1:
> Remove schedule\_travel, impact, player\_buff() and player\_buff variables.


  * Death Knight: Change to stateless.


  * Fix the static constant floats. That violates the C++ standard, and some compilers, including VS, object to it.


  * Brain Freeze proc chance for Nether Tempest is now 9%


  * Pre-emptive code for some upcoming changes


  * Fix spell haste reporting in textual output.
> Remove Mana Tide Totem from the simulator for now.
> Change Mastery sim-wide aura to give rating, instead of straight mastery. If override.mastery is given, the rating is for the max level player in the sim, otherwise the mastery rating is given by the actor who offers the mastery aura.


  * Action State: remove next pointer, move managment of state\_cache to action\_t.


  * Improve murder of crows accuracy for new patch, though it's still not correct.  Add copying spec in copy\_from.


  * Druid
> > Treants are not guardians
> > Fae Empowerment: Add Astral Empowerment buff


  * Priest: DP, reset some things and use debug\_cast


  * Make sure all stateless actions use composite\_haste() instead of

> haste().


  * Paladin: Change to stateless.


  * Hunter: Prepare Stampede


  * Mage: Cleanup Mirror Image code.


  * Icy veins fix


  * Mage T14 set bonuses


  * Properly unify enchant naming syntax.


  * Fix chardev parsing for live (gems were broken from blind enum usage).


  * Tweak Priest profiles.


  * Adjust ignite pct-based functions.


  * Remove TEST\_TIMEWHEEL


  * Harvest life now generates 10 fury per tick on the main target and 3 fury per tick on each additional target.


  * Hellfire now generates 2 fury per tick per target, instead of 10 per tick.


  * Mage ignite does not crit, nor get any target multipliers.


  * Fix pet spell haste.


  * Mirror Images done, I think -- thanks Reia


  * More Mirror Image work


  * Trying to fix Mirror Images


  * Bump simc version to 503-1
  * Fix setting the item id when downloading the item from item datadb
  * Handle item cache a bit better.
  * PRIEST: Update Shadow to 15851.


> Re-do Build 15851 data export.


> Try to make sure we reserve memory for all sample data, if size can be
> determined ( eg. == sim -> iterations ).


> Use auto\_dispose for some player lists.


> Some Mage hacks until client gets current spell data


> Updating a few Mage mechanics


> Beta Build 15851 (5.0.3) DBC Data


> Priest: Divine Fury for PW:Solace, added Rapid Renewal.


> Reorder some classes.


> Continue work on moving from object-oriented lists to owner-possesed
> lists ( or std::vector for now ).


> Player\_t: For simplicity, merge all base, initial and current variables
> together into one class, even though some of them don't require a base
> value.


> Skim through simulationcraft.hpp and change various things.
> - Move some things to cpp files
> - Change some static-function only classes to namespaces


> Add powershot support (though it is not in any profile yet).


> Save profiles with the item id if available for gear. Any non-overridden fields for the item will be shown in a comment underneath the item.


> SVN Tags


> Priest: Fix svn tags and use MoP consumables.


> Priest: Add DS profile


> Priest: Prepare ilvl 463 T14 shadow test profile


> Rogue: Change most actions to stateless, update targetdata.


> Hunter: Remove warning from hunter pet default\_spec().


> Support default specs for all pet types.


> Hunter: Really fix moc stats aggregation


> DBC auto extract: default to enUS once again.


> Add Tier 14 set bonus id's and decode\_set() stuff.


> Hunter: Fix crow stats aggregation


> Don't crash when spells have no description.


> Don't use NDEBUG if we're in Beta.


> Report Text: Don't print quiet pets.
> Hunter: Only report first Crow.


> Mage profile tweaks


> Make hunter pets class id 0 for dbc purposes. Export hunter pet specialization lists so find\_specialization\_spell() for pets works correctly.


> Add new header files to all project files.


> DBC Extract: Add LANG variable, print out invalid Input Path.


> Warrior: Change to stateless


> Warrior: add warrior\_action\_t, cleanup.


> Move generic programming tools and timespan from simulationcraft.hpp
> into separate header files.


> Typo


  * Add the new armor mitigation formula for > 85.
  * Add new armor values for enemies. (91 and 92 are best guesses but could be +/- 5 armor)


> Hunter: Change MoC pet list, use the shadowy apparition list/queue
> system.


> Hunter Pet: Add all specs, initialize them to not found.


> Fix MM Steady Focus haste buff and pets double-dipping in Rapid Fire.


> Keep track of number of refreshes to dots, and use this info for a better heuristic for DPET chart filtering: If the number of refreshes is greater than the number of executes, hide the action from the chart.


> Add readiness support for BM And MM, including correct handling of stacked murder of crows


> Level 93 armor value as per:


> Tiny cosmetic fix.


> Minor merge cleanup


> Work around assert with pet specs by just giving the ferocity abilities to all hunter pets.


> Hunter pets: prepare default _spec_


> Fix a bug with too many underscores in gem parsing, introduced in the
> previous commit.


> Enchant parsing: Improve system to better handle mixed enchants ( with
> some stat and spell effects ).


> Fix mage t13 4-piece bonus, plus get rid of some mistaken bypasses of mage\_spell\_t::execute().


> Improve demonology aoe action list some more.


> Item Enchant parsing: comment out all debug lines.


> Enchant parsing: Quick fix for +35 mastery / speed enchant boots.


> Mage Alter Time: Adjust buff states.


> change all merge functions to use references.


> Move sim\_t::analyze\_player( player\_t**) to player\_t::analyze\_player(
> sim\_t** )


> Remove sc\_log.cpp


> Actually add sc\_cooldown.cpp


> Add sc\_cooldown.cpp


> various cleanups


> Void Ray should not take 160 seconds to reach its target.


> Add the "kill shot glyph" functionality back. It's now integrated into Kill Shot by default. I left the name for now.


> Typo on t13 4pc buff


> Reactivate murder of crows. Fix behaviors for frenzy, focus fire, and rabid.


> Update Ret module. Still needs a good going over...


> Oops, accidentally deleted a line in the previous commit.


> Do the same for glyph of arcane power.


> Implement glyph of icy veins in safer places.


> Glyphs of Icy Veins and Arcane Power


> Hunter: Add moc attack stats as child stats of the summon spell.


> Fix profile svn properties.
# WoW 5.0.1
## SimC 501-10
> Revert "Use QT 4.8.2 libraries"


> Fix ranged vulnerability override.


> Use QT 4.8.2 libraries


> Create tag release-501-10


> Bring back bleeding override.


> Add all the new MoP foods.


> Some tweaks to mage module and profiles


> Add a "bool check\_func( player\_t**)" function point to buff\_stat\_t.
> When stat\_buff\_t::bump() is called if a check\_func is defined for that stat it is checked to see if it should bump that particular stat or not.**


> It's a hack, but add proper support for the Jade Spirit weapon enchant.


> Tick minor version ( to 501-10 ).


> GUI: if ( SC\_BETA ) include all profiles, not just T13.

## SimC 501-9
> Turn off default use of murder of crows until the numbers are more accurate.


> Add the Elemental Force weapon enchant.
> The melee version of it seems to have a 3 ppm from my testing.
> The caster version's proc rate seems to be between 6% and 8%ish. I chose 8% for now. Needs more testing.


> Update some profiles to use the new precombat system.


> Enchant System:


> Code consistency


> Minor comment improvement


> Adjust mindbender coefficient to match latest values.


> Introduce Murder of Crows. The implementation is still incomplete (e.g., it doesn't reduce the CD for targets below 20%) and the numbers are wrong (e.g., it hits like a treant), but the code and wiring of the summons, attacks, stats, actions, etc. should be correct.


> Mage: Fix Mage Armor buff. ( It is now a 3500 rating increase, not 5%
> mastery ).


> Absorb buff: Add some kind of absorb callback inside the absorb buff.
> Mage: Implement Incanters Ward.


> Mage Water Elemental: Remove unused snapshot variables.
> Use state pointer passed along as a argument in impact\_s, not execute
> state!


> Potions to spell data.


> One of the Hot Streak changes I made was unnecessary


> Hot Streak and Heating Up actions take place on impact. Inferno Blast needs to be counted as a crit, not just have its damage calculated as a crit. Fingers of Frost actions happen on cast.


> Water Elemental and Mirror Image fixes


> Unique Gear: Add maintenance static\_assert macro. Remove darkmoon card
> greatness.


> Mage: Alter Time, use auto dispose.


> player base actions with spell data: change inheritance from action\_t to
> spell\_t.
> stat\_buff\_t: parse A\_MOD\_ATTACK\_POWER ( fixes ap+sp blood fury ).


> stat\_buff\_t:


> Move most custom events directly to where they are needed instead of
> exposing them in simulationcraft.hpp . Provide a interface for the
> generic event starts instead ( start\_actionexecute(), etc. ).


> Use spell data when creating the blood fury buffs.


> Fix options parsing for imported player profiles.


> Remove the definitions for all those warlock talents that are not implemented.


> Mage profiles: Change Alter Time so it doesn't get canceled prematurely.


> Alter Time:
> Allow manually reseting the state prematurely.
> Don't restart buff cooldowns when rewriting buffs.


> Pets should not be benefiting directly from bloodlust (or other haste buffs) now that they get all of their owners' haste directly.


> HTML report: Don't try to use wowhead spell tooltips if spell ID is zero. Use wowhead spell tooltips for buffs if they have spell data.


> Don't use the "mh" suffix when naming main hand enchants, for less confusion among casters who might not even know dual wielding exists.


> Updating Mage profiles -- first try at Alter Time actions


> Remove crit reductions for Cata. All DoTs crit for 2x now.


> Attack Mechanics: Implement new extra BLOCK-roll. Pure speculation on
> how crit-block works now.


> Mage Alter Time: redo part of the concept and use a buff instead of
> event. This buff takes care of everything, which makes the interface to
> the user much simpler.


> Druid: Force of Nature - Feral, how much of the druids AP do they get?


> Fix trap\_mastery and explosive\_shot action script.


> Fix hunter test profiles.


> Druid: Force of Nature, balance version for now


> Mage: Further flesh out alter\_time


> Mage: Write a rough concept for Alter Time.


> Implement dual wielding for shivarra and wrathguard. Tuning numbers seem quite buggy on beta, but make the simulator match the current behavior for now.


> Improvements to Mage profiles


> Properly implement grimoire of supremacy, using separate pet implementations and real spell data.


> Return true when successfully parsing OPT\_MAP.


> Allow whitelisted spells with general tree (tree 0) to be forcibly included in spell lists.


> Abort simulator during setup, if we encounter an unknown option.


> Whitelist spells for the grimoire of supremacy pets. Also add an optional parameter to autoextract.bat to specify a folder from which to copy Item-sparse.adb into the extracted data folder.


> tick\_action changes: Don't do extra update\_flags snapshot inside the tick\_action for each tick - this means all multipliers need to be defined in the main action. Adjust warlock and priest actions accordingly. Make arcane missiles use tick\_action.


> Turn back on exotic beasts code; use "ab::" in template for some compilers.


> tick\_dmg expression: Use stateless methods to get a much cleaner
> solution.


> Mage: Introduce new precombat syntax.


> Action stateless tick(): Save tick\_dmg to dot -> prev\_tick\_amount, so
> that the tick\_dmg expressions once again works.


> Updating mage profiles


> Water Elementals apparently benefit from Orc racial now


> Invocation should halve MP5. Trying a method of preventing Arcane Missiles from benefitting from an extra Arcane Charge.


> Implement exotic\_beast to reduce pet ability CDs, and fix wild\_hunt in basic attack to add 100% damage but charge 120% focus. Uptimes are now 19% for MM/SV and 46% for BM, which is in the ballpark.


> Shaman:
> Feral Spirit scaling.


> Make warlocks cast CoE if the debuff isn't already up.


> Hunter pet action: Add special\_ability flag.


> Mage: some stateless bugfixes.


> Mage: stateless!


> Snapshot the stats of all pets when the player snapshots his own stats.


> Fix pet spell hit (again).


> Allow setting pets forcibly to quiet, overriding print\_pets\_separately
> option.
> Use for Warlock Wild Imps 1 to MAX.


> Implement Invigoration correctly, including proc and gain tracking.


> Priest: spirit increases attack hit as well.


> Priest: Use new pet sp/ap conversion, bring back orc racial.


> Pets: Move some functions to sc\_pet.cpp, fix small error on
> pet\_t::composite\_spell\_hit()
> Hunter: Use new pet ap/sp conversion, change claw\_t to basic\_attack\_t.


> Pets and enemies should not gain raid attribute buffs.


> Priest: Implement Tier14 Heal effects.


> Add some #ifndef NDEBUG conditionals to assert-if's.


> Regenerate Shaman profiles


> Shaman: Track auto attack sync / unsync on Wind Lashes also.


> Shaman:
> Fix a serious bug in shaman\_t::composite\_spell\_haste()
> Implement Primal Elementalist.
> Split Feral spirits into two distinct pets, reporting will have a single Spirit Wolf pet that contains the stats from both pets.
> Change Flurry and Unleash Wind to dynamically update swing speed when they proc.


> Rename pet\_t::coeff to pet\_t::owner\_coeff, add ap/sp scaling coefficients to it, and implement ap/sp scaling in pet\_t. Ensure pets don't gain the sp multiplier raid aura.


> action\_state\_t::copy\_state: fix rtt comparison, add some debug info.


> Remove spelldata\_t effect1/2/3()
> Fix small compile error in sc\_priest.cpp


> Priest: Tick actions are dynamic. Tested for penance and divine hymn,
> assuming it ( or keeping it as it was ) for mind sear.


> Move the typeid assert to action\_state\_t::copy\_state(), effectively disallowing the mixing of state types.


> Priest: Remove guardian pet layer.


> Priest: Use new tick action for penance, penance\_heal, mind\_sear and
> hymn\_of\_hope.


> Priest: Cleanup pet code.


> Hunter: Adjust pet scaling.


> Add an assert to ensure module authors don't implement a custom state type for an action without also using the same state for the tick\_action.


> Pets: Don't set AP and SP scaling of pets in pet\_t, since this isn't a
> globally valid setting even with the new pet system. Do it directly in
> your class pet code.


> Regenerate DBC data and add my cache file.


> Improve destruction aoe action list.


> Warlock: Pick up a few more triggered spell IDs from the spell data.


> D'oh -- forgot I had disabled two profiles in mage\_463.simc


> Just making sure the most up-to-date Mage profiles are pushed


> Pet composite attack power defaults to owner composite attack power. In addition, switch to new rules for other inherited properties; for example, crit was being double counted for hunter pets.


> Incanter's Ward passive buff support


> Add boolean action\_t::direct\_tick\_callbacks which causes tick damage callbacks to be called when assessing direct damage.


> stat\_buff\_creator: Attempt to automatically parse stat and amount from
> spell data.




> Add boolean action\_t::dynamic\_tick\_action which makes the tick action update state dynamically for each tick (using snapshot\_flags instead of update\_flags). Use this for the remaining warlock tick\_actions (hellfire, immolation aura, infernal immolation, and felstorm).


> Hunter: Fix Kill Command, use attack power from execute state.


> Hunter: Add Kill Command multiplier.


> Hunter: use the new rank string to find "Basic Attack" pet actions, and
> use this flag for the wild hunt bonus.


> DBC:
> Re-export DBC data to pick up rank strings.


> Inferno Blast always crits


> DBC: extract rank string. Needs regeneration of dbc.
> Temporarily add -Wno-missing-field-initializers to Makefile.


> Make the tick\_action stuff actually work as advertised, copying state correctly. Also make it not add the foreground action's tick results to its stats.


> Water Elemental gets 100% of Mage's spell power


> Pyroblast buff should be consumed on cast, not on hit


> Some Fingers of Frost fixes


> Add a new feature for automatically executing a background action to serve as the tick of a foreground periodic action. This works only for stateless, but correctly propagates the state of the foreground action to the background action, including converting the tick multiplier of the foreground action to a direct multiplier for the background action.


> Ice Floes should work now


> Ice Floes stuff


> Brain Freeze should proc on ticks, not on bomb application.


> DBC extractor: Don't use tabs.


> Hunter: More stateless adjustments, some code cleanup


> Some more cached item data.


> Hunter: Continue transformation to stateless.


> DBC Generator: Add a lot of whitespace to the spell whitelisting
> section.


> Whitelist Aimed Shot!


> Some mage fixes


> Implement "smooth" randomness for nightfall, as clarified by GC.


> Go ahead and update pet haste scaling to match GC's latest clarification.


> Fix pet spell hit - they get spell hit from expertise just like us.


> Properly initialize warlock pet melee attack.


> Pick up more things from spell data for warlocks.


> Simplify warlock summoning.


> Get rid of warlock\_main\_pet\_t and warlock\_guardian\_pet\_t.


> Fix stupid mistake from [r12644](https://code.google.com/p/SimulationCraft/source/detail?r=12644).


> Small cleanups.


> Warlock pets' melee swing timer is not reset or delayed by cast time spells, the swings are simply skipped if a cast is ongoing.


> Make pet haste scaling more consistent with how it currently works.


> Pets aren't gaining haste from temporary percentage-wise haste procs. Also, remove old haste/crit code from warlock pets.


> Merge new pet scaling into pet\_t.
> Remove class dependant coefficients ( mana, mastery, mana regen ). This
> can be better solved with inheritance on the pets that actually need
> this.
> Assume pet haste chooses from the highest owner haste, similar to crit.


> Implement new pet scaling in pet\_t, and update it according to latest info from GC.


> Update new (unused) pet scaling stuff based on responses from GC plus the assumption that they won't screw over people with expertise racials.


> Monk: Changed base regen to 13; updated tiger strikes; added refund to dodged/parried chi-using abilities


> Correct logic for ember\_react.


> Partial bombardment fix


> Hunter: Viper Venom, add cooldown duration.


> Hunter: Serpent Sting, use spelleffect\_data\_t::trigger() to directly
> access the trigger spell.


> Priest DP: roll the correct, unmultiplied dot tick damage to the new
> DP-dot.


> Priest Devouring Plague: Change to ignite-like mechanic.


> Slightly better trigger wiring.


> Add viper\_venom focus gains.  Removed obsolete roar of recovery.


> Shaman:
> Implement Elemental Blast.
> Fix certain stat buffs that were broken before.
> Make Fire Elemental spells benefit from Enhancement mastery.
> Implement T14 Set bonuses, all damage multipliers are additive.
> Allow Flurry to speed up / slow down remaining swing times.
> Correctly implement Flurry haste rating bonus.
> Fix Call of the Elements to not reset various cooldowns. Remove it from default action lists.
> Remove Stormlash Totem from default action lists until we get scaling numbers.


> Serpent Sting Scaling Data: pickup ID automatically, use extre
> coefficient.


> Use separate scaling spell for serpent sting so it now actually does damage.


> Druid
> > Spellstorm damage only gets buffed by one eclipse, even if both are up



> Hunter:
> Remove actions from the profiles, use default action priority list
> Cleanup hunter\_t::init\_actions so that all specs work with the default
> action list ( at least at level 85 ). Start using the new precombat list
> syntax.


> New pet scaling: Slightly different interpretation on the wording of
> armor/hp.
> Add mp5 scaling.


> Add code for the proposed new pet scaling.


> After giving it a bit more thought, move TD back out of the wow-class
> structs. Make sure all of them only accept their respective class
> pointer as a source, instead of a player\_t**.**


> Hunter: Adjust ranged weapon check.


  * Add a bunch of Mists enchants.
  * Add Alchemist's Flask.
  * Fix some warnings.


> Delete obsolete hunter pet spells: owl's focus, wolverine bite, etc.
> Consolidated checking for equipped range weapon.
> Added attacks to profiles (though they all do the wrong damaged).


> Druid
> > Refreshing Moon/Sunfire under eclipse seems to only update haste (tested), but not SP (tested), not the multiplier (tested), assuming not crit too (not yet tested)



> Make dot refresh/extend use the action's snapshot flags by default.


> Make the dot extend/refresh functions take state flags as an optional parameter instead of using the action's snapshot\_flags. This makes sense because the state-snapshotting behavior of a refresh event tends to depend on what spell causes it, not what spell is being refreshed.


> Improvements to Ice Floes. Needs some exclusion code.


> Priest: Move minimal interval mechanic to priest\_action\_t and fix it's
> debug output.


> Priest:
> Remove Dark Archangel.
> Use priest\_action\_t for inner will modifications.


> Make quiet actions actually be quiet.


> Make action\_t::player casts static casts instead of debug-casts.
> Move player-class targetdata class into the player-class.
> Add 

&lt;class&gt;

_action\_t for some classes_


> Make sure the talent string is recreated in the proper format before reporting happens.


> Call virtual player\_t::create\_options() after a player was created and
> not in the constructor.


> sc\_sim.cpp parse\_player: Fix pet parsing
> Priest: use static\_cast in p(), call create\_options() in
> priest\_pet\_t::priest\_pet\_t.


> Non-harmful pre-combat spell\_base\_t now have zero tick-time .


> The old touch of chaos melee swing mechanic is still in. Rename it to "melee" to avoid confusion.


> PRIEST: Use talent\_override based off number of targets.


> Change jinyu\_potion to jade\_serpent\_potion.
> Set SVN properties on the 463 mage profiles.


> Glyph of Ice Lance should not apply a base damage multiplier


> Jinyu potion renamed to Jade Serpent


> Skeletal beginnings of Ice Floes; don't really know how to do the rest


> Arcane should suck a lot less now that arcane charges are multiplying damage correctly


> Support Glyph of Mana Gem (increases charges to 10). More messing with Mage profiles.


> Mage: Mana gem, use sim\_t::range function.


> Tweak Priest profiles for AoE.
> Doesn't use the talent swap feature yet.


> Enable the new MoP special scaling category.


> Changing Mage profiles to a nrace without Mage bonuses until profiles are stabilized; then can reselect optimal race per spec.


> Remove check\_talent() from Mage spells


> Prevent the hellfire self-damage from being applied as damage to the target.


> Properly pick up mana costs per second from the DBC for channeled warlock spells.


> Whitelist Druid Treant pet spell.


> DBC: Add another cost per second field to spellpower\_data\_t.


> Turns out drain soul costs twice as much per tick as you'd think.


> Drain Soul is now much better than Malefic Grasp throughout the fight - seems like they just forgot to nerf DS.


> action\_t: Delay spell\_data\_t::not\_found error reporting until execute(), to prevent things like actions+=/talentX,if=talent.talentX.enabled from causing an error.


> Add new player option talent\_override, which takes the name of a talent and enables it, disabling the currently-enabled talent of the same tier if needed.


> Grimoire of Sacrifice changed. It is now the optimal Affliction talent for single target, while Demonology is back to using Grimoire of Service.


> Remaining warlock changes from latest beta patch.


  * Whitelist Tier 14 item set id's.
  * Add Priest Tier 14 set bonuses
  * Update Priest module for 15799.


> Hunter: Activate module. All three specs and no-spec simulate fine with
> default action lists now.


> Druid: Fix Fae Empowerment


> Minor fixes: Fix Tear Armor spell id and delete flaming arrow (it's from T12).


> Mage 463 profile improvements


> Build number needs bumping too.


> Initialized most(all?) spells and effects, cleaned up profiles a little, and got the hunter profiles to sim.


> Slight improvement to demonology action list.


> DBC data from build 15799, plus some updated warlock mechanics from same.


> Tweaks to Mage profiles


> Hunter: Add test profiles.


> Create a new action flag, quiet, which will prevent the action from showing up in the sample action sequence and from being counted as an executed foreground action. It will also cause the quiet flag to be set on the action's stats object.


> Support actors who have absolutely no action list.


> Don't execute actions that have background = true, even if they're in the foreground\_action\_list. This allows more dynamic background-ing of actions, and is necessary for execute\_pet\_action to work in its current form.


> Buff Creators:
> Move buff\_t**operator from buff\_creator\_basics\_t to buff\_creator\_t.**


> Some improvements to Mage profiles; further changes on hold until Rune of Power regen checked out.


> Cleaner fix for Frost Bomb


> Add placeholder action: mage\_bomb -- casts whichever bomb is found in talent spec


> This should fix Frost Bomb's hasted cooldown.


> Renaming Frost Bomb explosion functions for better report viewing.


> Fix for Frost Bomb primary target damage. Secondary target damage currently disabled.


> Add support for some Primal Diamonds


> Some items added to the item database.


> Fix Hunter compile errors.


> Druid
> > Fae Empowerment: Get buff spells from the specialization spell instead of hardcoded spellid



> Druid
> > Fae Empowerment: Now with spelldata
> > Balance action list tweaks to new eclipse gain mechanic
> > preplan\_mushrooms now makes you start with wild\_mushroom -> max\_stack() mushrooms



> Start adding MoP pet support. Redo compilation fix. Continuing cleanups.


> Make the hunter module compile.


> Hunter: Minor code cleanup.


> Hunter: Remove unused variables.


> Hunter: Small cosmetic changes.


> Hunter: Move hunter\_td\_t into hunter\_t. Add typedef for hunter\_t and
> hunter\_pet\_t base.


> Deletion of dead cata-code.


> Start MoP conversion:
> - move/add/delete talents and spells into MoP talents, spec-spells, glyphs etc.
> - rename "cast()" to "p()" and follow that style throughout
> - move Thrill of the Hunt to apply to all mana-costing attacks


> Minor optimization.


> Remove superfluous get\_target\_data() from action\_t::create\_expression() - it's done on demand now.


> Remove superfluous void ray from demonology single target action list.


> No sense in continuing the sim if a player has a buff expression referring to an unknown buff.


> Make buff/debuff expressions fully dynamic- and multi-target friendly. Kill the custom target\_haunt\_remains expression, since it's no longer needed.


> Allow expressions on the form target.targetnumber.foo.bar.


> Merge the target\_number action option into the old target option, using dynamic numerical targeting if the option is specified as a number and the traditional static targeting otherwise.
## SimC 501-8
  * General
    * Beta build 15781 DBC data.
    * Partial support for Jade Spirit enchant.
    * Rename lightweave embroideries according to new skill-based rank numbers and add rank 3.
    * Consolidate and Update Ignite-Like mechanic. So far implemented for Ignite, Piercing Shots, Blackout Kick and Echo of Light.
  * Monk
    * Implemented Tiger Strikes.
    * Energizing Brew
  * Priest
    * Added Divine Star.
    * Mind Spike / SW:Insanity remove dots without delay, including DP.
    * Update Chakra mechanic
    * Bring Back Serendipity and Surge of Light
    * Kill the old Spirit Shell implementation
    * Strength of Soul is once again a passive disc spell.
    * Beta Build 15781:
      * Implement PW: Solace and SW: Insanity
      * DP: Remove heal on impact
      * Change Archangel to specialization spell
      * Adjust new SW:D
      * Adjust Mind Spike
  * Mage
    * Implement Frost Bomb's haste scaling.
## SimC 501-7
  * General
    * Add 1% crit depression per target level difference
  * Monk
    * Implement BoK, RSK, FoF, Tigereye Brew, Tiger Palm,, Windwalker Mastery.
  * Shaman
    * Implement Ascendance
    * Add AoE profiles
  * Priest
    * Implement Cascade and Halo
  * Warlock
    * Dots triggered by SB:SoC or Soul Swap should not cost mana.
    * Implement SB: SoC as a separate spell, since dot can run parallel to normal SoC.
    * SB:SoC explosion doesn't refund a shard.
## SimC 501-6
  * General:
    * Beta Build 15762 DBC Data.
    * Added Player Base stats 85-90 for Priest, Warlock, Hunter
    * Remove helm enchants.
    * Add the Undead Racial: Touch of the Grave.
  * Priest
    * Rework Shadow Word:Death backlash.
  * Druid
    * Heart of the Wild now also increases Stamina.
  * Warlock
    * Use spell data value when determining the duration of grimoire of service summons.
    * Build 15762
      * Update agony for latest build.
      * Conflagrate glyph change.
      * Conflagrate still has a cooldown, even though it is not in the spell data anymore.
      * Soul Fire costs 160 fury now, down from 200.
  * Code changes:
    * Update the buff\_creator system to allow derived buff\_creators ( eg. stat\_buff\_creator\_t ) to directly modify basic parameters like .chance(), to shorten the whole interface.
    * Create a base called priest\_action\_t containing things common to priest\_spell\_t, priest\_heal\_t and priest\_absorb\_t. Same for monks, hunters and death knights.
    * Undead Racial: Touch of the Grave required adding a callback type, direct harmful spells. (i.e. Mind Blast procs it, casting a pure DoT spell doesn't. Devouring Plague does because it has a direct part, but SW:P doesn't despite it having tick\_zero).
## SimC 501-5
  * General
    * Don't execute off gcd actions while the actor is channeling.
  * Priest
    * Build 15752:
      * Mind Flay critical strikes no longer reduce fiend cooldown.
      * Devouring Plague healing component reworked.
  * Warlock
    * Implement Archimonde's Vengeance.
    * Implement Kil'Jaeden's Cunning (only the passive is supported for now).
    * Turn touch of chaos into a proper action, auto-attack style, instead of automatically enabling it whenever meta is up.
    * Implement Demonic Rebirth. All warlock specs' mp5 now scales with haste.
    * Turns out warlock pet melee base weapon damage exactly matches the warlock spell scaling coefficient for a given level.
    * Add confirmed warlock base mp5 for level 90, plus approximation for all other levels.
    * Buffed the UA spell power coefficient ( 0.2 -> 0.4 ).
    * Don't let the felguard continue felstorming after he's been sacrificed.
    * Optimal single target DPS for demonology involves grimoire of sacrifice on cooldown and then re-summoning the felguard.
    * Rain of fire damage was cut in half for destruction.
## SimC 501-4
  * General
    * Patch 15739 DBC data.
    * Fix in\_flight and in\_flight\_to\_target expressions, keep track of all current travel events.
    * Add a "target\_number" action option, which works like cycle\_targets but only selects a single target from the list of possible targets. Target number 1 is always the player's main\_target.
    * Callbacks that aren't specifically for harmful spells should actually be triggered for non-harmful spells as well.
    * Add a new proc type, OnDamageHealSpellCast, which reflects mechanics described in tooltips as "your healing and damaging spells". Fix a bunch of old procs which were OnSpellCast but should be OnHarmfulSpellCast or OnDamageHealSpellCast.
  * Priest
    * Devouring Plague's DD can proc DTR but when it does it has 0 orbs to use so it does 0 dmg and the DoT now does 0 dmg.
    * The direct dmg part of Devouring Plague can now crit.
    * Tweak Shadowy App damage numbers.
  * Druid
    * Astral Communion: cast time does not scale with haste.
    * Implement Bear Form additional haste/crit bonus from gear.
    * Primal Fury now only grants an additional combo point from single-target combo moves.
  * Shaman
    * Implement Flurry additional haste bonus from gear.
  * Warlock
    * Ensure that seeds of corruption can explode as a result of their own last tick.
    * Soulburn: Seed of Corruption no longer has a cooldown.
    * Seed of Corruption apparently can't proc the DTR.
    * Corruption triggered from Soulburn:SoC can proc things like DTR.
    * Add whiplash.
    * Use Drain Life coefficient from tooltips.
    * Soulburn pet summons have a shared cooldown.
    * Implement glyph of soul swap, and add support for soul swapping seed of corruption.
    * Implement havoc and flames of xoroth.
    * Implement fel armor passive.
    * Fix pet scaling with orc racial.
    * Pet special abilities can no longer be put on autocast, so remove them from their action lists. They now have to be explicitly used in the warlock's own action list. Executing pet actions are now off gcd.
    * The HoG damage itself is also aoe, not just the triggered shadowflame.
    * Make grimoire of service share a cooldown across all demons.
    * implement harvest life and use it in demonology aoe action list.
    * Beta Build 15739 :
      * Soul Leech now also works with Haunt.
      * Nightfall had the 5 times a minute cap removed.
      * Undocumented destruction changes: Immolate now has a 100% chance to generate an ember upon critical strike. Rain of Fire chance to generate an ember is down to 25%.
## SimC 501-3
  * Beta build 15726 data
  * Warlock
    * Life Tap amount now depends on max health
    * Mastery: Emberstorm now increases the effectiveness of Burning Ember consuming spells by 24%, down from 53%.
    * Fire and Brimstone spells don't cost mana.
  * Priest
    * Mind Blast: Generate Shadow Orbs only on hit
    * Shadow Orbs are now also generated by Shadow Word: Death.
  * Druid
    * Incarnation: King of the Jungle now also removes the positional requirement of Ravage.
    * Pounce no longer requires prowling.
    * Glyph of Savagery (New) Savage Roar can now be used with 0 combo points, resulting in a 12 sec duration.
    * Astral Communion (New) Commune with the sun and moon, gaining 20 Lunar or Solar energy every 1 sec for 5 sec. Generates the power type most beneficial to you. 5 sec cast (Channeled).
## SimC 501-2
## SimC 501-1
    * Beta build #1, classes/specs supported: **Shadow Priest**, **All Warlock**, **Enhancement Shaman**, **Elemental Shaman**, **Balance Druid**, **Feral Druid**, **Retribution Paladin**
    * **IMPORTANT**: This release is targeted at level **85** characters only. Higher or lower level characters are unlikely to have the correct stats and most level 90 talents are not yet implemented.
    * Support for MoP Beta build 15689
    * Druid
      * Add "preplant\_mushrooms" option to set the number of shrooms planted on the ground out of combat
      * Add "initial\_eclipse" option to set the amount of eclipse energy on the profile out of combat
    * Paladin
      * Add "seal.**seal\_name**" expression
    * Priest
      * Add "initial\_shadow\_orbs" option to specify the out-of-combat shadow orb count
      * Make use of the chain=1,interrupt=1 option for Mind Flay.
      * **Current Issues / Untested stuff / Unimplemented features**
        * Level 86 to 90 stats.
        * Level 90 talents.
        * Most non-dps increasing talents are not yet implemented.
        * Healing isn't updated yet, nor are Disc or Holy DPS
    * Shaman
      * Add "eoe\_chance" option to specify the Echo of the Elements proc chance in percents
      * **Current issues / Untested stuff / Unimplemented features**
        * Earth Elemental scaling
        * Feral Spirits scaling
        * Level 87 spell, Level 90 talents
        * Echo of the Elements may use a slightly incorrect damage resolution mechanism
        * Ability damage range and multiplier verification in game
    * Warlock
      * Add "cancel\_metamorphosis" action
    * General
      * Downloading profiles form armory, chardev and wowhead work. Talents are currently not used from the profiles, instead the sim currently enforces a "default talents" for each spec. Specialization is determined from the talents of the downloaded profile.
      * Generic bloodlust trigger has been changed to start 5 seconds into the fight (from target\_health\*25%)
      * Cataclysm Flasks / Food / Potions, Mists of Pandaria Flasks and Potions currently supported
      * Add support for pre-combat actions, adding option "precombat=1" in an action list removes the action from normal priority rotation, and uses it just before combat begins for the actor. Any "precombat=1" actions will automatically put the actor into combat after all of the pre-combat actions are executed.
      * Consolidate raid buffs into generic buffs/debuffs (also usable in expressions):
        * attack\_haste (5% attack haste)
        * attack\_power\_multiplier (10% ap multiplier)
        * critical\_strike (5% critical strike chance)
        * mastery (x mastery rating)
        * spell\_haste (5% spell haste)
        * spell\_power\_multiplier (10% sp multiplier)
        * str\_agi\_int (5% stat)
        * stamina (10% stamina)
        * magic\_vulnerability (debuff, +5% magic damage taken)
        * mortal\_wounds (debuff, -25% healing, _unused/unsupported_)
        * weakened\_armor (debuff, -4% armor, 3 stacks)
        * weakened\_blows (debuff, -10% physical damage)
        * physical\_vulnerability (debuff, +4% physical damage taken)
        * ranged\_vulnerability (debuff, +5% ranged attack damage taken)
        * slowed\_casting (debuff, -50% cast speed, _unused/unsupported_)
    * Data sources
      * Remove "armory\_throttle" feature
    * Options
      * Add a **very experimental** "ready\_trigger" option to change the simulator to run event based triggering on actor ready state, instead of polling. This is currently only supported by Shamans, and it will have negative-to-no effect on pure spell casting DPS classes.
      * Add a "spec" option to profiles, indicating the selected specialization of the actor
      * Add "separated\_rng" option
      * Option "deterministic\_roll" is now "deterministic\_rng"
      * Unify the syntax of armory, guild, wowhead, chardev and wowreforge options
      * Add "chain" option to actions, which will cause channeled spells to automatically be recast immediately following their second-to-last tick unless actions higher up in the priority list are ready
      * Add "combat" option to snapshot\_stats, setting it to 0 will disable snapshot\_stats entering the actor into combat (defaults to 1, i.e., the actor will go into combat when snapshot\_stats is executed)
      * Add "report\_raid\_summary" option to force the raid summary to appear in the html report
      * Deprecate option "bloodlust", use "buff.bloodlust.react" expression instead
      * Deprecate option "haste<", use "spell\_haste" or "attack\_haste" expression instead
      * Deprecate option "health\_percentage<" and "health\_percentage>", use "target.health.pct" expression instead
      * Deprecate options "invulnerable", "vulnerable", "not\_flying", "flying", use "target.debuff.xx" instead, where xx is one of "invulnerable", "vulnerable", or "flying"
      * Deprecate options "time**", "time**", use "time" expression instead
      * Deprecate option "travel\_speed", use expression "travel\_speed" instead
      * Add a **very experimental** "cycle\_targets" action option which causes it to attempt to execute on each available target in turn instead of just the main target. This is suitable for multi-dotting, for example: "/corruption,cycle\_targets=1,if=!ticking" will keep corruption up on all available targets.
    * Expressions
      * Change player resource expressions to "**resource**.regen", "**resource**.time\_to\_max",  "**resource**.max", "**resource**.deficit", "**resource**.max\_nonproc", and "**resource**.pct"
      * Add player resource expression "**resource**.net\_regen", returning (resource.gained -  resource.lost) / elapsed\_time
      * Add player resource expression "**resource**.pct\_nonproc"
      * Add dot expressions "spell\_power", "attack\_power, "haste\_pct", and "multiplier" which return the amount of respective stat the actor had during the last application, refresh or extension of the dot. Note that this expression only works for stateless actions.
      * Add dot expression "current\_ticks", returning the current number of ticks the applied dot has (based on the previous application, refresh or extension)
      * Add dot expression "n\_ticks", returning the current number of ticks the actor would receive for the dot (with the actor's current haste level)
      * Add action.**name**.enabled, returning true if your profile (class/spec) can use the action
      * Add glyph.**name**.enabled, returning true if your profile uses the glyph
      * Add talent.**name**.enabled, returning true if your profile has selected the talent
      * Add spell.**name**.exists to check if simc has the spell exists in the spell database
      * Add dot expression "new\_tick\_time", returning the tick time of a dot/channeled spell with the actor's current haste level
      * Add "charges" expression to return the number of charges for an action
      * Add "max\_charges" expresion to return the maximum number of charges for an action
      * Add "recharge\_time" expression to return the time it takes a charge to recharge
      * Add "max\_stack" expression for buffs/debuffs/auras
      * Add "tick\_multiplier" action expression that returns the **current** tick multiplier for the action if it was applied at the moment
      * Add "cooldown\_react" action expression. Returns true if the reaction time for the action cooldown has elapsed, or is zero. Reaction time is initiated by an abrupt reset of the cooldown period.
    * Spell query
      * Spell query now accepts an optional actor level option, specified by adding a "@**level**" suffix to the spell query
      * Add replacement spell information to spell\_query output
      * Support multiple Power types per spell in spell\_query output
      * Support arbitrary number of effects in spell\_query output
    * Reporting
      * Separate spell data reporting from basic action/buff information
      * Print resource per second gain/loss for all resources
      * Add tracking of a new statistic, portion\_apse, and use it in the DPS Sources chart, to avoid over-representing the contributions of non-permanent pets
    * **Bug fixes**
      * Quote player names in saved profiles to allow spaces
      * Fix a bug with "restart\_sequence" action, resolving a locked sequence problem in certain rare cases

# Wow 4.3.3
## SimC 433-3
## SimC 433-2
  * Rogue
    * Register Deadly Poison on the target to be used in expressions
  * Shaman
    * Fix a bugs with <85 default action list.
## SimC 433-1
  * Chardev: Quote Player Names in profiles
  * Hunter
    * Explosive Shot ticks proc Sic'Em
# WoW 4.3.2
## SimC 432-2
  * Fix broken num\_ticks calculation for hasted dots - it wasn't rounding tick frequency to nearest millisecond
  * Death Knight
    * Update Blood Actions
  * Hunter
    * Update BIS profiles with the new actions from 4.3.2 changes
    * Fix broken pet imports because of another banner
  * Mage
    * Move Molten Fury, Invocation, Arcane Power, and Mana Adept to affecting all damage, not just the mage's
  * Paladin
    * Ancient Fury uses spell power, not attack, and doesn't inherit player's crit
  * Rogue
    * Update Legendary Daggers modeling to latest knowledge
  * GUI
    * Add option for toggling report\_pets\_separately
  * Items
    * Vial of Shadows and Cunning of the Cruel have been updated to reflect the new damage/ICDs
  * Other
    * Scaling Stats: tanks inherit all attack scaling stats
    * Target/Enemy: Enable tank-aoeing of auto\_attack/spell\_nuke, change default action list to hit all tanks

## SimC 432-1
**All PTR changes are in effect**, meaning the PTR option is once again disabled
_(Note: Vial of Shadows hasn't yet been updated as we're waiting to find out the new ICD)_

  * Death Knight
    * Fixed an issue introduced in [r10709](https://code.google.com/p/SimulationCraft/source/detail?r=10709) where all specs were benefiting from a 30 second Outbreak, which should only apply to blood
    * Update Rune Strike to only be used after a dodge/parry or when in Blood Presence
    * Update Blood actions
  * Druid
    * T13 4pc caster now increases Starsurge's damage by 10%
  * Hunter
    * Explosive Shot now uses variable dot base damage
    * Lock and Load no longer affects Arcane Shot
    * Default actions updated:
      * Use Arcane Shot during Lock and Load if needed
      * Black Arrow is now used for single target
  * Mage
    * Updated ignite mechanics to better match what we see in-game
  * Rogues
    * Further optimizations to subtlety rogues attacking from the front
  * Shaman
    * Elemental Precision only affects Fire, Frost, and Nature damage
    * Fix Bottled Wishes FE sync
  * Warrior
    * Heroic Leap was not inheriting crit properly
    * Update Heroic Leap to only be used when CS is up
    * Update SMF actions
    * Tier 13 melee 4pc was still tied to Raging Blow at 13%, when it should be a 6% proc chance on BT
    * Update Arms priority
    * Update Arms profile
  * GUI
    * Add Movement Fight Styles to GUI
    * Adjust LightMovement to use relative begin/end times
  * Items
    * Correctly identify use\_item actions for sharing on-use cooldowns
  * Other
    * Fix a possible crash with Spell Query
    * Make raid events start ten milliseconds into the encounter at the earliest, to ensure pre-combat actions go off before actors are stunned
    * DPS Error Chart: Change delta step for the normal distribution calculation
  * Reporting
    * Add option `separate_stats_by_actions` to separate stats by actions by appending their marker (the character found in the action priority list)

# Wow 4.3.0
## SimC 430-8
  * Fixes a bug that made it into 430-7 that causes issues with many classes

## SimC 430-7
  * Lastest PTR support for build 15201
  * Death Knight
    * Death Strike always consumes runes
  * Druid
    * Tweak Starfall usage
  * Hunter
    * Lock and Load wasn't being properly consumed by Arcane Shot
    * Black Arrow/Explosive Trap weren't always resetting the CD of ES
    * Multi-shot no longer consumes Bombardment
    * Vishanka only crits for 150% on live
    * Proc reporting for when BA/ES are off CD, but can't be used due to lack of focus
    * SV action list tweaks
  * Paladin
    * Update T13H Retribution profile
  * Priest
    * min\_inteval option is now available to all heals and now actually does something
    * New option of `no_dmg` for Mindflay
  * Shaman
    * Earthquake now properly ignores armor
  * Warlock
    * Doomguard now properly scales with haste
  * Warrior
    * Cleave, Execute, and Heroic Strike no longer trigger effects of the OH weapon
    * Heroic Leap
      * Can be used on all bosses, without losing melee time apparently, so remove the ranged position requirement
      * Added to the default action list for non-tanks
      * Can not be dodged or parried
    * SMF Action list updates
    * T13H SMF profile updates
  * Action Lists Expressions
    * `floor()` and `ciel()` are now able to be used in the expression system
    * `flying` and `no_flying` options have been added for action lists to be used with the new flying raid event
    * `postion_front` and `position_back` are able to be used in the expression system
  * Items
    * Pure casters get their innate crit damage bonus applied to discharge procs, hybrids don't
  * Other
    * Enemy targets will no longer hit each other
    * Fix some problems with creating adds and their player\_type
    * The default enemy should now attack all players with the role of `tank` in the sim
    * Fix a crash that occurred when using spell\_query built with MSVC
    * Fix stat/reforge plots so they once again show the charts
  * Raid Events
    * New `Flying` raid event has been added
      * Currently affects: Consecration, DnD, and the Hand of Guldan debuff
    * Events are now predictable, unless otherwise specified (default cooldown\_stddev=0 and no random variance on the first event)
  * Ultraxion Fight Style
    * Now includes a flying raid event so ground effects do no damage
    * Tweaks have been made to the raid events themselves to better mirror the actual fight
    * Feral, Rogue, Unholy, and Retribution action lists have been updated to work properly with this fight style

## SimC 430-6
  * Latest PTR support for build 15171
  * Dark Intent was not properly triggering on the correct actor when it was specified
  * Scaling and reforge plots now work with healing
  * Fix a possible crash when using the stun raid event
  * Priest
    * min\_interval option works for all heals now

## SimC 430-5
  * PTR support for 4.3.2 is enabled
  * Classes
    * Death Knight
      * Unholy T13H profile was using an extra gem
      * Death and Decay is properly spread to all targets
      * Howling Blast now hits all target for the proper amounts and applies Frost Fever when glyphed
      * Pestilence has been added, but needs further testing to see if it matches how it functions in-game
      * Butchery was granting RP even when you didn't have the talent
    * Druid
      * Fix Lifebloom working in expressions
      * Add basic Restoration actions
      * Restoration druids are now set to the healing role by default
      * PTR: Caster 4pc increases Starsurge by 10%
    * Hunter
      * Ignore another banner that was preventing pet import
      * PTR
        * Bombardment no longer has a charge
        * LnL no longer affects Arcane Shot
    * Paladin
      * Holy paladins are now set to the healing role by default
    * Priest
      * Fix Mind Spike clearing dots correctly
    * Shaman
      * Add Tier 13 Restoration 4 piece bonus
      * Glyph of Lava Burst does affect it's overload
    * Warrior
      * Improved Slam should reduce the cast time of Slam...
      * Slam's cast time should be decreased by haste
      * Flag Bloodthirst, Cleave, Execute, Heroic Leap, Heroic Strike, and Thunder Clap as proc\_ignores\_slot so they will successfully proc Gurth/Souldrinker when it's in the OH
      * Cleave was not benefiting from racial expertise
      * Add a basic implementation of Heroic Leap
  * Items
    * DTR-copied DD spells have the same travel time as the original spell
    * Gurthalak
      * Use the correct value for the heroic tick damage
      * Now support up to ten spawns at once
      * Handles DWing better
    * Add a proc\_ignores\_slot flag, to allow certain abilities to trigger weapon based procs from either slot, Gurthalak, No'Kaled, and Souldrinker all use these
  * GUI
    * Add Heal/Tank role options
    * Add Ultraxion fight style option, complete with stuns, etc!
    * Add step/amount options for Stat Plots and Reforge Plots
  * Other
    * BCP API: Report remote errors to the user.
    * Fix some spells not being parsed correctly
    * You can now use if=target.NAME.EXPRESSION
    * Dots that tick immediately (Rend, Explosive Shot, etc.) now properly tick immediately upon refresh or reapplication, instead of adding another tick

## SimC 430-4
  * Dots are now able to be cast on multiple targets, see [r10723](https://code.google.com/p/SimulationCraft/source/detail?r=10723)/[r10728](https://code.google.com/p/SimulationCraft/source/detail?r=10728) for more details
  * AoE effects (cleave, etc) now hit multiple targets again
  * Classes
    * Death Knight
      * Blood receives a 30 second CD reduction on Outbreak
      * Update actions to sync Berserking with Unholy Frenzy
    * Mage
      * Fix a possible crash when using Combustion
    * Paladin
      * Avenging Wrath, Communion's 2%, and Inquisition all affect all damage done by the paladin, not just the paladin's (eg Gurthalak)
      * Update Ret and Prot's action list
    * Shaman
      * Added AoE abilities and support, see [r10728](https://code.google.com/p/SimulationCraft/source/detail?r=10728)
      * Update Elemental's FS usage in the action list
      * Added support for Flame Shock spreading through Improved Lava Lash talent
    * Warrior
      * Update Arms action list
      * Update Arms T13H profile
      * Flag Berserker Rage as "use\_off\_gcd=1" for Fury/Prot
      * Berserker Rage properly increases rage gained from damage while active
  * Expressions:
    * Add pet.X.remains
    * Added sim., self., target., and others, see [r10723](https://code.google.com/p/SimulationCraft/source/detail?r=10723)/[r10728](https://code.google.com/p/SimulationCraft/source/detail?r=10728) for details
  * GUI
    * Revert back to QT 4.7.4 due to a lot of issues using 4.8
  * Items
    * Gurthalak updates, see [r10695](https://code.google.com/p/SimulationCraft/source/detail?r=10695)
    * Rathrak's ticks do not increase with haste
    * Windward Heart's ICD is now 20 seconds
  * Other
    * Fix a crash with the stun raid event
    * Fix a logic failure in raid\_event\_t::start()
    * Auras are now reported with player buffs, instead of in their own section

## SimC 430-3
  * Classes
    * Death Knight
      * Fix a bug when using Blood-caked Blade
      * T13 2pc proc 2 stack is overwritten by a normal proc 1 stack
      * Fix unholy ghoul crit rating to refresh along with player crit changes
      * Necrotic Strike is now available to use (healing effect not modeled)
    * Druid
      * Feral action list update
      * Feral/Moonkin damage talents that affect all damage done, now properly increase all damage (trinkets, etc)
    * Hunter
      * Fix a bug where importing pets was failing due to the new Christmas banner
    * Mage
      * Mirror images now spawn at the same distance as the owner
      * Slightly adjust unglyphed Mirror Image rotation
      * Better reporting on Mirror Image damage per usage
      * Hot Streaked Pyroblasts can now only be cast when you have Hot Streak
    * Paladin
      * Censure: Remove hotfixed 40% damage double dip ( now included in the dbc )
      * Merge Consecration stats -> DPET reported
    * Priest
      * HW:Sanctuary: Implement instant-spell behaviour ( IW, Mental Agility )
      * Add min\_interval= option for heals
      * Properly implement T13 2pc healing bonus
      * Update action lists
    * Rogue
      * Subtlety action list updates
      * Tricks of the Trade was not properly consuming energy when unglyphed
    * Shaman
      * Juggle around damage multipliers so they affect all damage. Very minor concrete effect in dps.
      * Unleash Wind cannot be dodged or parried, and may proc no'kaled.
      * T13 profile updates
      * Windfury cannot proc any item derived On-equip procs
    * Warlock
      * Dark Intent now also increases attack haste
      * Action list updates
    * Warrior
      * Opportunity Strikes once again trigger Deep Wounds
      * Truly fix the bug with Inner Rage granting it's benefit 100% of the time
  * Items
    * Changed Fury of the Beast ICD from 45 to 55s.
    * Adjust Shard of Woe for all schools
    * Kiril, Fury of Beasts should grant Agility and trigger off all melee hits
    * Hack to detect LFR items when using the local item DB
  * Other
    * Change aura\_delay from 150ms to 500ms, affects munching/rolling of Ignite, Deep Wounds, Piercing Shots
    * Vengeance: Don't decay for 10% if the target has been hit ( even for 0 damage )
    * Filter missing weapon error messages for quiet players
    * Add position\_switch raid event to switch back/ranged\_back to front/ranged\_front and back again
    * T11 profiles have been dropped
    * Make the progress bar in GUI function properly with any combination of (simulating, scaling, plotting and reforging)
    * Inform the user about what are being reforged in the progress bar
    * Update for the latest version of CharDev
    * Update to using QT 4.8.0 for the GUI

## SimC 430-2
  * Classes
    * Death Knight
      * Frozen Heart increases ALL frost damage done by the DK, not just it's own abilities
    * Hunter
      * T13 4pc ICD changed to 105 seconds from 45
      * Profiles
        * Glyphs were accidentally left out of the SV profile
        * MM's ring should have been reforge exp->crit not mastery->crit
        * Update all T13 profiles to use the Woodchucker scope
        * SV action list tweaked, see [r10526](https://code.google.com/p/SimulationCraft/source/detail?r=10526)
    * Mage
      * Flame Orb, Frostfire Orb, and Living Bomb's explosions don't trigger ignite
      * Profiles
        * Update Frost action list when the player has 4pc T13
    * Priest
      * Profiles
        * Smite profile now casts PWS every 15 seconds instead of 12
    * Rogue
      * Fix a bug causing T13 2pc to have 100% uptime
      * Fix a bug causing Tricks of the Trade applying 100% uptime to it's target
      * Fix a bug in Tricks of the Trade giving it's buff to the proper target
      * Fangs of the Father MH also increases Revealing Strike's damage
    * Shaman
      * Elemental Overload spells can proc the DTR
      * Profiles
        * Add the T13 4pc logic to the action list, instead of being hidden in the code when generating the profile
    * Warrior
      * Deep Wounds no longer benefits from Precision
      * Fix a bug where Inner Rage's benefit was applying 100% of the time
      * Rend damage calculation was missing a parenthesis, increases scaling damage by 50%
      * Strikes of Opportunities is considered a proc in-game and does not proc DW, etc.
      * Profiles
        * Arms profile was using Fury glyphs, oops
        * Add better reforging to the Arms profile
        * Update Inner Rage usage to account for T13 2pc
        * Update profiles to use Gurthalak
        * Update Arms/Fury to make use of 'off\_gcd'
    * Warlock
      * Hand of Guldan can miss again
  * GUI
    * Scaling - Add armor option
  * Items
    * Flintlocke's Woodchucker can no longer crit
    * Gurthalak is now simming as casting 3-4 mind flays per spawn
    * Rathrak ticks can crit
    * Souldrinker is like No'Kaled in that only attacks from the hand wielding the weapon can trigger it
    * Vial of Shadows
      * Scales with AP, not SP
      * Can now be dodged and parried
    * Vishanka
      * ICD changed to 15 seconds from 2
      * Can no longer miss
  * Other
    * Add support for "real" off-gcd actions. Specifying use\_off\_gcd=1 on an action will cause the action to be checked also during GCD periods, if it usable.
    * Live Build 15050 DBC Data
    * Goblin 1% racial haste affects swing/shoot/cast speed only
    * Make wait\_for\_cooldown honor the ability usable\_moving() so we don't get into hairy situations with raid events
    * Make movement/stun/invulnerable raid events put players into combat, to prevent infinite loops of non-harmful actions with gcd=0 fixes a lot of crashes with raid events
    * Reforge Plots has an updated graph, now with error bars
    * Stoneskin no longer increases armor by 10%, but reduces damage taken by 10%

## Simc 430-1
  * The PTR option is once again disabled
  * Death Knight
    * Festering Strike extends dots by 8 seconds, not by 6
    * Fix a bug with rune.cooldown\_remains checking the wrong rune
    * Fix a bug where T13 2pc was using T13 4pc's proc chance (25/40 instead of 30/60)
    * Update profiles
  * Druid
    * Update Balance default actions
    * Update Balance profiles
    * Add support for insect\_swarm/moonfire/stafire/sunfire(2/3) for multi-dotting simming
    * Add preliminary T13H profiles
  * Expressions
    * Add new if=prev.ACTION\_NAME to compare against the previous action performed
  * Guardians
    * Take spell power multipliers into account when snapshotting SP for guardians
  * GUI
    * The T13 profiles we have show up in the BIS tab
  * Hunter
    * Add preliminary T13H profiles
  * HTML Report
    * Use the latest version of jQuery, resolves a lot of issues
    * Fix a bug with Froststrom school
  * Items
    * Add scaling coefficients to bone link fetish and cunning of the cruel
    * Add Bone-Link Fetish's AoE
    * Add ICD's to Ti'tahk and Rathrak
    * Enable crits for Rathrak.
    * No'Kaled was triggering from either hand, when it only triggers from the hand that the weapon is in
    * Using Tryande's Doll would sometimes crash the sim
    * DTR was nerfed from 4.2.2, except for Moonkins/Warlocks, currently using 2/3 of the 4.2.2 value
    * Add Vishanka, Jaws of the Earth, assuming a 2 second ICD for now
  * Mage
    * Change usage of Arcane Torrent for Arcane
    * Fix Dragon's Breath glyph applying as 30 seconds instead of 3
    * Add preliminary T13H profiles
  * Paladin
    * Add T12 2pc for Protection
    * Add preliminary T13H profiles
  * Pets
    * Pets benefit from the 3% damage buff
  * Rogue
    * Update Assassination action list
    * Add preliminary T13H profiles
    * Add Fangs of the Fathers
      * Buff names are legendary\_daggers\_pX
      * Implemented with the following assumptions:
        * 100% chance to trigger stacking buff, but 2.5 second ICD
        * No ICD on Fury of the Destroyer
        * Each P3 stacking buff over 30 gives 5% chance to trigger FotD
  * Shaman
    * Update action lists
  * Warlock
    * Add T13 profiles
    * Take spell power multiplier into account when calculating burning embers cap.
    * Update action lists
  * Warrior
    * Add preliminary T13H profiles

# Wow 4.2.2
## Simc 422-6
  * Latest PTR changes and updates
  * Action List Expressions
    * Fix a discrepancy between dot expiration and the "remains" expression
    * The "temporary\_bonus" expression now takes into account attribute multipliers
  * Death Knight
    * Army of the Dead and Pet Ghouls don't gain increased energy regeneration from haste
    * Gargoyle Strike has a minimum GCD of 1.5, resulting in 16-17 casts per Gargoyle
    * Updated action lists for Frost and Unholy
  * GUI
    * Focus Magic is no longer checked on by default
  * Items
    * Added support for Ti'tahk, the Steps of Time on equip effect
    * More accurate modeling for No'Kaled, the Elements of Death
    * Vial of Shadow's damage scales with AP
    * More accurate ICDs for various trinkets [r10318](https://code.google.com/p/SimulationCraft/source/detail?r=10318)
  * Mage
    * DTR Proc rate tweaked to 12.5% from 13%
    * Frost now uses Frostbolt as it's filler all the time
  * Priest
    * Fix detection of T13 set bonuses, since Healing/Shadow sets share the same item name for chest/shoulders
  * Professions
    * Bonuses from Mining and Skinning were not working correctly
  * Racials
    * Berserking was changed in 4.2 to provide true haste, increasing energy regen, etc.
  * Rogue
    * Tricks of the Trade will default to the Rogue automatically if another target is not specified, assuming trading with another Rogue
  * Scale Factors
    * Fix a crash that would occur with a very specific set of conditions
  * Shaman
    * Added T13 Profiles
    * Changes to the default action list for Elemental
    * Fixed the interaction between DTR and Fulmination
    * Better interaction when using SWG with the GoUL
    * Nerf T12 2PC Elemental bonus to it's current state [r10276](https://code.google.com/p/SimulationCraft/source/detail?r=10276)
    * Chain Lightning was not proccing DTR
    * Fire Elemental modeling updated [r10277](https://code.google.com/p/SimulationCraft/source/detail?r=10277)
  * Warlock
    * Demon Armor is now usable
    * Drain Life now heals the warlock
  * Wowhead
    * Fix the Origin ID string when saving profiles

## Simc 422-5
  * Latest PTR changes
  * More accurate DTR modeling has been enabled, with actual spells being cloned, etc.
  * Bug Fixes
    * Death Knight
      * Gargoyle's strike can crit
      * Pillar of Frost wasn't consuming a rune if it was the very first action executed in the sim
    * Hunter
      * Piercing Shots wasn't benefiting from bleed damage increases
    * Paladin
      * Avenging Wrath wasn't benefiting heals
      * Seal of Insight was returning the wrong amount of mana
    * Shaman
      * Using Spiritwalker's Grace would sometimes cause a crash
    * Warlock
      * Burning Embers doesn't proc Wrath of Tarecgosa.
  * Updates
    * Death Knight
      * DRW's spells now match their counterparts
      * Rune Abilties now show you the specific ability that granted RP
      * Unholy Blight's modeling was updated to closer match live
    * Paladin
      * Most Holy Paladin talents were added/updated
      * Most Prot Paladin abilities/talents are now supported
    * Warlock
      * Demonology now uses incinerate filler if bane talent is not found

## Simc 422-4
  * Latest PTR changes
  * Bug Fixes
    * Exclude targets from raid heal/damage
    * Some secondary spells have the wrong level required in the DBC files, so now only the primary class spells are checked
    * The Stun raid event would sometimes crash the sim
    * Druid
      * Fix Primal Fury triggering
    * Paladin
      * Divine Favor's buff actually increase crit/haste now
      * Lay on Hands actually heals now
    * Warlock
      * Felstorm's damage was being reported incorrectly
      * Felstorm's damage was using the incorrect coefficient
    * Warrior
      * Bloodthirst's heal is now modeled, meaning it'll proc hurricane, etc
      * Fix a logic error that was always applying the spec passives
      * Fix Inner Rage's minimum level required
      * Fix Shattering Throw damage
      * Fix Shattering Throw's debuff having an infinite duration
  * Updates
    * Added healing information to the text output
    * Average Item Level is now reported on the HTML report for a player
    * Added most 4.3 Trinkets
    * Druid
      * Add Frenzied Regeneration action
      * Add Benefits of Nature's Swiftness
      * Add Leader of the Pack health/mana gains
      * Update Restoration mastery to Harmony mechanics
    * Priest
      * Add Guardian Spirit action
      * Add Pain Suppression action
    * Paladin
      * Add Divine Protection action
      * Add Divine Shield action
      * Add Holy Shock (heal) action
      * Add Glyph of Seal of Insight
      * Add Talents: Conviction, Daybreak, Enlightened Judgements, Infusion of Light, Paragon of Virtue
      * Divinity now increases healing taken
    * Warrior
      * Add Demoralizing Shout action
      * Add Retaliation action
      * Add Sunder Armor action
      * Add Bloodthirst heal
    * Hunter
      * Min/Max values for Kill Command

## Simc 422-3
  * Support for PTR build 14849
  * Bug Fixes
    * Couple of fixes to the text based report
    * Apparatus of Khaz'Goroth grants 2875 STR not 2865
    * Death Knight
      * Razorice damage doesn't benefit from the Razorice debuff
      * Fix to Razorice's base damage done
    * Druid
      * Wild Growth was checking the wrong talent to see if you had it
    * Mage
      * Arcane Potency was being consumed incorrectly
      * Combustion ticks can't proc DTR, Ignite's can
    * Priest
      * Fix crash when a Holy Priest cast PoH
      * Veiled Shadows and T12 2pc were not always applying correctly to the Shadowfiend's cooldown
    * Warlock
      * Fix Burning Ember's cap
  * Updates
    * Lots of fixes for those adventurous enough to build x64
    * You can generate a XML based report once again
    * Added 2pc PVP set bonuses
    * Use a 45 sec ICD for Mithril Stopwatch instead of 50
    * DTR Modeling
      * Updated Elemental and Balance actions with better DTR modelling
    * HTML Report
      * HPS ranking
      * Some charts have been moved around based on feedback
      * You can now click on the bars in the raid DPS chart to go to that player's breakdown
    * Death Knight
      * Updates to the T12H profiles
      * Frost actions updated
    * Druid
      * Update Balance T12H profiles
    * Hunter
      * Change Pet base crit to 5%
      * Update T12H profiles
      * Add T13N profiles
    * Paladin
      * T12 profiles no longer use items that don't exist in-game
    * Rogue
      * Combat profile updated
    * Warlock
      * T12H profiles updated
      * More accurate DTR proc rates

## Simc 422-2
  * Latest support for PTR build 14971
  * Tier 13 DPS set bonuses are all supported when using the PTR
  * Bug Fixes
    * The sim no longer crashes when an invalid flask is chosen
    * Ability breakdown in the text output shows the proper DPS again
    * Death Knight
      * Rime only procs off MH Obliterate
    * Warrior
      * Deep wounds benefits from 4% physical damage debuff
      * Precision affects deep wounds
      * Fix a crash when running without T12 2pc
      * Rend's damage wasn't being calculated appropriately
  * Updates
    * Buffs will now show the up-time at specific stacks automatically
    * DPS error chart improvements
    * Scaling by inverse hit/expertise for dual wield classes
    * When downloading a guild a 'raid\_summary.simc' file will automatically be generated that will run all downloaded members
    * Warlock
      * Improvements to Demo's default action list
      * Drain Life is properly benefiting from Soulburn again
      * Pets don't benefit from DI or FM cast on the owner
    * Warrior
      * Improvements to Arms' default action list

## Simc 422-1
  * Updated the DBC files to use 4.2.2 data
  * PTR has again been disabled
  * Bug Fixes
    * Fixed a bug introduced in 420-9 showing the wrong percentage breakdown of an ability
    * Fixed a bug crashing the sim that was affecting a few users
    * Hunter
      * Rabid Power can now stack up to 5 times
      * Hunters were reporting an extra 1200 agility for their character when using Tol'vir Potion
      * Sic'em was increasing the cost of Claw instead of decreasing
      * Fervor shouldn't trigger a GCD
  * Updates
    * Add scaling\_lag\_error and other statistic improvements
    * Add Damage Taken per Second chart
    * Add sim option confidence=x, default=0.95
    * GUI
      * Updates to the buff/debuff listings
    * Hunter
      * Update BM action lists

# Wow 4.2.0

## Simc 420-9
  * Bug Fixes
    * Lifeblood doesn't have a lockout cooldown with on use items
    * Fix +50 mastery rating to shield and +FR to cloak
    * Death Knight
      * Howling Blast is using Spell Crit
    * Mage
      * Fix Frostfire Orb Explosion
    * Priest
      * Train of Thought now uses RNG for 1/2 and properly lowers the cooldown on Penance
  * Updates
    * Added Stats Timeline Charts
    * Added Deaths Distribution Charts
    * Added Time Spent Charts
    * Add [Wowreforge.com](http://wowreforge.com/) profile imports ( wowreforge=`<profile`> ). Note that wowreforge currently does not support Engineering tinkers.
    * Improve mana/health calculation for players with less than 20 int/str
    * Paladin
      * 40% Censure Hotfix
    * Warrior
      * Prot warrior action list updates

## Simc 420-8
  * Support for Mac OS 10.5 has been dropped as well as power pc platform support from the command line client
  * Bug Fixes
    * Updated Strength to Parry formula
    * Fix an operator precedence issue with expressions
    * DK
      * Blood Boil is now usable even without runes while Crimson Scourge is active. Before, it was free but required runes to activate.
    * Mage
      * Choosing an invalid Focus Magic target won't crash the sim
    * Warlock
      * Fix Shadowflame dot detection, fixes Fel Hunter's Shadow Bite damage
    * Warrior
      * Fix a possible crash with Tier12 2 piece tank bonus.
  * Updates
    * Speedup calculation of error statistics during post-simulation processing. Should VERY noticeably reduce the runtime of simulations with high iterations.
    * Added options cache\_players and cache\_items to control exactly when the simulator will and will not use cached information.
    * Scale factor rankings
    * save\_talent\_str option to append the primary tree to the character name upon import
    * Various improvements to the speed of the simulator
    * Support for multiple action lists see [r9502](https://code.google.com/p/SimulationCraft/source/detail?r=9502)
    * Support for downloading glyphs, items, gems from BCP API (Note that general item download is disabled until Blizzard provides socket bonuses)
    * Better reporting of simulation settings in the HTML reports
    * Add tracking of temporary stat bonuses, use expression "temporary\_bonus.STAT".
    * Change DPS/DPSE Calculation to a average of a random sample over each iterated fight instead of composite\_damage / composite\_time, thus removing a bias toward the longer fights.
    * VPLC was hotfixed to increase its damage and proc chance
    * Mage
      * New action list logic for Arcane using choose\_rotation again
    * Shaman
      * Update Elemental profiles

## Simc 420-7
  * Bug Fixes
    * Hunter
      * Fix import from Battle.Net issue

## Simc 420-6
  * Bug Fixes
    * DTR has been added to the item db
    * Various maximum mana issues fixed
    * Disable old queuing code by default, leading to decrease in DPS for all profiles
    * Death Knight
      * Blood Boil should consume the Crimson Scourge buff
    * Druid
      * Insect Swarm was not gaining the 100% crit damage bonus from Moonfury
      * Lunar Shower was proccing even without the talent
      * Moonfire now generates eclipse energy based on the direction the bar is going
      * Fixed Starfire to not generate extra energy during Eclipse due to Tier12 4 piece bonus
      * Heart of the Wild does not affect base intellect
    * Hunter
      * Flaming Arrow shouldn't break Improved Steady Shot
      * Fix a crash with the Tailspin pet ability
    * Mage
      * FFB ticks don't roll the crit bonus from shatter
      * PoM was benefiting from an extra charge of Arcane Potency and not invoking a GCD for the PoMed action
    * Options
      * The override for 'expose\_armor' was incorrectly implemented as 'expode\_armor'
    * Paladin
      * Paladins enter a fight with zero Holy Power
    * Priest
      * Make sure we don't apply Empowered Shadows if we have no Orbs up to consume
      * Mind Spike should consume dots
    * Warlock
      * Summoning an Inferno or Doomguard was incorrectly consuming Soulburn
  * Updates
    * Added warnings for players when trying to use a variety of profession only benefits without the profession
    * Added support for the Eternal Shadowspirit Meta gem
    * Legendary items were mislabeled as Artifacts
    * Death knights, paladins, and warriors no longer receive any bonus to their chance to dodge from Agility
    * Players can now specify their position (front/back)
    * PTR mode has again been enabled for the release of the latest PTR
    * Resource charts are now generated for all resources
    * Added support for PvP set bonus detection to the sim
    * Death Knight
      * Added resource statistics for rune regeneration, blood tap, and runic empowerment
      * Track percentage of time spent at RP cap
    * Druid
      * Tier12 4 piece bonus is now affected by Euphoria
      * Update Balance's default action list
    * Hunter
      * Update default pet talents
    * Mage
      * Add PvP set bonuses
      * Presence of Mind is now treated as it is in-game, an action triggering a buff
    * Paladin
      * Add override option for PVP gloves
      * Implement Holy Shield
      * Track wasted AoW and DP procs
      * Update Protection and Retribution's default action list
    * Priest
      * Update Shadow's default action list
    * Rogue
      * Update Subtlety's default actions
      * Profile updates
    * Shaman
      * ~~Totems have been redesigned in the sim allowing new expressions concerning totems. See [r9292](https://code.google.com/p/SimulationCraft/source/detail?r=9292) for more details.~~
      * Default Action List tweaks
      * Add an expiration delay to Unleash Flame buff, allowing certain action priority lists to cast Lava Burst and Flame Shock so that both benefit form the Unleash Flame buff. The current default delay for the expiration is 300ms, with a standard deviation of 50ms. The new parameters "uf\_expiration\_delay" and "uf\_expiration\_delay\_stddev" control the delay.
    * Warlock
      * Profile updates
      * Update Destruction and Demonology's default action list
    * Warrior
      * Add support for T12 2pc for tanks
      * Update Arms' default action list

## Simc 420-5
  * Bug Fixes
    * When calculating the number of dot ticks gained due to haste, it appears Blizzard uses banker's rounding (round to nearest even integer). This fixes the sim being +/- a few haste rating for the correct break points for an extra tick
    * Europe added another banner, breaking profile importing in the GUI
    * Sorrowsong has a 100% chance to proc
    * Damage done by "direct-tick" spells (Arcane Missiles, Flame Orb, Consecration, Penance, etc.) is now reported as ticks instead of direct hits. These spells should now correctly report miss/crit percentages.
    * Death Knights
      * Morbidity was not applying correctly to DnD
      * Blood Plague crits for 2.06 not 2.09 with the meta
    * Hunter
      * Kill Shot's coefficient and base damage is amplified by the weapon multiplier
      * Aimed Shot's base damage is also amplified by the weapon multiplier
    * Paladin
      * Ret GOTAK would explode at the end of the sim, even if it wasn't up
      * Auto Attack and Censure weren't properly benefiting from haste
      * Fix base attack power being off by 20
      * Consecration's cooldown was not being properly set
    * Priest
      * Penance was double dipping in the Glyph of Penance
      * Fix Lightwell ticks
      * You can't summon a shadowfiend when you already have one active
    * Shaman
      * Fix Chain Lightning Elemental Overload chance
    * Warlock
      * Update Demo Profiles
  * Updates
    * wait\_until\_ready can now take an expression
    * Switch to using the new Blizzard API where possible
    * Unheeded Warning was hot-fixed
    * Death Knights
      * Update Frost actions to use Oblit when you have either 2F or 2U
    * Druid
      * Feral stopped using Unheeded Warning
      * Update Moonkin actions
    * Hunter
      * Update pet base attack numbers
    * Mage
      * Mage Armor now ticks every 5 seconds instead of being based on periodicity
      * Update profiles and Arcane default actions
    * Reporting
      * Improved reporting on spells that call other spells e.g. Prayer of Healing and Glyph of Prayer of Healing
      * Swing speed is now displayed
      * Fix the display of 'role' (dps/heal/tank)
      * Display the characters thumbnail in the report when available
    * Paladin
      * Remove the T12 2pc bug for Ret that no longer happens in-game
      * Update Ret profile
    * Priest
      * Use the delayed buff mechanic for Evangelism
      * Buff "chakra\_serenity\_crit" is now "serenity"
      * Add Holy Profiles
    * Warrior
      * Fury 1H profiles had four extra gems

## Simc 420-4
  * Bug Fixes
    * Dots that tick immediately were losing a tick when being refreshed
    * Dwyer's caber cooldown seems to be around 50s
    * Essence of the Eternal Flame has a 60 sec CD not 120
    * Fix for wowreforge urls when the server name had non-latin1 characters in it
    * Clean up loot rank urls
    * Time\_to\_die was returning the wrong value in multi-player sims sometimes
    * Weapon speed deltas will now show up in the report
    * Enchants
      * Hurricane and Power Torrent are now properly being triggered by heals
    * GUI
      * Fix some history load bugs, preventing scaling, plotting and reforge plotting to restore the correct values
    * Hunter
      * Hunter pet's inherit their owner's infinite focus
    * Mage
      * Flame Orb now properly triggers the Arcane Missiles buff
    * Plotting
      * Fix an issue when plotting 6+ stats
    * Priest
      * Fix bug in Divine Aegis introduced in 420-3
      * SW:D receives a 300% multiplier on targets below 25% regardless of the glyph being present
      * Atonement heals now "borrow" the execution time and mana consumption of the triggering spell, so that they have meaningful HPET and HPR in reports
  * Updates
    * Optimized sequence actions, resulting in very significant speedups for Arcane mages especially
    * Added support for an aura delay when proccing buffs to match in-game, see [r9151](https://code.google.com/p/SimulationCraft/source/detail?r=9151) for details
    * Added mana\_pct\_nonproc and max\_mana\_nonproc variables for use in action lists
    * Matrix Restabilizer now has a unique buff for each of its stats
    * Profiles now save any enchant\_STAT that were used
    * Death Knights
      * Updates to the Ghoul/AoTD
    * GUI
      * Add a drop-down for target level
      * Allow only 2 or 3 stats to be reforge plotted to avoid pointless simulating
    * Hunter
      * Update MM action lists
    * Mage
      * Arcane and Frost action list updates
    * Paladin
      * Action list updates
    * Priest
      * Improvements to Holy
      * New option for dispersion low\_mana
      * Profile updates
    * Rawr
      * Parse professions
    * Rogue
      * Add Fan of Knives
    * Shaman
      * Elemental profiles updated
      * Shamanism was hotfixed
    * Wowhead
      * Add random suffix, tinkers, and reforge support

## Simc 420-3
  * Bug Fixes
    * Fix tw region Battle.net parsing
    * Fix JSON parsing to allow unknown pets
    * Force Burning metagem crit\_multiplier to 1.0 for healing spells
    * Add a resource type for Clearcasting effects so they appear in the correct chart
    * Fix an encoding issue on some profiles
    * Correct armor values for 85/86 targets
    * Items
      * Fix heroic Necromantic Focus giving the wrong amount of stats
    * Hunter
      * Fix Sic'em/Wild Hunt interaction on Claw's cost
    * Mage
      * Evocation does not in fact take 6 seconds to cast
      * Mana Cost of Arcane Blast at 0 stacks corrected
      * Focus Magic feedback procs should now be livelike
      * Can't use PoM while AP is up
    * Priest
      * Fix Evangelism so it's decreasing the cost of spells, not increasing
      * Fix how Cauterizing Flames works to match in-game
      * Prevent PWS from being cast on targets with the weakened soul debuff, unless the 'ignore\_debuff' option is specified
      * Penance will heal the target, not always the caster
      * Holy Archangel increases healing by 3% per stack of Evangelism, instead of simply 3% regardless of stack size.
    * Warlock
      * Imp no longer double dips to it's glyph and orc racial
      * Dark Intent is not a harmful spell
      * Add Master Summoner's effect on summoning cost
  * Updates
    * Simulationcraft event system heavily optimized, resulting in 10%+ speedups in simulation for all, and significantly more for (temporary) pet-heavy profiles
    * Remove "big\_hitbox" option, Blizzard has fixed it
    * During reforge plotting, tell what stat the sim is currently reforging
    * Add "Rocket Barrage" racial
    * Raid Events
      * New heal raid event
      * Change damage/heal distribution from normal to uniform.
    * Items
      * Add 45 second ICD to Eye of Blazing Power and allow it to benefit from healing modifiers
    * Druid
      * Improve Feral action list
    * Mage
      * Updated Arcane priority list
      * Updated profiles
    * Priest
      * Lots of reporting updates to the healing report
    * Shaman
      * Add a delay of 950ms (with a 250ms standard deviation) to windfury procs to better model in game behavior
      * Add options "wf\_delay" and "wf\_delay\_stddev" to alter the amount of the Windfury proc delay in seconds.
      * Add a 300ms standard deviation to Windfury ICD
      * ~~Add an expiration delay to Unleash Flame buff, allowing certain action priority lists to cast Lava Burst and Flame Shock so that both benefit form the Unleash Flame buff. The current default delay for the expiration is 300ms, with a standard deviation of 50ms. The new parameters "uf\_expiration\_delay" and "uf\_expiration\_delay\_stddev" control the delay.~~
    * Warlock
      * Minor tweaks to BIS profiles
## Simc 420-2
  * Bug Fixes
    * Tweak enchant on\_use policy to fix some issues
    * Fix modify\_action not affecting html report and saved profiles
    * Fix Battle.net import for the korean region
    * Fix urls when pasting text to GUI, now all urls will be decoded before passed to the proper importation engine (Chardev.org, Battle.net)
    * Ensure that overrides.dark\_intent=1 enables feedback properly
    * target\_level and target\_race sim options are back, override values for all targets found in the target\_list
    * Druid
      * Fix Typhoon damage parsing
    * Shaman
      * Fix Stormstrike dodge calculation
    * Priest
      * PoH DA set to 30% non-crit, 60% crit
      * Disabled PoM DA
      * Atonement Crits cap at 150% normal cap
      * Grace correctly uses it's stack number
  * Updates
    * Update Battle.net pet parsing
    * Add "World Lag" setting to GUI
    * Force "C" locale in both command line and GUI clients. This should fix some string formatting issues.
    * Add 64 bit compilation to CLI makefile for Windows
    * Add an experimental "cast\_delay" action expression. Simulates a "decision", that may cause casting a spell at opportune time to fail. Currently causes a mean of ~600 milliseconds of delay on top of the cast time (including GCD) of the previously finished, player executed action
      * Add profile level options brain\_lag and brain\_lag\_stddev which control the normal-distribution delay activated by cast\_delay
    * Add a player specific "world\_lag" (default 100ms) and "world\_lag\_stddev" (default 10% of world\_lag) options to simulate the in game equivalent. World lag is used to extend ability cooldowns, if the ability has one. Actor executable abilities with cooldowns require a client-server communication to happen before the cooldowns starts in the client, which takes a world\_lag amount of time.
    * Make sure override.dark\_intent=1 enables feedback properly
    * Items
      * Add some missing 4.2 items to local item database
      * Apparatus of Khazgoroth appears to have been hotfixed on Live 4.2 to do about 1.66x the amount per stack and ensure that Judgements, Hammer of Wrath and other Paladin abilities can proc it
      * Normal version Necromantic Focus only does 39 Mastery per stack not 42. Assuming Heroic is 45
    * Hunter
      * Update Marksman Hunter "BiS" profiles
    * Priest
      * Update profiles to remove impossible items
      * Add an experimental support for simplistic "double dotting system" and add example profiles for it
    * Shaman
      * New modeling for Fire Elemental, resulting in significant DPS gains. Need information on Fire Blast and Fire Nova cooldown ranges, and distribution
      * Add Maelstrom Weapon stack usage to reports under "Procs" heading
      * Allow both hits of Stormstrike a chance to proc Static Shock
      * Various "BiS" profile tweaks
    * Warlock
      * Update Doomguard simulation model
      * Various "BiS" profile tweaks
      * Remove impossible items from profiles
    * Warrior
      * Implement Blood and Thunder
## Simc 420-1
  * Bug fixes
    * Hunter: Add Munching&Rolling to Piercing Shots
    * Hunter: Fix Bug on Piercing Shots, set td\_multiplier to 1.0
    * Hunter: Let's use mail belts and feet!
    * Hunter: Fixed action list to reflect careful aim to nerf to 90%
    * Moonwell Chalice is 1700 Mastery on use, not Intellect
    * Warrior: Unholy Frenzy benefits from Unshackled Fury.
    * Shaman: Fire Elemental spells benefit from spell power debuff on target.
  * Updates
    * GUI: Show T12 BiS profiles in the GUI.
    * 4.2.0 is now the default. Remove all the PTR stuff.
    * Remove the 4.1.0 Tier 11 Profiles.
    * Balance Druid profile tweaks
    * Shaman: Simplify default action lists slightly. Reorganize swing reset/clipping for enhancement, should be "more proper" behavior now. Functionality for patchwerk fights is identical.
    * Removed the AfflDrain Warlock profiles.
    * Tweaked Subtlety Rogue action list and gear.
    * Tweaked Arms Warrior profiles.
    * Tweaked Fury Warrior profiles.
    * Tweaked Feral Druid profile.
    * Add fire\_elemental and earth\_elemental buffs purely so that we can see their uptimes. Both check ->up() off their execute()'s.
    * Remove Dispersion,moving=1 from Shadow Priest action lists.
    * Shaman: Don't eat Unleash Wind charges for clipped swings due to hard casting. Don't use Unleash Elements in Elemental profiles with Glyph of Unleashed Lightning.
    * Add attribute matching to spell query. Anything but equality comparison may result in weird behavior. Comparison operator is the attribute bit number.
    * Added Hunter and DK T12N profiles.
    * Implement Druid Tier12 2pc Heal
    * Add .simc files for comparing warlock tier bonuses.
    * Always override the default name for an item when generating via id with a random suffix.
    * Add Raid\_T12H\_DTR.simc
    * Reaction Time: Change Distribution a little bit, expected value should be 0.65s
    * Infinite\_Resource: Moved from sim to player; allow negative resource amounts with infinite\_resource=true
    * Priest Heal profiles updated
    * Added Target\_Death\_Pct for [issue 712](https://code.google.com/p/SimulationCraft/issues/detail?id=712)
    * More tweaks to Shaman profiles and action lists.
    * Small action list tweak for Retadins.
    * Fire elemental received 1.5% base melee crit, hurrah. Allow fire\_elemental\_totem action to be expressable by our system. Change action lists to accommodate for the change.
    * Implement Valanyr
    * Adds the parameter "type" to damage\_event\_t, allowing the user to specify a damage type other than holy.


# Wow 4.1.0
## Simc 410-13
  * Bug fixes
    * Reports: Plot lines should line up properly on the x-axis
    * Mage: Remove Pyroblast glyph effect from the hot\_streak\_crit() value of Pyroblast.
    * Mage: hot\_streak\_crit() should apparently only be using player\_crit.
    * A bunch of issues fixed.
    * direct\_tick "dots" will no longer trigger tick\_callbacks
    * Warlock: Hand of Gul'dan and Chaos Bolt may not miss.
    * Don't crash if we don't have a weapon equipped.
    * Don't allow discharge type procs to proc from themselves etc.
    * set DOT\_REFRESH for Rip.
    * Create a snapshot() call in schedule\_travel() that records total\_crit(), haste() and p->composite\_mastery() so that we can reference them later. The mastery snapshot was used to fix [Issue #552](https://code.google.com/p/SimulationCraft/issues/detail?id=#552) with Combustion.
  * Updates
    * PTR: DBC Data updated to Build 14333.
    * PTR: All PTR Patch Notes have been implemented.
    * PTR: All Tier 12 set bonuses now implemented.
    * PTR: All 4.2.0 trinkets now implemented.
    * PTR: All specs now have Tier 12 Heroic profiles added. Most have T12 Normal profiles too. Note that: the Heroic profiles assume that all of the non-Heroic items can be upgraded to 391, the legendary isn't currently included, the Normal profiles disallow **any** item that requires killing a Heroic boss from either Tier 11 or Tier 12. Note that BM and SV Hunter profiles are currently just cut&paste jobs of the MM profiles. Hopefully they'll be updated soon.
    * PTR: A number of classes had their action lists improved.
    * PTR: Implemented support for the Legendary proc. The proc rates still need to be determined via testing once 4.2.0 goes live.
    * Sim OH weapon speed when appropriate
    * All Tier 10 support has been removed.
    * Minimum itemlevel extracted from the client files is now ilvl 318. Maximum is 410.
    * Scaling: Add scale\_expertise/crit/hit/mastery\_iterations options
    * If ptr=1 is set ptr.wowhead.com will come before www.wowhead.com when searching for items (both are behind the localdb by default).
    * Naming conventions for profiles has changed.
    * ICD on Lightweave Embroidery was hot-nerfed to 64sec. Proc rate seems unchanged.
    * Some improvements have been made to how we model reaction time. Check [r8774](https://code.google.com/p/SimulationCraft/source/detail?r=8774) for the initial implementation.
    * Callbacks added for heals and absorbs.
    * Per the wiki, queue\_lag is unaffected by latency, and channel\_lag is equal to double latency. Fixed analyze\_lag() to reflect this.


## Simc 410-12
  * Bug fixes
    * International Battle.net is displaying anothern nonsense banner before letting us import characters. Someone needs to figure out a generic way to bypass this stuff.
    * Fix a bug that was preventing PI and Essence of the Red from stacking when it should have been PI and Hero
    * PTR
      * Shaman: Enhancement tier 12 4 piece bonus does not affect searing/magma totem.
      * Balance Druid T12 4pc applies after Euphoria from my testing.
      * Don't look in the DBC entry for Aftermath when determining ISF's cooldown (there's no cooldown now).
  * Updates
    * The default source for item data is now the local database. Only if it can't find the item in the local database will it move onto wowhead, and mmo-champion etc.
    * "Examples" tab in the GUI is gone, replaced by "Help" tab, pointing to our starters guide.
    * GUI has gained an option to define the order of item data sources for the simulator.
    * Add support for Corruption: Absolute from the Cho'gall Encounter
    * Death Knight
      * Update 2H Unholy Profile. Fixes [Issue 677](https://code.google.com/p/SimulationCraft/issues/detail?id=677)
      * Added procs to record what Killing Machine was used on for DK's.
    * Added an ability\_lag and ability\_lag\_stddev to action\_t which is defined an ability will use instead of the other sorts.
    * PTR
      * PTR Build 14265 DBC Data
      * Whitelisted Tier 12 set bonus spells
      * Implemented the announced changes for DK's, Druids and Paladins.
      * Add support for Death Knight Tier 12 4pc.
      * Support Jaws of Defeat trinket with a new Cost Reduction type of item effect.
      * Add support for Variable Pulse Lightning Capacitor.
      * Mage, Balance Druid and Warlock Tier 12 2pc set bonuses. For now using lag values of 0.74 avg and 0.62/2 stddev.


## Simc 410-11
  * Bug fixes
    * Fix Battle.net importing for Windows GUI EU users
    * Paladin
      * Hand of Light double dibs in CoE
      * Hand of Light shouldn't double dip in other target debuffs, just CoE
    * Warlock
      * Guardians do not scale with metamorphosis, but do gain their own demonic pact.
    * Round maximum weapon damage up in item database. Matches in-game.
  * Updates
    * ~~Add "Safety Catch Removal Kit" enchant with 88 (ranged) haste rating~~
    * PTR: Initial implementation of 4.2 trinkets
    * Add OnSpellDirectCrit and OnSpellTickCrit, and change current OnSpellCrit to be both.
    * Display
      * Show - instead of 0.0000 in scale factor grid in multi-player HTML report, for improved readability.
    * PTR: PTR Build 14241 DBC Data
    * Remove some overrides now that the PTR DBC is updated
    * Warrior
      * Add an Arms profile that doesn't charge
    * MAC
      * Add XCode 4 project for simulationcraft, requires OS X 10.6 and an Intel machine (no PPC support anymore). Uses LLVM 2.0 backend, does not use sparkle. Consider this an experimental way to build Simulationcraft for OS X.

## Simc 410-10
  * Bug fixes
  * Updates
    * wowhead have been changing their format yet again.

## Simc 410-9
  * Bug fixes
  * Updates
    * Various wowhead data format updates, preventing proper item parsing
    * Local item database can now be composed of client data and cache files
    * Latest Patch Note Changes on PTR
    * Hunter
      * Update the shoulder enchants on the 359 profiles
    * Shaman
      * Add Tier 12 set bonuses for Elemental and Enhancement
      * Add Glyph of Unleashed Lightning
      * Change Lava Lash damage calculation based on Elitistjerks discussion
    * Warlock
      * Immolation Aura is now called by 'immolation\_aura'
    * Warrior
      * Report the 2% Crit Rampage gives

## Simc 410-8
  * Bug fixes
    * Fix parsing of Glyph of the Ascetic Crusader when importing from Rawr
    * Druid
      * Fix 359 profile from using a 372 ring
    * EU Battle.net presents some nice banner (once) for every http query done to the page, messing up every single armory import.
  * Updates
    * PTR: DBC Data for build 14133
    * Druid
      * PTR: Update default actions based off tier 12
    * Mage
      * Flame Orb ticks don't trigger ignite
    * Warlock
      * Make Felhunter the default Demonology pet
      * Drain Life hotfix nerf
      * Clean up default action lists for affliction.
    * Warrior
      * Update Arms actions to use OP more often

## Simc 410-7
  * Bug fixes
  * Updates
    * Support changes in (EU) Battle.net format
    * Warrior: Update Arms profiles with better stance dancing

## Simc 410-6
  * Bug fixes
    * Druid: Fix assertion with Symbiosis/Harmony.
  * Updates

## Simc 410-5
  * Bug fixes
    * General
      * Fix command line client output to honor ptr argument
    * Warrior
      * Remove Glyph of Colossus Smash error
  * Updates
    * General
      * PTR: 14107 DBC data imported
      * Support changes in (US) Battle.net format
    * Players
      * Tanks scale with Expertise
    * Druid
      * PTR: Lunar Shower now has an additional effect: While you are under the effect of Lunar Shower, Moonfire generates 8 Solar Energy and Sunfire generates 8 Lunar Energy. Old change that made MF/SF/IS produce 8 eclipse energy seems to be reverted
      * PTR: Ferocious Bite energy change implemented
      * PTR: Strength only grants 1 AP on the PTR
      * PTR: Glyph of Ferocious Bite change implemented
    * Paladin
      * Add support for Grand Crusader generating HOPO
      * Prot paladins scale with Strength
    * Warlock
      * Implement imp glyph/racial bug introduced in 4.1.



## Simc 410-4
  * Bug fixes
    * Hunter
      * Shots were incorrectly costing 0 focus
      * T12 4pc should only trigger when you're wearing the set
  * Updates
    * GUI
      * Added additional options for iterations
    * Warlock
      * More reports are being generated automatically with a variety of information, see http://simulationcraft.org/
      * Remove stamina scaling, the effect is too small to be statistically significant for any reasonable number of iterations

## Simc 410-3
  * Bug fixes
    * General
      * Fix a crash in html reporting
      * Support the changed battle.net talent format.
    * Death Knight
      * Added dummy Glyph of Death Gate
    * Druid
      * Tweak the eclipse energy gain a bit, should behave exactly as ingame, where the direction stays neutral until you proc one eclipse.
    * Mage
      * Frostfire Orb can now trigger Brain Freeze.
    * Warlock
      * Fix Shadow and Flame's trigger
      * Fix the trigger on Incinerate
  * Updates
    * General
      * Added PTR Build 14002 data
      * Added Live Build 14007 data
      * Re-enabled PTR support
    * Death Knight
      * Updated Frost profiles
      * PTR: DK 2pc melee Tier 12 set bonus
    * Druid
      * PTR: Insect Swarm now generates 8 Lunar Energy for druids with Eclipse.
      * PTR: Moonfire now generates 8 Solar Power for druids with Eclipse.
      * PTR: Sunfire now generates 8 Lunar Energy for druids with Eclipse.
      * PTR: Balance 4 Pieces - While not in an Eclipse state, your Wrath generates 3 additional Lunar Energy and your Starfire generates 5 additional Solar Energy
      * PTR: Druid 4pc melee Tier 12 set bonus
    * Hunter
      * Update MM profiles per feedback
      * PTR: Hunter 4pc Tier 12 set bonus
    * Paladin
      * PTR: Paladin 4pc melee Tier 12 set bonus
    * Priest
      * PTR: Add Shadow Priest Tier 12 4pc Set Bonus.
      * PTR: Add initial guess of Shadow Priest Tier 12 2pc set bonus.
    * Warlock
      * Fix Demo profile from using three profession, switch to tailoring over enchanting
    * Warrior
      * Updated and fixed Arms Warrior profile
      * PTR: Tier 12 2pc melee set bonus

## Simc 410-2
  * Bug fixes
    * General
      * Add separate composite\_player\_XXX\_multiplier machinery for heals and absorbs. The 3% damage buff - not to mention Tricks of the Trade - should not be increasing heals and absorbs.
    * Spell Query
      * Fix an issue where the wrong class was sometimes chosen.
    * Druid
      * FB refreshing Rip actions are dependent on Blood in the Water
    * Priest
      * Grace on the target should buff only Priest heals, not all heals.
      * Update a Priest in-game bug with updated DI values.
    * Shaman
      * Fix a crash, caused by Enhancement profiles and certain types of raid events
  * Updates
    * General
      * Add Z50 Mana Gulper stub. Doesn't actually restore mana at present.
    * Priest
      * Update Healing 4pc set bonus to 4.1.0 mechanics
      * Shadowfiend crit bug in-game has been fixed.
    * Warrior
      * Add Glyph of Rapid Charge support.
      * Replace Glyph of Cleaving with Glyph of Rapid Charge for Arms profile
      * Replace healing Arms talent with Blitz for Arms profile

## Simc 410-1
  * Bug fixes
    * Fixed bug when SC\_USE\_PTR is not set.
    * Some Healing fixes to Druids and Priests from reia.
    * Spell query displayed energy/rage costs incorrectly
    * Priest
      * Fix for Surge of Light proc chance
    * Warlock
      * Guardians use snapshotted stats
      * Hopefully fix Doom Guard's Doom Bolt damage on PTR
  * Updates
    * Core
      * The first 4.1.0 Live release using Live Build 13914.
      * Added a big\_hitbox option to targets which if set to 1 (the default) means that the hitbox is large enough to be able to use abilities like Charge while in melee range.
    * Death Knight
      * Frost action list adjusted: higher priority on blood tap, unholy presence for DW
      * Frost profiles updated: 7/31/3 IBT spec for DW and 2H, more haste reforging on the DW profile
    * Druid
      * Full Restoration Tree support
    * Warlock
      * Update Affliction Drain profiles
    * Warriors
      * Arms: Modify action list and talents to see a 2000 DPS increase via some various improvements including using Charge on cooldown when big\_hitbox is set. Thanks to Bazinbear from Spinebreaker for these.
    * Misc: Removed the PTR conditionals and DBC includes from the build.

# Wow 4.0.6
## Simc 406-19
  * **Latest PTR support for all classes**
  * Bug fixes
    * Fix the DPS timeline
    * Fix a bug with target's health percentage
    * Players should no longer keel over and die when simulating raid damage
    * Fix a tooltip error on replenishment/attack haste in the GUI
    * Volcanic Potion grants Intellect not Spell Power
    * Change the division operator from / to % in action lists
    * Fix Loot Rank link for ranged weapon dps
    * Death Knight
      * Howling Blast is using melee crit
      * Pet special abilities were glancing
    * Priest
      * Power Word: Shield mana cost hotfix
      * Strength of Soul affects Heal, Flash Heal, and Greater Heal
    * Rogue
      * Rupture and Garrote don't proc Main Gauche
    * Warrior
      * Slam was incorrectly set to 145% weapon damage on live
  * Updates
    * New label= option to track specific action line usage
    * /mythical\_mana\_potion works like /mana\_potion
    * Support for essence of the red, override.essence\_of\_the\_red=1
    * Death Knight
      * Update Frost action list and profiles
    * Mage
      * Update profiles
## Simc 406-18
  * Bug fixes
    * Death Knights
      * Just kidding, KM really only does proc from auto attack
      * Refined Blood Strike disease multiplier to 18.75% instead of 19%.
  * Updates
## Simc 406-17
  * Bug fixes
    * Fix a crash with iterations=1
    * Death Knights
      * Fix a crash with auto attack
      * Killing Machine procs from all main hand attacks
    * Paladin
      * Judgement was not consuming mana
  * Updates
    * Mage
      * Update Frost profile
## Simc 406-16
  * Bug fixes
    * Fix interaction between self-movement and raid-movement events
    * Fix target gaining infinite\_RESOURCE as well as the player
    * Fix Blood/Night Elf import issue from battle.net
    * Death Knights
      * Rune of Razorice now properly increases frost damage taken
      * Fix NoCS interaction with OH attacks
      * Move Blood Tap higher up in the priority list to coincide with PoF use
      * KM was incorrectly interacting with IT
    * Hunter
      * Fix base attack power
    * Warrior
      * PTR: Mastery was not being decreased properly for Fury
  * Updates
    * A variety of statistical information has been added for normal runs and when calculating scale factors
    * Can now specify dps\_plot\_positive=1 to change the behavior of dps\_plot. Plots points from 0 to step\*points instead of -step\*points/2 to +step\*points/2
    * Death Knight
      * Unholy profile improvements
    * Mage
      * Improve Frost based profiles per user chardev suggestion
    * Shaman
      * Implement Earth Elemental Totem (and guardian), further damage testing needed.
## Simc 406-15
  * **Latest PTR support for all classes**
  * Bug fixes
    * Fix target health recalculation to converge properly
    * Support Cogwheels when importing
    * Death Knights
      * Add Orc racial to Army, Ghoul, and Gargoyle
  * Updates
    * Further updates to "**reforge\_plot**" including GUI interface
    * Generate new format for wowreforge optimizer link
    * Mage
      * Improve Arcane BIS profile
      * Allow customization of Water Elemental actions
    * Rogue
      * Improve Combat BIS profile
    * Priest
      * Separate Mind Blast reporting based upon number of Orbs present
## Simc 406-14
  * **Latest PTR support for all classes (13750)**
  * Bug fixes
    * Add duration to Darkglow- and Sword Guard Embroidery
    * Death Knight
      * Presence changes should consume all RP, not runes
      * Blood Strike is giving 19% per disease on live, not 12.5%
      * Fix Death and Decay base tick damage, allow Death and Decay to crit
      * Fix Dual Wielded Obliterate / Frost Strike / Plague Strike off-hand abilities
      * Fix Blood Plague and Frost Fever base tick damage
      * Fix Frost Fever crits to 200%
      * Fix Glyph of Frost Fever to be additive with Virulence
      * Fix Runic Corruption uptime tracking
      * Use DBC data for Gargoyle's strike
    * Hunter
      * Fix Wild Quiver
      * The Beast Within reduces the focus cost of spells, as well as attacks
      * Improved Steady Shot is only swing haste
    * Warlock
      * Glyph of Corruption does not proc from Drain Life ticks
    * Warrior
      * Stance changes weren't consuming rage
      * Changing stances causes 4P T11 DPS buff to drop
  * Updates
    * Add "dot.**name**.ticks\_remain" expression
    * Add "**reforge\_plot**" option to do simulation requested in [Issue 355](https://code.google.com/p/SimulationCraft/issues/detail?id=355)
      * reforge\_plot\_iterations allows the specification of iterations per step (defaults to sim iterations)
      * reforge\_plot\_step sets the amount of stat delta per reforge step
      * reforge\_plot\_amount specifies the amount of stat points to reforge
      * reforge\_plot\_stat defines the list of stats to reforge
      * reforge\_plot\_output\_file sets the output file name for the generated CSV data, defaults to stdout
      * reforge\_plot\_debug toggles the debug output per reforge step on or off
    * Change hasted\_num\_ticks() rounding to represent in-game testing at breakpoints
    * Death Knight
      * Tweak Frost default action list
      * Implement a better Ghoul modeling, still not perfect; update Ghoul expertise formula
      * Update Army of the Death attack values to be more accurate
      * Add "**rune**.cooldown\_remains" expression
      * Update 2H Unholy BIS Profile
    * Hunter
      * Implement improved pet parsing from Battle.net profiles and allow talentless pets in sim
    * Mage
      * Add ability to use Frost Armor
      * Change piercing ice stats reporting
      * Piercing Ice now affects Water Elemental crit rate (unverified)
      * Shatter affects target crit debuff
      * Combustion updates as per recent discussion
    * Priest
      * Added Atonement reporting
      * Holy fire dot triggers Atonement
    * Warlock
      * Affliction default action list tweaks
## Simc 406-13
  * Bug fixes
    * Death Knight
      * Presence was incorrectly never consuming a rune
      * Rime procs were incorrectly granting RP from rune abilities
    * Druid
      * Eclipse buff clears also clears at 0.
    * Hunter
      * Multi-shot will correctly trigger Wild Quiver
      * Fix bug in downloading Beast Master spec explicitly
    * Warrior
      * Stances correctly increase all damage done (including trinkets) now
  * Updates
    * Add http proxy support
      * syntax  : proxy=type,host,port
      * example : proxy=http,proxy.mywonderfulcorp.com,3128
      * example : proxy=http,10.120.45.2,8080
    * Druid
      * Action list update for dot refreshes for Moonkins
    * Hunter
      * Action List update for Explosion Shot
## Simc 406-12
  * Bug fixes
    * Fix HTML output header misalignment
    * Hunter
      * Lock and Load resets Explosive Shot cooldown
    * Druid
      * Fix various Eclipse related issues
    * Mage
      * Fix various Arcane related crashes
    * Warlock
      * Fix Shadow Mastery bug with PTR profiles
  * Updates
    * **Latest PTR support for all classes (13707)**
    * Beginnings of a "DPS range chart in raid summary (enable with report\_rng=1)
    * Include scale factor error in HTML reports
    * Mage
      * Evocation removed from Fire/Frost
      * Frost talent update
    * Warlock
      * Update Affliction default action lists slightly
## Simc 406-11
  * Bug fixes
    * Death Knight
      * Frost Strike Offhand does not generate runic power
      * Epidemic now uses proper ranks
    * Mage
      * Correct extra mana cost while Arcane Power is active
      * Flame Orb ticks now proc Master of Elements
    * Paladin
      * Correct management of Holy Power
    * Warrior
      * Raging Blow now includes racial expertise bonus
  * Updates
    * **Latest PTR support for all classes**
    * Death Knight
      * Split Runic Power gains from Frost Presence and Improved FP
    * Hunter
      * Improve Hunter profiles (scopes)
    * Mage
      * Improve Arcane default action priority list
    * Paladin
      * Change Holy Power into a normal resource instead of a buff
## Simc 406-9
  * Bug fixes
    * Death Knight
      * Fix race specific base stats
      * Fix Death Coil coefficient to match hot-fix
      * Fix base AP calculations
      * Runic Empowerment does not proc from OH Frost Strikes
  * Updates
    * **Latest PTR support for all classes**
    * Add convergence information on how error reduction relates to iterations
    * Add support for more PvP enchants
    * Add support for Lifeblood
    * Add death informations in html report
    * More performance improvements in generated HTML scripting
    * Death Knight
      * Improved default action lists
      * Add rune management reporting
    * Hunter
      * Add support for trap launching
      * Add AOE actions to default priority list
      * Improved default action lists
      * Improve BiS sets
    * Mage
      * Improve default action lists
## Simc 406-8
  * Bug fixes
    * Restrict Vengeance to > 0.
    * Death Knight
      * Might of the Frozen Wastes, doesn't affect spells
      * Rune Regeneration doesn't benefit from Icy Talons or Improved Icy Talons
      * Fix Runic Empowerment sometimes triggering the wrong rune
      * Attacks need to hit to trigger Runic Empowerment
      * Rank 2 of Epidemic gives 3 ticks in-game, we were using 2
      * Enhanced action priority list
  * Updates
    * **Full support for current PTR mechanics**
    * Enhance performance of large multi-player simulation reports
    * Enhance Rawr import to handle new and old formats (new format supports random suffixes)
    * New items: Necromantic Focus, Apparatus of KhazGoroth
    * Death Knight
      * Split MH/OH abilities when appropriate
      * Track Runic Empowerment Procs and Wasted Procs
    * Warrior
      * Add Crit Block
    * Shaman
      * Improve Maelstrom Weapon model accuracy
    * Hunter
      * Finish support for remaining pets
      * Add all unique pet specials (raid buff/debuff replacements)
## Simc 406-7
  * Bug fixes
    * Rogue
      * Assassins Resolve now affects Envenom
    * Mage
      * Properly detect Glyph of Armors and Glyph of Living Bomb
    * Hunter
      * Make sure pets are copied when using copy\_from=
    * Warlock
      * Dark Intent now properly works on tick crit callbacks
    * Fix a crash with absorbs
    * Fix role overrides
    * Fix url string format decoding

  * Updates
    * Massive rework of html styling
    * All Feb 18th hot-fixes
    * Add fight\_style= option
    * Add report\_details=0 option
    * Add Vengeance
    * Add extended stats reporting ( ETPE, TTPT )
    * Druid
      * Improvements to Balance action list
    * Rogue
      * Simplify Rogue virtual HAT proc mechanism
    * Shaman
      * Support for Spiritwalkers Grace
    * Warrior
      * Improvements to Fury/Arms action lists
      * Add Blitz, Charge and Juggernaut
      * Rend updated to match current mechanics
    * Warlock
      * Allow switching of main pets during combat

## Simc 406-6
  * Bug fixes
    * Shaman
      * Fix interaction between Fire Elemental and Searing Totem

  * Updates
    * Less aggressive filtering for action list reporting
    * Massive memory reduction through streamlining of wow client data access
    * Hunter
      * Support for Aspect of the Fox
    * Rogue
      * Improved Combat default action priority list
    * Warlock
      * Use of BoD over BoA for Affliction default actions

## Simc 406-5
  * Bug fixes
    * Fix a bug in Battle.net class parsing for Death Knights
    * Death Knight
      * Fix Endless Winter's cost on Mind Freeze
      * Fix Horn of Winter to actually have a cooldown

  * Updates
    * Scale factor noise is now calculated by default as: ( delta\_p -> dps\_error + ref\_p -> dps\_error ) / divisor, i.e. If you're not running with enough iterations you will see a scale factor of 0.00
    * Trinkets
      * Shard of Woe heroic reduces the base mana cost of spells by 205. Holy and nature school reduction remains at 405.
    * Death Knight
      * Module cleanups
    * Hunter
      * Add ilevel 359 profiles
    * Priest
      * Module cleanups
    * Paladin
      * Ilevel 372 BiS profile update
    * Warrior
      * Default action list tweaks for arms and fury/2h

## Simc 406-4
  * Bug fixes
    * Item data sources
      * Fix mmo-champion gem parsing
    * Enchants
      * Fix Lightweave Embroidery to proc on SpellDamage
    * Death Knight
      * Fix Killing Machine to proc only from main hand attacks (1, 3, 5 PPM)
      * Add Might of the Frozen Wastes to properly apply to 2handed attacks
      * Fix Endless Winter (was granting strength)
      * Fix invalid buff uptimes
    * Hunter
      * Fix pet parsing from Battle.net
      * Fix buff benefit calculations
    * Warlock
      * Fix Warlock base int at 85

  * Updates
    * HTML output tweaks
    * Change how resource reductions are calculated to support Shard of Woe change
    * Items
      * Fury of Angerforge now has a 15 second duration and a 5 second ICD
      * Heart of Ignacious now has a 2 second ICD
    * Death Knight
      * Unholy dual wielding profile now uses double Fallen Crusader
      * Add Rune of Cinderglacier
    * Hunter
      * Move AoTH before snapshot\_stats
      * Beast Mastery action list tweaks
    * Mage
      * Lower Arcane Blast mana cost as per hotfix note
    * Rogue
      * Virtual party support back for solo Subtlety
      * Add clarification about critical\_strike\_intervals
    * Shaman
      * Elemental default action list tweaks
    * Warlock
      * Move Fel Flame dot refresh to spell impact

  * Features
    * Korean Battle.net profile download
    * Remove local item database from default item sources until bugs are resolved

## Simc 406-3
  * Bug fixes
    * This build fixes a bug with Shadow Priests where they were benefiting from Darkness twice.
    * Properly treat fel spark as a 2-stack buff.
    * LttS, War Academy, Improved Slam, Glyph of MS all stack additively for Slam and MS

  * Updates
    * Haste scaling removed from Death and Decay.

  * Features
    * The "casting" raid event now also interrupts players to simulate use of /stopcasting with interrupts.
    * An initial implementation of a local item database has also been added along with an option to specify a search path for items. See [data importation](EquipmentOptions#Items.md)

## Simc 406-2
  * Bug fixes
    * Rawr characters should import again.

  * Updates
    * Hotfixes for warriors and shadow priests.
    * Starfall reversed to its old behaviour.
    * Moonfury 15% => 10%