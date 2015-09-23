

# Options
  * **initial\_rage**
> - When a warrior is simulated, it will start out at 40 rage, assuming that charge/shout are used pre-combat. If Bull Rush is used, it will have 55 rage. initial\_rage will set the warriors upon entering combat to any value.

# Actions
  * stance (choose)

    Options:

    The following 2 options are intended to be used with berserker stance, simulating stance swapping for increased rage income that is seen on many bosses. Other stances will work, though.

     1. swap -- The amount of time between events.
     Examples:
     ```
## Swaps to battle stance every time battle stance is down.
 /actions+=/stance,choose=battle,if=buff.battle_stance.down

## Swaps to defensive stance every 20 seconds for 1.5 seconds
## then swaps back to the characters starting stance.
 /actions+=/stance,choose=defensive,swap=20
     ```