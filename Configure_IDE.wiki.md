

# Eclipse

## Setting up Eclipse as IDE

  * Get Eclipse C++ from http://www.eclipse.org/downloads/ and start it
  * Run File -> Import -> Git -> Projects from Git
  * Choose URI as Source and add https://code.google.com/p/simulationcraft/ to the URI-field
  * Choose the branches you want to checkout ( master branch is enough to get you started ) and the folder the project should be saved at
  * Proceed and choose "Import as General Project", specify the projectname and your finished

### Alternate Method (Eclipse C++ juno [4.2])
  * Get Eclipse C++ from http://www.eclipse.org/downloads/ and start it
  * Select Help -> Install new software..
  * Add "http://dl.google.com/eclipse/plugin/4.2" in the 'Work with:' field (NOTE: CHANGE 4.2 To whatever version you are using!)
  * Select Google Plugin for Eclipse and go through install steps.
  * Run File -> Import -> Google -> Google Project Hosting
  * If it asks to install Subclipse, do it and restart, then follow the previous step.
  * Choose the branches you want to checkout ( master branch is enough to get you started ) and the folder the project should be saved at
  * Click Check out as a project in the workspace and specify project name and you're done.

### Configuring Eclipse with MinGW
  * Get MinGW, install it and add it to your PATH environment. See [HowToBuild#Command\_Line\_Interface\_using\_MinGW](HowToBuild#Command_Line_Interface_using_MinGW.md)
  * Right-click on your created project -> New -> Convert to a C/C++ Project.
    * Convert to C++ Project, Project Type 'Makefile project' and use the  MinGW GCC toolchains
    * Go to Project -> Properties -> C/C++ Build and change the Builder settings, build location to /engine workspace path. You can append OPTS=-g to the build command if you want to build with debug symbols, and -jN if you want to compile with N threads.
  * You should now be able to compile the project ( Shortcut CTRL + B to build all ). If you specify a run configuration you can directly run simc from eclipse, if you built with debug symbols you can debug in eclipse with gdb.



## Tips and Tricks
  * You can set a additional PATH variable for a builder in Eclipse. Go to the build configuration -> Environment add a new variable ( name=PATH Value=C:\Mingw\bin ). This is handy if you do not have MinGW in your Windows PATH, or don't want to.
### Configuring the Code Scanner for C++11
  * Go to Project -> Properties -> C/C++ Build -> Settings -> Tool Settings -> GCC C++ Compiler -> Miscellaneous -> Other Flags. Add "-std=gnu++0x" to it.
  * Go to Project -> Properties -> C/C++ General -> Paths and Symbols -> Symbols -> GNU C++. Click "Add..." and paste "`__`GXX\_EXPERIMENTAL\_CXX0X`__`" (ensure to append and prepend two underscores) into "Name" and leave "Value" blank.