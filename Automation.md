**Is there an error? Something missing? Funky grammar? Do not hesitate to leave a comment.**

**The Automation tab was removed in SimulationCraft 801-01 as it had been unmaintained for an extended period of time**

Other tools like [AutoSimc](https://github.com/SimCMinMax/AutoSimC) exist to perform similar tasks.

# Introduction

As of Simulationcraft 6.0.1 release 1, there is an Automation tab under the Import section that helps automate creation of comparison sims. For example, this tool would help you quickly generate a simulation to compare various talent, glyph, gear, or rotation configurations. This simulation is essentially a raid sim containing one actor for each configuration specified, so you will automatically get charts ranking the actors for DPS, HPS, DTPS, and TMI.

This wiki entry explains how to use the tool and what each of the settings does.

# Interface

The interface is shown in the screenshot below.

> ![http://wiki.simulationcraft.googlecode.com/git/images/automation_tab.png](http://wiki.simulationcraft.googlecode.com/git/images/automation_tab.png)

The left column starts with a Comparison Type drop-down box that allows you to choose the type of comparison you want to run. It also contains a set of drop-down boxes to choose class, spec, race, and level, which will be used for all actors. It then has five text fields to define default talents, glyphs, gear, and rotation. Depending on the comparison type chosen, some of these boxes may be disabled.

There is a help text section at the top of the screen above the center and right columns that provides basic instructions on how to use the tool. These instructions will change based on the chosen comparison type.

The center column contains the Configurations text box, which allows you to specify different configurations, and the Footer text box. The Configurations text box will save whatever text you put in it per comparison type, so you can change comparison types without losing your entry for the other comparison types. More detail on the input syntax can be found below in the sections for each comparison type, or at the end in the [Appendix: Syntax](Automation#Appendix:_Syntax) section. The Footer text box is used to add options to the end of the generated profile.

The right column contains shorthand abbreviations that may be used in [Rotation Comparisons](Automation#Rotation_Comparisons); see that section for more details.

# Getting Started & Defaults

When you first view the Automation tab, it will be filled in with some basic defaults, and the Comparison Type drop-down box will be set to "None," which is non-functional. You can change the defaults in the left column in this state, but to do anything useful you'll have to choose a comparison type from the drop-down box in the upper left. Refer to the appropriate section below for specific information on each comparison type.

The Default Talents text box will accept talent inputs in the usual simc format - both `talents=0123123` and `0123123` will work seamlessly, as the code checks to make sure that the resulting character profile starts with `talents=`. Similarly, the Default Glyphs text box will accept a string of glyph names with or without the `glyphs=` precursor.

The Default Gear and Rotation text boxes accept usual simc gear and action specifications, but do not do any sanity checks. So for example, any of the following are acceptable inputs in the Default Gear box:
```
 #specifying gear line by line
 head=fake_helm,id=11111
 neck=fake_amulet,id=22222
 shoulder=fake_shoulders,id=33333
   
 #specifying gear all on one line
 head=fake_helm,id=11111 neck=fake_amulet,id=22222 shoulder=fake_shoulders,id=33333
    
 #specifying a gear set stored in a text file
 gear_filename.simc
```

The Default Rotation box works much the same way. However, the Default Rotation box may be left empty or used to define additional options that apply to every player. The sim will automatically use the default APL that corresponds to your spec if it sees that no action list has been defined.  The final box in the left column is only used for the Rotation configuration type, so it is disabled and labeled "Unused" by default. This box will be described in more detail in the [Rotation Comparisons](Automation#Rotation_Comparisons) section.

Finally, the Footer text box allows you to add custom commands to the generated profile. This is placed at the end of the profile, after all actors have been defined, so this is an appropriate place to define special boss configurations or global simc options (like `optimal_raid=0`).

Note that when the automation script generates a simulation, it's basically just bolting together your defaults and adding some lines based on what you enter in the center column. As such, you can use almost any tricks you want in these text boxes that work in a standard simc file. In other words, you have the entire [Textual Configuration Interface](TextualConfigurationInterface) syntax at your disposal.

For example, you could enter `1231231 name=Bob` in the Default Talents box, and it would happily work - but all of your actors would be named Bob. For more detail on this, see [Appendix: Syntax.](Automation#Appendix:_Syntax)

# Talent Comparisons

When you select the "Talents" comparison type, the "Default Talents" text box becomes disabled and the center column becomes the "Talent Configurations" text box. In this box, you can specify a list of talent strings, for example:
```
  0000000
  1111111
  2222222
  3333333
  1231231
  3213213
```

When you hit the "Import!" button, the script will generate a new actor for each line of text, setting the talents of that actor appropriately. Each actor will use the default glyphs, gear, and rotation specified in the left column, but the first will have `talents=0000000`, the second will have `talents=1111111`, and so on. Each actor will be named appropriately as well (ex: T\_0000000, T\_1111111, etc.).

Since the script is just pasting together bits of text, you can use standard SimC [TCI](TextualConfigurationInterface) tricks here to specify additional options. For example, with the input

```
  1111111 name=Alice
  2222222 name=Bob glyphs=focused_shield
  3333333 name=Carl glyphs+=/focused_shield
```

the automation script will create 3 actors.
  * The first will have `talents=1111111` and be named Alice.
  * The second will have `talents=22222222` and be named Bob, and will have only the focused\_shield glyph rather than whatever you've specified in the Default glyphs box.
  * The third will have `talents=3333333` and be named Carl, and will have the glyph of focused shield active in addition to any glyphs specified in the Default Glyphs box.


If you look at the Simulate tab after pressing "Import!", you'll see that the script is smart enough to append the extra options to the end of the character profile. It does this so that they take precedence over anything you've specified in the defaults. It also checks to see whether you've supplied the `talents=` portion or not, and adjusts the output as appropriate, so the following is a legitimate input:
```
  1111111 name=Alice
  talents=2222222 name=Bob
```

Note, however, that the very first thing specified for each configuration **has** to be the talents. `name=Alice 11111111` will **not** work (and will probably generate an error, or at least undesired results!).

The tool expects each new configuration to be a new line - in other words, separated by a single carriage return, with no blank lines in-between. If you leave a blank line (two carriage returns), it will assume that you want a blank line to separate configurations instead, and act accordingly. This is explained in more detail in [Appendix: Syntax](Automation#Appendix:_Syntax).

# Glyph Comparisons

The Glyph comparison type is very similar to the talent one. The Default Glyphs text box will be disabled, and a list of glyph configurations can be specified in the Configurations text box:
```
  alabaster_shield
  focused_shield
  final_wrath
  alabaster_shield/focused_shield/final_wrath
```

Since glyph names can be rather long, the automation tool will assign a simple numerical name to each configuration by default (ex: G\_001, G\_002, etc.). Of course, this can be overridden by specifying options:
```
  alabaster_shield name=Albert
  focused_shield name=Foucault
  final_wrath name=Finn
  alabaster_shield/focused_shield/final_wrath name=Alfalfa
```

As with talents, the glyph configuration needs to be the first thing on each line (so `name=Albert glyphs=alabaster_shield` will not work). Also as with talents, the tool expects each configuration to be one long string followed by a new line character (carriage return). Do not use blank lines unless you've already read [Appendix: Syntax](Automation#Appendix:_Syntax) and know what you're doing.

# Gear Comparisons

The gear comparison type is a little different, insofar as the input is expected to be a series of items separated by carriage returns. As a result, the Configurations text box will expect you to use a blank line to separate different configurations. In other words, this is how you would specify three gear sets, each containing only head, chest, and legs:
```
  head=fake_helm,id=11111
  chest=fake_chest,id=22222
  legs=fake_legs,id=33333
  
  head=another_fake_helm,id=11112
  chest=another_fake_chest,id=22223
  legs=another_fake_legs,id=33334
  
  head=a_third_fake_helm,id=11113
  chest=a_third_fake_chest,id=22224
  legs=a_third_fake_legs,id=33335
```

You can specify additional options in two ways - either after any individual item (separated by a space), or on its own new line. The example input below shows both:
```
  #change this configuration's talents and glyphs with space-separated syntax
  head=fake_helm,id=11111
  chest=fake_chest,id=22222 talents=1233213 glyphs=alabaster_shield
  legs=fake_legs,id=33333
  
  #again, but split into multiple lines for no good reason
  head=another_fake_helm,id=11112
  chest=another_fake_chest,id=22223 talents=1231231
  legs=another_fake_legs,id=33334 glyphs=alabaster_shield
  
  #this time, change talents and glyphs on new lines
  head=a_third_fake_helm,id=11113
  chest=a_third_fake_chest,id=22224
  legs=a_third_fake_legs,id=33335 
  talents=1111112 
  glyphs=alabaster_shield/focused_shield
```

Note that since gear is specified after everything else, the tool doesn't bother to move any additional options to the end. So for example, the second configuration above would end up looking like this on the Simulate tab:
```
  #again, but split into multiple lines for no good reason
  head=another_fake_helm,id=11112
  chest=another_fake_chest,id=22223
  talents=1231231
  legs=another_fake_legs,id=33334
  glyphs=alabaster_shield
```

# Rotation Comparisons

Rotation comparisons are more flexible with regards to input because there are two main modes of using the Rotation comparison setting: Longhand and Shorthand.

> ## Longhand Mode
> In longhand mode, you specify each action list in full, just the way you would in a profile, with each action on a new line separated by a carriage return. Thus, the tool expects you to use two carriage returns (a blank line) to separate configurations, as shown in the example below:
```
  actions+=/crusader_strike
  actions+=/judgment
  actions+=/avengers_shield
 
  actions+=/judgment
  actions+=/crusader_strike
  actions+=/avengers_shield
 
  actions+=/avengers_shield
  actions+=/crusader_strike
  actions+=/judgment
```

> As with Gear comparisons, extra options can be specified on any line (space-separated) or on a new line (probably easiest):
```
  name=Alice
  actions+=/crusader_strike
  actions+=/judgment
  actions+=/avengers_shield
 
  actions+=/judgment
  actions+=/crusader_strike name=Bob
  actions+=/avengers_shield
 
  actions+=/avengers_shield
  actions+=/crusader_strike
  actions+=/judgment
  name=Eve
```
> And also as with Gear comparisons, we don't bother moving space-separated options to the end of the profile. The second configuration will look like this on the Simulate tab:
```
  actions+=/judgment
  actions+=/crusader_strike
  name=Bob
  actions+=/avengers_shield
```
> See the [Actions Header and Footer](Automation#Actions_Header_and_Footer) section for information about specifying actions or settings that apply to all configurations.

> ## Shorthand Mode

> In shorthand mode, you supply a set of abbreviations (or "shorthands") that specify the rotations you want to test. For example, the three configurations defined in the [Longhand section](Automation#Longhand_Mode) could be specified as follows:
```
  CS>J>AS name=Alice
  J>CS>AS name=Bob
  AS>CS>J name=Eve
```

> As you can see, this mode uses a ">" to separate actions and a single carriage return to separate actors. It also allows additional simulation options to be specified inline (space-separated). The sim will automatically attempt to invoke shorthand mode if it doesn't find "actions+=" or "actions=" in the configuration.

> Shorthand mode also supports full use of conditionals, using the usual syntax with "+" standing for ",if=". So for example,

> `SotR+DP`

> might convert to

> `shield_of_the_righteous,if=buff.divine_purpose.react`

> The shorthand abbreviations are defined in the third column's Rotation Abbreviations edit box, which becomes enabled when switching the comparison type to Rotation. Ability, Option, and Operator shorthands are defined similarly, as described below. The [Options Shorthands](Automation#Options_Shorthands.md) section fully describes the syntax for options and the [Operator Shorthands](Automation#Operator_Shorthands) section fully describes operator syntax.

> ### Ability Shorthands
> Shorthands for abilities, buffs, talents, and glyphs must be defined in the first section of the sidebar under the ":::Abilities, Buffs, Talents, Glyphs:::" section. They use the very simple syntax `Shorthand=longhand_ability_name`, separated by carriage returns, as such:

```
   CS=crusader_strike
   J=judgment
   AS=avengers_shield
   GC=grand_crusader
```

> For most specs, the Rotation Abbreviations text box should load with a default set of shorthand abbreviations. If it doesn't, feel free to submit a ticket containing suggested shorthands so that we can add them for your spec.

> The text box is editable for a reason - if you don't like a particular abbreviation (maybe you want to use `C` instead of `CS` for `crusader_strike`), you can change it! You can also add your own entirely new shorthands by adding them to the list.

> Ability shorthands can also be used to represent a combination of an ability and fixed options. For example, if you define

```
  ASGC=avengers_shield,if=buff.grand_crusader.react 
```

> it will replace every instance of `ASGC` with `avengers_shield,if=buff.grand_crusader.react` just as you told it to. However, doing so will prevent you from using the built-in options syntax described in the next section, because specifying additional options using the '+' syntax will cause an error. For example,

```
  ASGC+E
```

> would translate to

```
   avengers_shield,if=avengers_shield,if=buff.grand_crusader.react,if=target.health.pct<=20
```

> which will cause an error when SimC tries to build the action list.

> ### Options Shorthands
> Shorthands for options can be specified under the ":::Options:::" heading. By default, choosing a spec will load a set of default option shorthands (ex: `E=target.health.pct<=20`). For example, if we define an option `GC=buff.grand_crusader.react`, we could specify the shorthand

```
   AS+GC 
```

> which translates to

```
   avengers_shield,if=buff.grand_crusader.react 
```

> These options can be combined with logical operations just like their longhands can. For example, given the definitions
```
   DP=buff.divine_purpose.react
   E=target.health.pct<=20
   NF=target.debuff.flying.down
```

> We could specify a shorthand like

```
   CS+DP&(NF|!E)
```

> which translates to:

```
   /crusader_strike,if=buff.divine_purpose.react&(target.debuff.flying.down|!target.health.pct<=20) 
```

> The operators <pre>+-*/<=</pre> are all supported as well. Note that <pre>></pre> is not supported, since that's the delimiter to signify a new action. You can also define your own option shorthands just like you can define ability shorthands.

> Options are special, in that they support two additional pieces of syntax:

  * The "#" character indicates a required numeric argument. For example, the definition `HP#=holy_power>=#` allows you to specify an option to only use an ability if you have greater than or equal to some numeric argument. An example of usage would be `SotR+HP4`, which the tool would automatically translate to `/shield_of_the_righteous,if=holy_power>=4`. Note that if specified this way, the numeric argument is not optional - e.g. you would need a separate definition `HP=holy_power` if you wanted just that portion.
  * The text "$ability" stands for the ability being modified by the conditional. For example, the definition of `BR=buff.$ability.remains` could be used as follows:
```
      SS+BR>2 
```
> > translates to
```
     /sacred_shield,if=buff.sacred_shield.remains>2 
```


> Note that both of these conditionals can be used in a single definition, as in the `AC#=action.$ability.charges>=#`.

> ### Operator Shorthands
> Operators are special options that require an additional ability, buff, talent, or glyph (the "operand") to operate upon. The syntax for defining operators is the same as the syntax for defining options, including the "#" and "$ability$ replacements. However, operators add another piece of substitution syntax:

  * The text "$operand" stands for the shorthand of the operand.

> The basic syntax for using an operator/operand pair in a shorthand is "`B.C`", where `B` is the operand (the ability, buff, glyph, or talent being operated upon) and `C` is the operator.

> To illustrate how this works, consider a case where you want to cast a spell only if a particular buff is active. For example, maybe we want to create a shorthand for
> ` /avengers_shield,if=buff.grand_crusader.react `

> We've already seen how we can do this with just an ability declaration, or as an ability+option combination. However, we can also do this in operator form. Given the ability definitions
```
    AS=avengers_shield
    GC=grand_crusader 
```

> and the operator definition ` BA=buff.$operand.react `, we can construct the shorthand

```
   AS+GC.BA 
```

> which translates to the desired `avengers_shield,if=buff.grand_crusader.react`.

> Just like other options, an option containing an operator can be combined with other operators via logical operations. So for example,

```
   AS+GC.BA&E 
```

> translates to

```
   /avengers_shield,if=buff.grand_crusader.react&target.health.pct<=20 
```

> While everything the operator system lets you do can already be accomplished by defining special options, the operator system gives you a lot more flexibility. For example, the definition "`BR#=buff.$operand.remains>#`" lets you implement buff checks for anything defined in your Abilities section without having to write a separate option for each one (like our ASGC example).

> _**Note:**_ The Rotation Abbreviations text box is saved when exiting the program, so that your custom abbreviations will still be there when you start it again. However, note that it is **not** saved independently for each spec. Thus, when you switch the Class or Spec drop-down boxes, the tool will load the set of defaults for the new spec, and will "forget" any custom definitions you may have added. If there are definitions you use frequently, it is advisable to keep them in a text file somewhere for easy copy/pasting.

> ## Actions Header and Footer

> When choosing the Rotation comparison type, the "Default Rotation" text box is renamed to "Actions Header" and the "Unused" box is renamed "Actions Footer" and becomes enabled. This is because it is very common to want certain actions that apply to all rotations (like /auto\_attack) without having to explicitly define shorthands. The Actions Header and Actions Footer boxes provide support for this. As you might guess, the text in the Actions Header box is placed in the profile immediately before the text generated from the Rotations Configuration input, and the text in the Actions Footer box is placed immediately after the text generated from the Rotations Configuration input.

> So for example, if I just want to run a comparison of several different holy power generator priorities, I might define the following Actions Header:
```
  actions.precombat=flask,type=greater_draenic_stamina_flask
  actions.precombat+=/food,type=talador_surf_and_turf
  actions.precombat+=/seal_of_insight
  actions.precombat+=/sacred_shield
  # Snapshot raid buffed stats before combat begins and pre-potting is done.
  actions.precombat+=/snapshot_stats
  
  actions=/auto_attack
  actions+=/eternal_flame,if=buff.eternal_flame.remains<2&buff.bastion_of_glory.react>2&(holy_power>=3|buff.divine_purpose.react|buff.bastion_of_power.react)
  actions+=/eternal_flame,if=buff.bastion_of_power.react&buff.bastion_of_glory.react>=5
  actions+=/shield_of_the_righteous,if=holy_power>=5|buff.divine_purpose.react|incoming_damage_1500ms>=health.max*0.3 
```
> which would take care of precombat actions (applying a seal, flask, food, and pre-casting Sacred Shield if it's available) as well as enabling auto-attack and defining holy power consumers.

> If I also want to add a line to the end of every profile that attempts to refresh Sacred Shield, I could put the following text in the Action Footer:
```
  actions+=/sacred_shield
```

> If I enter `CS>J` in the Rotation Configurations text box, the total APL generated will then be:
```
  actions.precombat=flask,type=greater_draenic_stamina_flask
  actions.precombat+=/food,type=talador_surf_and_turf
  actions.precombat+=/seal_of_insight
  actions.precombat+=/sacred_shield
  # Snapshot raid buffed stats before combat begins and pre-potting is done.
  actions.precombat+=/snapshot_stats
  
  actions=/auto_attack
  actions+=/eternal_flame,if=buff.eternal_flame.remains<2&buff.bastion_of_glory.react>2&(holy_power>=3|buff.divine_purpose.react|buff.bastion_of_power.react)
  actions+=/eternal_flame,if=buff.bastion_of_power.react&buff.bastion_of_glory.react>=5
  actions+=/shield_of_the_righteous,if=holy_power>=5|buff.divine_purpose.react|incoming_damage_1500ms>=health.max*0.3 

  actions+=/crusader_strike
  actions+=/judgment

  actions+=/sacred_shield
```

# Appendix: Syntax

The Configurations text box is actually a little more flexible than described in each section. To be able to support both modes, it has to support separating configurations by both a single carriage return (for talents, glyphs, and shorthand rotations) or two carriage returns (for gear and longhand rotations). In fact, it actually supports both of these for all configuration types.

It first attempts to split the input to the text box based on two carriage returns ("\n\n" in coding speak). It then checks to see if that gives it more than one configuration to work with. If so, it uses those results to attempt to generate the profiles. In this case, it will ignore any comments (lines starting with "#") and treat the first non-comment line of each configuration as the first line of input.

If splitting on "\n\n" yields only one configuration, it tries to split the input once again, this time based on a single carriage return ("\n"). In this case, you really shouldn't be using comments (though technically, single-word comments like "`#this`" won't break anything).

As such, you could use either method in each mode, so long as you only used one or the other. For example, this is a perfectly reasonable input for a talent comparison:
```
 #remember, this mode ignores comments
 0000000 name=untalented
 
 #flagrant
 #comment
 #spam
 1111111 name=One
 
 2222222
 #peek-a-boo
 name=Two
 
 3333333
 name=Three
```
However, it's also unnecessarily verbose, which is why I've suggested using single carriage returns for the talent, glyph, and shorthand inputs. Likewise, you could certainly define a Gear comparison like this:
```
  head=fake_helm,id=11111 chest=fake_chest,id=22222 name=Alice
  head=fake_helm_2,id=11112 chest=fake_chest_2,id=22223 name=Bob
  head=fake_helm_3,id=11113 chest=fake_chest_3,id=22224 name=Eve
```
or a Rotation comparison like this:
```
  actions+=/crusader_strike/judgment/avengers_shield name=Alice
  actions+=/judgment/avengers_shield/crusader_strike name=Bob
  actions+=/avengers_shield/crusader_strike/judgment name=Eve
```
But that might get difficult to read if you were specifying an entire gear set or rotation and additional options.

The key point here is that either input mode will work, but **don't mix them**. The following talent comparison input will **fail in a spectacular fashion** when you try to simulate:
```
 #WARNING: NEVER DO THIS
 0000000 name=Alice
 1111111 name=Bob
 
 2222222 name=Carlos
 3333333 name=Don
 
 1231234 name=Eve
```
The sim will take this to mean you have three actors. It'll skip the comment in the first actor and properly figure out that you want "talents=0000000". But at the end of the profile it will then add
```
 name=Alice
 1111111
 name=Bob
```
which isn't what you want, and the "1111111" line will trigger an error when you hit Simulate.