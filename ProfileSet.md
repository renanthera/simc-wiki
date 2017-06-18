# Profile Sets

Profile sets are a new way of batch-simulating actors. Simulationcraft currently has two ways to do large (multi-actor) simulations. First, inputting multiple actors without any additional options will simulate all actors in the same environment (i.e., a raid). Adding `single_actor_batch=1` option will segregate the actors to simulating separately in individual phases.

Profile sets add a third simulation mode. Instead of simulating multiple profiles under the same environment, profilesets first simulate a baseline profile, and then each profileset individually in a separate simulation environment.

This has several benefits, the largest being that profile sets only require memory during run time for two simultaneous actors (i.e., the baseline which is kept in memory during the whole simulation run, and the individual profile set environment that is destroyed after it finishes). This should essentially remove the memory-related issues of conventional simming (i.e., multi-actor or `single_actor_batch=1`), where the simulator allocates memory for all actors at the initialization phase of the simulator.