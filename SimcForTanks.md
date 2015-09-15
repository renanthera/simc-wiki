**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Simulationcraft as a Tank
Simulationcraft now supports a number of options to facilitate simming and analyzing tank performance.

# Enemies
If you simulate a tank, the default boss "Fluffy Pillow" will not only take hits from the raid, but also deal a lot of damage to any tank in the simulation. However, you can also choose to use one of several other preconfigured enemies or create a custom enemy that's more to your liking.

## TMI Bosses
TMI bosses are standardized bosses that approximate certain content levels. You can choose these bosses from the "TMI Standard Boss" drop-down box on the Options -> Global tab of the GUI. If this drop-down is left at "custom," it will instead look for your custom definition of a boss (see below) or, if none is defined in the profile, spawn a Fluffy Pillow.

![http://wiki.simulationcraft.googlecode.com/git/images/tmi_boss_drop_down.png](http://wiki.simulationcraft.googlecode.com/git/images/tmi_boss_drop_down.png)

You can also specify TMI bosses using the Textual Configuration Interface. To define an enemy as a Tier 15 Heroic 25-man TMI boss, you would use the option `tmi_boss` like so:
```
 enemy=Not_A_Fluffy_Pillow
 tmi_boss=T15H25
```
The [Enemies](Enemies) page goes into more detail about the syntax for these bosses.

## Custom Bosses

You can also define a custom action list for an enemy similar to how you control your own character:
```
 enemy=fluffy_pillow
 actions=auto_attack,damage=200000,attack_speed=2.5,aoe_tanks=1
 actions+=/spell_nuke,damage=300000,cooldown=30,attack_speed=0.1,target=Warrior_Protection_T14H
 actions+=/spell_aoe,damage=10000,cooldown=2,cast_time=0.1
```
This will make the boss cleave any tank for 200k (before mitigation), will hit only your tank every 30secs for 300k with a spell, and hit the whole raid every 2 seconds for 10k. You can also add other [raid events](RaidEvents) to the fight, such as stuns or movement phases.

See the [Enemies](Enemies) page for more details about the actions and options available for defining custom enemies.

# Healers

If you sim your tank and take a look at your character's health timeline, you see that he very quickly drops below zero and goes into negative hit points. SimC does this because it assumes you want information about the full encounter, but don't want to bother with the details of incoming healing. There's nothing wrong with this, and for the most part it gives accurate results. However, if you have spells or effects that depend on your current health percentage, this can still be problematic.

If you add a healer to the raid, you can tell him to heal your tank with "target=name\_of\_your\_tank":
```
 Priest_Holy_T17N.simc
 target=Theck
 scale_player=0
```

The `scale_player=0` option just tells the sim that you don't want it to calculate scale factors for the healer, since that takes extra time and you're unlikely to be interested in that information.

# Assessing Your Tank

Simulationcraft provides a number of ways for you to analyze your tank's performance.

## Player Stats
The sim automatically reports several metrics about your character. When simulating a tank, it will automatically report DPS, Damage Taken Per Second (DTPS), Healing Per Second (HPS) and Absorption Per Second (APS), and a tanking metric described below called Theck-Meloree Index (TMI).

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_metrics.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_metrics.png)

The DTPS, HPS, and APS reporting may be little unintuitive at first, so it warrants further explanation. DTPS is the net damage per second your character actually takes, so any absorbed damage won't count in that value. Absorbs are counted as HPS in SimC, because healers often want absorbs counted as part of their throughput. As such, we report the three metrics as:

` X DTPS, Y HPS (Z APS) `

Meaning that you actually took X damage per second, and produced Y total healing and absorption per second, Z of which was the absorption component. That means your DTPS before absorbs is actually X+Z and you produced Y-Z healing per second.

The report will also contain an extra table containing statistics for DTPS, TMI, and Maximum Spike Damage (MSD), much like the DPS/HPS table that you may be familiar with on DPS and healing specs.

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_extra_table.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_extra_table.png)

You will also find extra timelines on your report detailing your DTPS and Resolve amounts:
![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_dtps_timeline.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_dtps_timeline.png)
![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_resolve_timeline.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_resolve_timeline.png)


### TMI, ETMI, & MSD
The Theck-Meloree Index, or TMI, is a tanking metric that was developed to measure damage smoothness and susceptibility to spike damage. The metric is fully explained [here](http://www.sacredduty.net/theck-meloree-index-standard-reference-document/), but in short, it produces a number (in thousands) that is roughly proportional to the size of your largest damage spikes (in percent of max health). For example, if your report says it calculated a TMI of 125k, it means you're taking spikes that are up to 125% of your maximum health. The metric accounts for both size and frequency of those spikes, so for example, a TMI of 125k could mean about one spike that's 125% of your health or several spikes that are 120% of your health. Minimizing TMI will generally mean your damage intake is smoother and you are less susceptible to dying from a damage spike.

The report will contain a chart showing you the distribution of TMI values observed over all iterations:

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_tmi_distribution_chart.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_tmi_distribution_chart.png)

TMI only considers effects caused by the tank and the boss. In other words, it ignores external healing and absorption entirely. You can safely add healers to your simulation without significantly altering the calculated TMI value. An alternative form of the metric called "Effective TMI" (ETMI) includes all sources of healing and absorption, and will be shown on the report if you are in a group. You can modify this setting from the "Show ETMI" drop-down box on the Options->Globals tab in the GUI:

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_tmi_options.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_tmi_options.png)

By default TMI uses a six-second window to calculate spike damage. This can also be customized via the GUI (shown above), or using the `tmi_window` [character option](Characters#Optional.md). The window size is reported in the table of tank metrics, and a TMI generated using a window that it not 6 seconds will have the window size specified in the name (e.g. TMI-5.0 in the summary line of the report shown in the [Player Stats](SimcForTanks#Player_Stats) section).
```
  # Define a paladin and use a 5-second TMI window
  paladin=Paul
  tmi_window=5
```

The tanking table also contains information about Maximum Spike Damage (MSD). This is a more direct calculation of the maximum spike size observed in the simulation, calculated on a per-iteration basis. Unlike TMI, it does not take spike frequency into account. To illustrate that, you might note that the TMI in the table above is 59.4k, while the MSD is only 6.4%. This is a case where the boss is hitting very weakly (because the T16N10 boss has been massively squished in the alpha WoD branch), so the max spike size is very small at only ~6% of your health. But since it's doing so very frequently, the TMI is significantly larger. Minimizing TMI in this case will be very similar to minimizing DTPS, because in this limit TMI functions much like a DTPS metric. In the general case where a boss is hitting much harder, MSD will usually be slightly smaller than TMI.

## Enemy Stats

You can take a look at fluffy pillow's attack table to see how your tank dodged/parried/blocked etc. You can also look at the damage breakdown for the boss to see what percentage of that damage came from each action, and thus what percentage was physical vs. magical damage. Note that the pie chart will be showing you the total damge breakdown for the boss, so if you have multiple tanks in the simulation (or the boss has spell\_aoe actions and there are multiple players) it may be a little more complicated to analyze.

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_fluffy_pillow_pie_chart.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_fluffy_pillow_pie_chart.png)

## Scale Factors
Tanks have several additional options for calculating scale factors. These include scaling over DTPS, healing taken per second (HTPS), TMI, and ETMI. These can be selected from the "Scale Over" drop down box on the Options->Scaling tab:

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_scale_over.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_scale_over.png)

You can also change the scaling metric with the `scale_over` [option](StatsScaling#Basics):
```
 paladin=Paul
 calculate_scale_factors=1
 scale_over=dtps
```

The scale factors and bar plot will be produced as usual, though the values will be negative (hopefully) for DTPS, TMI, and ETMI because a lower number is better in those metrics.

![http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_scale_factors.png](http://wiki.simulationcraft.googlecode.com/git/images/simc_for_tanks_scale_factors.png)

# Advanced Setups

This section will discuss advanced topics in tank simulation.

## Taunting
>(**Simulationcraft 6.0.1 release 1 and later**)

Simulating tank swaps is possible in newer versions of SimC. If there are two or more tanks in the simulation, the enemy will have one action list for each tank, and its default action list will look something like this:
```
 actions=/run_action_list,name=Alice,if=current_target=Alice
 actions+=/run_action_list,name=Bob,if=current_target=Bob
```
Note the use of the `current_target` conditional here. In Simulationcraft, the `target` variable is static and set upon actor creation. To facilitate tank swaps, we've added a `current_target` variable that stores the player the enemy is currently attacking. Player taunts change this variable, which then causes the boss to run a different action list in the example shown above.

Each tank's action list will be a copy of the enemy's usual default action list. If you define a custom action list for the tank, the simulation will copy that instead (and replace it with the /run\_action\_list default). So in the following example, the simulation would create a new action list for each tank in the simulation (actions.Alice, actions.BoB, etc.) containing the `auto_attack`, `spell_dot`, and `melee_nuke` entries we've defined.
```
 enemy=Fluffy_Pillow
 apply_debuff=1 
 actions=/auto_attack
 actions+=/spell_dot,if=!ticking 
 actions+=/melee_nuke,apply_debuff=2,cooldown=5
```

Each tank's taunt has been implemented by name (taunt for Warriors, reckoning for Paladins, growl for Druids, etc.). They can be implemented in a player's action priority list just like any other ability:
```
  actions+=/taunt
```
However, since taunts are off-GCD, this line will cause the tank to taunt the boss on cooldown (every 8 seconds). Generally, you will want to specify a conditional to limit the use of taunt. One option is to use time-based conditions:
```
  # taunt after 150 seconds have elapsed
  actions+=/taunt,if=time>150 
  # taunt every 30 seconds
  actions+=/taunt,line_cd=30
```
Another option is to take advantage of the `damage_taken` debuff. In the example boss above, `apply_debuff=1` tells the sim to apply one stack of the `damage_taken` debuff, which increases all damage taken by 1% per stack, every time the enemy deals damage. You could then query the enemy's `current_target`'s debuff stack size with `target.current_target.debuff.damage_taken`. The example below shows a paladin and warrior taunting off of each other at 60 stacks of the debuff:
```
  paladin=Alice
  _other character definition stuff_
  actions=/reckoning,if=target.current_target.debuff.damage_taken>60
  
  warrior=Bob
  _other character definition stuff_
  actions=/taunt,if=target.current_target.debuff.damage_taken>60
```
Note that you could append "`&target.current_target!=Alice`" to Alice's reckoning conditional to make sure she doesn't try to taunt off of herself.

You can customize the rate at which the debuff stacks using the `apply_debuff` option. When specified as a character option (`apply_debuff=1` in the example enemy above), it sets the default amount the boss applies with each damaging event. If used as an action option (`apply_debuff=2` in the `melee_nuke` action definition above), it sets the amount of stacks applied by that action. The action option takes precedence, so in the above example `melee_nuke` would apply two stacks, not three. Likewise, if we wanted to add a `spell_nuke` which did not apply the debuff, we could define it as:
```
  actions+=/spell_nuke,apply_debuff=0
```

The "dual\_tank\_example.simc" profile, found in the "profiles" folder, demonstrates a complete sim with Alice and Bob taunting off of one another throughout the simulation.