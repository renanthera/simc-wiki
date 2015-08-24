
# Introduction

This is going to be quick and dirty. Also, it will only work if you have Visual Studio 2013 FULLY UPDATED.

Detailed information, not necessary to use it:
http://blogs.msdn.com/b/vcblog/archive/2013/04/04/how-to-build-faster-and-high-performing-native-applications-using-pgo.aspx

# Details

If you want to build an optimized release using the profile guided optimization (PGO), it's fairly simple. The files necessary for doing this are already included when you clone/pull with git.

Typically these databases are up to date enough that you do not need to worry about re-training, and realistically it probably is only necessary to re-train the profile once every content patch (6.0, 6.1, etc.)

Anyway, if you want to simply build with PGO:
  1. Open simc\_vs2013.sln
  1. Right click either simc or simcGUI\_qt5.4.0 in the solution explorer.
  1. Mouse over "Profiled Guided Optimization", and click "Update", do **NOT** use "Optimize". Optimize is used when you are re-training.
  1. It will take 2-3 times longer than usual to build.


If you want to add more training to the database:
  1. Repeat steps 1-2 from above
  1. Instead of clicking "Update", click "Instrument"
  1. After it has compiled, go back to that menu and select "Run Instrumented/Optimized Application"
  1. Run the program how you want to train it.
  1. Exit program after you are done.
  1. Go back to the menu you were at previously, and this time click "Optimize". It will rebuild the database files to include the training you have just done, and then will compile a release version.