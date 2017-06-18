# Profile Sets

Profile sets are a new mechanism of batch-simulating actors. Simulationcraft currently has two ways to do large (multi-actor) simulations. First, inputting multiple actors without any additional options will simulate all actors in the same environment (i.e., a raid). Adding `single_actor_batch=1` option will segregate the actors to simulating separately in individual phases.

Profile sets add a third simulation mode. Instead of simulating multiple profiles under the same environment, profile sets first simulate a baseline profile, and then each profile set individually in a separate simulation environment.

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

You can also control which metric is used to collect from profile sets with the ```profileset_metric``` option (default `dps`). Note that output may be odd for metrics that do not support extended data collection (e.g., percentiles).

### Supported options for profile sets

Profile sets support the vast majority of simulation and player scope options. You can control the number of threads, override spell data, use `target_error` or `iterations` in an individual profile set without it leaking to other profile sets. You can also specify output options for individual profile sets, in which case the corresponding report is generated. Note that the profile set simulations are currently run with `report_details=0`, so detailed reporting of actions and buffs is unavailable.

Options that do not work in profile sets include (but are not limited to): various output-only options such as ```spell_query```, scale factor calculation, any kind of plotting, or adding additional players (e.g., ```armory```, ```copy```, or ```class_name``` options).