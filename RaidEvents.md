_This documentation is a part of the [TCI](TextualConfigurationInterface) reference._

**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**



# Shortcut syntax
  * **fight\_style** (scope: global; default: "") is a string to declare a predefined set of raid events. It acts as a shortcut for **raid\_events** and will change this setting. It means it will effectively clear all events declared so far (without affecting events declared after).
```
 fight_style=HelterSkelter
```
Acceptable values are:
  1. _Patchwerk_ will set up an empty raid events list. This is a perfect stand still and DPS fight.
  1. _CastingPatchwerk_ will set up a fight similair to `Patchwek` but the master target will be casting instead. It is equivalent to:
     ```
     raid_events+=/casting,cooldown=500,duration=500
     ```
  1. _LightMovement_ will set up a fight with infrequent movement. It is equivalent to:
     ```
     raid_events+=/movement,players_only=1,first=45,cooldown=85,distance=50,last=360
     ```
  1. _HeavyMovement_ will set up a fight with frequent movement. It is equivalent to:
     ```
     raid_events+=/movement,players_only=1,first=10,distance=25,duration=4
     ```
  1. _HecticAddCleave_ will set up a fight with regular add spawns and frequent movement. Similar to the Tier15 encounter Horridon (but without the vulnerability on the boss). The events scale with `max_time`, with 450 it is the same as:
     ```
     raid_events+=/adds,count=5,first=22,cooldown=33,duration=22,last=337
     raid_events+=/movement,players_only=1,first=22,cooldown=33,distance=20,last=337
     raid_events+=/movement,players_only=1,first=13,cooldown=13,duration=7
     ```
  1. _HelterSkelter_ will set up a "crazy" fight. It is equivalent to:
     ```
     raid_events+=/casting,cooldown=30,duration=3,first=15
     raid_events+=/movement,cooldown=30,distance=20
     raid_events+=/stun,cooldown=60,duration=2
     raid_events+=/invulnerable,cooldown=120,duration=3
     ```
  1. _CleaveAdd_ will set up a fight that regularly spawns an add the actor cleaves down. The event scales with your input `max_time`, with 450 it is the same as:
     ```
     raid_events+=/adds,count=1,first=22,cooldown=33,duration=22,last=405
     ```
  1. _Beastlord_ will set up a fight similair to the Tier17 encounter Beastlord Darmac. The events scale with `max_time`, with 450 it is the same as:
     ```
     raid_events+=/adds,name=Pack_Beast,count=6,first=15,duration=10,cooldown=30,angle_start=0,angle_end=360,distance=3
     raid_events+=/adds,name=Heavy_Spear,count=2,first=15,duration=15,cooldown=20,spawn_x=-15,spawn_y=0,distance=15
     raid_events+=/movement,first=13,distance=5,cooldown=20,players_only=1,player_chance=0.1
     raid_events+=/adds,name=Beast,count=1,first=10,duration_stddev=5,duration=67,cooldown=112,cooldown_stddev=0,last=292
     ```
  1. _Ultraxion_ will set up a fight similair to the Tier17 encounter Beastlord Darmac. The events scale with `max_time`, with 450 it is the same as:
     ```
     raid_event=/flying,first=0,duration=500,cooldown=500
     raid_event+=/position_switch,first=0,duration=500,cooldown=500
     raid_event+=/stun,duration=1.0,first=45.0,period=45.0
     raid_event+=/stun,duration=1.0,first=57.0,period=57.0
     raid_event+=/damage,first=6.0,period=6.0,last=59.5,amount=44000,type=shadow
     raid_event+=/damage,first=60.0,period=5.0,last=119.5,amount=44855,type=shadow
     raid_event+=/damage,first=120.0,period=4.0,last=179.5,amount=44855,type=shadow
     raid_event+=/damage,first=180.0,period=3.0,last=239.5,amount=44855,type=shadow
     raid_event+=/damage,first=240.0,period=2.0,last=299.5,amount=44855,type=shadow
     raid_event+=/damage,first=300.0,period=1.0,amount=44855,type=shadow
     ```

# Classic syntax
  * **raid\_events** (scope: global; default: "") is a string sequence specifying the events affecting the whole raid. See [TextualConfigurationInterface](TextualConfigurationInterface).
```
 raid_events+=/damage,amount=20000,cooldown=10
 raid_events+=/movement,cooldown=30,distance=40
```

1. All events are periodic. The following options are available to you:
   * _cooldown_ or _period_ (default: 0) specifies the periodicity of the event, in seconds. When lesser than or equal to zero, the event will occur every 1ms. TOCHECK.
   * _duration_ (default:0) specifies the duration of the event, in seconds. When lesser than or equal to zero, the event will last 1ms. TOCHECK.
   * _distance_ specifies the distance of the movement event, which will take raid/personal movement cooldowns into account.
    ```
    #This example will make the raid spend 15s moving every 30s.
    raid_events+=/movement,cooldown=30,duration=15
    ```
1. The duration and cooldown are always following a normal distribution (see [Wikipedia - Normal distribution](http://en.wikipedia.org/wiki/Normal_distribution)). The following settings help you adjust this:
    * _cooldown\_stddev_ (default: 0) is the _standard deviation_, in seconds, of the cooldown. When left to zero, it will be defaulted to 10% of the cooldown.
    * _duration\_stddev_ (default: 0) is the _standard deviation_, in seconds, of the duration. When left to zero, it will be defaulted to 10% of the duration.
     ```
     #This example will make the raid spend 10s moving (with a 5s standard deviation) every 30s (with a 10s standard 
     duration).
     raid_events+=/movement,cooldown=30,cooldown_stddev=10,duration=10,duration_stddev=5
     ```
1. You can also specify bounds for duration and cooldown, using the "<=" and ">=" operators with those keywords (note that _periodic_ won't work for specifying bounds for the cooldown though). If you don't specify any bounds, Simulationcraft will use 50% and 150% of the base value as the lower and upper bounds.
   ```
   #This example will make the raid spend 15s moving every 30s. Both duration and cooldown follow a normal law but the 
   cooldown will always be greater than 28s and lesser than 32s (rather than 27s and 33s with the default settings).
   raid_events+=/movement,cooldown=30,cooldown>=28,cooldown<=32,duration=15

   #This example will make the raid spend 15s moving every 30s. Both duration and cooldown follow a normal law but the 
   duration will always be greater than 14s and lesser than 16s (rather than 13.5s and 16.5s with the default settings).
   raid_events+=/movement,cooldown=30,duration=15,duration>=14,duration<=16
   ```
1. The following settings allow you to force the events to only occur during a certain phase:
    * _first_ (default: 0) specifies the first time, in seconds, the event will occur. 
    * _last_ (default: 0) specifies the last time, in seconds, the event may occur. It will not force the event to occur at this time, though. When lesser than or equal to zero, this setting will be ignored.

      With WoW 8.0 (BFA):

    * _first\_pct_  specifies the boss health pct when the event will first occur and be scheduled.
    * _last\_pct_  specifies the boss health pct when the event will last occur and no longer be scheduled.
    * _force\_stop_ (default: false) specifies if a raid event which is up when _last_ or _last\_pct_ occurs will be instantly canceled or not

    ```
    #This example will make the raid spend 15s moving every 30s. It will only happen after two minutes.
    raid_events+=/movement,cooldown=30,duration=15,first=120

    #This example will make the raid spend 15s moving every 30s. It will only happen during the first three minutes.
    raid_events+=/movement,cooldown=30,duration=15,last=180
    ```

# Filtering affected players
1. You may also make raid events distinguish between players and pets:
    * _players\_only_ (default: 0) specifies whether or not the raid event should only target players. When set to '0' both players and pets are affected by the raid event and when set to '1' only players are affected. Note: The **distraction** event is the only event that enables players\_only by default.
      ```
      #This example will stun all players in the raid every 30s for 5s, but will ignore all pets.
      raid_events+=/stun,players_only=1,cooldown=30,duration=5
      ```
1. The following setting allows you to set a per player chance that the raid event will affect them:
    * _player\_chance_ (default: 1.0) specifies a % chance for the raid event to affect each eligible player and pet. By default, 100% (1.0) of eligible players and pets are affected by each raid event.
      ```
      #This example has a 25% chance of distracting players for 5s every 60s
      raid_events+=/distraction,player_chance=.25,duration=5,cooldown=60
      ```
1. you can use distance\_min and distance\_max conditions (the distance in yards, extending from the boss) so that only ranged or melee characters are affected. See also the **distance** setting for characters.
   ```
   #This example will make the raid spend 15s moving every 30s, only players closer than 10m from the boss will be 
   affected.
   raid_events+=/movement,cooldown=30,duration=15,distance_max=10

   #This example will make the raid spend 15s moving every 30s, only players further than 20m from the boss will be 
   affected.
   raid_events+=/movement,cooldown=30,duration=15,distance_min=20
   ```
1. (BFA only) Finally, you can use player\_if= expressions to filter the affected players. This allows you to leverage the might of the already available expressions system from the action-priority system.
   ```
   #This example will make the raid spend 15s moving every 30s, only players with health percentage below 50 will be 
   affected.
   raid_events+=/movement,cooldown=30,duration=15,player_if=health.pct<50

   #This example will make the raid spend 15s moving every 30s, only players with role 'spell' and level of at least 100.
   raid_events+=/movement,cooldown=30,duration=15,player_if=role.spell&level>=100
   ```

# Adds
See also **target\_adds** in the [target properties](#Target) section if you rather want to spawn adds who will live through the whole fight.

The _adds_ keyword allows you to make adds periodically spawn. Default actions list may not include aoe actions but you can mention some of them, using conditions based on the number of targets, see [ActionLists](ActionLists). The _duration_ parameter will be the adds' lifespan.
  1. _count_ (default: 1) is the only specific option, it specifies how many adds will spawn.
```
 #This will make a fury warrior rotation use "cleave" as soon as there is at least one add.
 actions+=/cleave,if=target.adds>0
```

Spawning new adds via _adds_ has several unique parameters that affect how adds are spawned.
  1. The number of adds spawned per wave can be specified
    * _count_ (default: 1) specifies the number of adds to be generated.
    * _count\_range_ (default: 0) specifies if you want to generate up to _count_ +/- _count\_range_ adds, randomly choosen for each wave.
```
  #This example creates waves of 3 adds that exist for 15 seconds at a time every 60 seconds, starting at 5 seconds.
  raid_events+=/adds,count=3,first=5,duration=15,cooldown=60
  #This example creates waves of 5 adds with a count_range of 3, meaning between 2 and 8 adds will be generated for each wave.
  raid_events+=/adds,count=5,count_range=3,first=5,duration=15,cooldown=60
```
  1. If you wThe number of adds spawned per wave can be specified
    * _count_ (default: 1) specifies the number of adds to be generated.
```
  #This example creates waves of 3 adds that exist for 15 seconds at a time every 60 seconds, starting at 5 seconds.
  raid_events+=/adds,count=3,first=5,duration=15,cooldown=60
```
  1. The following setting allows you to name the adds part of the wave being defined.
    * _name_ (default: Fluffy\_Pillow\_WaveXX\_AddY) grants a specific name to the set of adds spawned.
```
  #This example names the wave 'Hogger'
  raid_events+=/adds,count=3,name=Hogger,first=5,duration=15,cooldown=60
```
  1. The health of the adds can also be manually specified if desired
    * _health_ (default: 100,000) determine's the starting health points of each add spawned in that wave.
```
  #This example gives all adds in the wave 75,000 health
  raid_events+=/adds,count=3,first=5,duration=15,cooldown=60,health=75000
```
  1. The following options require **distance\_targeting\_enabled=1** in order to function. The location of an add defaults to 0,0 (stacked on top of the main target). This can be changed in a few ways:
    * _spawn\_x_ and _spawn\_y_ (default: 0) set the x,y coordinates that a wave of adds will spawn at.
    * _distance_ (default: 0) sets the distance from 0,0 that the adds will spawn. The exact location is randomly generated, but will be _distance_ yards away.
    * _min\_distance_ and _max\_distance_ (default: 0) sets a band of space away from 0,0 that the adds will be able to spawn in. The exact location is randomly generated, but will be between _min\_distance_ and _max\_distance_ yards away. If either is omitted, the for that will be considered the minimum and be set to 0.
```
  #This example spawns 2 adds at the location 5,10
  raid_events+=/adds,count=2,first=5,duration=15,cooldown=60,spawn_x=5,spawn_y=10
  #This example spawns 4 adds at a distance of 10 yards away, randomly placed in an cone
  raid_events+=/adds,count=4,first=5,duration=15,cooldown=60,distance=10
  #This example spawns 3 adds at a distance of 0 - 30 yards away, randomly placed
  raid_events+=/adds,count=3,first=5,duration=15,cooldown=60,max_distance=30
  #This example spawns 2 adds at the location 5,10
  raid_events+=/adds,count=2,first=5,duration=15,cooldown=60,spawn_x=5,spawn_y=10
```
  1. The angle in which adds will spawn changes based on a few factors.
    * If _spawn\_x_ and _spawn\_y_ are omitted, so that the adds spawn centered at 0,0, then _angle\_start_ is (default: 90 degrees), and, _angle\_end_ is (default: 270 degrees). This creates a cone in which the adds will spawn that is on the near side / behind Fluffy Pillow.
    * If _spawn\_x_ or _spawn\_y_ are specified, so that the adds spawn centered somewhere other than at 0,0, then _angle\_start_ is (default: 0 degrees), and, _angle\_end_ is (default: 360 degrees). This creates a circle around the specified location in which the adds will spawn.
    * Valid range for _angle\_start_ and _angle\_end_ is 0 - 360 degrees. If more than 360 degrees is specified it will be modulused to a valid value. If a negative value is specified it will be assigned a default value.
```
  #This example spawns adds between 60 and 240 degrees at 0,0
  raid_events+=/adds,count=2,first=5,duration=15,cooldown=60,angle_start=60,angle_end=240
  #This example spawns adds between 180 and 90 (450; either will work) degrees at 0,0
  raid_events+=/adds,count=2,first=5,duration=15,cooldown=60,angle_start=180,angle_end=90
  #This example spawns adds between 90 and 270 degrees at 10,15
  raid_events+=/adds,count=2,first=5,duration=15,cooldown=60,angle_start=90,angle_end=270,spawn_x=10,spawn_y=15
```
  1. When randomly selecting where adds will be spawned, there is also the option of having all adds of that wave be stacked on top of each other or spread out.
    * _stacked_ (default: 0) sets whether all adds from a wave are at the same or different coordinates.
```
  #This example spawns 5 adds at a distance of 15 - 35 yards stacked up
  raid_events+=/adds,count=5,first=5,duration=15,cooldown=60,min_distance=15,max_distance=35,stacked=1
```

# Casting
The _casting_ keyword allows you to make a raid event with the following effect:
  1. The target will cast a spell your players must interrupt. There is no action condition relative to the target's casting but off-gcd interrupts do not need to be present in the actions list: they will be automatically used by the Simulationcraft.

There is no specific option for this keyword.
```
 #This example will make the boss incant a spell for 2s every 6s.
 raid_events+=/casting,cooldown=6,duration=2
```

# Distraction
The _distraction_ keyword allows you to periodically lower your players' skill, simulating those times of a fight when your players are distracted and unable to focus on their dps rotation because they have to focus on their environment. By default, the **players\_only** option is enabled for the distraction event. Also, see the **skill** command for more information.

Here are the specific options:
  1. _skill_ (default: 0.2) is the skill loss suffered by the players.
```
 #This example will make your ranged players heavily distracted for 10s every 1min.
 raid_events+=/distraction,cooldown=60,duration=10,skill=0.4,distance_min=10
```

# Invulnerability
The _invul_ and _invulnerable_ keywords can be used to make the target periodically invulnerable, clearing all dots on it (debuffs will remain though, because of a bug). There is currently no way to use actions list to switch on another target but you can still use actions conditions to detect whether your target is currently invulnerable or not; see [ActionLists](ActionLists).

There is no specific option for this keyword.
```
 #This example will make your target invulnerable for 10s every 1min.
 raid_events+=/invulnerable,cooldown=60,duration=10
```

# Incoming damage
The _damage_ keyword allows you to periodically make your raid suffer a uniformly distributed amount of damage. Note that simulated raid members can die from this damage.

Options are:
  1. _amount_ (default: 1) is the average amount of damage suffered by every player on every occurrence of the event, before mitigation.
```
 #This example will make your players suffer 20k damages every 30s.
 raid_events+=/damage,cooldown=30,amount=20000
```
  1. _amount\_range_ (default: 0) is the range of damage into one direction.
  1. _type_ (default: holy) is the type of damage.

# Incoming heals
The _heal_ keyword allows you to periodically heal your entire raid without going to the trouble of making healer profiles. This is useful to counteract the effects of the _damage_ event.

Options are:
  1. _amount_ (default: 1) is the average amount of healing to each player on every occurrence of the event.
```
 #This example will heal your players for 20k every 30s.
 raid_events+=/heal,cooldown=30,amount=20000
```
  1. _amount\_range_ (default: 0) is the range of of the heal amount, used to add some randomization.
  1. _to\_pct_ (default: 0) when greater than zero will heal every player in the raid up to that percentage of their health. Takes precedence over _amount_ and _amount\_range_ if those are also specified.
  1. _to\_pct\_range_ (default: 0) is the range of the percent heal amount, used to add some randomization.
```
 #This example will heal every player to 70% of health every 5s.
 raid_events+=/heal,cooldown=5,to_pct=70
```

# Movement
The _movement_ and _moving_ keywords can be used to force your raid to move, forcing the players and their pets to interrupt their casts and making them unable to use their spells for the duration of the move. Some spells will still be usable, through, depending on your actions list

Here are the specific options:
  1. _move\_distance_ (default: 0) is the distance, in yards, the players have to run on (staring from their current location: all players, whether they are 5 yards or 30 yards away from the boss, will run on the same distance) . When different from zero, it will prevail on _duration_ since the movement speed (taking into account possible speed bonuses) and distance will be used to evaluate the run duration. When equal to zero, this setting will be ignored.
  1. _to_ (default: -2) is the player's distance to the boss after moving. Only a 0 or positive value is processed. -1 means a default distance based on the player's role. -2 or lower means the current distance (i.e. the player moves and then returns to her current position). Currently the distance change happens instantaneously at the end of the movement event; if you need to check distance while moving, divide the event into several.
  1. _direction_ (default: omni) is the directionality flag for the movement event. Valid values are _omni_, _away_, and _towards_. Currently only affects what kind of actions can be used during the movement event.
  1. _min\_distance_ (default: 0) sets a minimum distance for the movement event. When combined with max\_distance allows for a single movement event to have differing distances.
  1. _max\_distance_ (default: 0) sets a maximum distance for a movement event.
  1. _distance\_range_ (default: 0) Works similarly, gives a range to move\_distance. Distance\_min/max will set a upper/lower limit, and can shift the distribution.

```
 #This line, added to a warlock's actions list, will make him/her use life tap when moving.
 actions+=/life_tap,moving=1

 #This example will make your players move for 5s every 20s. Our warlock will still use life tap.
 raid_events+=/movement,cooldown=30,duration=5

 #This example will make melee players run on 20 yards.
 raid_events+=/movement,cooldown=30,distance_max=10,move_distance=20

 #That will create a 60 second cooldown movement event with a stddev of 10 seconds, and only affects the player
 #25% of the time. The distance will be 60 yards 50% of the time, and the other 50%  will be between 40-60 yards.
 # raid_events+=/movement,cooldown=60,cooldown_stddev=10,distance=60,distance_min=40,distance_max=60,distance_range=20,player_chance=0.25
```

# Stuns
The _stun_ keyword can be used to make your raid periodically stunned and unable to do anything.

There is no specific option for this keyword.
```
 #This example will make your players stunned for 10s every 1min.
 raid_events+=/stun,cooldown=60,duration=10
```

# Vulnerability
The _vulnerable_ keyword can be used to make the target periodically vulnerable, causing you to do twice more damages to the target. It is possible to change your actions list to keep your best cooldowns for those moments, see [ActionLists](ActionLists).

There is no specific option for this keyword.
```
 #This example will make your target vulnerable, taking twice as much damage for 20s every 80s.
 raid_events+=/vulnerable,cooldown=80,duration=20

 #This example will make your target vulnerable, taking 3x the normal damage for 10s every 120s.
 raid_events+=/vulnerable,cooldown=120,duration=10,multiplier=3.0

 #This line will disable automatic bloodlust 
 override.bloodlust=0

 #This line, when added to a shaman's action list, will make bloodlust cast on the first vulnerable moment.
 actions+=/bloodlust,vulnerable=1,time_to_die<=100
```