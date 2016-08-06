

# Downloading the Source

  * Downloading via !Git
    * OSX and most Linux installs should already include **git**, if not, try to install it through your package manager or  go [here](http://www.tigris.org).
      * Use the git command found on the [source page](http://code.google.com/p/simulationcraft/source/checkout)
    * Git client integrated with Windows Explorer: [TortoiseGit](http://code.google.com/p/tortoisegit/)
      * See [UsingTortoiseGitWithSimcraft](UsingTortoiseGitWithSimcraft) for help on installing/using TortoiseGit.
    * Git client for Windows (cmd line interface): [Git for Windows](http://code.google.com/p/msysgit/)
      * Use the git command found on the [source page](http://code.google.com/p/simulationcraft/source/checkout)

  * Downloading release code
    * For each releases you can find a source code archive used to build that release on the download page
    * Helpful if you want to simply insert a quick modification (or fix a bug!)
    * Not really helpful if you want to live on the bleeding edge of ongoing development

# Building SimulationCraft

  * Building the command line interface (CLI) is very easy on all platforms
  * Building the graphical user interface (GUI) is considerably harder
    * The GUI was built using [Qt](http://qt-project.org/)
    * Building the GUI requires that the Qt libraries be downloaded and installed
    * Qt DLLs are used at runtime, so they need to be in your PATH; to create a release package, a subset must be shipped with it.
    * Refer to platform-specific directions below

# Building SimulationCraft on Windows

## Graphical User Interface using Microsoft Visual Studio

  * Download and install  [Microsoft Visual Studio Express 2013 for Windows Desktop](http://www.microsoft.com/visualstudio/eng/downloads#d-express-windows-desktop)
  * If using Visual Studio 2013, please ensure that you have the [4th major update installed.](http://support.microsoft.com/kb/2994375) The 32-bit version of simc will not function properly without it.
  * Download and install [Qt 5.5.0 for Windows 64-bit (VS 2013 )](http://www.qt.io/download-open-source/#section-2). The file you want will look similar to qt-opensource-windows-x86-msvc2013\_64-5.5.0.exe. Note that if you are running on a 32-bit machine, please install that version instead.
  * Add C:\Qt\Qt5.5.0\5.5\msvc2013\_64\bin to your [PATH](HowToBuild#Adding_directory_to_PATH).
  * If you have installed QT to a different location, edit `your_simc_source_dir\vs\Qt_vs2013.props`
  * Open `your_simc_source_dir\simc_vs2013.sln` project file
  * Build SimcGUI\_qt5.5.0 solution on x64 architecture
  * WebEngine configuration is the chrome-based browser, however it tends to have issues with some configurations of windows 7.
  * WebKit configuration is the legacy browser, and does not have any issues that we know of.
  * Creates executable `your_simc_source_dir\bin\<debug/release>\SimulationCraft64.exe`

### Advanced Settings
  * Make sure you have openssl (ssleay32.dll) available, or install  [OpenSSL Light](http://www.slproweb.com/products/Win32OpenSSL.html).
  * If you want to deploy SimulationCraft.exe without having QT installed and added to PATH, execute win64\_release\_mcvc(11/12).bat (after adjusting the path inside if necessary). This will copy over the necessary DLL's which you need to send along with the executable.

### Alternate way for Microsoft Windows
  * Install Visual Studio and Qt as above
  * Once your Qt version is installed, open a developer command prompt for it (shortcut in start menu), for example `Qt 5.6 64-bit for Desktop (MSVC 2015)`.
  * In the command prompt, navigate to `your_simc_source_dir`.
  * In `your_simc_source_dir`, issue the command
    * `qmake -r -tp vc -spec win32-msvc<version> simulationcraft.pro`, where **version** is your Visual Studio version (e.g., 2013 or 2015).
    * Output should look something like `Reading <your_simc_source_dir>/lib/lib.pro` (similarly for `gui` and `cli`).
  * Open the generated `simulationcraft.sln` in `your_simc_source_dir` with Visual Studio.
    * Three solutions are available, `Simulationcraft Engine`, which is the core library, `Simulationcraft CLI`, which is the command line client (i.e., simc.exe), and `Simulationcraft GUI`, which is the graphical user interface (i.e., Simulationcraft.exe).
  * For release builds, you can also enable Profile Guided Optimization by issuing the qmake command above with PGO=1
    * `qmake PGO=1 -r -tp vc -spec win32-msvc<version> simulationcraft.pro`.

## Graphical User Interface using MinGW
  * Download and install [Qt 5.4.0 for Windows 32-bit (MinGW 4.9.1, OpenGL, 852 MB)](http://download.qt-project.org/archive/qt/5.4/5.4.0/).
  * Make sure you have openssl (ssleay32.dll) available, or install  [OpenSSL Light](http://www.slproweb.com/products/Win32OpenSSL.html).

  * Building with QtCreator:
    * Start QtCreator and open the `simcqt.pro` project file from your SimulationCraft folder; it will prompt you to setup Debug & Release build configurations.
    * Build All (From the build menu, click the hammer icon in the lower left, or hit Control-B)
    * Clicking the computer icon in the lower left (Control-T) pops up the target selector that lets you pick Debug or Release config.
    * You can run from inside QtCreator with the green triangle icon (Control-R).

  * If you want to be able to run your `SimulationCraft.exe` from _outside_ QtCreator, you need to move it from the `debug` or `release` folder into the top-level source folder and make the Qt libraries available through one of two options:
    * Add Qt and MinGW to your  [PATH](HowToBuild#Adding_directory_to_PATH).
    * Run the batch script `GUI_dll_setup_mingw.bat` to copy DLLs from Qt and MinGW into `your_simc_source_dir`

## Command Line Interface using Microsoft Visual Studio
  * Download and install  [Microsoft Visual Studio Express 2013 for Windows Desktop](http://www.microsoft.com/visualstudio/eng/downloads#d-express-windows-desktop)
  * Open `your_simc_source_dir\simc_vs2013.sln` project file
  * Build `simc`Solution (`Build` -> `Build Solution` or `F7` by default)
  * It doesn't matter if it's done with webengine/webkit, those are only options for the gui.
  * Creates executable `your_simc_source_dir\simc.exe`

## Command Line Interface using MinGW

  * Download a MinGW compiler and add it to your  [PATH](HowToBuild#Adding_directory_to_PATH).
    * Recommended: Install [Qt 5.4.0 for Windows 32-bit (MinGW 4.9.1, OpenGL, 852 MB)](http://download.qt-project.org/archive/qt/5.4/5.4.0/) which comes with a modern MinGW, and is required to build the GUI anyway.
      * Add C:\Qt\Qt5.3.0\Tools\mingw49\_32\bin to your  [PATH](HowToBuild#Adding_directory_to_PATH).
  * Open command prompt window and run
    * `cd your_simc_source_dir\engine`
    * `mingw32-make`
  * Creates executable `your_simc_source_dir\engine\simc.exe`

# Building SimulationCraft on Linux

## Command Line Interface

  * If not already installed, install the following packages:
    * `g++`
    * `build-essential`
  * `cd your_simc_source_dir/engine`
  * `make`
  * This builds an optimized executable named `simc`

## Graphical User Interface

  * Install qt5-qmake. On Ubuntu, the package is called `qt5-default`.
  * Install `libqt5webkit5-dev`.
  * `cd your_simc_source_dir`
  * `qmake simcqt.pro`
  * `make`
  * Optional: Install to `~/SimulationCraft`:
    * `make install`

## Install Script

  * run the `install` script found in the main SimC folder. This will create a command line + GUI version, install it to  your home directory/SimulationCraft and install a .desktop file for it.

## Building Debian/Ubuntu packages

If you wish to have SimulationCraft installed via debian packages rather than make install, and packages for your distribution are not (yet) available, you can build your own.
Mind that debian package data is not included in the core sources, and is only present on git.
The debian data structure is maintained following the guidelines from git-buildpackage: http://honk.sigxcpu.org/projects/git-buildpackage/manual-html/gbp.html

### Accessing the debian/ data

According to **gbp** documentation (see above), every supported debian/ubuntu distribution has its own debian/ data directory on a separate branch on git. So, if you were to access debian/data for ubuntu/precise:

  * `git clone https://code.google.com/p/simulationcraft/`
  * `cd simulationcraft`
  * `git checkout ubuntu/precise`

### Requirements

A basic understanding of debian/ contents and package building is not strictly required for package building per se, but comes very helpful.

To build debian source packages you will need the following tools at the very least:

  * `sudo aptitude install devscripts dpkg-dev git git-buildpackage debhelper autotools-dev`

If your plan is to upload the packages to the PPA this is sufficient. In order to build binary packages, you will need a derivate of either **debuild** or **pbuilder**.
While debuild is simpler to use and requires almost zero knowledge (you just run **debuild -us -uc** to build a package), i would recommend **pbuilder** or better yet **pbuilder-dist**, as they have the great benefit of not tainting your running distribution with building dependencies.
For more information see: https://wiki.ubuntu.com/PbuilderHowto

### Building the source package

If your distribution is supported on the source tree (you can check by typing **git branch**), then building the source package is quite straightforward. An example for ubuntu/precise, release 5.4.8-4 (check releases with **git tag**):

  * `git checkout ubuntu/precise`
  * `./debian/_gbp_build release-548-4`

This will leave you with debian source data in ~/tmp/gbp/precise.

### Building the binary package

If you're not using the PPA builder and wish to manually build the package, you can either do it using `debuild`, from the directory where your debian source data is in:

  * `dpkg-source -x simulationcraft-x.y.z_foo.dsc`
  * `cd simulationcraft-x.y.z`
  * `debuild -us -uc`

or use pbuilder, after having configured it (see Requirements section), e.g.:

  * `pbuilder-dist trusty amd64 build simulationcraft-x.y.z_foo.dsc`

### Releasing a new simulationcraft version on a supported release

If a new simc version needs debian support, you can build a new source release by following a few simple steps. Example for ubuntu/precise, updating to release-548-4:

  * `git checkout ubuntu/precise`
  * `git merge release-548-4`
  * `dch -i` - Make sure you follow the version numbering trend, and explicitly type the release name on the right of the version (in this case, `precise`).
  * `./debian/_gbp_build release-548-4`
  * git commit and push your changes

Please be mindful, if you're considering to upload the source packages to a PPA, that Launchpad only accepts one source tarball for every given source, so if you are publishing more than a release (which is likely the case), subsequent builds should avoid adding the source tarball. This is done by changing the last command to this:

  * `./debian/_gbp_build release-548-4 -sd`

### Adding support for more Debian/Ubuntu releases

Only a few releases are supported currently, so if you wish to add support for other releases, follow these steps:

  * Identify the closest supported release
  * Duplicate the branch and name it according to the desired release, e.g.:
    * `git checkout ubuntu/trusty`
    * `git checkout -b ubuntu/utopic`
  * Adjust debian metadata to reflect the change, including but not necessarily limited to:
    * **debian/changelog** - Add a new entry or edit the last one with the right release name
    * **debian/control** - If dependency package names differ on your release, or even if you're just building against a different library version, make sure you edit the proper data (for example, check the diff between ubuntu/precise and ubuntu/trusty, which are built against a different QT major release)
    * **`debian/_gbp_build`** - Update it to reflect your change in the current branch name
    * **debian/gbp.conf** - Same as above
  * git commit and push your changes

# Building SimulationCraft on OSX

Building SimulationCraft on OS X requires you to install the XCode development environment, and in most cases, the command line tools.

## Command Line Interface / Makefile builds

  * `cd your_simc_source_dir/engine`
  * `make`
  * This builds an optimized executable named `simc`

## Graphical User Interface / Qmake builds
  * Install Qt 5
    * If you use Qt 5.1, you should fix the install names for Qt frameworks by pointing the `qt/fix_qt51_osx_paths.sh` to your qt install directory (the `clang_64` directory). This is only relevant if you are building a release, though, or intend to use the `macdeployqt` binary to create a framework independent bundle of `SimulationCraft.app`.
  * In terminal, issue "qmake simcqt.pro". This will create a `Makefile` in your simc source directory.
  * If you receive an error from Qmake such as `Project ERROR: Could not resolve SDK path for 'macosx10.9'`, you will need to explicitly tell make what OS X SDK to use, for example `qmake QMAKE_MAC_SDK=macosx<version> simcqt.pro`, where <version> is your OS X version (e.g., 10.10, 10.11). Note that the "OS X" version here is at least partly determined by your Xcode version, and may not match 1:1 with your operating system version.
  * Then, issuing "make" in the terminal will build SimulationCraft.app to your source directory.

## Graphical User Interface / XCode builds

XCode builds no longer supported

## Release package

The easiest way to build a release package for OS X is to use the qmake system. Open a terminal and issue "qmake simcqt.pro" in the simc source directory, followed by "make create\_release" will build an optimized GUI and command line clients, and package them in a disk image file. You can also build the release package through the XCode project, by building the `Create Release` target. Note that in this case, you will need to specify the `release` configuration to get optimized versions of the command line and the GUI client.

# Tips and Tricks
## Adding directory to PATH
  * On Windows7 go to Control Panel -> System -> Advanced system settings -> Environment Variables
    * Under System Variables search for PATH. Click Edit and append it with a semicolon `;` , followed by your desired directory path.
    * For other versions of windows, see [http://www.computerhope.com/issues/ch000549.htm](http://www.computerhope.com/issues/ch000549.htm).
## GNU Make Options
    * Add -j n  where n is the number of threads used for compiling
    * The GCC flag -dM will stop the compiler after the preprocessing pass and make it dump all #define