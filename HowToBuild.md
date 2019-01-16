# Downloading the Source

  * Downloading via Git
    * The repository address can be found on the [SimulationCraft Github page](https://github.com/simulationcraft/simc). Click the green **Clone or Download** button on the right.
      * OSX and most Linux installs should already include **git**, if not, try to install it through your package manager.
      * You can download Git for all platforms directly from [here](https://git-scm.com/downloads).
      * Git client integrated with Windows Explorer: [TortoiseGit](https://tortoisegit.org/)
        * See [UsingTortoiseGitWithSimcraft](UsingTortoiseGitWithSimcraft) for help on installing/using TortoiseGit.

  * Downloading release code
    * For each releases you can find a source code archive used to build that release on the download page
    * Helpful if you want to simply insert a quick modification (or fix a bug!)
    * Not really helpful if you want to live on the bleeding edge of ongoing development

# Building SimulationCraft

  * **Starting from Simulationcraft 8.1.0 release 2, libcurl (https://curl.haxx.se) is required for armory imports**
  * Building the command line interface (CLI) is very easy on all platforms
  * Building the graphical user interface (GUI) is considerably harder
    * The GUI was built using [Qt](http://qt-project.org/)
    * Building the GUI requires that the Qt libraries be downloaded and installed
    * Qt DLLs are used at runtime, so they need to be in your PATH; to create a release package, a subset must be shipped with it.
    * Refer to platform-specific directions below

# Building SimulationCraft on Windows

## Building using Microsoft Visual Studio

  * Download and install  [Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com)
  * Download and install [Qt 5.9.1 for Windows 64-bit (VS 2017 )](https://www.qt.io/download) or newer.
  * Download [CURL](https://curl.haxx.se) sources and compile if you intend to use the `armory` or `guild` options or import characters in the GUI
    * Unpack the sources to a directory (for example D:\Dev)
    * Start Visual Studio native command prompt for your platform (for example "x64 Native Tools Command Prompt for VS 2017")
    * Navigate to the directory `<curl install path>\winbuild` (for example D:\Dev\curl-7.63.0\winbuild). Note that if you cloned the GIT repository of CURL, you will need to invoke `buildconf.bat` in the `<curl install path>` to generate the prerequisite files.
    * Compile libcurl (and curl) by issuing the command `nmake /f Makefile.vc mode=dll`
    * Once compilation ends, with default options you should have a directory `<curl install path>\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl` (for example D:\Dev\curl-7.63.0\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl). Note that if you are compiling on 32-bit platform, `x64` will be `x86`
    * Add `<curl install path>\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl\bin` to your [PATH](HowToBuild#adding-directory-to-path) or copy `<curl install path>\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl\bin\libcurl.dll` to `your_simc_source_dir`
    * Create a new environment variable name `CURL_ROOT` that contains the value `<curl install path>\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl`
  
  * Add C:\Qt\Qt5.9.1\5.5\msvc2017\_64\bin to your [PATH](#adding-directory-to-path).
  * If you have installed QT to a different location, edit `your_simc_source_dir\vs\Qt_vs2017.props`
  * Open `your_simc_source_dir\simc_vs2017.sln` project file
  * Select `WebEngine` configuration to build a release version of Simulationcraft. **If you do not need to import characters or guilds from Blizzard API endpoints (armory), you can select the `WebEngine-NoNetworking` configuration. In this case, you also do not need to download and compile libcurl.**
  * Build Project simc for command line interface (CLI). Creates executable `your_simc_source_dir\x64\WebEngine\simc.exe`
  * Build project SimcGUI_qt5.9.1 for the Graphical User Interface (GUI). Creates executable `your_simc_source_dir\x64\WebEngine\SimulationCraft.exe`

### Advanced Settings
  * If you want to deploy SimulationCraft.exe without having QT installed and added to PATH, execute win64\_release\_mcvc(11/12).bat (after adjusting the path inside if necessary). This will copy over the necessary DLL's which you need to send along with the executable.

### Alternative way using command line QMake with simulationcraft.pro
  * Install Visual Studio and Qt as above
  * Download, build and perform installation steps for CURL as [above](#building-using-microsoft-visual-studio)
  * Once your CURL and Qt versions are installed, open a developer command prompt for it (shortcut in start menu), for example `Qt 5.8 64-bit for Desktop (MSVC 2017)`.
  * In the command prompt, navigate to `your_simc_source_dir`.
  * In `your_simc_source_dir`, issue the command
    * `qmake -r -tp vc -spec win32-msvc<version> simulationcraft.pro`, where **\<version>** is your Visual Studio version (e.g., 2017).
    * Note that for newer Qt versions the `<version>` may be omitted from the command
    * You can also specify `CURL_ROOT` for the qmake command if you do not want to provide it in an environment variable. For example `qmake CURL_ROOT="D:\Dev\curl-7.63.0\builds\libcurl-vc-x64-release-dll-ipv6-sspi-winssl" -r -tp vc -spec win32-msvc simulationcraft.pro`.
    * Output should look something like `Reading <your_simc_source_dir>/lib/lib.pro` (similarly for `gui` and `cli`).
  * Open the generated `simulationcraft.sln` in `your_simc_source_dir` with Visual Studio.
    * Three solutions are available, `Simulationcraft Engine`, which is the core library, `Simulationcraft CLI`, which is the command line client (i.e., simc.exe), and `Simulationcraft GUI`, which is the graphical user interface (i.e., Simulationcraft.exe).
  * For release builds, you can also enable Profile Guided Optimization by issuing the qmake command above with PGO=1
    * `qmake PGO=1 -r -tp vc -spec win32-msvc<version> simulationcraft.pro`.

### Alternate way using QtCreator with simulationcraft.pro
  * Install Visual Studio and Qt as above
  * Once your Qt version is installed, open `your_simc_source_dir`/simulationcraft.pro file with QtCreator.
  * Build Simulationcraft CLI/GUI

# Building SimulationCraft on Linux

  * Linux compilation using various g++ versions (at least 5, 6, and 8 series) may fail at the linking stage if Link Time Optimization (LTO) is used in conjunction with the new curl-based networking interface. Error message output will have something akin to `lto1: internal compiler error: in odr_types_equivalent_p, at ipa-devirt.c`. In this case, either switch `llvm-clang` compiler, use `SC_NO_NETWORKING` if you don't need the HTTP interfaces in Simulationcraft (to use `armory` or `guild` options), or stop using LTO in compilation.

## Command Line Interface & Graphical User Interface using Cmake (preferred)
 * If not already installed, install `build-essential`, `libcurl-dev`, and `pkg-config` (e.g., a compilation toolchain, libcurl include headers, and library metainformation tool).
  * Install qt5-qmake & qt5-webengine if you want to build the GUI. On Ubuntu, the package is called `qt5-default`.
  * `cd your_simc_source_dir`
  * `mkdir build && cd build`
  * `cmake ../`
  * `make`
  * This builds target `simc` (CLI) and `qt/SimulationCraft` (GUI)
  * Additional cmake options:
    * `cmake ../ -DCMAKE_BUILD_TYPE=Release` for Release build
    * `cmake ../ -DCMAKE_BUILD_TYPE=Debug` for Debug build
    * `make simc` build CLI only, no need to have Qt installed.

## Command Line Interface (classic build)

  * If not already installed, install `build-essential`, `libcurl-dev` (e.g., a compilation toolchain and libcurl include headers).
  * `cd your_simc_source_dir/engine`
  * `make optimized`
  * This builds an optimized executable named `simc`
  * Additional options:
    * Build with clang: Add CXX=clang++, eg. `make optimized CXX=clang++`
  * Note that if you issue the build with `SC_NO_NETWORKING=1`, `libcurl-dev` package is not necessary

## Graphical User Interface (using qmake)

  * Install qt5-qmake & qt5-webengine. On Ubuntu, the package is called `qt5-default`.
  * `cd your_simc_source_dir`
  * `qmake simulationcraft.pro`
  * `make`
  * Optional: Install to `~/SimulationCraft`:
    * `make install`

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
  * `make optimized`
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
