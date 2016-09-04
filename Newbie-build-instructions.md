Newbie instructions on how to build Simulationcraft from source on Windows 10.
The entire first-time setup will take anywhere from 30-60 minutes depending on the speed of your computer/internet. 

1: Install Visual Studio 2015 Community Edition - https://www.visualstudio.com/
- Use custom installation, enable the following options:
-- Programming Languages - Visual C++
-- Common Tools – Git for Windows, Github Extension for Visual Studio

2: Install TortoiseGIT - https://tortoisegit.org/download/
- Default settings are fine

3: Install QT 5.7.0 - http://download.qt.io/official_releases/qt/5.7/5.7.0/qt-opensource-windows-x86-msvc2015_64-5.7.0.exe
- Default settings are fine – Skip the account creation.

4: Add QT 5.7.0 to your windows environment path.

5: Open My Computer, go to the drive that you want to copy all simc files to.  Right click in the directory section, and “Git Clone.”   Under URL, paste in the following: https://github.com/simulationcraft/simc.git

Click OK, and then it will download the entire repository. This will take a few minutes. As the repo is around 700 MB large.

By default this will clone the repository into C:\simc\

6: Go to C:\simc\WinReleaseScripts\ and run the file named WinGenerateSLN.bat, this will create a file in the C:\simc\ folder named Simulationcraft.sln

7: Open simulationcraft.sln
- Under Solution Explorer there will be items named Simulationcraft CLI and Simulationcraft GUI. CLI is the command line interface, GUI is the normal client that most people on Windows use. 

8: Right click Simulationcraft GUI – Click Build – After this has completed, a file named Simulationcraft.exe will show up in your C:\simc\ folder.

9: If you get errors about missing dlls when attempting to load Simulationcraft.exe, that means that you may not have successfully completed step #4. Windows is finicky about updating paths, and it may require a restart of the computer as well. 