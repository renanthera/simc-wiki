# [SimulationCraft](http://www.simulationcraft.org/)
## Wiki
Welcome to the SimC wiki.

To get you started, checkout [StartersGuide](StartersGuide), or select a topic from the Table of Contents on the right.

## Simulationcraft with Windows 10 and AMD Ryzen processors

Simulationcraft (both GUI and command line versions) have performance scalability issues in multi-threaded profiles on AMD Ryzen processors on Windows 10. The exact root cause is currently unknown. Using the same hardware on other operating systems (i.e., Linux distributions) do not suffer from the same performance scalability issues.

The issues start appearing when Simulationcraft is run using a configuration that uses more threads than physical cores in a single Ryzen CCX, and performance significantly regresses when the number of threads exceeds a single Ryzen CCD. From user reports, it seems that this issue is only present on Windows 10 (various versions, although newer builds improve the situation slightly), and for example Windows 7 does not suffer from the same behavior.

The current "easy" method for working around the issue is to use [Windows Subsystem for Linux 2 (WSL2)](https://docs.microsoft.com/en-us/windows/wsl/install-win10), and build a Linux version of Simulationcraft that you run inside Windows 10. Anecdotally, this also seems to improve simulation performance by some amount compared to native Windows 10 builds (built with VS 2019). **Note that you need Windows 10 version 2004, build 19041 or higher to use WSL2.**