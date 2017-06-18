# Profile Sets

Profile sets are a new mechanism of batch-simulating actors. Simulationcraft currently has two ways to do large (multi-actor) simulations. First, inputting multiple actors without any additional options will simulate all actors in the same environment (i.e., a raid). Adding `single_actor_batch=1` option will segregate the actors to simulating separately in individual phases.

Profile sets add a third simulation mode. Instead of simulating multiple profiles under the same environment, profilesets first simulate a baseline profile, and then each profileset individually in a separate simulation environment.

This has several benefits, the largest being that profile sets only require memory during run time for two simultaneous actors (i.e., the baseline which is kept in memory during the whole simulation run, and the individual profile set environment that is destroyed after it finishes). This should essentially remove the memory-related issues of conventional simulation modes (i.e., multi-actor or `single_actor_batch=1`), where the simulator allocates memory for all actors at the initialization phase of the simulator.

Note that profile sets only output summary information about the simulated actor. This includes at most the minimum, first quartile, median, mean, third quartile, and maximum metric values, as well as the standard deviation and the number of iterations used. The full information content is only available in JSON reports, the textual report only outputs the median value, and the HTML report includes all but standard deviation and number of iterations.

## Usage

Profile sets can be created in the simulator with the following format:
```
<baseline profile definition>

profileset.<profileset name>=<option-1>
profileset.<profileset name>+=<option-2>
...
profileset.<profileset name>+=<option-N>
```

You can only include a single baseline profile in the profile set simulation. Profile set names must be unique. In reporting, the profile set name is what differentiates the results. If you want to use whitespaces in the profile set names, enclose the name in double quotes (```profileset."white space"=...```).